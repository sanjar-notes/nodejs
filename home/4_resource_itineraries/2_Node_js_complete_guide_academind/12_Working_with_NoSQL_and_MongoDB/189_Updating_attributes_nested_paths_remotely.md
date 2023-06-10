# Updating attributes, nested paths remotely
Created Saturday 10 June 2023 at 04:45 pm

## 1. Update some (or just one) attribute
We've already seen this, using instance with `.save`. The following is a way to update without the need for an instance.
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
Use path
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