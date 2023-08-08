## 286. Why Editing Fails

<strong><em>no description</em></strong>

Editing fails here and do you have an idea why it fails? 

It fails because of my check here, I compare the product user ID to the request
user ID. 

Now we have a type problem again, I should convert both to a string because I'm
also checking for type equality. 

So with this change, both converted to a string and not this strange object id
thing, with this in place, now if I login or if I'm logged in with the right
account, now I can update this and I can also delete this. 

So this now all works with the right account, so with the account who created it
but it will not work if I login with the wrong account because if I login there,
so this is now the account which did not create it, I can view it on the normal
pages, I can add it to my cart if I want to but under admin products, I do not
see it and even if I would see it, I could not interact with it. 

---