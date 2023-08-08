## 389. How Does Authentication Work?

<strong><em>no description</em></strong>

So how does authentication work in a rest API then? 

Well we obviously still have our client and server and the client still sends
authentication data to the server, so the email and the password let's say. 

In the past, we then would have checked that data on the server and if it is
valid, we would have established a session. 

Now we don't use a session anymore because restful APIs are stateless, they
don't care about the client, you learned about that strict decoupling of server
and client and every request should be treated standalone, that means every
request should have all the data it needs to authenticate itself. 

With a session, the server needs to store data about the client, the server then
stores that a client is authenticated and that's just not how rest APIs work. 

The server will not store anything about any client, so we don't store sessions
on a rest API and therefore this approach will not be used anymore. 

Obviously we will still validate the input on the server, we'll still check for
the validity of the e-mail password combination but then instead, we return a
so-called token to the client. 

That token will be generated on the server and will hold some information which
can only be validated by the server and this token will then be stored in the
client, so there in storage in the browser, there are specific storage
mechanisms for this and the client can then attach this token to every
subsequent request it sends to the server. 

So this stored token is then attached to every request that targets a resource
on the server which requires authentication. 

That token can only be validated by the server which created the token and if
you change that token on the frontend or you try to create it to fake that you
are authenticated, that will be detected because the server used a certain
algorithm for generating the token which you can't fake because you don't know
it or you don't know the private key used by that server for generating the
token to be precise. 

That token contains json data or javascript data in the end plus a signature
which as I mentioned is generated on the server with a special private key which
is only stored on the server and this gives us a so-called json web token. 

This json web token is then returned to the client and the signature as I
explained can only be verified by the server, so you can't edit or create the
token on the client. 

Well you can but then the server will detect this and will treat the token as
invalid. 

This is how we generate the token or how we do authentication in rest APIs. 

We have the token which can be checked by the server but which does not to be
stored on the server and this gives us an elegant way of authenticating requests
in a rest API world. 

Now let's implement this. 

---