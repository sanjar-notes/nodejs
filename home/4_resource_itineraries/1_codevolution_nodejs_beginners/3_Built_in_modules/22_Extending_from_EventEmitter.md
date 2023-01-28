# 22. Extending from EventEmitter
Created Saturday 28 January 2023 at 12:57 pm

## Doing it
We learnt about the events module that returns an "EventEmitter" like class, that has `.emit` and `.on` for emitting and registering events.

There's another way to use the `events` module - by inheriting from it. See the [code](https://github.com/exemplar-codes/codevolution-nodejs/commit/e3e4c991ab34370428f93d84745c8978ee1d0d56).

FIXME: compositions would have worked just as well.

## Why
1. Manage, emit and respond to it's own events.
2.  We can use multiple modules without tight coupling of events.
3. It's like an isolated events chamber. Easier to manage and debug.
4. Event collisions (due to name/symbol) are prevented (which would not be the case if a single EventEmitter instance)
5. Events are cleaned up automatically when the custom class instance dies.

FIXME: learn how this is done systematically

Core modules like `fs`, `streams` and `http` also inherit from the `events` module.