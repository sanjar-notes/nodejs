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
[Code (commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/377fd1dd1fcca8be4837f8995b4597a2ccf0905f)

Note:
1. If there are multiple files, these functions are called for all of them (depending on `multer().array`, `multer.any()` etc of course). Expected behavior. [Code](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/06b4fde4beb384f5a93c65e6951a83352334233d)

FIXMEs - 
1. how to prevent saving, i.e. check the file for harmful content. Is there a function like `rejectFile() => bool`
2. delegate save to a web service - how to set destination to a URL, or access a hook multer defines so we can use a cloud service SDK (to save file on the cloud), instead of on disk.
	1. Is this irrelevant?
	2. If an error occurs from the cloud service, how to relay errors back to Express middleware chain (since process is async and we don't have access to `next`)
