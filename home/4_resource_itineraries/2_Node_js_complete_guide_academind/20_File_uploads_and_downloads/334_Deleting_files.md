# 334. Deleting files
Created Thursday 31 August 2023

## `fs.unlink`
The fs modules's `unlink` function helps. Essence:
```js
/**
* @param {String} path
* @param {Function} callback with first arg being error (null if success)
* 
*/
function unlink(path, callback = (err) => {}) {}
```


## Usage
```js
const fs = require('node:fs');

// 1. General
fs.unlink(pathToFile, (err) => {});


// 2. in Express
app.use((req, res, next) => {
  // code
  
  fs.unlink(pathToFile, (err) => { if(err) next(err); });
  // doesn't trigger error mw if null (success), works for async mws too.
})


// 3. in Express if deletion result is not needed (fire-n-forget)
app.use((req, res, next) => {
  // code
  
  fs.unlink(pathToFile);
})
```


## A minor bug I faced with stream and piping (ignorable)
The problem:
```js
app.use("/get-pdf", async (req, res, next) => {
  // feature: generate PDF on disk, send it and then delete the generated file.
  
  const pdfDoc = new PDFDocument();
  const mySaveFileStream = createWriteStream(filePath);
  
  pdfDoc.pipe(mySaveFileStream);
  pdfDoc.pipe(res);

  // PDF gen code

  pdfDoc.end(); // automatically fires `res.end()`

  // I wish to remove the file now
  fs.unlink(fileName); // FOCUS 1: does not work!!
});
```

The fix:
```js
...
  pdfDoc.pipe(mySaveFileStream);
  pdfDoc.pipe(res);

  res.on('close', () => { fs.unlink(fileName); });

  // PDF gen code

  pdfDoc.end();
});
```

Other hacky fixes (that work):
```js
  // pdf gen code
  pdfDoc.end();
  setTimeout(() => { fs.unlink(pathToFile); }, 0); // hack 1
  nextTick(() => { fs.unlink(pathToFile); });      // hack 2
```


Code - https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/069100033b3d7a4bb66ce92205b8c00dd2a51d93