## 164. More Sequelize methods
Created Thursday 27 April 2023 at 01:02 am

## Check existence/count
```js
// model
!!await Product.count(); // some products exist

!!await Product.count({where: {name: 'Sanjar'}}); // given product exists


// instance
// N-M relation or many side of 1-N
!!await user.countProducts(); // some associated products exist

await user.hasProduct(42); // simplest, returns bool. Alternatively, use countProducts with 'where' option

await user.hasProducts([1, 2]); // check associated products exist


// for 1-1 or 'one' side of 1-N
!!await product.userId; // null means absent
```


## Get all associated instances
```js
// for N-M or 'many' side of 1-N

await user.getProducts(); // get all

await user.getProducts({ where: {id: '2'}} ); // get one product

// for 1-1 or 'one' side of 1-N
await product.getUser(); // returns null if non-existent
```


## Update an instance
```js
user;
user.name = "New name"; /* OR equiv */ user.set({name: "new name"})
await user.save();


// in one go
await user.update({name: 'New name', ... /*other fields if needed*/});
```


## List down properties and methods
```js
// model from instance
const User = user.constructor;

// get methods
console.dir(Object.getPrototypeOf(user)); // instance
console.dir(Object.getPrototypeOf(User)); // model, in this case, stuff like findByPk is at the end (down), greyed out

// instance properties (not methods)
user.rawAttributes; // doesn't have the values though
user.id; // value
```
FIXME: this was a huge headache, why isn't there an inbuilt way to list down all methods