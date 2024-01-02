# 21. Events module
Created Saturday 28 January 2023 at 12:23 pm

The events module is meant to help with the event driven programming paradigm, that's very popular in the Node.js ecosystem since Node.js focuses on non-blocking execution.

In simple words, suppose your code (that you're going to write) is going to be used as part of an external entity. And your code has the responsibility to let the external entity know when certain events have occurred within your code. The external entity is most probably a high level system like a UI or or even a script, and your code is probably some low-level/domain-specific code being used as a system code or external library.

This module, will help you write such a "piece of code", i.e. a JS module that emits events.

## Importing the events module
- The module exposes a class.
- This class is usually named "EventEmitter" instead of "Events". This is optional since the name does not matter in CommonJS.
- To start working with events, create an instance. This instance can be used to register and emit events.
```js
const EventEmitter = require("node:events");
const emitter = new EventEmitter(); // constructor syntax, no arguments needed by default

// you'll export tangible functions, object etc, like usual
//
// you'll also export the `emitter` (above), so the importing file can add events that it wishes to listen for, i.e. the import module will subscribe to your module
```

Note (FIXME - gpt ok, makes sense, check again): 
- If only one instance of this module (which emits events) is going to be used, the above is fine.
- if multiple instances of the module are needed, just create a class (or use factory function pattern) that contains both the work code, as well as the emitter. This way we don't generate any data in the module, and data and emitter instances belong to the usage scope, allowing for multiplicity with isolation, and safety from shared state or Node's cache on first run limitation.

## Registering and emitting events
The class has the two functions:
1. `.on(eventNameOrSymbol, callbackFn)` - register a callback to respond to events (i.e. it will run when the event occurs).
2. `.emit(eventNameOrSymbol, [arg1, arg2])` - emit an event. The optional arguments are passed as is to the registered callback function, they are data associated with the event.
```js
const EventEmitter = require("node:events");
const emitter = new EventEmitter();


emitter.on("order-pizza", () => { console.log("Order placed"); });

emitter.emit("order-pizza");
```
- Event identifiers can be strings or `Symbol`.
- A "listener" a short term for "registered callback for an event".

Note (optional - not part of the course): 
- `.once` - used to register a callback that executes only the first time (same syntax as `.on`)
- `.addListener` is an alias of `.on`
- `.removeListener(eventNameOrSymbol, callback)` - removes an existing listener for the given event. Of course, the callback cannot be an anonymous function here, since function comparison is intractable. Note: this removes only one instance of the listener - i.e. it won't remove duplicates if they exist.
- `.removeAllListeners(eventNameOrSymbol)` - remove all registered callbacks for a given event.
- `.eventNames()` - returns an array of all events.

## Examples and patterns
### 1. Pass data with an event - callback arguments
```js
emitter.on("order-pizza", (instructionsText) => {
  console.log(`Order received! Baking a pizza`);
  if (instructionsText) console.log(`Instructions: ${instructionsText}`);
});

emitter.emit("order-pizza", "Add extra cheese");
```
### 2. Pass multiple data with an event - callback arguments
```js
emitter.on("order-pizza", (instructionsText, sides) => {
  console.log(`Order received! Baking a pizza`);
  if (instructionsText) console.log(`Instructions: ${instructionsText}`);
  if (sides) console.log(`Sides: ${sides}`);
});

emitter.emit("order-pizza", "Add extra cheese", "French fries and soda");
```
### 3. Multiple callbacks can be registered for the same event
```js
emitter.on("order-pizza", () => console.log("Callback 1 called"));
emitter.on("order-pizza", () => console.log("Callback 2 called"));

emitter.emit("order-pizza");
```
### 4. Emitting events from callbacks is allowed
Nothing unusual, but this can be hard to reason about in a large codebase. There's possibility of inadvertent infinite loops. Also, since separations of concern in software is preferred, the emitting module most likely doesn't call main "events" on its own.
```js
emitter.on("pizza-ready", () => console.log("Order is ready!"));
emitter.on("order-pizza", () => {
  console.log("Order received!");
  // make pizza code here
  emitter.emit("pizza-ready");
});

emitter.emit("order-pizza");
```


## Non-blocking nature of events
- Registering an event is a non-blocking operation, obviously.
- Emitting events is a blocking operation, since it triggers the registered callbacks to run. *There is a possibility that callbacks themselves use promises, but anyway, atleast the queueing up is synchronous*.
Example:
```js
console.log("Sync 1");
emitter.on("order-pizza", () => console.log("Callback 1 called"));
console.log("Sync 2");
emitter.on("order-pizza", () => console.log("Callback 2 called"));
console.log("Sync 3");
emitter.emit("order-pizza", "Add extra cheese", "French fries and soda"); // blocking
console.log("Sync 4");


/* Output

Sync 1
Sync 2
Sync 3
Callback 1 called
Callback 2 called
Sync 4

*/
```