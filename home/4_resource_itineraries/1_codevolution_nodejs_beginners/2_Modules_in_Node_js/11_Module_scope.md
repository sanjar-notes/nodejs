# Module scope
Created Tuesday 24 January 2023 at 12:44 am

## Experiment
Let's create two modules:
1. batman.js
	```js
	const superHero = "Batman"
	console.log(superHero);
	```
2. superman.js
	```js
	const superHero = "SuperMan";
	console.log(superHero);
	```
In a third (main) file `index.js`
```js
require('./batman.js')
require('./superman.js')
```

What happens when we run `index.js`? Specifically, what is the value of `superHero`?
The output is:
```sh
Batman
Superman
```

Result: Both names are logged, **there are no collisions, overrides or errors**.


## Module scope
Each module has it's own scope. Module scope is internally implemented using the IIFE(Immediately Invoked Function Execution) pattern. i.e. All code inside a module is run actually run inside an IIFE.

The experiment's code can be edited to an equivalent form in a single file:
```js
(function() => {
 	const superHero = "Batman"
	console.log(superHero);
})();

(function() => {
	const superHero = "SuperMan";
	console.log(superHero);
})();
```

So, before a module is exported, Node.js wraps all it's code in an IIFE, effectively creating the "module" scope. This is good for two reasons:
1. We don't have to worry about conflicting variable or function names.
2. We don't have to worry about unintended reads/writes to variables from other modules.
3. This is proper encapsulation.
4. Re-usability remains unaffected.


## Summary
- Each loaded module in Node.js is wrapped inside an IIFE, creating a private scoping of code.
- IFFE allows us to repeat identifiers without any conflicts.