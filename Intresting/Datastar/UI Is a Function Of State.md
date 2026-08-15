---
title: "ui = fn(state) done right"
source: "https://yagni.club/3m3anpetejc23"
author:
published: 2025-10-14
created: 2026-08-15
description: "If \"ui = fn(state)\" has ever resonated with you as a frontend developer you owe it to yourself to consider we as an industry have been going about it all wrong for years.Likely your state already lives on the backend and by syncing it to the frontend to render UI we're adding measurable amounts of unnecessary complexity. If you're to radically simplify if you development environments and production deployments then read on…"
tags:
  - "clippings"
---
If "ui = fn(state)" has ever resonated with you as a frontend developer you owe it to yourself to consider we as an industry have been going about it all wrong for years. Likely your state already lives on the backend and by syncing it to the frontend to render UI we're adding measurable amounts of unnecessary complexity. If you're to radically simplify if you development environments and production deployments then read on…

Some preamble before we get started:

- If you are sold on local-first syncing for reasons like data sovereignty and privacy this isn't for you. Consider authoring local native apps though!
- I realize the irony that I am authoring this in a heavily client side application with local-first features. <3 leaflet!
- If you are vibes based and LOVE authoring JavaScript/TypeScript for the frontend this isn't for you.
- If your identity is strongly tied to a front-end framework this likely isn't for you.
- If you think offsetting server costs by moving computation to the client is a good trade off… this isn't for you.
- If you're dead set on SPA-like navigation this isn't for you.
- If while reading you find yourself thinking "you can't implement continuous media playback across navigations" this isn't for you.

If you have an open mind, want to simplify your development and build some of the most performant frontends you've ever built then you might get something out of this. I don't aim to convince die-hard JS devs, but hopefully connect some dots for people who find themselves tired of conversations like this in 2025:

OK so you hopefully have heard of something a long the lines of:

> ui = function(state)

Idea being you should be able to derive your UI via pure functions that are provided the entire state of the world. It's a great model and is simple to reason about. The issue is how we go about implementing this. React popularized component driven development that really does embody this idea.

```jsx
function Button({ label }) { 
  return <button>{label}</button> 
}
```

It's really great and beautiful in its simplicity. However when you extrapolate this in practice real-world applications with a lot of complex state we're looking at:

- Syncing that state from the backend to the frontend to render any updates after initial page load
	- Now you're bring things in like [Tanstack Query](https://tanstack.com/query/latest), [Redux](https://redux.js.org/), [signals](https://preactjs.com/guide/v10/signals/) etc.
	- Polling API endpoints or getting pushed JSON
	- Deserializing that JSON to store in memory. Oh the deserialization! Oh the humanity!
- Hydrating components on the frontend when server rendering
	- Sending initial HTML along with the state needed to render so that it can then re-render in to a client side renderable app for future updates.

Now if your state really does only live locally, great, but still consider authoring a native app.

```
This isn't for you
```

That is a lot of extra work to get some HTML on the page when your backend can serve HTML directly and is the true owner of your state anyway.

This is just the read path too. What about updating state? Well again we have a beautiful out of context example.

```jsx
function App() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <button onClick={handleClick}>
        Count: {count}
      </button>
    </div>
  );
}
```

With a real-world application we're looking at:

