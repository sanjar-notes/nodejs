# 325. Storing files in database
Created Tuesday 29 August 2023

## Don't save files in db
Files should not be stored in a database, they are too big, it's too inefficient to store them in a database and query them from there. 


## What to store in db, then?
The actual file (content) should be stored in a filesystem or some external place (cloud), i.e. "the store".

What should be stored in db - path/link and relevant metadata. i.e. some way to retrieve the file from the "store".

## General idea
The general idea is - "db should store only scalar values and references". 
Advantages:
- lazy loading
- O(1) delete, move
- file sharing via links
- Async create/copy (detached from the request-response flow).
- SPA apps work out of the box - since files are not part of the data req-response flow.
- Lightweight database.


## Get save path in `multer`
The save path is available in `req.file.filename` (or `req.files`)
This works even if `diskStorage` config is used.

We just store it in the db.
```js
// 'add' controller
const product = new Product({
  title: req.body.title,
  imageUrl: req.body.imageUrl || req.file?.path, // here
  description: req.body.description,
  price: req.body.price,
  userId: req.user._id,
});

await product.save();
```

Here's the actual [code (commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/e4f1f98e063d64d4f126f5beb682c0c8c3903e10)
