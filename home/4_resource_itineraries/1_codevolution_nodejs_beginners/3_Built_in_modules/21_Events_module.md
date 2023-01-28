# 21. Events module
Created Saturday 28 January 2023 at 12:23 pm

The events module is meant to help with the event driven programming paradigm, that's very popular in the Node.js ecosystem since Node.js focuses on non-blocking execution.


## Importing the events module
- The module exposes a class.
- This class is usually named "EventEmitter" instead of "Events". This is optional since the name does not matter in CommonJS.
- To start working with events, create an instance. This instance can be used to register and emit events.
```js
const EventEmitter = require("node:events");
const emitter = new EventEmitter(); // constructor syntax, no arguments needed by default
```


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
Event identifiers can be strings or `Symbol`.


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
Nothing unusual, but this can be hard to reason about in a large codebase.
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
- Emitting events is a blocking operation, since it triggers the registered callbacks to run.
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