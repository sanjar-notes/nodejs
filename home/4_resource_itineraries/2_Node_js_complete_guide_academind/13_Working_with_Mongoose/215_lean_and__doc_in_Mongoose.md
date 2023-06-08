# 215. `.lean()` and `._doc` in Mongoose
Created Thursday 8 June 2023 at 09:20 am

## An annoying default
Mongoose has an annoying default - each documents returned in a query response don't have their attributes attached as keys. See this for clarity:
```js
// printing the response (looks fine)
product = {
  _id: new ObjectId("64814fc6b09a7e369573ad6d"),
  price: 1000,
  title: 'A laptop',
  description: 'A performant, quiet laptop',
  imageUrl: 'https://upload.wikimedia.org/wikipedia/commons/b/bb/Alienware_M14x_%282%29.jpg',
  userId: new ObjectId("64814fc6b09a7e369573ad69"),
  __v: 0
}

// but, observe the keys (Object.keys(product))
[ '$__', '$isNew', '_doc' ] // wtf? attributes are absent

// However, direct (dot) access on the object will work, despite key being absent
product.title
```

Title is simple and direct attribute of Product, still it's absent in keys array. Weird.

The reason behind this is that a Mongoose document object is more complex than a plain object, and the people behind Mongoose were OK with keys not being directly available - for efficiency's sake.


## Accessing POJO equivalent (`.doc` property)
One can still access the product as a POJO, easily, by using `._doc` property - this has all the keys as expected.
```js
product._doc == 
{
  _id: new ObjectId("64814fc6b09a7e369573ad6d"),
  price: 1000,
  title: 'A laptop',
  description: 'A performant, quiet laptop',
  imageUrl: 'https://upload.wikimedia.org/wikipedia/commons/b/bb/Alienware_M14x_%282%29.jpg',
  userId: new ObjectId("64814fc6b09a7e369573ad69"),
  __v: 0
} 

Object.keys(product._doc) ==
[ '_id', 'price', 'title', 'description', 'imageUrl', 'userId', '__v' ]
```


## Keeping it simple (the `.lean()` escape hatch)
Doing `._doc` in business logic feels like a bad idea.
Mongoose provides a way to directly get documents with all properties. The entities returned in this case are POJOs.

To do so, just do a `.lean()` at the end of a query. Of course, this applies only to READ queries.

```js
const myProduct = await Product.findOne(); // weird, have to use .doc
const myProducts = await Product.find(); // weird, have to use .doc on each element

// simpler
const myProduct = await Product.findOne().lean(); // simple
Object.keys(myProduct); // contains attributes as expected

const myProducts = await Product.find().lean();
Object.keys(myProduct[0]); // contains attributes as expected
```

Note: 
- `.lean()` is very useful, especially when for client side APIs and serializers.
- Using `.lean()` does have a disadvantage - the returned entities are POJOs, and therefore lack the methods and properties a Mongoose object would have.