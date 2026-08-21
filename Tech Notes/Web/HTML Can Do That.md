---
title: HTML Can Do That
source: https://chrisburnell.com/html-can-do-that/
author:
  - "[[Chris Burnell]]"
published: 2026-08-08
created: 2026-08-19
description: HTML has been gobbling up swathes of what used to be JavaScript’s remit. This page lists a bunch of dynamic functionality that we can now achieve with just HTML.
tags:
  - clippings
  - web
  - html
---
HTML has been gobbling up swathes of what used to be JavaScript’s remit. This page lists a bunch of dynamic functionality that we can now achieve with just HTML.

---

## \<dialog>

Available since March 2022
- Chrome 37+
- Edge 79+
- Firefox 98+
- Opera 24+
- Safari 15.4+
- Chrome Android 37+
- Firefox for Android 98+
- Opera Android 24+
- Safari on iOS 15.4+
- Samsung Internet 3+
- WebView Android 37+

Opened and closed entirely with `command` and `commandfor` HTML attributes that describe what command is being directed at which element, matched by `id`.

```html
<button command="show-modal" commandfor="example-dialog">Open dialog</button>
<dialog id="example-dialog">
    <p>Look, Ma! No JavaScript!</p>
    <form method="dialog">
        <button type="submit">Close</button>
    </form>
</dialog>
```

---

## popover

Available since January 2025
- Chrome 114+
- Edge 114+
- Firefox 125+
- Opera 100+
- Safari 17+
- Chrome Android 114+
- Firefox for Android 125+
- Opera Android 76+
- Safari on iOS 17+
- Samsung Internet 23+
- WebView Android 114+

Light dismiss, Esc to close, no managing `z-index` to wrangle it onto a top later. All managed with `popover` and `popovertarget` attributes in HTML.

Same deal as the \<dialog> above: no JS, just HTML attributes!

```html
<button popovertarget="example-popover">Toggle popover</button>
<div id="example-popover" popover>
    <p>Same deal as the &lt;dialog&gt; above: no JS, just HTML attributes!</p>
</div>
```

---
## Grouped \<details>

Available since September 2025
- Chrome 120+
- Edge 120+
- Firefox 130+
- Opera 106+
- Safari 17.2+
- Chrome Android 120+
- Firefox for Android 130+
- Opera Android 80+
- Safari on iOS 17.2+
- Samsung Internet 25+
- WebView Android 120+

A shared `name` attribute turns a group of `<details>` into an exclusive accordion. Open one and the others close automatically. Magic!

```html
<details name="example-group">
    <summary>First</summary>
    <p>Open the seond one and watch this close on its own.</p>
</details>
<details name="example-group">
    <summary>Second</summary>
    <p>First one’s hidden now.</p>
</details>
```

---

## command & commandfor

Available since December 2025
- Chrome 135+
- Edge 135+
- Firefox 144+
- Opera 120+
- Safari 26.2+
- Chrome Android 135+
- Firefox for Android 144+
- Opera Android 89+
- Safari on iOS 26.2+
- Samsung Internet 29+
- WebView Android 135+

*Note:* So far only `show-modal`, `close`, `request-close`, `toggle-popover`, `show-popover`, and `hide-popover` have landed stable in browsers. We can look forward to invokers supported in the future to increment/decrement values, interact with media elements, copy text, etc.

Two separate HTML buttons controlling *one* popover. No scripting.

`show-popover` opens this and `hide-popover` closes it!

```html
<button command="show-popover" commandfor="example-command-popover">Open</button>
<button command="hide-popover" commandfor="example-command-popover">Close</button>
<div id="example-command-popover" popover>
    <p><code>show-popover</code> opens this and <code>hide-popover</code> closes it!</p>
</div>
```

---

## Native input pickers

Available since March 2017
- Chrome: Colour 20+, Range 4+, Date 20+
- Edge: Colour 14+, Range 12+, Date 12+
- Firefox: Colour 29+, Range 23+, Date 57+
- Opera: Colour 12+, Range 11+, Date 11+
- Safari: Colour 12.1+, Range 3.1+, Date 14.1+
- Chrome Android: Colour 25+, Range 57+, Date 25+
- Firefox for Android: Colour 27+, Range 52+, Date 57+
- Opera Android: Colour 12+, Range 11+, Date 11+
- Safari on iOS: Colour 12.2+, Range 5+, Date 5+
- Samsung Internet: Colour 1.5+, Range 7+, Date 1.5+
- WebView Android: Colour 4.4+, Range 4.4+, Date 4.4+

Colour, range, and date pickers, built right into the browser.

*Your mileage may vary with these elements; although, hand-written JS solutions tend to vary wildly, and I think we can expect form elements to receive more love over the coming years.*

```html
<label>Colour <input type="color" value="#5f8aa6" autocomplete="off"></label>
<label>Range <input type="range" min="0" max="100" value="50" autocomplete="off"></label>
<label>Date <input type="date" autocomplete="off"></label>
```

---

## \<datalist>

Available since March 2019
- Chrome 20+
- Edge 12+
- Firefox 4+
- Opera 9.5+
- Safari 12.1+
- Chrome Android 33+
- Firefox for Android 79+
- Opera Android 20+
- Safari on iOS 12.2+
- Samsung Internet 2+
- WebView Android 4.4.3+

*Note:* This isn’t yet supported across the board with all input types, e.g. colour or date inputs.

Native autocomplete suggestions, no dropdown library required.

```html
<label>Favourite HTML element <input type="text" id="example-datalist-input" list="example-datalist" autocomplete="off"></label>
<datalist id="example-datalist">
    <option value="a">
    <option value="abbr">
    <option value="address">
    <!-- ... -->
</datalist>
```

---

## loading="lazy"

Available since March 2022
- Chrome 77+
- Edge 79+
- Firefox 75+
- Opera 64+
- Safari 15.4+
- Chrome Android 77+
- Firefox for Android 79+
- Opera Android 55+
- Safari on iOS 15.4+
- Samsung Internet 12+
- WebView Android 77+

This image defers loading until it’s near the viewport. Not an [`IntersectionObserver`](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) in sight.

![Chris Burnell’s avatar.](https://chrisburnell.com/images/avatar@2x.jpeg)
```html
<img src="/images/avatar@2x.jpeg" loading="lazy" width="200" height="200" alt="Chris Burnell’s avatar.">
```

---

## hidden until-found

Available since December 2025
- Chrome 102+
- Edge 102+
- Firefox 148+
- Opera 88+
- Safari 26.2+
- Chrome Android 102+
- Firefox for Android 148+
- Opera Android 70+
- Safari on iOS 26.2+
- Samsung Internet 19+
- WebView Android 102+

Navigating to the fragment link below reveals the hidden section. The browser automatically removes `hidden="until-found"`.

[Jump to hidden content](#example-until-found)
```html
<a href="#example-until-found">Jump to hidden content</a>
<div id="example-until-found" hidden="until-found">
    <p>Yahaha! You found me!</p>
</div>
```

---

Built by [Chris Burnell](https://chrisburnell.com/) for [HTML Day 2026](https://2026.html.energy/) during the [Online Event](https://zacharykai.net/events/htmlday) run by [Zachary Kai](https://zacharykai.net/) on .