# Fetching products (multiple)
Created Friday 19 May 2023 at 02:08 am

## Fetching all products (for index page)
```js
class Product {
	// some code here
	
  static fetchAll() {
    const db = getDb();
    return db
      .collection('products')
      .find() // has generator behavior by default
      .toArray() // to avoid? generator behavior of `find` and get back a proper JS array
      .then(products => {
        console.log(products);
        return products;
      })
      .catch(err => {
        console.log(err);
      });
  }
}
```

Syntax for find all:
```js
const prdocust = await db.collection('collection_name').find().toArray();
```

Note: 
1. `next` - `.find` in MongoDB has generator like behavior, and supports a chainable function `.next()` that returns the next "page" (as in pagination). This is relevant since databases could have millions of documents. Syntax: `.find().next()`
2. `toArray` - `.find()` in MongoDB has a chainable function `toArray()`  that converts the response to a proper JS array. This is needed since the default `.find()` is not a proper array.
3. A document returned here has attributes added as simple keys - `Object.keys`, JSON and spread operator work just fine. This is also true for other queries. The `_id` just gets stringified (`.toString(`).

[Add fetch all to Product model - Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/11d58dff5301c53960d70b81fb4f5fccdb056c8b)