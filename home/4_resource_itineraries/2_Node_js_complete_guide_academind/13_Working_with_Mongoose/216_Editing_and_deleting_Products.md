# 216. Editing and deleting Products
Created Sunday 7 May 2023 at 09:09 pm (binge)
Created Tuesday 30 May 2023 at 02:47 am (code)

Note: Since Product and associated user (seller) is being ignored by us, assume every user can change add/products. Change to be made: update product actions in Admin controller to work on all products, instead of associated with user. [Code]()

Fetch a product, change the attributes, and save.
```js
ShopController.postEditProduct = (req, res, next) => {
  const prodId = req.body.productId;
  const { updatedTitle, updatedPrice, updatedDescription, updatedImageUrl } = req.body;


  // fetch the product instance
  const product = await Product.findById(prodId);

  // update the values
  product.title = updateTitle;
  product.price = updatedPrice;
  product.description = updatedDescription;
  product.imageUrl = updatedImageUrl;

  // call save
  await product.save();
};
```

Alternatively, one can use `findByIdAndUpdate` or `findOneAndUpdate`. Example:
```js
const prodId = req.params.productId;

const product = await Product.findByIdAndUpdate(
  prodId,
    {
	  title: req.body.title,
	  imageUrl: req.body.imageUrl,
	  description: req.body.description,
	  price: req.body.price,
	}
);

// or equivalenty
const product = await Product.findOneAndUpdate(
	{ id: prodId },
    {
	  title: req.body.title,
	  imageUrl: req.body.imageUrl,
	  description: req.body.description,
	  price: req.body.price,
	}
);
```
The previous one accepts `_id` string as argument, the latter one needs it in an object or a as direct ObjectId.


## 217. Deleting a product
Mongoose does have a static delete function on the model, but it's named rather un-intuitively. 

The name is `.findByIdAndDelete`. Example:
```js
ShopController.postDeleteProduct = (req, res, next) => {
  const prodId = req.body.productId;
  
  await Product.findByIdAndDelete(prodId);

  redirect('/products');
}
```
FIXME: it seems there's no instance method for deletion, in Mongoose. Not a problem though.

Note:
- `findOneAndDelete` is also available, but has the same `*ById` direct string caveat.
- There are very similar deletion methods, but they end in `Remove` - `findByIdAndRemove`, `findOneAndRemove`. The difference is superficial, so stick with `*Delete` ones.
- There is yet another method called `.deleteOne()` that takes in a condition object, like `findAndDeleteOne`, but it *does not* return the deleted object. Avoid this generally.

## Delete all instances of the model
`Product.deleteMany()` when called without an argument deletes all instances of the model.