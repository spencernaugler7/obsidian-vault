## Attributes

Declarative controls for requests, swapping, and targeting.

### Requests

- [hx-get](https://four.htmx.org/reference/attributes/hx-get) - issues `GET` request to specified URL
- [hx-post](https://four.htmx.org/reference/attributes/hx-post) - issues `POST` request to specified URL
- [hx-put](https://four.htmx.org/reference/attributes/hx-put) - issues `PUT` request to specified URL
- [hx-patch](https://four.htmx.org/reference/attributes/hx-patch) - issues `PATCH` request to specified URL
- [hx-delete](https://four.htmx.org/reference/attributes/hx-delete) - issues `DELETE` request to specified URL
- [hx-query](https://four.htmx.org/reference/attributes/hx-query) - issues `QUERY` request to specified URL

### Request Control

- [hx-trigger](https://four.htmx.org/reference/attributes/hx-trigger) - controls when element issues requests
- [hx-swap](https://four.htmx.org/reference/attributes/hx-swap) - controls how response is inserted
- [hx-target](https://four.htmx.org/reference/attributes/hx-target) - controls where response is inserted
- [hx-select](https://four.htmx.org/reference/attributes/hx-select) - controls which response part is inserted
- [hx-swap-oob](https://four.htmx.org/reference/attributes/hx-swap-oob) - marks response elements to swap into page by ID
- [hx-select-oob](https://four.htmx.org/reference/attributes/hx-select-oob) - picks response elements to swap into page by ID
- [hx-confirm](https://four.htmx.org/reference/attributes/hx-confirm) - shows confirmation dialog before request

### Scripting

- [hx-on](https://four.htmx.org/reference/attributes/hx-on) - runs inline JavaScript when event fires

### Data

- [hx-vals](https://four.htmx.org/reference/attributes/hx-vals) - adds values to request parameters
- [hx-include](https://four.htmx.org/reference/attributes/hx-include) - includes additional element values in request
- [hx-headers](https://four.htmx.org/reference/attributes/hx-headers) - adds custom headers to request
- [hx-encoding](https://four.htmx.org/reference/attributes/hx-encoding) - sets request encoding type

### History

- [hx-push-url](https://four.htmx.org/reference/attributes/hx-push-url) - pushes URL into browser history
- [hx-replace-url](https://four.htmx.org/reference/attributes/hx-replace-url) - replaces current URL in browser history
- [hx-history-elt](https://four.htmx.org/reference/attributes/hx-history-elt) - marks element to swap on history restore

### Enhancements

- [hx-boost](https://four.htmx.org/reference/attributes/hx-boost) - converts links and forms to AJAX
- [hx-preload](https://four.htmx.org/reference/attributes/hx-preload) - preloads content before user triggers request
- [hx-pending](https://four.htmx.org/reference/attributes/hx-pending) - shows custom content during requests

### Advanced

- [hx-indicator](https://four.htmx.org/reference/attributes/hx-indicator) - specifies loading indicator element
- [hx-status](https://four.htmx.org/reference/attributes/hx-status) - handles responses differently by status code
- [hx-sync](https://four.htmx.org/reference/attributes/hx-sync) - synchronizes requests between elements
- [hx-validate](https://four.htmx.org/reference/attributes/hx-validate) - validates before submitting request
- [hx-disable](https://four.htmx.org/reference/attributes/hx-disable) - disables elements during request
- [hx-ignore](https://four.htmx.org/reference/attributes/hx-ignore) - disables htmx processing for element
- [hx-preserve](https://four.htmx.org/reference/attributes/hx-preserve) - preserves element during swaps
- [hx-morph-skip](https://four.htmx.org/reference/attributes/hx-morph-skip) - freezes an element during a morph swap
- [hx-morph-skip-children](https://four.htmx.org/reference/attributes/hx-morph-skip-children) - morphs an element’s attributes but keeps its children
- [hx-action](https://four.htmx.org/reference/attributes/hx-action) - specifies URL to receive request
- [hx-method](https://four.htmx.org/reference/attributes/hx-method) - specifies HTTP method for request
- [hx-config](https://four.htmx.org/reference/attributes/hx-config) - configures request behavior

## Events

Lifecycle hooks for requests, responses, swaps, and errors.

### Request Lifecycle

- [htmx:config:request](https://four.htmx.org/reference/events/htmx-config-request) - fires before request data is encoded
- [htmx:confirm](https://four.htmx.org/reference/events/htmx-confirm) - fires before handling `hx-confirm`
- [htmx:before:request](https://four.htmx.org/reference/events/htmx-before-request) - fires immediately before `fetch()`
- [htmx:before:response](https://four.htmx.org/reference/events/htmx-before-response) - fires after `fetch()`, before `response.text()`
- [htmx:after:request](https://four.htmx.org/reference/events/htmx-after-request) - fires after `response.text()`
- [htmx:response:error](https://four.htmx.org/reference/events/htmx-response-error) - fires for HTTP status 400 or higher
- [htmx:before:swap](https://four.htmx.org/reference/events/htmx-before-swap) - fires before DOM update
- [htmx:before:settle](https://four.htmx.org/reference/events/htmx-before-settle) - fires after DOM insertion, before settle tasks
- [htmx:after:settle](https://four.htmx.org/reference/events/htmx-after-settle) - fires after settle tasks
- [htmx:after:swap](https://four.htmx.org/reference/events/htmx-after-swap) - fires after DOM update
- [htmx:finally:swap](https://four.htmx.org/reference/events/htmx-finally-swap) - at the end of swap lifecycle
- [htmx:finally:request](https://four.htmx.org/reference/events/htmx-finally-request) - fires after lifecycle ends, including failures
- [htmx:error](https://four.htmx.org/reference/events/htmx-error) - fires after request or swap exception
- [htmx:abort](https://four.htmx.org/reference/events/htmx-abort) - aborts in-flight request

### Elements

- [htmx:before:init](https://four.htmx.org/reference/events/htmx-before-init) - fires before element initialization
- [htmx:after:init](https://four.htmx.org/reference/events/htmx-after-init) - fires after element initialization
- [htmx:before:process](https://four.htmx.org/reference/events/htmx-before-process) - fires before DOM node processing
- [htmx:after:process](https://four.htmx.org/reference/events/htmx-after-process) - fires after DOM node processing
- [htmx:before:on:init](https://four.htmx.org/reference/events/htmx-before-on-init) - fires before htmx wires the hx-on attributes
- [htmx:before:cleanup](https://four.htmx.org/reference/events/htmx-before-cleanup) - fires before element data removal
- [htmx:after:cleanup](https://four.htmx.org/reference/events/htmx-after-cleanup) - fires after element data removal
- [load](https://four.htmx.org/reference/events/load) - fires after element initialization

### History Events

- [htmx:before:history:update](https://four.htmx.org/reference/events/htmx-before-history-update) - fires before browser history update
- [htmx:after:history:update](https://four.htmx.org/reference/events/htmx-after-history-update) - fires after browser history update
- [htmx:after:history:push](https://four.htmx.org/reference/events/htmx-after-push-into-history) - fires after history push
- [htmx:after:history:replace](https://four.htmx.org/reference/events/htmx-after-replace-into-history) - fires after history replacement
- [htmx:before:history:restore](https://four.htmx.org/reference/events/htmx-before-restore-history) - fires before history restoration

### View Transitions

- [htmx:before:viewTransition](https://four.htmx.org/reference/events/htmx-before-viewTransition) - fires before view transition starts
- [htmx:after:viewTransition](https://four.htmx.org/reference/events/htmx-after-viewTransition) - fires after view transition completes

### Triggers

- [intersect](https://four.htmx.org/reference/events/intersect) - fires when element enters viewport
- [every](https://four.htmx.org/reference/events/every) - fires at each polling interval

## Config

Settings to customize htmx behavior and defaults.

### Core

- [htmx.config](https://four.htmx.org/reference/config/htmx-config) - configures htmx behavior globally
- [htmx.version](https://four.htmx.org/reference/config/htmx-config-version) - reports current htmx version (read-only)
- [htmx.config.prefix](https://four.htmx.org/reference/config/htmx-config-prefix) - sets secondary attribute prefix
- [htmx.config.metaCharacter](https://four.htmx.org/reference/config/htmx-config-metaCharacter) - replaces `:` in attribute modifiers
- [htmx.config.extensions](https://four.htmx.org/reference/config/htmx-config-extensions) - restricts extension registration by name

### Request Settings

- [htmx.config.defaultTimeout](https://four.htmx.org/reference/config/htmx-config-defaultTimeout) - sets default request timeout in `ms`
- [htmx.config.mode](https://four.htmx.org/reference/config/htmx-config-mode) - sets request mode for `fetch()`

### Swaps

- [htmx.config.defaultSwap](https://four.htmx.org/reference/config/htmx-config-defaultSwap) - sets default swap style for responses
- [htmx.config.allowEmptySwapAfterOOB](https://four.htmx.org/reference/config/htmx-config-allowEmptySwapAfterOOB) - controls whether OOB swaps prevent empty main swaps
- [htmx.config.noSwap](https://four.htmx.org/reference/config/htmx-config-noSwap) - sets HTTP status codes that skip swap
- [htmx.config.transitions](https://four.htmx.org/reference/config/htmx-config-transitions) - enables View Transitions API support
- [htmx.config.defaultSettleDelay](https://four.htmx.org/reference/config/htmx-config-defaultSettleDelay) - sets swap-to-settle delay in `ms`
- [htmx.config.defaultFocusScroll](https://four.htmx.org/reference/config/htmx-config-defaultFocusScroll) - scrolls to focused element after swap

### Morphing

- [htmx.config.morphIgnore](https://four.htmx.org/reference/config/htmx-config-morphIgnore) - preserves attribute prefixes during morphing
- [htmx.config.morphSkip](https://four.htmx.org/reference/config/htmx-config-morphSkip) - skips morphing for specific elements
- [htmx.config.morphSkipChildren](https://four.htmx.org/reference/config/htmx-config-morphSkipChildren) - skips morphing children of specific elements
- [htmx.config.morphScanLimit](https://four.htmx.org/reference/config/htmx-config-morphScanLimit) - limits siblings scanned during morph matching

### Indicators

- [htmx.config.includeIndicatorCSS](https://four.htmx.org/reference/config/htmx-config-includeIndicatorCSS) - includes built-in loading indicator CSS
- [htmx.config.indicatorClass](https://four.htmx.org/reference/config/htmx-config-indicatorClass) - sets class hidden by built-in indicator CSS
- [htmx.config.requestClass](https://four.htmx.org/reference/config/htmx-config-requestClass) - sets class applied during requests

### Behavior

- [htmx.config.history](https://four.htmx.org/reference/config/htmx-config-history) - controls htmx browser history management
- [htmx.config.implicitInheritance](https://four.htmx.org/reference/config/htmx-config-implicitInheritance) - enables implicit attribute inheritance
- [htmx.config.inlineScriptNonce](https://four.htmx.org/reference/config/htmx-config-inlineScriptNonce) - sets nonce on inline scripts generated by htmx
- [htmx.config.logAll](https://four.htmx.org/reference/config/htmx-config-logAll) - logs all htmx events to console

## Methods

JavaScript methods for advanced control.

### Request Methods

- [htmx.ajax()](https://four.htmx.org/reference/methods/htmx-ajax) - issues an htmx request

### DOM

- [htmx.find()](https://four.htmx.org/reference/methods/htmx-find) - finds first matching element
- [htmx.findAll()](https://four.htmx.org/reference/methods/htmx-findAll) - finds all matching elements
- [htmx.process()](https://four.htmx.org/reference/methods/htmx-process) - processes htmx attributes on element
- [htmx.swap()](https://four.htmx.org/reference/methods/htmx-swap) - swaps HTML content
- [htmx.initialize()](https://four.htmx.org/reference/methods/htmx-initialize) - manually initializes htmx

### Event Handling

- [htmx.on()](https://four.htmx.org/reference/methods/htmx-on) - listens for htmx events
- [htmx.onLoad()](https://four.htmx.org/reference/methods/htmx-onLoad) - executes callback when elements load
- [htmx.trigger()](https://four.htmx.org/reference/methods/htmx-trigger) - triggers custom events

### Extensions

- [htmx.registerExtension()](https://four.htmx.org/reference/methods/htmx-registerExtension) - registers htmx extension

### Timing

- [htmx.parseInterval()](https://four.htmx.org/reference/methods/htmx-parseInterval) - parses time intervals to milliseconds
- [htmx.timeout()](https://four.htmx.org/reference/methods/htmx-timeout) - creates timeout `Promise`

HTML tags provided by htmx.
- [\<hx-partial>](https://four.htmx.org/reference/tags/hx-partial) - targets multiple elements with one response