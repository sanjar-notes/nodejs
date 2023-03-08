# 82. Layouts in Pug
Created Monday 6 March 2023 at 01:01 am

Many pages on the frontend have common elements that are always there - headers, footers, style files, etc.

- Declare template placeholder - `block` followed by key name.
	```pug
	//- my-project/views/my-layouts-folder/main-layout.pug
	doctype html
	head
	  meta(charset="UTF-8")
	  meta(name="viewport" content="width=device-width, initial-scale=1.0")
	  meta(http-equiv="X-UA-Compatible" content="ie=edge")
	  block title
	  link(rel="stylesheet" href="/css/main.css")
	  block styles
	body
	  header.main-header
	    nav.main-header__nav
	      ul.main-header__item-list
	        li.main-header__item
	          a.active(href="/") Shop
	        li.main-header__item
	          a(href="/admin/add-product") Add Product
	  block content
	```
- Using the layout placeholder - same, block followed by keyname. Value passed as child.
	```pug
	extends my-layouts-folder/main-layout
	
	block title
	  title Page Not Found
	block content
	  h1 Page Not Found!
	```
	evaluates to 
	```pug
	doctype html
	
	head
	  meta(charset="UTF-8")
	  meta(name="viewport" content="width=device-width, initial-scale=1.0")
	  meta(http-equiv="X-UA-Compatible" content="ie=edge")
	   title Page Not Found
	  link(rel="stylesheet" href="/css/main.css")
	body
	  header.main-header
	    nav.main-header__nav
	      ul.main-header__item-list
	        li.main-header__item
	          a.active(href="/") Shop
	        li.main-header__item
	          a(href="/admin/add-product") Add Product
	   h1 Page Not Found!
	```

Note: not using a block is fine.

---

Active link wrong value in add-products page
https://github.com/exemplar-codes/templating-engines-w-express-js/commit/f280d6508731d952f29b4938283f8acf87ec0763

Solution - remove default active link, pass some variable that's used to conditionally determine the class.
```pug
//- `layouts/main-layout.pug`
nav.main-header__nav
      ul.main-header__item-list
        li.main-header__item
          a(href="/" class=(myActivePath === 'shop-page' ? 'active': '')) Shop
        li.main-header__item
          a(href="/admin/add-product" class=(myActivePath === 'on-admin-page' ? 'active': '')) Add Product
```
```js
// shop.js
  res.render('shop', {
    prods: adminData.products, 
    docTitle: 'My shop', 
    myActivePath: 'shop-page',
  });
```
```js
// add-product page
res.render('add-product', { myActivePath: 'on-admin-page' });
```

[Code](https://github.com/exemplar-codes/templating-engines-w-express-js/commit/b3240643503169b4f09ecf165649c9a94110e2b9)

Note: 
- Of course, passing in arbitrary tokens is not a good way to handle active link (I did this to demo that there's no systematic way to do this in Pug, afaik). A better way would be to pass a prop determine function as prop, or make the whole link a layout placeholder.
- Ternary expressions are fine in Pug
- Parentheses are to add JS code inside attribute clause values. Nesting them is fine too.


## Pug (conclusion)
These was a good overview of Pug, but there are still more patterns and features available. 
- See [docs](https://pugjs.org/api/getting-started.html)
- [freeCodeCamp - Pug Full tutorial for beginners](https://youtu.be/kt3cEjjkCZA) , 1 hr video - covers many things