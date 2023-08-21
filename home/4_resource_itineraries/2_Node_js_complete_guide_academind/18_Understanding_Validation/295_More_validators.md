# 295. More validators
Created Tuesday 22 August 2023

## Simple validators
1. Equal to - `.equals(idealValue)`
2. String without space - `isAlphanumeric()` - `[0-9][a-z][A-Z]`
3. Check if string `isString()` - string or not. `23` is an error, `"23"` is fine.
4. Number within range: `isFloat({ min, max })`
	- Unlike the name, works fine with integers.
	- Works fine with strings (number as strings) too.
5. Integer within range:  `isInteger({ min, max })` - like isFloat, but strict about value being an integer.
	- Works fine with strings (number as strings) too.
6. Check if number - `isNumeric()` - checks if string/number is numeric.
	- Works fine with strings (number as strings) too.

Example:
```js
.check().isFloat({ max: 12 })
```