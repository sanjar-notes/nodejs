## 164. More Sequelize methods
Created Thursday 27 April 2023 at 01:02 am

## Update an instance
```js
user;
user.name = "New name"; /* OR equiv */ user.set({name: "new name"})
await user.save();


// in one go
await user.update({name: 'New name', ... /*other fields if needed*/});
```


## Get all associated instances
```js
await user.getProducts();

// more granular
await user.getProducts({ where: {id: '2'}} );
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