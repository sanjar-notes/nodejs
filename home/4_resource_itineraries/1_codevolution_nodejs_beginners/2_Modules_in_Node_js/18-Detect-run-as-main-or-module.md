---
tags:
  - main
  - direct
  - module
  - direct-vs-module
  - detect
---
# 18. Detect run as main or module
Created Mon Jan 1, 2024 at 1:11 PM

*There's a simple way in Python to know if current file is being run directly or as an import, using the `__main__` variable. Any such way in Node.js?*

Yes, there is.

## CommonJS
```js
if (require.main === module) {
  console.log('This file is being run directly.');
} else {
  console.log('This file is being imported as a module.');
}
```


## ESM
```js
// mainModule.mjs

if (import.meta.url === `file://${process.argv[1]}`) {
  console.log('This ESM module is being run directly.');
} else {
  console.log('This ESM module is being imported as a module.');
}
```