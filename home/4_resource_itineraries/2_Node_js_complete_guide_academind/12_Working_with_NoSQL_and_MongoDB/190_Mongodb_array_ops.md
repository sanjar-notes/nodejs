## 190. MongoDB array ops
Created Saturday 10 June 2023 at 05:49 pm

## 1. Update element in array

Suppose we have the following situation
```js
const sampleProduct = {
  _id: 'someId...',
  price: '',
  title: '',
  description: '',
  imageUrl: '',

  versions: [{ name: 'name1', title: '' }, { name: 'name2', title: '' }]
};

const productId = ...// given

// goal: update the title field
```

### 1.1 Update element in array - If element position is known
```js
// change the 2nd version, i.e. arr[1]

await db.collection("products")
		.updateOne(
			{ _id: new ObjectId(productId) }, 
			{ $set: { "versions.1.title": 'new title' } }
		);
```

### 1.2 Update element in array - by criteria
There are two steps here:
1. Locate the parent document - same as before, using `_id`
.2. Locate element of nested array by criteria. This has a special notation: `path_to_array.elementProperty: eqValueOrComplexCriteria`. This is added to the locator option (i.e. first argument of `update*`) itself. Memory aid - skip the index in the dot notation.
3. Update the element by using `$` in it's path. `$` refers to the index of the found array, which we don't know of course (since we never fetch the array or the element). The setting is done usually, using `$set`. Of course, we can still update other parts of the document in the same query.
```js
// change the `title` of version whose 'name' is 'name1'

await db.collection("products")
		.updateOne(
			{ _id: new ObjectId(productId), "versions.name": "name1" }, 
			{ $set: { "versions.$.title": 'new title' } }
		);
```

## 2. Append to array -`$push`
This can be done by fetching the document, mutating the array and then `.save()` ing it. But this is expensive and sometimes not practical (if the array is very large).

`$set` won't help here. We need to the `$push` operator for this.
```js
// situation
const myDocument = await db.collection('myCollection').findOne('...');
// myDocumet looks like this
// { _id: ..., scores: [3, 1, 4, 1] }

// goal: to add '5' to this array, without fetching the whole array

// code
await 
	db.collection('myCollection')
	  .updateOne({ _id: myDocument._id }, { $push: { scores: 5 } });
```

```js
// syntax
.updateOne({...}, { $push: { 'path_to_array': value_to_append } })
```
Note: 
- A new array will be created if it doesn't exist. Nice!
- Replace `$push` by `$addToSet` to add element only if doesn't exist.
- Of course, we can push into independent arrays with a single `$push` in the same query. Example:
	```js
	await 
	db.collection('myCollection')
	  .updateOne(
		  { _id: myDocument._id }, 
		  { $push: { scores: 5, fouls: 1 } }
	  );
	// adds `5`, to the scores array, and `1` to the fouls array
	```


## 3. Delete from array - `$pull`
Fetching, mutating and `.save` is a way to do this, but it may be expensive or impractical to do.

`$set` won't help here. We need to the `$pull` operator for this.
```js
// situation
const myDocument = await db.collection('myCollection').findOne('...');
// myDocumet looks like this
// { _id: ..., scores: [31, 12, 43, 17], 
//	fouls: [ { byUser: 'vader', star: 2 }, { byUser: 'thanos', star: 5 }] }


// goal: remove `43` from this array, without fetching the whole array
// code
await 
	db.collection('myCollection')
	  .updateOne({ _id: myDocument._id }, { $pull: { scores: 43 } });


// goal: remove `fouls` element with `byUser` thanos'
// again, it's simple
await 
	db.collection('myCollection')
	  .updateOne({ _id: myDocument._id }, 
		  { $pull: { fouls: { byUser: 'thanos'} } }
	  );
```

```js
// syntax
.updateOne({...}, { $pull: { 'path_to_array': eqValueOrComplexCriteria } })
```
Note:
- Just like with `$push`, deletions can be carried out in independent arrays with a single `$pull` in the same query.


For more ops, checkout https://www.mongodb.com/docs/manual/reference/operator/update-array/