# Edit and delete product
Created Sunday 7 May 2023 at 10:01 am

Let's add **edit** and **delete** methods to the Product model.
- I have changed the views to consider `_id` now, and un-commented the routes and controllers. [Code](https://github.com/sanjar-notes/nodejs-notes/commit/2739dc9428537250f43c797eff2da927ab37fce5)
- Change the getAdminProduct action to use the new Product model. [Code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/0e45905cb94edea184b2780f67d75d08f7f53596)

```js
const mongodb = require("mongodb");

class Product {
  constructror(id) {
    this.id = id;
    // ... some code
  }
  // ... some code

  update() {
    const idObject = new mongodb.ObjectId(this.id);
    const db = getDb();

    const updatePayload = { ...this };
    delete updatePayload._id; // since this is a string now

    return db
      .collection("products")
      .updateOne({ _id: idObject }, { $set: updatePayload })

      .then((result) => {
        console.log(result);
      })
      .catch((err) => {
        console.log(err);
      });
  }

  delete() {
    const idObject = new mongodb.ObjectId(this.id);
    const db = getDb();

    return db
      .collection("products")
      .deleteOne({ _id: idObject })

      .then((result) => {
        console.log(result);
      })
      .catch((err) => {
        console.log(err);
      });
  }
}
```

- **Update** (`updateOne()`)takes two arguments
  1.  A query filter, example - id or conditions
  2.  Second is an object, which should atleast have `$set` key with the update payload. MongoDB does "merged updation" by default. It's ok to send `_id`, but it must be an object not a string and must be the same as the existing one (FIXME check that it must be same or not).
- Id: having `_id` in the `updateOne` payload is optional. If present, it should of type `ObjectId`, otherwise mongodb will throw an error.
- Delete is simple, there are two modes - `deleteOne()` and `deleteMany()`.

[Edit Product - code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/bc69c7c8498808f173ba6216ebc437af247e330e)
[Delete Product - code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/b4f51b381f6abb037125121b543579a8707c5436)