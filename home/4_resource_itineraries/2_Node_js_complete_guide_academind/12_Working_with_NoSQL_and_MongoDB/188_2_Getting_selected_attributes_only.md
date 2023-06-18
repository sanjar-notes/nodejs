# 188.2. Getting selected attributes only
Created Saturday 17 June 2023 at 06:28 pm

## What is this
The SQL equivalent would be: `SELECT * FROM someTable` vs `SELECT x, y from someTable`.


## With `.find`
To get selected attributes with `.find` - chain the `.project` function with arguments.

```js
db.collection('myCollection')
  .find(/* some code here */)
  .project({ myAttribute: `0_or_1`});
```


## With `.findOne`
To get selected attributes with `.findOne` - pass the projection document as under `projection` attribute, in the config (second) argument.

```js
db.collection('myCollection')
  .findOne(
    { /* some code here */ },
    {
	  projection: { myAttribute1: `0_or_1` }
    }
  )
```
Note: Chaining to `.findOne` won't work.


## The projection document (object)
Consider the following document.
```js
{
  title: '',
  price: '',
  description: '',
  imageUrl: '',
}
```

There are 3 simple variations:
1. Default - `{}`. Return all. This is the same as if projection wasn't used.
2. Return only - all ones
	```js
	{ price: 1, title: 1 }

	// return object will be
	// { _id: ..., price: ..., title: ...}
	```
3. Skip - all zeros
	```js
	{ price: 0, title: 0 }
	// return object will be
	// { _id: ..., description: ..., imageUrl: ...}
	```

Note:
- `_id` will be present always, except if it's suppressed explicitly in the projection. `{ _id: 0 }`