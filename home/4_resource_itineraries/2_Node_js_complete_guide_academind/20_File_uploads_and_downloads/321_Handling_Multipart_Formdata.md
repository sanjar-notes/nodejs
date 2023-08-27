# 321. Handling Multipart Formdata

We are currently interpreting the body as "urlencoded" (by using express's middleware). This can be checked by seeing the request type which is "application/x-www-form-urlencoded".

Unfortunately, express doesn't have a parser that could be used with file payloads. body-parser also doesn't support this.

---

We are going to use 'multer', a package that can interpret request bodies containing files. It's simple to use - it exposes a middleware.

Since we added the input.file to our form, we need to change our request type to become 'multipart/formdata'. This is done by using the "enctype" attribute on the form, value being "multipart/formdata".

This will help express to ignore the urlencoded middleware, and multer will oiit up. Already learnt this btw.