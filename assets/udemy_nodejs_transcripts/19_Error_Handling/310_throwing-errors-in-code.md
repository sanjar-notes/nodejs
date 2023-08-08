## 310. Throwing Errors in Code

<strong><em>no description</em></strong>

Let's start in app.js and there, I have some code where I do get my user out of
the session and then I find the user by ID in a database and then I store the
found user in my request object so that for the entire request, I can access
that user object, it's a mongoose user object and I also catch any potential
errors that might be happening. 

Again because it's really important, this catch block will not fire if I don't
find the user with this ID, it will only fire if there are any technical issues
you could say, if the database is down or if the user of this app does not have
sufficient permissions to execute this action. 

Now we kind of have our own error handling in place and again we're not working
with technical error objects here but here I am checking whether we do have a
session user and I do have a solution for the case that this is not the case
because if I would not add this check, then I could try to find a user without
the session object existing and that would then crash our app. 

So it makes sense to write clever code that avoids such scenarios and tries to
only execute code that will succeed. 

It might of course still fail and for some reason, we might still not find that
user even if we have it stored in a session, maybe because the user was deleted
in a database in-between. 

So it would make sense to also check for the existence of user or for the
opposite, so if user does not exist and if it does not exist, here we could also
return next without storing the request user. 

So just that we are super safe that we don't store some undefined object in the
user object but that we continue without the user instead if we can't find the
user. 

Here in the catch block, logging it is not really useful though. 

It will make more sense to throw a new error here where we simply wrap the error
object we get here. 

Throwing this error has a significant advantage which I will show you in a
second but with that, this looks good. 

We added an extra check and if we do have some technical issue, we throw a real
error and as it turns out, expressjs gives us a way of taking care of such
errors, that is why I'm doing it like this. 

Alternatively, we could of course also simply call next here to continue without
request user being set or anything like that but I want to throw an error
because we had a technical issue connecting to our database and that is
something that might be a bigger problem than just a non-existing user. 

---