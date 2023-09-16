# 188.2. Getting selected attributes only
Created Saturday 17 June 2023 at 06:28 pm

## What's this, SQL equivalent
The SQL equivalent would be: `SELECT * FROM someTable` vs `SELECT x, y from someTable`.


## 1. With `.find`
To get selected attributes with `.find` - chain the `.project` function with arguments.

```js
db.collection('myCollection')
  .find(/* some code here */)
  .project({ myAttribute: `0_or_1`});
```


## 2. With `.findOne`
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


## More about the projection document (object)
Consider the following model instance (mongodb document).
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
2. Return only - all `1`
	```js
	{ price: 1, title: 1 }

	// return object will be
	// { _id: ..., price: ..., title: ...}
	```
3. Skip - all `0`
	```js
	{ price: 0, title: 0 }
	// return object will be
	// { _id: ..., description: ..., imageUrl: ...}
	```

Note:
- `_id` will be present always, except if it's suppressed explicitly in the projection. `{ _id: 0 }`
- Passing `_id` as `0` or `1` is allowed in both return (all `1`) and skip (all `0`) documents. No error.
- A document should be all `1` or all `0` not both. `_id` is an exception, as discussed.