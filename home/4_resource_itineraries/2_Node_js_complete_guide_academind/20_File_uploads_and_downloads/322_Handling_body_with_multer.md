# 322. Handling body with `multer`
Created Sunday 27 August 2023

Multer docs: https://www.npmjs.com/package/multer
Multer article (LogRocket): https://blog.logrocket.com/multer-nodejs-express-upload-file/
## Using multer - add a middleware
```js
app.use(multer().single('myFormFieldId'));
```

Accept single file having fieldname. File available in `req.file`.

It's an object containing original filename, mimetype, encoding and also the buffer (collected one). It also has some more metadata of course.

note: 
- Multer parsed "body" doesn't contain field names from `req.body` that it's adding to `req.file` (or `req.files`). memAid: `req.body` for text/unaccepted fields and `req.file`/`req.files` for files. See [code](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/b5960a4d6a1e0fc73e5909f14b56835dd0242f4d) 


## Other functions `multer().`
- `.any()` - accept all files. `req.files` is an array of files.
- `.none()` - accept only text fields. Throws error if file is uploaded.
- `.array(['fieldName1, 'fieldName2'], [=maxCount])`. `req.files` has the array of files.
- `.fields` - accept a mix of files. `req.files`. Most complicated.


## File to be stored at location
In the example above (`.single`), `req.file.buffer` had the file content.
This is too low level, so `multer` offers an option to save file in the filesystem. 

Doing this is simple: add the `dest` config in the middleware setup.
It's a path (string).
```js
app.use(
  multer({ dest: 'images_dir'})
  .single('myFormFieldId')
)

// file will be saved at project_path/images-dir/
```

Now the file will be saved to project_root/images_dir.

Now `req.file` contains the usual metadata, but instead of the buffer, it now has the file's path.

notes:
- Saved filename is a hash with no extension.
- All kinds of path are supported for 'dest':
	1. simple string ('xyz') - files will be stored at `project_root/xyz/`
	2. absolute paths are supported (store anywhere on the computer)
	3. relative paths are supported (w.r.t project level)