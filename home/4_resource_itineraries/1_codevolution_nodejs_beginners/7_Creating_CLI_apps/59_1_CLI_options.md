# 59. CLI options
Created Thursday 9 February 2023 at 02:24 am

## `process.argv`
- Returns command line text (used to run the script) as an array. No need to import.
- Removes spaces, appropriately (i.e. will retain space in bash strings)
- CLI commands and `node` commands give same* output. \*node and file path is different, options are the same

Example output:
```js
console.log(process.argv);

// node index.js
[
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/node',
  '/home/sanjar/MEGAsync/Work_Section/study_dir/cse_dir/app_development/web_dev/projects/codevolution-nodejs/sanjarcode-first-node-cli/index'
] //--- 1 

// sanjarcode-pokedex
[
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/node',
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/sanjarcode-pokedex'
] //--- 2

// sanjarcode-pokedex hello
[
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/node',
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/sanjarcode-pokedex',
  'hello'
] //--- 3

// sanjarcode-pokedex --pokemon=mew
[
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/node',
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/sanjarcode-pokedex',
  '--pokemon=mew'
] //--- 4

// sanjarcode-pokedex 'hello world'
[
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/node',
  '/home/sanjar/.nvm/versions/node/v18.13.0/bin/sanjarcode-pokedex',
  'hello world'
] //--- 5
```


## (Optional) - "yargs" package to parse options
"yargs" parses CLI options into an object. It:
- Exposes a function.
- Accepts `process.args` as input.
- Returns an object with where key `argv` is an object, with option name as key and option value as value.
- Assumes CLI options are passed as `--optionName=valueText`, space separated of course.

Example (assuming, `yargs` package is installed:
```js
const yargs = require('yargs');
const myOptions = yargs(process.argv).argv;

// with CLI options `--pokemon=mew`
console.log(myOptions.pokemon); // 'mew'

// with CLI options `--darkmode=true`
console.log(myOptions.darkmode); // 'true'
```

[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/059f0b132c3b37085c7f3805a5cbe30eb7e93cca)