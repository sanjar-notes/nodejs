## How the 3 relations work in NoSQL
We'll be focusing on MongoDB with Mongoose here.

The 3 relations:
1. One-one: directly embed the whole document.
	- Syntax: `User: { Cart: {...} }`
	- Another way keep the related docs in different collections. 
	- <details><summary>Why this works</summary>Embedding is the simplest way to ensure isolation to a given entity. *Ignorable*: Another way, perhaps more memory efficient, is to store the id, but have the instance be stored in a different collection altogether</details>
1. One-many: use a `ref` inside the many side model. 
	- Syntax: `Proudct: { seller: { ref: 'User' }` 
	- <details><summary>Why this works</summary>Because an attribute can only have a one `ref`, and it doesn't have to be the same for different instances.</details>
3. Many-many: use an array of `ref`s. 
	- An alternative way is to have an explicit junction collection. This is the best practice.
	- <details><summary>Why this works</summary>Since both sides can have multiple connections, embedding (isolation) doesn't make sense - since they've got to be independent. Array because we need to have multiple connections</details>

FIXME: implement and check problems
Problems:
1. 1-1, and 1-N enforcement. There is no built in way to achieve enforcement in MongoDB, since it has no built uniqueness construct (whereas SQL has the `UNIQUE` constraint). This is solved either by custom code, or is done in the business logic.


## Problems with `ref` in Mongoose
1. **Ref** default value - there's no simple way initialize the `ref`s in a model, as their value is meant to be `ObjectId` instead of object. One has to write the code to create the ref instance and attach during creation. [There is a way to achieve this - see StackOverflow](https://stackoverflow.com/a/66630813/11392807). Example:
	```js
	const UserSchema = new Schema({
	  name: { type: String, required: true },
	  email: { type: String, required: true },
	  cart: {
	    ref: "Cart",
	    type: Schema.Types.ObjectId,
	    required: true,
	    default: null,
	  },
	});
	
	const User = mongoose.model("User", UserSchema);

	const SAMPLE_USERS = [
	  {
	    name: "SanjarOne",
	    email: "SanjarOne@gmail.com",
	    cart: { items: [] }, // doesn't work directly now, since ref needs to be an id - simple looping and User.create won't work.
	  },
	];
	```
2. `ref` parts have to be updated specifically - Updating part of a `ref` and saving the parent instance doesn't actually update the ref.
	```js
	const user = ...populate("cart");
	const cart = user.cart;

	const matchingItem = cart.items.find(...);
	matchingItem.quatity +=1; // won't happen

	await user.save();

	await cart.save(); // have to save the ref individually
	```