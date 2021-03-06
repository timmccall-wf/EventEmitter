[![Build Status](https://travis-ci.org/mccalltd/EventEmitter.png)](https://travis-ci.org/mccalltd/EventEmitter)

EventEmitter
============

> Simple Interface for Publishing JavaScript Events.


Features
--------

- Operates as a standalone object.
- Easy to make existing classes EventEmitters.
- Available in all JavaScript runtime environments.
- AMD/CommonJS compatible.
- Small set of memorable methods: `on`, `off` and `emit`. That's it.
- Standardized signature for event listeners: `function(sender, args)`.
- Event namespacing.
- Chainable API for easy and elegant use.


Usage
-----

#### Standalone Usage:

```javascript
var emitter = new EventEmitter();
```

#### Add Listeners:

```javascript
var listener = function() {};
emitter.on('event', listener);                 // Add listener for event.
emitter.on('event', listener, { once: true }); // Add one-time listener.
emitter.on('event.namespace', listener);       // Add listener for namespaced event.
```

#### Remove Listeners:

```javascript
emitter.off();                // Remove all listeners for all events.
emitter.off('foo');           // Remove all listeners for event 'foo', including child namespaces.
emitter.off('foo', listener); // Remove a specific listener for event 'foo'.
emitter.off('foo.namespace'); // Remove all listeners for namespaced event.
emitter.off('.namespace');    // Remove all event listeners with 'namespace'.
```

#### Emit Events:

```javascript
var args = { prop: 'value' };
emitter.emit('event');                        // Emit event with no args.
emitter.emit('event', args);                  // Emit event with args.
emitter.emit('event', args, { async: true }); // Emit event asynchronously.
```

#### Chain Everything:

```javascript
emitter
  .on('foo', function() { console.log('foo'); })
  .emit('foo') // -> 'foo'
  .off('foo')
  .emit('foo'); // ->
```

#### Extend Classes With EventEmitter:

```javascript
// Add EventEmitter behaviors to your classes:
function Thing() {}
EventEmitter.extend(Thing.prototype);

// Now 'Thing' acts as an EventEmitter:
Thing.prototype.setName = function(name) {
  this.name = name;
  this.emit('named', { name: name });
};

var thing = new Thing();
thing.on('named', function(sender, args) {
  console.log('The thing is called: ' + args.name);
});
thing.setName('banana');
// -> 'The thing is called: banana'
```
