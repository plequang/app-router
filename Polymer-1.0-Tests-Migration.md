## Migration
* migrate to new `<dom-module>` element registration
* Migrate to new properties declarations (https://www.polymer-project.org/1.0/docs/migration.html#properties)
* added `<span>` around all text content binding (https://www.polymer-project.org/1.0/docs/devguide/data-binding.html#binding-to-text-content)
* removed curly brackets areound declarative event handlers (https://www.polymer-project.org/1.0/docs/migration.html#declarative-handlers)
* `this.querySelector('::shadow app-router')` not working anymore. Couldn't get `Polymer.dom(this).querySelector('app-router')` to work either, so used this.$.router instead.

## Problems
### Polymer `<template>`
https://erikringsmuth.github.io/app-router/#/databinding/#polymer-template

Not working anymore, as template.createInstance(model) has gone.

Templates are instantiated using `document.importNode(template.content, true);`, so no model is bound to them.
As appRouter.createModel is not called anymore, data binding events are also not fired.


### http://localhost:8080/tests/functional-tests/test-typecast.html
Not tested, because Polymer templates are not working (see above)


### Accessing the parent scope
https://erikringsmuth.github.io/app-router/#/databinding/#accessing-the-parent-scope
Is not working, as templateInstance in elements does not exists anymore.

### Init on attachedCallback
This is causing problems, for example in the test-session.html test.
The first state-change event is fired too early, before the session from `<user-session>` is bound to to the demo-app element.
In the case of test-session.html, it works when initializing the app-router the demo-app ready() callback.

### test-session-global

What this test aims to do is to "publish" the session object from the `<user-session>` element in `<demo-app>` to the inner
`<user-session>` elements in `<login-page>` and `<home-page>`.

I was not able to have it working, and I'm not sure this is possible with Polymer 1.0.


### test-scroll-hash-mode
Not migrated the page3 test, that is using core-scaffold. core-scaffold has gone, don't know if it has been replaced by something.

### test-polymer-element-event

domReady does not exist aymore, added an attached callback test

### core-animated-pages
All tests using core-animated-pages have bot been migrated.
