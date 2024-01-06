# 60. 2 CLI prompts
Created Thursday 9 February 2023 at 03:38 am

[inquirer](https://github.com/SBoudrias/Inquirer.js#readme) is an awesome package to create interactive CLIs.

It:
- Takes in input interactively (i.e. waits for input)
- is Promise based
- Accepts an array of prompts, returns an object containing responses.

Code should suffice
```js
const inquirer = require("inquirer");
const prompt = inquirer.createPromptModule();

prompt([
  {
    type: "input", // for text input. More: checkbox, confirm, editor
    name: "pokemon",
    message: "Enter a pokemon name to view its first 5 moves",
  },
]).then((answerObj) => {
  const pokemonName = answerObj.pokemon; // "name" becomes the key
  printFiveMoves(pokemonName);
});
```
[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/fc0fd51858b9a44fbbbf0c3d7117bfe28b83a484)

- It has several default prompts and is also highly configurable.
- Lots of plugins are available.