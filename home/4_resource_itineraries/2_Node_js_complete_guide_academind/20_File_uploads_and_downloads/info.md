continue: https://height.app/OitGt6StRG/T-199

deleteing files is the only thing left. Add it to fs module pages. `fs.unlink` doesn't work for some reason. I may have solved the issue:

---
The same was happening with me.

```js
// doesn't work

// some code
fs.unlink(pathToFile);
```

but
```js
// works fine

// some code
setTimeout(() => { 
  fs.unlink(pathToFile); 
}, 0);
```

My 'some code' part was creating the file using `createWriteStream`. I think the problem is that streams happen in the microtask (high priority queue), and the stream may have ended but the file is still on hold. Doing `setTimeout` moved the `unlink` code to a low priority queue. In other words, the order is guaranteed to be correct now, so it works.

The error I was getting was essentially 'file not found'.


A better, and more sensible way to fix the problem:
```js
const filePath = '';
const fileBeingWrittenStream = fs.createWriteStream(filePath); // whatever

fileBeingWrittenStream.on('end', (err) => {
  if(err) console.log(err);
  else fs.unlink(filePath);
});
```
---