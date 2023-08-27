# 322. Handling body with `multer`
Created Sunday 27 August 2023

The simplest way is to add:
```js
app.use(multer()).single('myFormFieldId');
```

The file is now made available in `req.file`. It's an object containing original filename, mimetype, encoding and also the buffer (collected one). It also has some more metadata of course.

---

If the previous seems to low level, `multer` offers an option to save the file in the filesystem. To do this: we need to add some configs to the middleware generator.
```js
app.use(multer({ dest: 'images_die'}))
.single('myFormFieldId')
```

Now the file will be saved to project_root/images_dir. Fixme: how to pass relative and absolute path here (saving stuff in the code doesn't make sense).

Now `req.file` contains the usual metadata, but instead of the buffer, it now has the file's path.

FYI: the filename is a hash with no extension.

---
