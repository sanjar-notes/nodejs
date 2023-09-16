# Updating attributes, nested paths remotely
Created Saturday 10 June 2023 at 04:45 pm

By remote, I mean we never fetch the document from the DB. We just make a call to update.

## 1. Update some (or just one) attribute
Nothing new here. Just that `updateOne` does "merged updation", so partial attributes are OK.
```js
const sampleProduct = {
  _id: 'someId...',
  price: '',
  title: '',
  description: '',
  imageUrl: '',
};

const productId = ...// given

// goal: update the 'description' field, without fetching Product from db

await db.collection("products")
		.updateOne(
			{ _id: new ObjectId(productId) }, 
			{ $set: { "description": 'new description', title: 'new title' } }
		);
```


## 2. Update nested/embedded attribute
Use dot path as key
```js
const sampleProduct = {
  _id: 'someId...',
  price: '',
  title: '',
  description: '',
  imageUrl: '',

  seller: { name: '', phoneNumber: '' }
};

const productId = ...// given

// goal: update the seller 'phoneNumber' field, without fetching Product from db

await db.collection("products")
		.updateOne(
			{ _id: new ObjectId(productId) }, 
			{ $set: { "seller.phoneNumber": 'new number' } }
		);
```