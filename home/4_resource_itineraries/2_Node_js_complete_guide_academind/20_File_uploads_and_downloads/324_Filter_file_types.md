# 324. Filter file types
Created Sunday 27 August 2023

## General filter
This nothing but a way to reject/accept files. Think of it as a hook within multer.

To add: use the `fileFilter` config when setting up multer. The value is a function. See:
```js
const myFileFilter = (req, file, cb) => {
	const isAcceptedOrNot = ...;
	
	return cb(null, isAcceptedOrNot);
};

app.use(multer({ fileFilter: multerFileFilter }).any());
```

If a file was filtered out - `req.file` will be undefined or `req.files` array will not have it (whichever applicable).

Note:
- Of course, `dest` or `diskStorage` configs can be used with this.

## File type filter
This is just a specific case of the filter
```js
const myFileTypeFilter =
  (req, file, cb) => {
    if (file.mimetype === 'image/png' ||
	    file.mimetype === 'image/jpg' ||
	    file.mimetype === 'image/jpeg'
    ) {
      console.log("File accepted");
      return cb(null, true);
    }
    console.log("File rejected");
    cb(null, true);
  };

app.use(multer({ fileFilter: multerFileFilter }).any());
```

[Code (commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/27c5b3730de2bbadf5667eec57a0bd8b8e92f63d)