---
tags:
  - file-uploads
  - multipart
  - formdata
  - multer
  - enctype
---
# 321. Handling Multipart Formdata

## Current body parsing - `urlencoded`
We are currently interpreting the body as `urlencoded` (by using express's middleware). This can be checked by seeing the request type which is `application/x-www-form-urlencoded`, which is default content type.

Unfortunately, Express doesn't have a parser that could be used with file payloads. The `"body-parser"` package also doesn't support this.


## Using `multer`
Multer is a node.js middleware for handling multipart/form-data, which is primarily used for uploading files. It's mentioned at Express (http://expressjs.com/en/resources/middleware/multer.html)

for us, `"multer"` is an npm package that can interpret request bodies containing files.

Installation: `npm install multer`

It's simple to use -just add a middleware.


## form `enctype`
In addition to the `<input type="file" />` that we added to our form, we need to change our request  content type to become `"multipart/form-data"`.

This is done by using the `"enctype"` attribute on the form, with value `"multipart/form-data"`.

note: setting this will help Express know the content type, so it can ignore the `urlencoded` middleware, and `multer` will take it up. Already learnt this btw.

I added it globally (code): https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/94dc6cc8bead1d08ebb6ccf291fbdf3ea4d9478f

If using fetch, axios in a JS app, make sure payload is either string or FormData. See https://github.com/sanjar-notes/web_dev_fundamentals/issues/108

## What happens to other form fields
No change in `req.body`, except type file ones are removed. Multer takes care of this.
So simple fields are still accessible via `req.body.myFormField`.