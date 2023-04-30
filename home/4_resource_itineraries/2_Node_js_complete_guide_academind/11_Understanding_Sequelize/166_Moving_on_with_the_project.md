# 166. Moving on with the project
Created Monday 1 May 2023 at 03:15 am

- The cart has been added, but there's an issue still. The Product <--> User relation has two meanings - one is for product sellers, and the other for product buyer. Our current code is not wrong, since items added to Cart will be done from the main products page. **This**, however, should be indicated in the code.

	Let's used named relations for indicating this. Only Product to User code will change:
	```js
	User.hasMany(Product, { as: "seller" });
	Product.belongsTo(User, { onDelete: "CASCADE", as: "seller" });
	
	User.hasOne(Cart, { as: "buyer" });
	Cart.belongsTo(User, { as: "buyer" });
	```
- Upon exploration, I can see that the Cart has a `createProduct` magic method, since it's we related the two (Cart and Product) to list down (read) products in a Cart, and also add existing Products (created by sellers). But it makes no sense to create a Product using a Cart, and we should remove magic properties of this kind from the Cart model. **This is a usual thing in Sequelize projects, since Sequelize, by default assumes that two models can do all CRUD ops once related**. This "creation" behavior can be turned off using the following syntax:
	```js
	User.hasOne(Cart); // no change
	Cart.belongsTo(User); // no change

	Cart.belongsToMany(Products, { through: CartItem, as: false }); // removes magic methods from Cart (about Product creation)
	
	Products.belongsToMany(Cart, { through: CartItem }); // no change
	```
	Note, the Cart model still has the `add*` and `set*` methods, and the `get*` methods of course.