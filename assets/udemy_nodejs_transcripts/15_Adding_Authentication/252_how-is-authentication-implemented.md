## 252. How is Authentication Implemented?

<strong><em>no description</em></strong>

How is authentication implemented? 

Same set up, we get a user, we get our backend, the server side code and the
database and now typically, a user will send a login request. 

Now obviously for that, a user, a visitor of our page needs to have signed up
before but after you signed up, you can login with your email and password and
on the server, we check whether that email and password combination is valid,
whether we have a user with that e-mail and that password in our database. 

If that is the case, we create a session for this user and you learned how this
works in the last module and this session then identifies this user. 

This is required because otherwise without a session, even if we find out that
the credentials are valid, for the very next request the user would be logged
out again because remember, requests interact separated from each other, they
don't know anything about each other, we need a session to connect them, that is
why we create one with the user or the authentication information. 

We then return a 200 response, so basically a success response and we obviously
also store the cookie belonging to that session on the client, we return that
with that response so that we really established a session. 

And thereafter, the user is able to visit our restricted routes because now this
cookie is sent with every request, on the server we can connect this cookie to a
session and in the session we have the information whether that user is signed
in or not and if the user is signed in, we can grant access to certain
resources, this is how authentication is implemented in any web application that
renders views, we'll learn a different way of adding authentication later when
we work with a rest and graphQL APIs but for a traditional web app as we are
building it here where we do render ejs or handlebars or whatever templating
engine you use, where we render such views, there we will use this session based
authentication approach. 

---