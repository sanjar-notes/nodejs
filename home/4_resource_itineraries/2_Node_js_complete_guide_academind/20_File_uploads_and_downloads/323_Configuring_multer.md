# 323. Configuring multer
Created Sunday 27 August 2023

## Can't access `req`
Currently, the most config we have done is to use the `dest` option for specifying the destination. <details><summary>But this isn't enough</summary> the destination (or logic of) is static and any rename logic will also be static, since we don't have `req` </details>


## Accessing `req` with `diskStorage`
In addition to the simple `dest`, multer accepts a much more powerful config. This config has to be created in a certain format, the config key is 'storage'. Code:
```js
const multer = require('multer');

// create the config
const myMulterConfig = multer.diskStorage({
  /**
  * @param {Function} cb - callback that communicates value to multer. First param is an error. Pass null if there's no error. It's like 'next' (express middleware param)
  *
  * @param {Object} file - object containing metadata about the file, including buffer (if applicable)
  *
  * @param {Object} req Request object from Express.js

  */
  destination: (req, file, cb) {
    cb(null, 'images-dir'); // error, value
  },
  filename: (req, file, cb) {
    cb(null, 'file-name');
  }
});

// use in middle setup
app.use(
  multer({ storage: myMulterConfig })
  .single('myFormFieldId')
);
```
