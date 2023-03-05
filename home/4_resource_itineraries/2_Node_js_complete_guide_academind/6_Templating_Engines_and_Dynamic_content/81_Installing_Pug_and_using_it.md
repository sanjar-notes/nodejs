# 81. Installing Pug and using it
Created Sunday 5 March 2023 at 10:22 pm

## Install, connect, use with Express.js
1. `npm install pug`
2. `app.set('view engine', 'pug')` - set view engine. The argument `'pug'` works because pug *automatically* registers with express.
3. `app.set('views', 'path_to_templates_folder')` - set views folder. Optional (default is `my-project/views`).
4. `res.render('my_template_name')` - .pug extension is optional if engine `pug` is set. Can also pass in path to template file, if `"views"` Express app settings in unset.


## Pug syntax
Pug syntax is simple, concise.
1. Indentation matters, no closing tags, no angled brackets
2. class is specified with chained dot notation `div.my-class`. Same with id (with `#`)
3. attributes directly after tag (and classes) inside parentheses.
4. `div` is the default tag, if no tag is specified.

Example (Pug, vs HTML):
![](../../../../assets/Pasted%20image%2020230305233623.png)
![](../../../../assets/Pasted%20image%2020230305233513.png)

Code (same as above):
```pug
doctype html
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(http-equiv="X-UA-Compatible" content="IE=edge")
        meta(name="viewport" content="width=device-width, initial-scale=1.0")
        title Add Product
    body
        header.main-header
        nav.main-header__nav
            ul.main-header__item-list
                li.main-header__item
                    a.active(href="/") Shop
                li.main-header__item
                    a(href="/admin/add-product") Add Product
```
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    <header class="main-header">
        <nav class="main-header__nav">
            <ul class="main-header__item-list">
                <li class="main-header__item"><a class="active" href="/">Shop</a></li>
                <li class="main-header__item"><a href="/admin/add-product">Add Product</a></li>
            </ul>
        </nav>
    </header>
</body>
```

Note: 
- In VScode:
	- Pug auto-completion works out of the box. 
	- There's no built-in formatter, however. An [extension](https://marketplace.visualstudio.com/items?itemName=ducfilan.pug-formatter) is available though.

