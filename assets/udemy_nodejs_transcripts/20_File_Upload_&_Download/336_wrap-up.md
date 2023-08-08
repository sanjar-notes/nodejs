## 336. Wrap Up

<strong><em>no description</em></strong>

That's it for this module, you learned a lot about files, you learned how to add
file upload functionality, both in the form and then most importantly on the
backend by using multer, this nice middleware which automatically extracts files
from incoming requests and stores them as specified by us and which also is able
to filter out certain file types if we want to. 

You learned how to store files, both for adding and editing items, so how to
manage that and you of course also learned how to download files, how to serve
them statically with the help of that static middleware expressjs ships with and
how to make sure that this uses the right path and alternatively or depending on
your requirements, how you can serve files as a response in a route, like with
get order here in the shop.js controller where we saw multiple different options
of serving a file that already existed, for example by loading it into memory
and then returning it or that you could stream such a file instead or that you
can even generate files on the fly if required, depending on what your
application requirements are. 

With that you learned a lot of things about how to work with files, with
streams, with responses and this hopefully helps you implement file related
features into your next application. 

---