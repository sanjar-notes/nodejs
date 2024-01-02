# fetch available v18
Created Wed Jan 3, 2024 at 12:39 AM

The `fetch` API (like in browsers) is available by default from Node ***v18*** onwards. It's a globally available function. No CLI options or imports needed. 🎉🥳

```js
fetch("https://api.github.com/users/sanjarcode")
  .then((resp) => resp.json())
  .then(console.log);

// runs as is without issues
```