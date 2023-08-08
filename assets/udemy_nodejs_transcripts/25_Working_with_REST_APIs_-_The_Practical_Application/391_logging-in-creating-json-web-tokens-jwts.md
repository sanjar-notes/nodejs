## 391. Logging In & Creating JSON Web Tokens (JWTs)

<strong><em>no description</em></strong>

So we're at the point where we know that the user did enter valid credentials,
now we want to use that information to generate such a json web token which I
showed you on the slides. 

For that let's quit the server here, the node server and let's install a new
package, the package I want to use is called jsonwebtoken, one word, this is a
package which allows us to conveniently create such new json web tokens. 

We can now restart a server and we need to import this into this file, so here,
I'll import it, store it in a constant named jwt, the name is of course up to
you the json web token package or the object it exposes. 

Now down there after checking the password, I want to generate a new token
stored the token and I'll store the constant named token and then here I'll use
the jwt package and there the sign method, this creates a new signature and
packs that into a new json web token. 

We can add any data we want into the token, like for example we could store the
user email, so access the loaded user e-mail and the user id, access the loaded
user _id and since it's a mongodb object ID here, let's convert that to a
string. 

So now I'm storing some user data in the token, of course you should not store
the raw password in here because that would be returned to the frontend, to the
user to whom the password belongs but still not ideal, email and user ID should
be fine however and then you need to pass a second argument which is that
secret, so that private key which is used for signing and that is now only known
to the server and therefore you can't fake that token on the client. 

I'll enter secret here, typically you want to use a longer string like some
super secret secret or even longer, also check out the official docs of the json
web token to learn more about it all. 

I'll also set a third argument where I configure this and there, I'll set an
expiry time of one hour with this syntax so that the token becomes invalid after
one hour. 

Now this is a security mechanism you should add because the token is stored in
the client, now of course by the client to whom it belongs but technically, that
token could be stolen. 

If the user does not logout, another person copies the token from his browser
storage and then he can use it on his own PC forever. 

Well not forever now at least because after one hour, the token becomes invalid,
so this is a good security mechanism which is like a nice, finds a nice balance
between usability where you would want infinite sessions and security where you
would want to limit this to like one second. 

Now this is all a nice in-between solution which is pretty common. 

So now we have a token which we can return to the client, so here indeed I will
now return a response with status code 200 where I add some data, we can add a
message if you want but I will only add that token which I generated and a user
ID and that is my loaded user ._id toString. 

Now that data needs to be provided because in the react app I gave you, I'll be
looking for that ID and I'll be storing it, by the way you should also take one
hour because in that react app, I'll log you out after one hour and all that
storing and so on will be done by the frontend, now I'll show you how it gets
stored in a second of course. 

So let's now go back to our auth route and connect our login route to our auth
controller and there, the login action and now with that, let's go back to the
frontend and work on the code there as well. 

So in the frontend here in the app.js file where we have the sign up handler, we
have to look for the login handler here and we should fix the url there too, the
url is localhost 8080/auth/login, we need to pass an object where we now also
change the request method to post and where we pass our data. 

So just as with signing up, we can actually copy that logic from there, the
headers and the body, copy that and move it to login, we don't pass the name in
the body though but password and email will be passed. 

Now there is another small adjustment required, here you can actually directly
access auth data e-mail and auth data password. 

Now with that, save that and go back to your react app and try logging in with
the credentials you created a couple of lectures ago. 

It should work, this error still is coming from the status which we'll fix soon
and here we also see that I'm logging something, we see that token that was
generated and the user ID. 

In your chrome browser dev tools, you can also go to the application tab and
there go to the local storage, select your domain and you will see that token
here, that is the token we generated on the server. 

The other data is data I'm storing here or that was stored way back by other
application so we don't need that, that has nothing to do with our app. 

We have the expiry date which I generated on the client to know when I should
remove the token because it expired and this is the token itself. 

Now you can also take that token and visit jwt.io, there you can learn more
about json web tokens first of all and you can also paste your token into that
area on the left and this allows you to look into your token, you don't see your
secret but you can now validate it. 

If you enter your secret which you chose on the server, some super secret
secret, then you should end up with that same token you copied in and indeed if
I replace it, it does not change. 

And here you also see that payload data you added on your server side, you could
theoretically extract that on the client too and that is why you should not
store super sensitive data in there but this now also shows you that if I try to
generate this token on my own, let's say I also edit it like change the email
address, the token changes on the left and therefore if I edit this, it will not
be validated because now the token is not the same as it was when it was
generated on the server with this secret. 

So if I try to generate my own one with a different secret, I'll end up with a
different token and if I try to edit the data in there, I also do so I can't
mess around with the token in the client, the server will detect this. 

This is how we can login and how we work with tokens to know whether we are
logged in. 

We're missing one important piece of information though, we have the token, now
we also need to attach the token to requests that require authentication because
right now, well I am logged in, I only see these options after logging in but
theoretically deleting, editing and so on does not really care about the token. 

We should change this, we should also connect new posts to our user and we
should make sure that only users who created a post can edit or delete it. 

So still some work to do. 

---