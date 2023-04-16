# 161. Creating a User model
Created Sunday 16 April 2023 at 02:02 pm

Let's a new model, called User. A user can create products, and also buy products. Of course, a user will have their cart (i.e. "associated" cart). There are two parts to the User model
1. Base data- name and email.
2. Associations - the relations to cart, product etc.

We'll not worry about user authentication right now.

Let's work on the first part. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/83b849694089ad439d4a115d5227bc21fb4f30c4)

---
A user is related to other data in our shop - cart, products etc. Sequelize supports creation of such associations. There are 3 basic kinds of associations (between models/tables):
1. One to one - each record in table A is related to at most one record in table B.
2. One to many
3. Many to many

/rough START
## Sequelize associations (basics)
- **Source and target model** - s.someRelation(t) where s and t are source and target. This has nothing to do with foreign key placement, since it's determined by the relation too. s and t just make it easier to specify the order of arguments (since s.someRelation(t) is *similar* to someRelation.call(this, s, t))
- **Placement of foreign key**.
	- A.has*(B) - FK placed in B
	- A.belong*(A) - FK placed in A
- Recommended way to create associations - use relations in pair. Syntax for the basic 3
	1. 1-1 - `A.hasOne(B); B.belongsTo(A)`
	2. 1-N - `A.hasMany(B); B.belongsTo(A)`
	3. Many-many - `A.belongsToMany(B, { through: 'ABjunction' }); B.belongsToMany(A, { through: 'ABjunction' });` <details><summary>String/object</summary>Note, through can be a string, or even a model we defined (the foreign keys for both will be added to it automatically). This is actually better since we can add extra data here (i.e. in the junction table). If a string is passed, a junction model is still created, but has to be accessed via one of the participating models (doesn't exist in our code directly).</details>
	Why pairs - pairs make sure both model *know* about the relation, and have to have auto-generated (aka mixins) methods to get associated stuff from both sides.
- **Default lifecycle hooks** - by default, Sequelize has 'SET NULL' for deletion and 'CASCADE' for updation operation.
	
## Sequelize association (medium)
- **Multiple associations between the same 2 models** are *possible*. For this, pass an `as` (alias) config (second argument of .has* or .belongs*).
- **Foreign key name** - The foreign key names are automatically decided by Sequelize, but can be specified using the `foreignKey` option (second argument of .has* or .belongs*).
- **Association based on field other than FK** - we've had associations between models that used FK. But it's possible to create associations based on a non FK field too. **However**, this requires the field to be **unique**. Why do this? - doing this makes the generated mixins more tangible (example if username was used for the association instead of userid - we'd have mixins like `.getUsername()`, which is more useful compared to `.getUserid()`). Syntax:
	```js
	Person.hasOne(B, { sourceKey: '' }); // sourceKey here since it's the one being copied (to B)
	B.belongsTo(A, { targetKey: '' });
	
	// ommitting either side means use id for that side, i.e. id <--> someField
	```

Note: the option argument (2nd argument) here is referring to the `target`. e.g. `Product.belongsTo(User, { onDelete: 'CASCADE'} )` means talking about the deletion of target (i.e. User), and what happens to the source (Product) when this happens.

## Sequelize association (advanced)
#todo read-from-docs
- More granular eager loading

## Sequelize association querying
- Sequelize adds mixins to get associated models of the model being queried. Example:
	```js
	User.hasMany(Account);
	Account.belongsTo(User);

	// the following functions are now available (on instances)
	user.getAccounts();
	account.getUser();
	```
- Lazy vs eager load - when a model is queried, it's associated models are not returned (by default), and another call needs to be made using the mixin. This can be overriden, and the associated model(s) can be fetched in the fetch call itself, by using the `include` keyword as query option (i.e. object passed as second argument)
- Sequelize does not support direct manipulation of associated models, i.e. it has to be done in explicit steps. Exception - Creation of a new model (with associated models) is possible, if they too are new.

/rough end

We wish to have the following relations between the model, in this project.
![](/assets/161_Creating_a_User_model-image-1.png)