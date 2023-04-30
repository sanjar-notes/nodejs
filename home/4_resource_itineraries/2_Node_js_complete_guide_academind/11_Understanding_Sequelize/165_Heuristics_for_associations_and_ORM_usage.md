# 165. Heuristics for associations and ORM usage
Created Thursday 27 April 2023 at 10:22 pm

Moving on with the project. Adding the cart and cartItem models creates the table, but existing data population (product, user) isn't working. [Code - works fine, I've commented the new changes](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/e32916953625da75b65621a81792391eabae90d6)
	- Problem: the`cartItem` and `Product` associations are not consistent, *apparently*. Sequelize doesn't raise any errors, but what happens really is that tables are created, but they have no associations (*strange*). [Commit](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/a42d0560de62142833fed6f8eef0ee84c227ffa9)
	- Also, the `afterBulkSync` hook, that I use for data population doesn't run either.
	- Solution - the association was wrong, so I removed it. I'll rewrite it.

## Thinking out loud (pasting from scratchpad)
```
// table, yes
User =  {
    products: [<Product>],
    cart: <Cart>
    ...
}

// tables, yes
Product = {
    user: <User>
}

// cart, corresponds to use (1-1)
Cart = {
    items: [{<Product>, quantity: Integer}]
}

// no other choice but
cartItem:
cartId (imp), productId (~imp), quantity (ok)
```

Words
- User has a Cart
- Cart belongs to a user
- User has a Product
- Product belongs to a user

Product may belong to many carts (OK)
Cart contains many products (with associated quantity) - weird, go below the level of abstraction of ORM, need a table with (cartId, productId, quantity). Let's name this table 'cartItem'. Tables are like models, go back to ORM abstraction. Talk about cartItem now:
- Cart has many cartItems. cartItem belongs to one cart.
- A cartItem is associated with one product. A product may be associated with many cart items (since quantity may differ).
All done w.r.t cart, product and cartItem (the incidental model).
Let's revise all possible associations
- Cart, cartItem - done
- Cart, product - cannot be done directly, so this whole process, ignore.
- Product, cartItem - product belongsToMany cartItem, seems weird --> go down a level of abstraction.
    - Table wise, cartItemTable.root + add productId FK seems fine.
    - So cartItem.belongsTo(Product) and Product.hasMany(cartItems)
    - Doing both ways since I may wish to find all cartItems a product is present, too, for analytics/recommendations.

cartItem *<--> Product
cartItem  <--> Cart

The code works (tables with desired FKs are generated):
```js
User.hasMany(Product);
Product.belongsTo(User, { onDelete: "CASCADE" }); // ignore the onDelete, it's contextual to the project

User.hasOne(Cart);
Cart.belongsTo(User);

Cart.hasMany(cartItem);
cartItem.belongsTo(Cart);

// using both sides (as is usual) since I wish to have analytics about Product and User who may buy them
Product.hasMany(cartItem);
cartItem.belongsTo(Product);
```

But, it may be better to avoid having associations with the incidental (junction) table, and use it via `through`. copying some stuff from above and rewriting.

This:
```js
cartItem *<----> Product
cartItem  <----> Cart

// is? equivalent to
(cartItem/Cart) *<----> Product

// could be rewritten to avoid direct association with the junction (cartItem) model
Cart* <---> Product 'through' cartItem
```
---
### Heuristics for associations, and ORM usage
The following are rules I derived from the "thinking" above.
Notes:
1. First write down in words, simply use 'associated' and specify type of relation (1-1, 1-N, N-M). If there's extra data needed in addition to the association, note this down (we'll need a junction model here).
2. For the ones where association is simple (no data needed), use the Sequelize defaults.
3. For the ones where extra data was needed, create junction models. Then consider all possible associations of the junction model(s) with the actual (generally two) models that we were trying to associate. Repeat from #1. Until step 3 is empty.
4. If at any point, the Sequelize relation wording seems weird/wrong (example: products belonging to or having many cart items), go down a level of abstraction and see in which model table the FKs would be added for each of the possible Sequelize relation. Place the FKs in the correct tables, and choose the Sequelize relation that will ensure this (using the source-target-FK placement rule). Now that we have tables, move back up and create models for the tables. Continue.

Jargon:
1. Sequelize relation - hasOne, belongsTo, hasMany, belongsToMany
2. source-target-FK - the "needy" one stores the FK

Note:
1. It is implied that table-level data for all models is added appropriately. After then only, do we start thinking about associations.

### Weak check
> I'll paste a file where I thought and wrote down some rules from the thinking. Verify if it makes sense, and suggest corrections, or things I should consider. Note: I'm starting out with backend development, and therefore deliberately leaving out too nitty gritty details.
> 
> &mdash; *Sanjar*

>Based on the information you provided, it seems like you have a good understanding of how to define associations between models using Sequelize. The rules you derived from your thinking process are also reasonable and could be useful for future development.
>
> One suggestion I would make is to be more explicit about the type of relation (1-1, 1-N, N-M) between the models in your comments, especially for more complex relationships. This will make it easier for you (or other developers) to understand the relationships later on.
> 
> Another suggestion is to use the through option when defining associations with junction tables, as you mentioned in your example. This can make the code more readable and easier to understand, especially if there are multiple junction tables involved.
> 
> Overall, it seems like you have a good grasp of the basics of defining associations between models using Sequelize. As you gain more experience, you may find that there are additional nuances or best practices to keep in mind, but these rules should serve as a good starting point.
> 
> &mdash; *ChatGPT*