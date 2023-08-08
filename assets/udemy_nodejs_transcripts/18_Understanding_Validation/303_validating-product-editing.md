## 303. Validating Product Editing

<strong><em>no description</em></strong>

So let's now make sure that when we edit a product, we don't break our app as
we're currently doing it if we enter something wrong but that we instead simply
validate the input. 

Well we are validating it already because I do have all my validators added on
the edit product route in the routes folder but in the controller action that
belongs to that, we should also repeat the code from adding a product, so all
that code where I fetch the errors and then check for the existence of errors,
we should grab that and add it to post edit product as well and there before we
start doing anything, so before we find a product, before we do that, I will
actually use my validation errors if we got any and then re-render the page with
the title of edit product, editing set to true because we are still in editing
mode but has error also set to true and the product data populated like this,
with the values the user entered. 

And with that if we save that, that's all we have to do because we're reusing
the same view we use before, so we already got everything we need for outputting
the errors and now if I do leave out that price field, I get title is not
defined. 

Yeah here when I try to set the data which I return, here in this post edit
product actions, it's all named updated title, updated price, so we should be
using that. 

So let's use updated title here, updated price, updated image url and down
there, it's updated desc, so this was a little mistake on my side, these values
which I extracted were named differently. 

Now after renaming that if I try to submit this again, now I simply get invalid
value, again you could override that default message in the way I showed it
earlier in this module. 

We also see that our image url was lost, yeah but simply because I assign this
incorrectly, I assign the price to the image url and the other way around. 

We should of course do it this way and now if I update this, now all the data is
kept and I still get this error. 

So now we get this validation in place too, now one thing we can do of course we
can again set that red border by repeating that same way we did in the login or
in the sign up pages. 

We get our class here, we conditionally add a css class and we do the same in
edit product, so there for this input I do add my class when there is an error
for the title input, the same of course for the image url and all the other
inputs, so that does not change. 

Here for the image url, I do get this css class here if we do have an error on
the image url. 

Let's do the same for the price of course real quick, split up what we get thus
far and then let's here check the price to see whether we add this invalid css
class. 

And for the text area, it's exactly the same, we just need to do one little
change to our css code because here I'm checking for description and so the
invalid class might be added to that text area. 

Thus far in my css code, in the forms css file, I only add or change the text
color if invalid was added to the input, now we should simply group another
selector or add another selector to that group here and simply check whether
invalid is added either to an input or to a text area and in both cases give it
a red colored border. 

And with that in place, we now just have to make sure that we pass these
validation errors which we are checking in edit product now, that we passed that
with our responses. 

So in the admin controller starting with get add product, there validation
errors should be an empty array because we got no validation errors in this
place, for post add product however, here we should have validation errors which
is equal to errors array, so these errors which we did fetch. 

For get edit product, there again I will pass validation errors as an empty
array because we have no errors here when we just get the page but for post edit
product when we do return our error page basically, then I want to set
validation errors back to errors array like this. 

And now we do pass that data so if I now hit update here, you see this is red,
only interesting pieces, the title is red as well. 

Well that makes sense because here I still have something in my validation set
up in the routes folder, here alphanumeric, we did remove that if you remember
because it should be isString otherwise the whitespace, the blank is not
allowed. 

So if I change that and I hit update now, I actually fail and I do fail because
the cast to object id failed for that value. 

Now what's wrong here? 

Well keep in mind for editing, we need that hidden input where I do have my
product ID right and I do load that product ID when I first render this page but
if I re-rendered it due to a validation error, so due to this render function in
my if check here, well then I only set title, image url, price and description. 

I also need to set _id though, otherwise it will render the page but if I try to
submit it that ID will be missing and I need that ID because I extract it here. 

So what I should do is I should simply pass _id here and set this equal to prod
ID which I am extracting when this is submitted the first time. 

So now I'm passing _id and this means that if I now go to admin products, edit
this and let's say I change the price, this works but now let's also do
something that breaks validation, so now this was reloaded due to our failing
validation. 

And now if I edit this, it will still work because now we also did store and
re-render that product ID and that is how we can add validation and provide a
relatively good user experience. 

---