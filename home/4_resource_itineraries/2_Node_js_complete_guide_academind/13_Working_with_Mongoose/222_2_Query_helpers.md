# 222.2. Query helpers
Created Sunday 18 June 2023 at 07:55 pm

One can add custom functions to be chained to query methods (`find*()`) that return a mutated document. [Mongoose documentation link](https://mongoosejs.com/docs/guide.html#query-helpers)

To do this, add functions to the `Schema` config (second argument) under the `query` attribute. It is done in the same way as `methods`/`statics`. 

Technically, this is a way to extend Mongoose's chainable query builder API.
 
Example:
```js
User.find().populate("cartId"); // too much ODM in business logic

// a better equivalent
UserSchema.query.getFullUser = function () { 
    return this.populate("cartId");
  }
	
User.find().getFullUser(); // better - more abstract
User.findOne(/* code */).getFullUser();
```

<br />

For more info, see docs - https://mongoosejs.com/docs/guide.html#methods