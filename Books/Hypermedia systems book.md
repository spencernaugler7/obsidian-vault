---
source: https://hypermedia.systems/book/contents/
tags:
  - books
  - hypermedia
  - htmx
---
## Htmx Patterns

##### Boosted Links

```html
<a href="/settings" hx-boost="true">Settings</a> <1>
```

##### Boosted Forms

```html
<form action="/messages" method="post" hx-boost="true"> <1>
  <input type="text" name="message" placeholder="Enter A Message...">
  <button>Post Your Message</button>
</form>
```

when clicking the link or submitting the form the entire page is not replaced. Only the body of the page is replaced. Why do it? no need to replace all the loaded static assets and css provided by the `<head>` tag content. Normal links and forms replace the entire page and have undesireable behavior known as *a flash of unstyled content*.


> [!note]
> you can remove redundant `hx-boost="true"` calls by adding it to a parent `<div>`.
> ```html
> <div hx-boost="true"> <1>
>  <a href="/contacts">Contacts</a>
>  <a href="/settings">Settings</a>
>  <a href="/help">Help</a>
>  <a href="/help/documentation.pdf" hx-boost="false"> <2>
>   Download Docs
>  </a> <!-- opt out of boosting by readding this tag -->
> </div>
> ```

by default, htmx “targets” the element that triggers a request, and will place the HTML returned by the server inside that element.


