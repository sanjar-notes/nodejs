## 191. One Note About Updating Products

<strong><em>no description</em></strong>

Now one important note about the update video, what I did there is I actually
passed an object id in admin.js controller to my product constructor. 

Now actually I could also just pass product id as a string and therefore remove
my object id creation up there in the mongodb import, all of that is happening
in the controller now and if I do that and I try editing this and change the
price to 16, you see now it fails. 

Now if we go to the product model and we have a look at the save method, there I
am actually looking for the right object but I'll have a problem with updating
it because there, I'll try to set my object ID to a different object id to a
string because here I'm just referring to this which will hold the unmodified
objectid. 

So what I should do is I should automatically convert the objectid, the ID here
which is a string to an object and the object in the constructor so that I can
remove it down there because _id will now always be an object id field, no
matter if I'm using it in a filter or if I'm using it for updating. 

So now with that if I edit this again and I change the price to 18, now this
works again because now I'm not trying an invalid update by trying to change the
ID to some invalid value. 

So this is just an important note I wanted to add, you don't have to convert the
ID in the controller file, you can leave that untouched but you can do a general
conversion in the product.js model file which is the better approach of doing
that. 

---