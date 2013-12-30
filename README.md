EventEmitter
============

Client-Side JavaScript Events a la Node.js

Usage
-----

```javascript
// Standalone usage (not extending anything here):
var emitter = new EventEmitter();

// Adding listeners for events (single and multiple):
emitter.on('event', function listener() {});
emitter.on({
  foo: function onOne() {},
  bar: function onOne() {},
  baz: function onOne() {}
});

// Adding one-time listeners (single and multiple):
emitter.once('event', function listener() {});
emitter.once({
  foo: function() {},
  bar: function() {},
  baz: function() {}
});

// Removing listeners:
emitter.off();                // Remove all listeners for all events.
emitter.off('foo');           // Remove all listeners for event 'foo'.
emitter.off('foo', listener); // Remove a specific listener for event 'foo'.

// Fetching listeners:
emitter.listeners('foo');     // Returns an array of listeners for event 'foo'.

// Everything is chainable:
emitter
  .on('foo', function() { console.log('foo'); })
  .once('bar', function() { console.log('bar'); })
  .emit('foo') // -> 'foo'
  .emit('bar') // -> 'bar'
  .emit('bar') // ->
  .off('foo')
  .on('foo', function(who) { console.log('another foo for ' + who); })
  .emit('foo', 'you') // -> 'another foo for you'
  .off();
```
