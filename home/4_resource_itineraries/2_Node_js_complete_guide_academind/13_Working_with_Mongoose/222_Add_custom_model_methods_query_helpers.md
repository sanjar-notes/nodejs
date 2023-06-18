## Adding custom model methods (222)
Created Sunday 14 May 2023 at 06:34 pm

### Adding custom model methods
To add custom model methods, use the options (second argument) of the `Schema` constructor.

Static methods (and attributes) can also be added.

Syntax:
```js
const mongoose = require('mongoose'); const Schema = mongoose.Schema;

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
- Static attributes can be added under `statics`, in addition to functions. This is not possible with `methods`, since instance data is meant to be part of the schema.


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

