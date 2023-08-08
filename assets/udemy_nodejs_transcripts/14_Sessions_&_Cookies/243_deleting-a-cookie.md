## 243. Deleting a Cookie

<strong><em>no description</em></strong>

We're now using sessions everywhere and we have our dummy authentication process
in place, it's missing crucial features like log out and so on and that will all
come in the authentication module but we have something in place and you might
have noticed that of course regarding the log out, I always just deleted the
session cookie. 

That is what I did in the assignment too, I deleted the session cookie to
demonstrate what happens if we then try to do something that is relying on data
that is stored in the session, it will fail because the session cookie which is
required to identify the correct session is not there. 

Now deleting just the cookie is of course not ideal because right now for
example if we have a look at compass and into our sessions collection, I have
three sessions here because I always just deleted the cookie. 

Now there is a cleaner way of doing that and that cleaner way is to use a method
provided by the session middleware, now let me show this to you and for that,
I'll first of all go to my views and there to the navigation and next to my
login button here, I'll actually add another field, another list item into which
I'll add a form which should lead to log out and use a post method  and in that
form, I'll have a button like this which is of type submit where I'll say log
out. 

Now if we save that and we reload our page, we see log out next to login, now to
make sure the styling is correct, we need to add that list item class here which
we also have on the list item here and after adding this, if we reload this
looks better and now I've got my log out button here. 

Now when I click this, I want to clear any session I might have  and for that I
of course need to register a new route. 

So let's head over to our auth routes and let's add a new post route here
because we will send a post request which goes to log out and there, I will
trigger a post log out action in my controller. 

Now this action of course does not exist yet so let's head over to the auth
controller and maybe duplicate the post login route here, name it post log out
and in there, what I want to do is I want to clear my session. 

We can do this by reaching out to our session object and then we can call
destroy there, this is a method provided by the session package we're using. 

Now this also takes a function which we pass to it which will be called once
it's done destroying the session and in there, request session will then not be
available anymore because we got rid of that session. 

We can recreate it for the next request when we do this again, then it will be
set again but in here, all the session data will be lost because the session was
destroyed. 

So here I will then actually redirect back to my starting page with res redirect
slash, we also get a potential error here which we can try to log to the
console. 

Now with that we have the post log out button registered. 

Now let's head back to our application and first of all, let's login. 

Now let me open the developer tools again, I've got no session cookie here, I
can click login and redirected session cookie is set and we can now use that
session. 

Now if we go to compass real quick and we refresh, we see we have four objects
now which makes sense, we had three before, now we have four and now let me
click log out. 

We are redirected, the session cookie here actually still exists but you see the
session was deleted over there and the session cookie still exists but that is
no problem because no matching session will be found so that is fine, it's
basically not doing anything and it will be renewed once we login again, then
this will be overwritten and when we close the browser, it would also be deleted
because it's not a permanent cookie, it's a session cookie which means it's a
cookie that does not have an expiry date in the future, it does not have a max
age, it will simply get deleted when we close the browser and it's worthless in
this state here. 

So now as you see if I click around, I have a problem with my orders here, I'll
fix that in a second but you see the cookies there, most importantly the session
was cleaned up back there though. 

---