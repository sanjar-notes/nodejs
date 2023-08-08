## 285. Adding Protection to Post Actions

<strong><em>no description</em></strong>

We're restricting the amount of products we can see and that is one great step
forward but it still doesn't mean we can't send requests somehow by creating our
own pages where we still try to delete another product. 

So we should also add protections in our post actions, like in post edit and
post delete product, there we want to check that the product I try to delete is
really created by the user who is currently logged in. 

So in post edit product, there I might want to add a check once I found the
product that should be edited where I see if I'm allowed to edit that product. 

So here in the then block where I have that product fetched from the database,
there I will quickly check if product user ID is not equal to request user ID
because if it's not equal, then this means the wrong user is trying to edit
this. 

So here I then want to return and simply redirect back to the starting page
let's say because we try to do something fishy here, we don't want to continue,
so all the other code will now not run. 

We would still go into that then block though as you learned because the next
then block is still executed even if I do redirect here, so to circumvent this,
I'll add then right after save here so a nested then block so to say and now we
have protection in place that ensures that we can start editing products that
don't belong to us. 

To quickly check this, I'll temporarily remove my filter so that I can see all
the products again and I will log in with the wrong account, so with test2 and
now what we should see is that when I edit this and add a couple of exclamation
marks and I click update, I'm redirected but the edit wasn't saved because I
essentially ended up in my extra check here and I was redirected back but
without saving the changes because this code was never executed. 

Now let's try the same for deleting before I re-add my filter here. 

For deleting I also want to check if I'm really allowed to delete that product
and we can easily implement this by changing our deletion method here and use
delete one and there I want to delete the product where the ID is equal to the
prod ID but also where the user ID is equal to the request user ID. 

So both has to be true now, the Product ID alone is not enough, the user id also
has to match and therefore even if we have a valid user id, it will not delete
this product if the user ID does not match. 

So if I save this and I go to admin products with the wrong account still and I
click delete, you see the product doesn't go anywhere, still there. 

Now let me add that filter in get products again so that we can't even see it
and now we have the best possible set up because now we can really only see it
in that account where we are able to interact with it. 

So if I do login with that valid account, there I do see it and there I now also
should be able to edit it, though if I try that, it fails. 

So let's explore what's wrong here in the next lecture. 

---