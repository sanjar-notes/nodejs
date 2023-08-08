## 193. Fixing the "Add Product" Functionality

<strong><em>no description</em></strong>

Deleting works but when I try to add product and I'll just enter some dummy data
here, that fails and it seems to fail because I would imagine that in save here,
we somehow make it into this if block. 

So that _id is the problem and that makes sense because I actually do initialize
_id here at the beginning by creating a new mongodb object id. 

So even if we pass no ID and this therefore is undefined, this will create an
object and store it in _id, so _id down there will always be defined and if it's
just such an empty or automatically generated object id object, this should be
the issue here. 

So how can I overcome this? 

Well for example with a ternary expression, we can check if ID exists basically,
so if this returns true in an if statement and if it's the case, then I want to
create my object id object otherwise I'll store null and null will be treated as
false down there. 

So with this tiny change in place, with this ternary expression added in the
product model, we should be able to add a product real quick with some dummy
values and now it's created. 

So now this is working and it was just the fact that we were always creating
such an objectid object which we shouldn't. 

---