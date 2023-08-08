## 220. One Important Thing About Fetching Relations

<strong><em>no description</em></strong>

I want to show you something which we don't need here but which is really neat
and which you should be aware of. 

Keep in mind that in our product model, we're storing a user ID. 

Now let's say when we fetch all products as we're doing it in the admin
controller in get products with find, let's say we actually want to get all the
user data for the related user and not just the ID because right now, if my
console log my products here in find in get products in the admin controller and
I reload my admin products page here, we see in the console, this is what gets
logged, an array of products and that array of course only or the objects in
there only have the user ID. 

Now this is of course not what we need in all cases, sometimes we want to fetch
the related user data too, now we could do that manually. 

Here inside the then where we got the products, we could loop through the
products and then write queries where we get the users with find by ID with the
IDs that we have received but this is a bit cumbersome. 

Mongoose has a useful utility method which we can add after find and that is
populate. 

Populate allows you to tell mongoose to populate a certain field with all the
detail information and not just the ID, so here I could add populate and then
you first of all describe the path which you want to populate, in my case thats
just the user id field but you could also point at nested paths if you had these
but here it's just the user ID and then that is it for now. 

If I now save this and I reload this page, you'll see actually the user ID is
now not just the ID but the full user object and that can of course be really
helpful for fetching data because this gives you all the data in one step
instead of writing nested queries on your own. 

By the way, you can also select which kind of data should be received and you
can not just do that in populate but also in find. 

After find, you can call select and this allows you to define which fields you
want to select or unselect, so which fields should actually be retrieved from
the database and there you pass a string where you could say for a product,
maybe you want to get the title and the price but you don't need description and
anything else. 

So you could then add title and price like this and you could even exclude
something like the ID by adding a minus in front of it and the same can be done
on populate by passing a second argument, this would be a string where you say
ok I want to get the name and that's it, the ID will by the way always be
retrieved unless you explicitly exclude it. 

If you do that and you now reload this page,  you already see some data as
missing here because we did not retrieve it and you see it in the data that gets
logged here too, we only retrive the title and the price, we explicitly excluded
the ID. 

For the user, we didn't explicitly exclude the ID so we got that and we got the
name which we defined here. 

So that's just a little side note about data fetching with mongoose and
something I wanted to make you aware of. 

We don't need that here, it actually breaks our application but it's still
something that's nice to know. 

So I will comment this out and I just want you to keep in mind that you can
automatically populate related fields and fetch the related data and that you
can also control which fields are returned, both for the main document and also
for populated documents. 

With that, let's go back to the state in which we need the app in and let's
instead work on things like the cart and orders. 

---