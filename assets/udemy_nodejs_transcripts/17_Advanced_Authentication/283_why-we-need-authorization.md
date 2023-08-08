## 283. Why we Need Authorization

<strong><em>no description</em></strong>

So we worked a lot on resetting passwords. 

Let's now work on authorization. 

And with that, I mean that not every authenticated user is allowed to do
everything. 

A good example would be this one. 

I'm not logged in now. 

Let me log in with this user here. 

Test a test dot com. 

Here, I might be able to add a product and I can delete products, but right now
I can delete all products no matter if I created them or if someone else created
them. 

And the same is true for editing them. 

Authorization means that I restrict the permissions of a logged in user, so
every user might be able to add anything to the card, including products created
by the user. 

But you might not be able to delete and edit products which were not created by
you. 

So for now, I can do that, but that's exactly what I want to work on next so
that we can't do this. 

Now, how can we implement that? 

Well, when I create a new product and let me quickly do that, remember, I'm
locked in with test at test com. 

This was created by test at test dotcom. 

When I create this product here, we have it here and we can see it in the
product collection. 

Obviously it's linked to the user with an ID that ends with E five. 

And if we have a look at all our users, let me delete this one here. 

Then we see this is the one with E five. 

It is to test a test dot com user. 

Now if I log in with my test to account. 

So test to here. 

Then if I go to Avon products. 

I can also edit and delete that and that is exactly what I want to prevent. 

Let's do that in the next lecture. 

---