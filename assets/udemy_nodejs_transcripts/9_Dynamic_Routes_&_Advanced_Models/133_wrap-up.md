## 133. Wrap Up

<strong><em>no description</em></strong>

So that's it for this module, again we learned a lot and practiced a lot. 

You learned about dynamic routing and that you can pass dynamic path segments by
adding a colon to the express router path, the name after the colon is then the
name by which you can extract the data on request params. 

As a side note you can have more than one dynamic segment per route, this is
absolutely possible. 

You can also work with optional query parameters, these are the parameters you
append with a question mark at the end of your url and you can have multiple
ones separate with an ampersand and you can extract these values with request
query and then the name of your param. 

Now you don't need to register or name these parameters in your route registry,
you totally don't add them there, you can just start extracting them but since
they're optional, you should also have a check in place to see if that parameter
was passed in case you are depending on it. 

We also continued working on models and we added a cart model which only holds
static methods because we don't really create a cart that often, instead we just
want to work with the data storage behind it. 

You also saw that you can interact between models, for example delete a cart
item if a product is deleted but as I also mentioned towards the end of this
module, it's not that good if we only work with files for data storage because
accessing them is a bit slow to be honest and in general, there are better
options, most importantly of course, databases. 

So let's move on to how we can work with databases in a node express app in the
next module. 

---