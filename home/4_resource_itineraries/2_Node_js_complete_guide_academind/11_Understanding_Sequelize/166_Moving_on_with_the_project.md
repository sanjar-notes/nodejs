# 166. Moving on with the project
Created Monday 1 May 2023 at 03:15 am

- Named associations - The cart has been added, but there's an issue still. The Product <--> User relation has two meanings - one is for product sellers, and the other for product buyer. Our current code is not wrong, since items added to Cart will be done from the main products page. **This**, however, should be indicated in the code.

	Let's used named relations for indicating this. Only Product to User code will change:
	```js
	User.hasMany(Product, { as: "seller" });
	Product.belongsTo(User, { onDelete: "CASCADE", as: "seller" });
	
	User.hasOne(Cart, { as: "buyer" });
	Cart.belongsTo(User, { as: "buyer" });
	```
	[Actual code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/b0616fba264f0d2360f208d35254b64b37931c83)
- Query restriction - Upon exploration, I can see that the Cart has a `createProduct` magic method, since it's we related the two (Cart and Product) to list down (read) products in a Cart, and also add existing Products (created by sellers). But it makes no sense to create a Product using a Cart, and we should remove magic properties of this kind from the Cart model. **This is a usual thing in Sequelize projects, since Sequelize, by default assumes that two models can do all CRUD ops once related**. This "creation" behavior can be turned off using the following syntax:
	```js
	User.hasOne(Cart); // no change
	Cart.belongsTo(User); // no change

	Cart.belongsToMany(Products, { through: CartItem, as: false }); // removes magic methods from Cart (about Product creation)
	
	Products.belongsToMany(Cart, { through: CartItem }); // no change
	```
	Note, the Cart model still has the `add*` and `set*` methods, and the `get*` methods of course.
	FIXME: does not work, the createProduct magic method is still there.
- Update the sample populater. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/e2452b496f2926fa70a4a13ee580a2363363fd80)
- Update cart get, and post endpoints. Also fix the `add=true` bug in the EJS files. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/34d6bf733832713de6e8e72c46d909e5ce3cc49f)


## Concise way create associated model along with junction model data
There is a more concise way to create associated models, if `through` was used. We don't need to work directly at the junction model level. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/eca88369ea1ad5afb8c6807ac6bc9c59a4c03a0c)
```js
// Context: existing associations
Cart.belongsToMany(Product, { through: CartItem }); 

Cart.hasMany(CartItem); // to get magic methods for CartItem
CartItem.belongsTo(Cart); // to get magic methods for Cart


// verbose
const newCartItem = await cart.createCartItem({ quantity: 1 });
await newCartItem.setProduct(prodId);
await newCartItem.save();

// or, equivalently
await cart.addProduct(prodId, { through: { quantity: 1 } }); // concise
```

## Moving on - adding orders
- An order is a "frozen" instance of a cart. 
- A user may have multiple users at the same time. 
- An order has CartItems.
- An order should survive even if the Cart it was created from gets deleted.

So basically, it is a cart, but with additional data like shipping address, and other things. Also, we need to do a deep copy when the user checks out, since the cart may change. For this deep copy, we should create an instance method, so as to keep the logic in the model, instead of the controller - "fat models/skinny controllers" best practice.

- Let's try to think of the order association. User and Order is a simple 1-N relation. For the CartItems and Products, I think "associations" are not the way to do this, since an "Order" is a table of "frozen" records, and associated instances could change - which does not make sense. **Copying** is the main thing, instead of **association**.

Since we're copying, we'll not get any magic methods (even read only ones, since an Order is a frozen Cart), which implies that we'll need to write the code our-self. We could get over this by having a 1-1 relation between Order and Cart, with a "hook" that observes any changes in `Cart` (assume we have created an associated `Order` already), and whenever there is, it copies and dissociates that part (`CartItem`) of the Cart. Now, the `CartItem` is related to `Order` instead of a `Cart`, and we never do any updation from the `Order`, this means that the `CartItem` is effectively frozen. The advantage is that we can access the `Product`, and also have magic methods. **This is impossible using hooks** in Sequelize, since hooks here are only at the model level, and cannot observe/react to changes in the associated models. 
**So**, I'll duplicate the code for `Order`, as in `Cart`. We'll just create copies of `CartItem`s that belong to just `Order`. 
Maybe I'll create duplicate `CartItem` and create the `OrderItem` model, this is not required however, if we indicate that `CartItem` is used in both `Order` and `Cart`.  The `Cart` will be null for a `CartItem` belonging to an `Order`, of course.

*Trade-offs*: we get the magic methods, but have to duplication, and memory consumption is twice.

[Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/b6d9bef7c370453f7e808ed4aec974ca4a10052d)

Next:
- Add the Order button - [code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/c0004337d7bed8a4f77a2d4542068b54515b68c3)
- Orders list page - [code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/c82a41a99cd2077b4e593428ed7ba11b867d3bed)
- Order detail page - [code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/19b3e61959d09e8e31fb51b8d79bc131eb2f97e4)
- Various fixes - BE and FE

## Fetching model instances with associated models (eager load)
Use the `includes` option, and provide the models to be fetched in an array, like so:
```js
Cart.belongsToMany(Product, { through: CartItem });
Product.belongsToMany(Cart, { through: CartItem });

const productsOfCart = await cart.getProducts({
	includes: { model: [CartItem] }, // syntax
});

product[0].cartItem.xyz; // works
```
This is like the concise creation (including junction) data way. That one ("write") used `through`, this one ("read") uses `includes`. Note: the key is plural.

I've used this for both cases in this app. Check code at this [point in time](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/tree/d90536c66d48a0a31bc778bd9b778c77fe35ec96) - global search for "includes:".