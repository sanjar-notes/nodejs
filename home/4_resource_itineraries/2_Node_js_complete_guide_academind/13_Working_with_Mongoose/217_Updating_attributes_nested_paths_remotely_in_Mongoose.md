# 217. Updating attributes, nested paths remotely in Mongoose
Created Saturday 10 June 2023 at 04:45 pm

This is almost the same as with MongoDB (vanilla).

Of course, one can use the `findByIdAnd*` to avoid creating ObjectId, but the second argument remains the same.

Note: Avoid using `MyModel.update()` since it skips schema validations. MongoDB

## 1. Update some (or just one) attribute
We've already seen this, using instance with `.save`.

The following is a way to update without the need for an instance.
```js
// consider the model schema
const productSchema = new mongoose.Schema({
  price: { type: Number, required: true },
  title: { type: String, required: true },
  description: { type: String, required: true },
  imageUrl: { type: String, required: true },
});

const productId = ...// given

// goal: update the 'description' field, without fetching Product from db

await Product.findByIdAndUpdate(productId, 
	{
	  $set: { "description": 'new description' }
	}
);
```


## 2. Update nested/embedded attribute
```js
// consider the model schema
const productSchema = new mongoose.Schema({
  price: { type: Number, required: true },
  title: { type: String, required: true },
  description: { type: String, required: true },
  imageUrl: { type: String, required: true },

  user: { name: String, email: String, required: true },
});

// goal: update the email field

const productId = ...// given

await Product.findByIdAndUpdate(productId, 
	{
	  $set: { "user.email": 'new email' }
	}
);
```


## 3. Update array item
```js
// consider the model schema
const productSchema = new mongoose.Schema({
  price: { type: Number, required: true },
  title: { type: String, required: true },

  versions: [{ name: String, description: String }],
});
const productId = ...// given
```

### 3.1 If element position is known
```js
// goal: update the second version's description
await Product.findByIdAndUpdate(productId, 
	{
	  $set: { "versions.1.description": 'new descr' }
	}
);
```
### 3.2 Update element by criteria
```js
// Case 2: by criteria
const versionId = ;// given
// goal: update the description of a version with given id
await Product.updateOne(
	{ 
	  _id: new ObjectId(productId), 
	  "versions._id": new ObjectId(versionId)
	},
	{
	  $set: { "versions.$.description": 'new descr' }
	}
);
```


## 4. Array ops (should be on a different page, FIXME)
MongoDB operators (`$push`, `$pull`, `$addToSet`) work fine. Already noted [in the MongoDB section](obsidian://open?vault=nodejs-notes&file=home%2F4_resource_itineraries%2F2_Node_js_complete_guide_academind%2F12_Working_with_NoSQL_and_MongoDB%2F190_Mongodb_array_ops).

Mongoose does provide methods, provided you have the array instance (fetched, that is). See https://mongoosejs.com/docs/api/array.html