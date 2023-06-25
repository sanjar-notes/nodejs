## 221. `.select` and `.populate`

## `.select` - get only some attributes
Syntax:
```js
.find(/* someId */) // until now. This is like SELECT *, i.e. get all attributes


.find(/* someId */)
.select('key1 key2 ke3.nestedKey3 -_id')

// can be used with .findOne or .findById too
.findOne(/* some criteria */)
.select('key1 key2 ke3.nestedKey3 -_id')
```

Example:
```js
await Product.find()
	.select('name price -_id')

await Product.find()
	.select('-name -price')
```

Note:
- Excluded attributes (keys) don't appear, even if `.lean` is used.
- Just like with MongoDB projections - the `_id` is always fetched, except if excluded explicitly.
- Just like with MongoDB projections - only inclusions or exclusions (but not both) can be present as argument. `-_id` is an exception to this rule (i.e. both `"title price -_id"` works fine).


## `.populate` - eager load
In Mongoose in a give document, the documents associated with `ref` attributes are lazy loaded, i.e. accessing them will just return the `_id`, instead of the whole document.

The "population" construct in Mongoose help with eager loading. The simplest way is to use the `.populate()` method, which returns the whole doc for a ref attributes, instead of just `_id`.

Example:
```js
// Product has a 'User' ref called 'userId'

const myProduct = await Product.findById(productId);
const seller = myProduct.userId; // ObjectId


// eager loading
const myProduct = 
	  await Product.findById(productId).populate('userId');
const seller = myProduct.userId; // an object
```

Syntax:
```js
MyModel.find().populate('key1 key2 key3 key4.nestedKey')
// Note: nested keys can also be targeted for eager loading
// Note2: works with all query methods, not just `.find`
```


## Eager load but only some attributes - populate with select
`.populate()` supports attribute selection within it ('select' as second argument)
```js
Product.find()
	.populate('userId', 'name'); 
// eager load the userId object, but exclude its 'name' attribute


// chaining (a potential equivalent), DOES NOT WORK
// not an error, this is valid
// but populated fields cannot be 'select'ed using .select, they are immune
Product.find(/* ... */)
	.populate('userId')
	.select('-userId.name')
```

Of course, `.populate` works with any `find*` function.

Note:
- Chaining `.select` and `.populate` is not an error, but populated fields won't be affected by the `.select`. Code already shown above.
- Populating an attribute after `.select` will still cause the population to be performed. `.populate` works even if `.select` has excluded the attribute being populated.