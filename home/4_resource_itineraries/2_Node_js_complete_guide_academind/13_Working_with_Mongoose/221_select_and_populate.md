## Getting only some attributes - `.select()` (220)
Syntax
```js
.find(/* someId */) // until now. This is like SELECT *, i.e. get all attributes


.find(/* someId */)
.select('key1 key2 ke3.nestedKey3 -key3')

// can be used with .findOne or .findById too
.findOne(/* some criteria */)
.select('key1 key2 ke3.nestedKey3 -key3')
```

Example:
```js
await Product.find()
	.select('name price -_id')
```

Note:
- Excluded attributes (keys) don't appear, even if `.lean` is used.
- Just like with MongoDB projections - the `_id` is always fetched, except if excluded explicitly.
- Just like with MongoDB projections - only inclusions or exclusions (but not both) can be present as argument. `-_id` is an exception to this rule (i.e. both `"title price -_id"` works fine).


## Eager loading aka `.populate()` (220)
In Mongoose, Documents associated with `ref` attribute are lazy loaded, i.e. by default, accessing them will just return the `_id`, instead of the whole document.

The "population" constructs in Mongoose help with eager loading. The simplest way is to use the `.populate()` method, which returns the whole docs for the ref attributes, instead of just `_id`s.

Example:
```js
// Product has a 'User' ref called 'userId'

const myProducts = await Product.find(productId);
const sellers = myProducts[0].userId; // ObjectId


// eager loading
const myProducts = await Product.find(productId).populate('userId');
const seller = myProducts[0].userId; // object
```

Syntax:
```js
.find().populate('key1 key2 key3 key4.nestedKey')
// Note: nested keys can also be targeted for eager loading
```

<br />

`.populate()` supports attribute selection within it
```js
Product.find()
	.populate('userId', 'name'); 
// eager load the userId object, but exclude it's 'name' attribute


// same as (FIXME, check once)
Product.find(/* ... */)
	.populate('userId')
	.select('-userId.name')
```

Of course, this works with any `find*` function.