- Tanstack Query, [zustand](https://github.com/pmndrs/zustand), ([pick your poison](https://dev.to/joodi/modern-react-state-management-in-2025-a-practical-guide-2j8f)) or calling `fetch` inside a useEffect where hopefully you remembered to account for all the various loading and error states involved in making a network request OH AND that your useEffect dependency array is g2g
	- Even with Tanstack Query you need to understand how to author a mutation and how that impacts your local cache etc.
	- Do you really want to baby-sit your client side cache?!
- OK this update also needs to sync the change to the backend over the network
	- I HATE the network it's so slow…
	- Better do this as an [optimistic update](https://xcancel.com/DelaneyGillilan/status/1968763070366228729#m) …
	- OK so I have some pretend state, on top of the copy of the backend state… wait wtf I thought it was just supposed to be `ui = fn(state)`! Shit!
- t

I've built many applications like this. I've enjoyed using some of these tools/approaches. I admired how well abstracted and nicely designed the API is for tanstack-query (it really is good software!!). All this stuff feels like a known quantity or just how you build modern applications. I joined the cargo cult.

However I've come to realize it's all unnecessary. You may have dug yourself in to a deep hole with this kinds of architecture and are just feeling like…

![](https://yagni.club/api/atproto_images?did=did:plc:q7my6v2x7bwrc54xt5j56uhv&cid=bafkreid74do2u3s6waphn37un7zvoabkqtseyb3yrkxesrz3zluhvfktqi&width=1200&v=1)

There is a better way.

You've probably been waiting for me to mention " [hypermedia](https://hypermedia.systems/) " so here it is.

initiating shill mode

[Datastar](https://data-star.dev/) is your path to salvation. Datastar is a 10kb hypermedia shim+framework. There are many [like](http://htmx.org/) [it](https://unpoly.com/), but this one is mine (mine as in choice, not the author!).

There are plenty of pages out there comparing Datastar to other frontend frameworks, hypermedia or not. How you can do the same thing with [htmx](http://htmx.org/) etc… I won't do that here, but will maybe loop back and add some more links to that. What I will say quickly however is yes you can do this with any library or framework (it's mostly a matter of leveraging http effectively) Datastar does it in the most terse and direct way. API design matters and Datastar does a bang up job here.

I want to focus on how using something like Datastar puts you in the pit of success by encouraging these properties:

- Keep most of your state on the backend. Backend is the source of truth always.
- Leverage "fat morphs" (replace most of page with new html). Render the whole page on each update.
- Separate your updates from reading when rending your UI ([CQRS](https://www.geeksforgeeks.org/system-design/cqrs-command-query-responsibility-segregation/)).

I think most people might trip up here. Yes you're going to have to write less frontend code and more backend code. Business logic doesn't disappear, but [incidental complexity](https://outbox.matthewphillips.info/archive/perils-of-reactivity) does.

I'm going to throw you a bone… You can keep using JSX and components alright? Not only that you can literally use any backend language you're planning on learning next weekend when you get some free time.

You'll need your http server and for the sake of simplicity a single route… I'll call this a Single Route Architecture.

```jsx
import { Hono } from "hono";
import { streamSSE } from "hono/streaming";
import { EventEmitter, on } from "node:events";

let counter = 0;

function Counter({ count }: { count: number }) {
  return <button data-on-click="@post('/')">Count: {count}</button>;
}

function Body({ count }: { count: number }) {
  return (
    <body data-on-load="@get('/')">
      <Counter count={count} />
    </body>
  );
}

function Page({ count }: { count: number }) {
  return (
    <html>
      <head>
        <script
          type="module"
          src="https://cdn.jsdelivr.net/gh/starfederation/datastar@1.0.0-RC.5/bundles/datastar.js"
        ></script>
      </head>
      <Body count={count} />
    </html>
  );
}

const app = new Hono();
const events = new EventEmitter();

app.get("/", async (c) => {
  const seereq = c.req.raw;

  if (req.headers.get("datastar-request")) {
    return streamSSE(c, async (stream) => {
      const ac = new AbortController();

      stream.onAbort(() => {
        ac.abort();
      });

      try {
        for await (const _ of on(events, "inc", { signal: ac.signal })) {
          const htmlString = (<Body count={counter} />).toString();
          await stream.writeSSE({
            event: "datastar-patch-elements",
            data: \`selector body\nelements ${htmlString}\`,
          });
        }
      } catch (err: any) {
        if (or err.code !== "ABORT_ERR") {
          throw err;
        }
      }
    });
  }

  return c.html(<Page count={counter} />);
});

app.post("/", async (c) => {
  counter++;
  events.emit("inc");
  return c.body(null);
});

export default {
  port: 3000,
  fetch: app.fetch,
};
```

[GitHub - derekr/ui-fn-state-done-right: Bun app showcasing simple ui = fn(state) idea using Datastar](https://github.com/derekr/ui-fn-state-done-right)

This is the whole app. No backend or frontend monorepo splitting. No frontend or backend bundling/splitting. This is with Bun+Hono, but can be done w/ node (tsx), deno and other JS runtimes. There's an optional Datastar [TypeScript SDK](https://github.com/starfederation/datastar-typescript) for working with SSE as well if your needs are more complex than this.

Clicking the button makes a POST request which increments the counter and emits the `inc` event. When the page loads a SSE connection is established where we iterate over the events object keeping the connection alive and handling any `inc` events. When the event is fired we pass the count to `Body` for "re-rendering" and send the whole html payload over SSE back to the client.

This basic example is realtime multiplayer btw. Anyone that accesses the app is seeing the exact same view and when they click the shared count is incremented and pushed to everyone.

There are lots of nuanced benefits to this approach with regards to efficiency and how much you can send over the wire etc… (hint: it's a lot more than you think).

Pay attention to how we kept the `ui = fn(state)` principal while still communicating over the wire, but with way less overhead and complexity. Your templating language or components still just take whatever state is needed and render based on that. In a real-world application your state typically includes things like current user/session, posts for that route, presence data for multi-player experiences…

And while this is a simple example this basic architecture can [scale to almost any kind of experience](https://checkboxes.andersmurphy.com/). That one SSE connection can push updates from anywhere, not just an action or mutation triggered by the user. Imagine using the same exact setup above to push updates from a background job or process like [AI chats](https://conductorsam.com/). You bring your own event bus/messaging system and push some more updates over SSE.

So if you're even a little curious about simplifying your web projects without sacrificing performance or capabilities come by the [Discord](https://discord.gg/bnRNgZjgPh) and see what it's about. Lot's of smart craftspeople with lots of experience that you'll learn a ton just be hanging out for a bit and absorbing these concepts.

If you're happy and productive writing React or other client heavy apps that's great.

```
This isn't for you
```

## Resources

[https://data-star.dev/guide/getting\_started](https://data-star.dev/guide/getting_started)

The example in this post is simplified to help highlight the `ui = fn(state)` concept. If you want to learn more about using Datastar with Bun you should check out [The Datastar Chat Example repo](https://github.com/Mortalife/datastar-chat-example-ts/tree/main).

Curious about how far people are taking the concept with Datastar? Check out these amazing projects:

- [https://example.andersmurphy.com](https://example.andersmurphy.com/)
	- [https://www.youtube.com/watch?v=xzC3g0qIRro&t=2312s](https://www.youtube.com/watch?v=xzC3g0qIRro&t=2312s)
- [https://cells.andersmurphy.com](https://cells.andersmurphy.com/)
- [https://checkboxes.andersmurphy.com](https://checkboxes.andersmurphy.com/)
- [https://conductorsam.com](https://conductorsam.com/)