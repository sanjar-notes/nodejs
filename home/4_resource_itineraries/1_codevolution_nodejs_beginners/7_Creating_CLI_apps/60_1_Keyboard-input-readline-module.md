# 60. 1 Keyboard  input readline module
Created Sat Jan 6, 2024 at 1:25 PM

The [readline](https://nodejs.org/api/readline.html) module can be used for reading input into programs.
A promise version [readline/promises](https://nodejs.org/api/readline.html#promises-api) is it's marked experimental. Works by default in v20.

The APIs of the module allow for very granular control if needed - like position of cursor, row/column position, reading a line vs per character reads.

I'll demonstrate two commonly needed interfaces:
1. Read a sentence (until user presses enter). Like C++'s cin.
2. Read single character

## 1. Read sentence (until 'Enter' is pressed)
Since we get back something once, I'm using async-await.

Logic (snippet)
```js
// node v20 ok
/**
 * Take sentence input, until you press 'Enter'
 * Like C++ cin
 *
 * @param {String} message
 * @returns {String}
 */
const prompt = async (message) => {
  const readline = require("readline/promises");
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });
  
  const answer = await rl.question(message);
  
  rl.close(); // stop listening
  return answer;
};
```

Sample program
```js
async function getGitHubName() {
  const username = await prompt("GitHub username: ");
  const resp = await fetch(`https://api.github.com/users/${username}`);
  if (!resp.ok) {
    console.log(
      "Error occurred",
      ",",
      "Code:",
      resp.status,
      ",",
      "Message:" + (await resp.text())
    );
  } else {
    const data = await resp.json();
    const name = data.name;
    console.log("User found. Name:", name);
  }
}

// lameSum();
getGitHubName();
```

## 2. Run code for single character
More like run some code on keypress. This continuously listens for keypresses.
Since each keypress runs some code, I'm using callback.

Example: this is what Metro (React native dev process) runs like - when 'r' is pressed it reloads.

Logic (snippet)
```js
// node v20 ok
/**
 * Continues listening for keypresses, and run code for each keypress
 */
const listenKeyPresses = (callback = (key, data) => console.log({ key, data })) => {
  const readline = require("readline/promises");
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });

  rl.input.on("keypress", callback);
  return rl;
};

listenKeyPresses.example = () => {
  listenKeyPresses((key, data) => {
    const isLetter =
      key.toLowerCase().charCodeAt() >= "a".charCodeAt() &&
      key.toLowerCase().charCodeAt() <= "z".charCodeAt();

    console.log(`\b${key} is a ${isLetter ? "letter" : "Non-letter"}`);
    console.log(data);
  });
};
```

This is very handy when testing, trying something new. Instead of creating a small frontend using HTML, CSS or JS, or setting up Postman. Just use this, setup key press and corresponding code run, and test quickly. Both input + output in the same terminal!