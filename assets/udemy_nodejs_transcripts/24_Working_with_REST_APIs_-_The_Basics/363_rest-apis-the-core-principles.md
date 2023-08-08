## 363. REST APIs - The Core Principles

<strong><em>no description</em></strong>

We're almost done with the theory part, now there are some core principles that
are indeed defined in theory and that are important for you to keep in mind
where at least there are two core principles I want you to keep in mind when
building rest APIs. 

The first one is the uniform interface principle, this simply defines that your
API will have or should have clearly defined API endpoints, you remember
endpoints were the combination of http methods and paths with clearly defined
request and response data structures. 

Put in other words, your API should be predictable and if possible and if open
to the public, it should also be well documented. 

So people should know which data does your API expect, which data does it give
back, which endpoints do I have and the thing that happens when a request
reaches to an endpoint should of course not change over time, it should be
predictable, it should be clearly defined. 

The second important principle I want you to keep in mind is the stateless
interactions principle and this will be super important when we later talk about
authentication. 

When building a rest API, the server and the client are totally separated, they
don't share a common history. 

So no connection history is stored and no sessions will be used  therefore
because every incoming request is treated as if no prior requests were sent. 

The server has a look at every request on its own, it does not store a session
for the client, it does not care about the client at all actually, that is also
a cool thing about resting APIs. 

You can build a rest API, open it up to the public like the Google Maps API is
for example and you don't care about the individual client, you just say hey
here are the endpoints I have, here's the data you get back for each endpoint,
here's the data I expect from you for my endpoints and then I don't care about
you, I don't store a session with you. 

We have a strong decoupling of the client and the server even if they were to
run on the same server because we're building our own API for our own frontend. 

We still would decouple both so that they work independently and just exchange
data. 

This means that every time we set up a new endpoint, we have to make sure that
it works independent from prior requests and a typical problem here is
authentication where once we logged in, future requests should be treated as
logged in and I will show you how to solve this in this course too of course. 

Now other principles which are less important or which you don't need to learn
by heart is the cachable principle which means on your rest API, you could send
back some headers that tell the client how long the response is valid so that
the client may cache the response. 

Client server separation is mentioned again, here it's more thinking about the
data storage, client and server are decoupled as I said and the client should
not worry about persistent data storage therefore, the server will be
responsible for this. 

We may have a layered system which simply means as a client when we send a
request to an API, we can't rely on that server we sent it to you immediately
handling the request, the server might instead forward the request or distribute
it to another server, Uultimately we only care about the data we get back which
should of course follow the structure that was defined by the API. 

Code on demand is a last optional principle and this basically just means the
rest API could also for some endpoints transfer executable code to the client. 

Now to be honest, in reality you don't see that too often, we're mostly talking
about well normal data we're using but still, these are the rest principles, the
top two ones are the important ones which will have great implications
especially on authentication. 

---