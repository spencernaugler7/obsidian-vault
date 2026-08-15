---
title: Misunderstanding SSE - YAGNI Club
source: https://yagni.club/3m475dwkjvc2o
author:
published: 2025-10-26
created: 2026-08-15
description: On my path of practicing simple software my existing understanding of systems, protocols and tools are challenged. My mental model for SSE (Server Sent Events) was a way to keep a connection open and send updates to the client from the server. Broadly this is correct, but read on as I break down what SSE actually is to see why you may be underutilizing SSE in your applications.
tags:
  - clippings
  - hypermedia
  - datastar
  - web
---
On my path of practicing simple software my existing understanding of systems, protocols and tools are challenged. My mental model for SSE (Server Sent Events) was a way to keep a connection open and send updates to the client from the server. Broadly this is correct, but read on as I break down what SSE actually is to see why you may be underutilizing SSE in your applications.

I was already using [SSE](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) as the mechanism for pushing html updates for all of my explorations so far, but was still tripping up on why I might reach for it for simple scenarios where I would only have a single response. After chatting in the [Datastar](http://data-star.dev/) discord I took a deeper dive to better understand [their position](https://data-star.dev/essays/event_streams_all_the_way_down) on always using SSE and improve my mental model.

First off: SSE has been around for forever, but everywhere I've worked over the last 20 years has either not utilized it well or couldn't quite figure out an effective way of using it beyond simple use cases or making it a key aspect of the architecture. Often conflating SSE with a special real-time protocol like WebSockets and not realizing it's just HTTP.

Over the years I've seen it used more and more like in local-first architectures that leverage SSE to poke the client, literally just a message that says 'poke', to then pull updates from a sync server. Initially I thought this was clever, but now realize that it's missing out on so much potential sitting right there in front of our faces.

![](https://yagni.club/api/atproto_images?did=did:plc:q7my6v2x7bwrc54xt5j56uhv&cid=bafkreiarhpu7ylk622wkcsbvudv32cudvm2bu3kgz2gygaxbkqgrx3aa2m&width=1200&v=1)

So… What is SSE?

It's a specification for text-based formatting of the response body.

Thanks for coming to my TED talk.

OK for real I had been conflating it with events specifically and how you handle those events on the client like using `EventSource`. Really all it is is:

```
event: event-name
data: first line of data
data: second line of data
id: 123
retry: 5000

event: another-event
data: {"json": "works fine"}

(blank line)
```

The rules:

- Each message is a series of lines
- Lines start with field names: ⁠event:, ⁠data:, ⁠id:, ⁠retry:
- A blank line (⁠\\n\\n) marks the end of a message
- That's literally it

Read more about the [Event stream format](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events#event_stream_format).

This SSE protocol uses the `text/event-stream` MIME type, just like HTML uses `text/html`, and APIs typically use `application/json`. When I send a `text/event-stream` response, the server can keep the connection open (by not closing it) and send 0, 1 or multiple messages over time. Each message follows the SSE format (⁠event:, ⁠data:, blank line), but the data payload itself can be anything - HTML, JSON, base64-encoded content, or plain text. This means I can use one consistent response pattern for all my interactions instead of switching between different response types.

Where this idea becomes really powerful is when pairing it with `fetch` on the client which unlocks handling SSE responses (`text/event-stream`) from any kind of request (`GET`, `POST` etc) instead of only `GET` when using using `EventSource`.

```
// EventSource: Only GET requests
new EventSource("/some-resource");

// fetch: Any HTTP method + SSE response
fetch('/contact', {
  method: 'POST',
  body: formData,
  headers: { 'Accept': 'text/event-stream' }
});
```

When reasoning about why I wouldn't just use a `text/html` response I could [morph in](https://data-star.dev/guide/getting_started/#patching-elements) with submission state for something like a simple contact form I was mostly thinking about:

- Handling a form submission/persisting data is simple
- Handling the response even with Datastar is simple

Which is true on the surface or happy path, but breaks down quickly.

- What about form validation?
- What about errors when persisting the submission to a data store?
- What about when I also want to kick off a background process or send an email on submission?

When using `text/html` I have to handle an all-or-nothing response and sequential bottlenecks.

```
All code examples will assume using Datastar and "fat morph" approach where you send the whole page and let Datastar efficiently update the DOM.
```

```
// text/html approach: Must wait for EVERYTHING to complete
app.post('/contact', async (req, res) => {
  // Validate (wait...)
  const validationErrors = await validateForm(req.body);
  if (validationErrors) {
    return res.send(renderContactPage({
      formData: req.body,
      errors: validationErrors,
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    }));
  }
  
  // Save to database (wait...)
  await saveToDatabase(req.body);
  
  // Send email (wait... 2-5 seconds!)
  await sendConfirmationEmail(req.body.email);
  
  // Update analytics (wait...)
  await trackSubmission(req.body);
  
  // Notify admin via Slack (wait...)
  await notifySlackChannel(req.body);
  
  // FINALLY respond after 5-10 seconds
  res.send(renderContactPage({
    formData: {},
    successMessage: 'Thank you! Your message has been sent.',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  }));
});
```

So even on success we're waiting for all of this to complete before sending a response back to the user. Lots of waiting. Lots that can go wrong with all those async operations. No way of notifying the user of progress unless you're emitting events for another part of the system to handle and notifying the user or updating page.

How about error handling?

```
// text/html: Handling partial failures is complex
app.post('/contact', async (req, res) => {
  try {
    await saveToDatabase(req.body);
    // Success! Data is saved. But now...
    
    try {
      await sendEmail(req.body.email);
    } catch (emailError) {
      // Email failed, but data IS saved!
      // What do I tell the user?
      return res.send(renderContactPage({
        formData: {},
        warningMessage: 'Your message was saved, but we couldn\'t send a confirmation email.',
        count: getSubmissionCount(),
        recent: getRecentSubmissions()
      }));
    }
    
    try {
      await notifySlack(req.body);
    } catch (slackError) {
      // Slack failed, but data saved and email sent!
      // Is this success or failure?
      return res.send(renderContactPage({
        formData: {},
        successMessage: 'Message sent! (Admin notification failed)',
        count: getSubmissionCount(),
        recent: getRecentSubmissions()
      }));
    }
    
    // Everything worked
    return res.send(renderContactPage({
      formData: {},
      successMessage: 'Thank you! Your message has been sent.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    }));
    
  } catch (dbError) {
    // Database failed - this is a clear error
    return res.send(renderContactPage({
      formData: req.body,
      errorMessage: 'Failed to save your message. Please try again.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    }));
  }
});
```

- Have to manually track of what failed or didn't across multiple try/catch blocks.
- What does success even mean in this flow?
- User won't know what actually happened until all operations succeed or partially succeeded which will be slow.

And validation?

```
// text/html: Need separate endpoints or client-side duplication
app.post('/validate-email', async (req, res) => {
  const isValid = await checkEmailExists(req.body.email);
  res.send(renderContactPage({
    formData: req.body,
    emailError: isValid ? null : 'Email already exists',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  }));
});

app.post('/contact', async (req, res) => {
  // Re-validate everything on final submit
  const emailError = await checkEmailExists(req.body.email);
  const messageError = req.body.message.length < 10 ? 'Message too short' : null;
  
  if (emailError || messageError) {
    return res.send(renderContactPage({
      formData: req.body,
      emailError,
      messageError,
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    }));
  }
  
  await saveToDatabase(req.body);
  
  res.send(renderContactPage({
    formData: {},
    successMessage: 'Message sent!',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  }));
});
```

- Multiple endpoints for field validation (or handling per-field validation branching logic in `/contacts`).
- Can't easily show validation progress.
- Inconsistency where async field validation passes, but maybe doesn't on submission.

So we can see using `text/html` ends up being more complex because it forces breaking up logic to handle the natural request/response (single shot) communication.

So how does SSE help?

```
// text/event-stream: Send multiple page updates as processing happens
app.post('/contact', async (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  
  const sendPage = (state) => {
    const html = renderContactPage(state);
    const body = html.match(/<body[^>]*>([\s\S]*)<\/body>/)[1];
    
    res.write('event: datastar-patch-elements\n');
    res.write(\`data: ${body}\n\n\`);
  };
  
  // Update 1: Show validation in progress
  sendPage({
    formData: req.body,
    statusMessage: '⏳ Validating your input...',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  const errors = await validateForm(req.body);
  if (errors) {
    // Update 2: Show validation errors
    sendPage({
      formData: req.body,
      errors,
      statusMessage: '❌ Please fix the errors above',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    return res.end();
  }
  
  // Update 3: Show saving in progress
  sendPage({
    formData: req.body,
    statusMessage: '⏳ Saving to database...',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  await saveToDatabase(req.body);
  
  // Update 4: Show email sending
  sendPage({
    formData: {},
    statusMessage: '⏳ Sending confirmation email...',
    successMessage: 'Your message has been saved!',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  await sendEmail(req.body.email);
  
  // Update 5: Complete
  sendPage({
    formData: {},
    statusMessage: '✅ All done!',
    successMessage: 'Thank you! Your message has been sent.',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  res.end();
});
```

Now using SSE we can patch in updates granularly, immediately and quickly all in the same route handler.

And error handling?

```
// text/event-stream: Each step can succeed or fail independently
app.post('/contact', async (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  
  const sendPage = (state) => {
    const html = renderContactPage(state);
    const body = html.match(/<body[^>]*>([\s\S]*)<\/body>/)[1];
    
    res.write('event: datastar-patch-elements\n');
    res.write(\`data: ${body}\n\n\`);
  };
  
  sendPage({
    formData: req.body,
    statusMessage: '⏳ Saving to database...',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  try {
    await saveToDatabase(req.body);
    
    sendPage({
      formData: {},
      statusMessage: '✓ Data saved successfully!',
      successMessage: 'Your message has been received.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    
  } catch (dbError) {
    sendPage({
      formData: req.body,
      statusMessage: '❌ Database error. Please try again.',
      errorMessage: dbError.message,
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    return res.end();
  }
  
  sendPage({
    formData: {},
    statusMessage: '⏳ Sending confirmation email...',
    successMessage: 'Your message has been received.',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  try {
    await sendEmail(req.body.email);
    
    sendPage({
      formData: {},
      statusMessage: '✓ Confirmation email sent!',
      successMessage: 'Your message has been received.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    
  } catch (emailError) {
    sendPage({
      formData: {},
      statusMessage: '⚠️ Data saved, but email failed. We\'ll retry later.',
      successMessage: 'Your message has been received.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
  }
  
  sendPage({
    formData: {},
    statusMessage: '⏳ Notifying team...',
    successMessage: 'Your message has been received.',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  try {
    await notifySlack(req.body);
    
    sendPage({
      formData: {},
      statusMessage: '✓ All done!',
      successMessage: 'Your message has been received.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    
  } catch (slackError) {
    sendPage({
      formData: {},
      statusMessage: '⚠️ Your submission is saved. Team notification failed.',
      successMessage: 'Your message has been received.',
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
  }
  
  res.end();
});
```

No error/success states leaking in to your route handler. Just passing in current state as it changes in to your template where all the display logic should live.

And validation.

```
// text/event-stream: One endpoint handles both validation and submission
app.post('/contact', async (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  
  const sendPage = (state) => {
    const html = renderContactPage(state);
    const body = html.match(/<body[^>]*>([\s\S]*)<\/body>/)[1];
    
    res.write('event: datastar-patch-elements\n');
    res.write(\`data: ${body}\n\n\`);
  };
  
  const { email, message, validateOnly } = req.body;
  
  // Live validation while typing
  if (validateOnly) {
    const emailError = await checkEmailExists(email);
    const messageError = message.length < 10 ? 'Message too short' : null;
    
    sendPage({
      formData: { email, message },
      emailError,
      messageError,
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    
    return res.end();
  }
  
  // Full submission with validation
  sendPage({
    formData: req.body,
    statusMessage: '⏳ Validating...',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  const emailError = await checkEmailExists(email);
  const messageError = message.length < 10 ? 'Message too short' : null;
  
  if (emailError || messageError) {
    sendPage({
      formData: req.body,
      statusMessage: '❌ Please fix errors',
      emailError,
      messageError,
      count: getSubmissionCount(),
      recent: getRecentSubmissions()
    });
    return res.end();
  }
  
  sendPage({
    formData: req.body,
    statusMessage: '✓ Valid! Saving...',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  await saveToDatabase(req.body);
  
  sendPage({
    formData: {},
    statusMessage: '✓ Saved!',
    successMessage: 'Thank you! Your message has been sent.',
    count: getSubmissionCount(),
    recent: getRecentSubmissions()
  });
  
  res.end();
});
```

- One endpoint handles both live validation and final submission.
- Same rendering logic for both scenarios.
- Can show validation progress during submission ("Validating..." → "Valid! Saving...").
- No duplication of validation logic.
- Live validation and submission validation are guaranteed to be identical.

The main point to take away is `text/event-stream` and SSE can do anything a `text/html` or `application/json` response can AND more. It's not a specialized tool for real-time features, but a better default to client-server communication that you're already doing, but over multiple request/response round trips and multiple resources.

With traditional approaches, you need different mental models for different scenarios:

- Simple form? Return ⁠text/html
- Need to update multiple elements? Add out-of-band swaps or multiple requests
- Want live validation? Create separate endpoints
- Need progress updates? Switch to polling or WebSockets
- Real-time features? Now you need WebSockets infrastructure

With SSE, you have one mental model:

- Client makes a request (GET, POST, PUT, DELETE)
- Server opens an event stream
- Server sends page states as they evolve
- Server closes the connection when done

That's it. Whether you send one update or a hundred, whether it takes 10ms or 10 seconds, the pattern is identical.

Your route handlers will feel more unified, easier to debug and reason about and easier to refactor later. Say you want to use a CQRS architecture you can move the rendering to a dedicated resource for the SSE connection and emit events from your submission handler and the plumbing is all the same. You only need to worry about `text/html` for your initial page loads and `text/event-stream` for everything else. No more deciding "should this be JSON or HTML?" or "should I use WebSockets for this?" or "do I need polling here?" One pattern handles all server-driven page updates. One way to handle all page updates.

So anyway I no longer think `text/html` is the simpler approach for page updates or that SSE is an "advanced" feature meant only for specific use cases like streaming or updates over time. It's a an often overlooked and simpler approach that I'm glad I have a better understanding of.