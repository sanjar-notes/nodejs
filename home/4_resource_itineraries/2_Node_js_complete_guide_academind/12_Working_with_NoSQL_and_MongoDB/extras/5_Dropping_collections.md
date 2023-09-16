# 5. Dropping collections
Created Sunday 25 June 2023 at 09:25 pm

## Mongosh
```sh
> use 'some-xyz-database'
> db.myCollectionName.drop()
```


## Node.js
```js
const { getDb } = require("path_to_util");
await db.collection('myCollection').drop();
```
Note:
- [getDb code](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a0e061c4294ee11922e7d8336372214e16c42c65)


## Delete all collections (Node.js)
Get list of collection and drop each one individually.

Example code:
```js
const db = getDb();

const collectionObjects = await db.listCollections().toArray();
const collectionNames = collectionObjects.map((obj) => obj.name);

Promise.all(
  collectionNames.map(async (collectionName) => {
	console.log("Dropping collection", collectionName);
	await db.collection(collectionName).drop();
  })
);
```
[Code](https://github.com/exemplar-codes/online-shop-sessions-and-cookies/commit/12ca720d866888ab02d996ea78a4d4a08e1c7e04)