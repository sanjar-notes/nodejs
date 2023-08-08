## 395. Adding Authorization Checks

<strong><em>no description</em></strong>

To check whether a user tries to edit or delete a post which does not belong to
him, we should go to on the node, rest API project, we should go to our feed
controller and there, find our update and delete methods of course. 

Let's start with updating a post. 

In there, we find a post by ID which is all right of course and we should keep
in mind that for a post, the creator will be the ID of the user who created
that. 

So even if we do have a post here, we want to check whether that creator ID is
equal to the ID of the currently logged in user so of the ID that belongs to the
token we received. 

So here I'll check if post creator is equal to, excuse me, creator toString to
convert this to a string, is equal to request user ID, so to the user ID I got
from my token. 

If that is equal, I'm allowed to continue, if it is not equal hence we need a
exclamation mark here, I'll throw an error. 

So here I'll create a new error, not authorized, set the status code to 403
which is a good status code for authorization issues and I'll throw that error. 

Now if I save that, let's check that, first of all let's delete a post which we
are allowed to delete, like that duck. 

If I delete that, now deleting obviously works because we never added any logic
to prevent this. 

Now let me logout and create a new user, we need a different email address, well
let's first of all try the same one, it should fail so here I'll just use Max
and it fails. 

Now let's use an unused e-mail address and it succeeds, let's now login with
that newly created user, now let's try editing because that is where we did add
protection, the cup which was not created by that user. 

This failed with a 403 error, let's now login with the user who did create it
and let's now try editing with this user and this now succeeds. 

So now we have this first check in place. 

Let's now also add it to our delete post logic there. 

There I find my post at the beginning and before we continue, here I basically
want to implement that same check. 

I'll check the creator which is the ID of the user and compare it to the user ID
extracted from the token and if they're not equal, I will throw an error, so now
only authorized users should be able to delete the post of course. 

Make sure to do that before you clear the image. 

Now after saving this, let's go back and delete this and it succeeds because
this was the right user. 

Let's logout, let's login with this user let's say and create a new post, a duck
with the image and some content and let's logout and login with the other user,
the user who did not create it and let's delete that there and you see that
fails. 

Now I didn't implement an error message there and of course you could also tweak
the frontend to not even show these buttons if you're not allowed to edit but my
idea here is to show you how you can protect this on the backend since of course
this is a node course. 

Therefore I deliberately let you do that so that you can see that we can prevent
this on the backend and indeed we can't delete this now with the wrong user. 

---