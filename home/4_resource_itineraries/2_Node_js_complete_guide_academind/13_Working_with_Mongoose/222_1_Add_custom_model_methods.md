# 222.1 Adding custom model methods
Created Sunday 14 May 2023 at 06:34 pm

### Adding custom methods to a model
To add custom methods to a model, use the options (second argument) of the `Schema` constructor.

<details>
<summary>Why add methods to the `Schema` and not the `Model`</summary>Since we already saw that a `Schema` may exist without a model (i.e. interstitial Schemas) - it only makes sense to attach models at the Schema level. Of course, they are available and will be used at the model level (since even a interstitial Schema will be accessed only as part of an actual model).
</details>

Static methods (and attributes) can also be added.

Syntax:
```js
const mongoose = require('mongoose'); 
const Schema = mongoose.Schema;

const userSchema = new Schema({/* */},
  {
	  methods: {
		addToCart (product) {
		  this.cart.items = /**/; // `this` is the model instance
		}
	  },
	
	  statics: {
		countItems () {
		  return this.cart.items.length;
		},
		readME: 'Hello, world' // data (not function) may be added under statics
	  },


	}
 );

module.export = mongoose.model('User', userSchema);
```


Notes:
- Remember to use normal functions instead of arrow in case of instance methods, to ensure `this` is available.
- We are adding these functions to the `Schema`, not the model. They will be used through the model, though, obviously.
- Static attributes can be added under `statics`, in addition to functions. This is not possible with `methods`, since instance data is meant to be part of the schema's first argument (data).


### Alternate way to add methods - just add keys
```js
const userSchema = new Schema({/* */});

userSchema.methods.addToCart = function (product) {
  // use a normal function instead of arrow, so that `this` is available
  this.cart.items = /**/; // do something
}

userSchema.statics.addToCart = function (product) {
// arrow or normal function, irrelevant, since this is a static method
  return this.cart.items.length;
}
```
Of course, one can mix and match both ways - options and/or direct key addition.

