# 4. Get all collections
Created Sunday 25 June 2023 at 09:14 pm

## Get collections (mongosh)
```mongosh
> use 'some-xyz-database'
> db.getCollectionNames()

# Output: ['orders', 'carts', 'products', 'users' ]
```


## Get collections (Node.js)
Code - `db.listCollections().toArray()`
```js
const db = getDb();

const collectionObjects = await db.listCollections().toArray();
const collectionNames = collectionObjects.map((item) => item.name);
```
Note:
- [getDb code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a0e061c4294ee11922e7d8336372214e16c42c65)

