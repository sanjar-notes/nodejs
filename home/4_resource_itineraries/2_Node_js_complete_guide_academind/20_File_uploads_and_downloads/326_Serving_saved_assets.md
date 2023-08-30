# 326. Serving saved assets
Created Tuesday 29 August 2023

## Why?
Since we only stored 'links' for images, we need to respond with files (content) when they are requested.
This can be done easily using express's static middleware functionality. Code:
```js
app.use(express.static('multer-uploads'));
```


## Approach 1 - getting the saved path
How to get the 'path' (since we're using `diskStorage` criteria)? 
It is available in `req.file.path`
The 'save' controller will change like this:
```js
const product = new Product({
  title: req.body.title,
  imageUrl: req.body.imageUrl ||  req.file?.path,
  description: req.body.description,
  price: req.body.price,
  userId: req.user._id,
});

await product.save();
```


### Express static doesn't work (fix)
This won't work, since Express ignores the first path (directory) and finds file inside it. So we need to trim this path before saving the path to the database.
```
projectRoot/multer-uploads/myImage.jpg (file system) --> myImage.jpg (database)
```

The middleware `app.use(express.static('multer-uploads'))`will work now, answering to URLs like `http://localhost:3000/multer-uploads/myImage.jpg`.
```js
app.get("/multer-uploads/:fileName", (req, res, next) => {
  res.sendFile(path.join(__dirname, "multer-uploads", req.params.fileName));
});
```
[Code(commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/621b530e03a3e0d43e2078f708e3b96d54766dee)

A little complex, right?

## Approach 2 - save unique name, without path, (simplifies approach 1)
Alternatively - we can omit the folder path from the database entirely - save each asset (image) with a unique name. This way, we can migrate to the cloud or change the `multer-uploads` folder without changing the middleware.

Example URL (will now look like):
```html
<img src="http://localhost:3000/myImage.jpg" />
<!-- simple src, no mention of directory or path-->
```

'save' controller (simple):
```js
// no mention of path, but make sure `filename` is unique
const product = new Product({
  title: req.body.title,
  imageUrl: req.body.imageUrl ||  req.file?.filename,
  description: req.body.description,
  price: req.body.price,
  userId: req.user._id,
});

await product.save();
```

Asset response middleware (complexity contained):
```js
// this can be as simple or complex as you want

// simple
app.use(express.static('multer-uploads'));

// complex - if needed
app.get("/multer-uploads/:fileName", (req, res, next) => {
  res.sendFile(path.join(__dirname, "multer-uploads", req.params.fileName));
  // or call an external service if you want
  // or use a cloud SDK
});
```

&nbsp;  
[Code(commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/d3998fdee97ab700ffb503229f8f17dd0e9bc187)
note: I ignored file access authorization, server code access here to keep it simple.