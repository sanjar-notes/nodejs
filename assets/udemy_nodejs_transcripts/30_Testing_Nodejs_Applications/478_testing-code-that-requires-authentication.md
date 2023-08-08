## 478. Testing Code That Requires Authentication

<strong><em>no description</em></strong>

Now in the last lectures, you'll learn a lot of useful things. 

You'll learn about these hooks, which are super important for setting up and for
clean up work. 

You also learn that for a code that interacts with the database, it could be
fine to really use a database. 

It just should be a dedicated testing database. 

Now, of course, it's all fine to use stubs, as we did here. 

In case you don't really need or want that database access in case you want to
speed up your tests, you can setup functionalities. 

And of course, we could have done that down there too. 

But I want to show both and both is fine. 

Now, obviously, as always in the Internet, you'll find people arguing strongly
for either of the two directions. 

But in practice you find good arguments for both alternatives, and therefore you
should go with the one you prefer and you can even change it on a per test
basis, depending on a test needs to be faster or really doesn't care about the
database access or if checking that database code might be useful too. 

Like for our status here where we implicitly also check that our default status
assignment works because we're checking for that default status to find here in
the model. 

Now with that, let me wrap this module up by also testing some functionality
from the feed controller. 

And here the interesting part, of course, is that here we actually have code
that relies on the user being authenticated, like for creating a post here. 

When we create a post, we actually do access the user ID, which should be part
of the request object. 

Now why is the user ID part of the request object? 

Because of the of middleware right here we add that. 

So how can we now test this since we now have a controller that actually
requires on the off middleware doing its job? 

How can we make this work if we only want to test the controller and not the
full flow? 

It's super easy to make this work because whilst it could look difficult at
first, it's important that you configure your tests, you pass in a request
response object and the next function. 

And if you have code that tries to get something out of the request object like
the user ID of course in the real app that is set by the middleware and we are
actually testing this middleware. 

But for the controller, we can just fake that and we can pass in a request
object that simply has a user ID and we're done, that's all. 

So let's now write a test for create post and let's interact with the database
here and then also make sure we do create a post successfully here and for
example, validate that this post then really was added to our users posts array
for this. 

I'll add a new file here in the test folder and I'll name it Feed Controller
JJ's and I'll have a look at the off controller and actually I will copy the
entire content from there and they added in the feed controller and now of
course change some things. 

I need access to Mongoose and so on though because here again I want to connect
to a testing database. 

So in here I will not need the user model though, but the the post mode model. 

So let's get that from models post and of course not the off controller but the
feed controller which I get from controllers feed. 

Now I'll therefore describe this as the feet controller. 

Doesn't hurt, I guess. 

And now time for the initialization work we're connecting to the testing
database. 

Could also be a different one here for the post if we want to, but I want to use
the same one. 

I will actually set up my dummy user because I need a user. 

A user created a post and that should be my dummy user. 

And we could set up some dummy posts, especially when we're testing different
controller actions like getting posts and so on. 

But for creating a post, of course I don't need one, so my dummy user is all I
need. 

So the test set up here is fine for me. 

I don't eat before each and after each. 

But I only need one test case here, so I'll actually get rid of the other one. 

I'll keep the after hook here though, and clean my users so that our tests are
not affected by it. 

Our test files are not affected by it. 

It does test file. 

Your really works stand alone on its own. 

So now let's work on that single test there. 

I want to test whether a post is created successfully and then add it to the
post array of my user, the user who created it. 

So it should add a created post. 

To the posts over. 

Off the creator. 

Something like this. 

Now, I'll not stop here. 

Instead, I really want to interact with the database, so no need to use. 

Sign in here and stop anything. 

And. 

We have a look at that feed controller. 

We now see that we need a couple of things on the request object. 

On the request object, for example, we need a file object that in turn needs a
path which is the path to the image, doesn't have to be a real path, just needs
to be there so that we can extract it can be a dummy string, though. 

We need a title, we need a content because we're setting this on our post and we
need that user ID. 

So back in the off controller should be in the feed controller file here where I
configure my request. 

As we saw, we're retrieving title and content from the body. 

Then we have a file object which has a path key and we have a user ID. 

So in the feed controller in the bottom body here we have title, which could be.


Test post with the content. 

A test post really doesn't matter, of course, unless you're testing it. 

We need a file object which needs a path key which can be ABC doesn't matter and
we need the user ID, which can be z set. 

We just need these fields because we're using them in the controller. 

This will then save a valid post to the database and we'll then extract a user
with the user ID. 

And now here we already have the first trap we could run into. 

The user ID does actually matter because the creator we assign here does not
matter. 

But to really work later and to be connected to the user object in the database,
we need a real user ID. 

Thankfully we got one. 

We're creating a user with our own hardcoded ID here, so let's use that instead
of x, y, z and pass that in. 

So now the feed controller should be able to save a post and then make the
connection to a user and add that post to that user object. 

Now to check whether that really worked. 

I need to get access to. 

Our user object outside of this controller function. 

And for this we can just. 

Store are the result of user safe here in a safe user constant and actually
return that here. 

In that controller will not change the behavior of the controller. 

We still send the response status code and everything that still works fine. 

But now our test has a look of validating that created user. 

And now in the feed controller here, we're not calling off controller log in or
anything like that. 

Instead we're calling feed controller, create post. 

We pass in our request object. 

Now for the response object, we need to make sure that we don't get an error. 

So we need to provide a status method and adjacent method even if we don't care
about what they do. 

But we need them. 

So I pass in a dummy response object here to which is an object which needs
these two methods so that they can be called without throwing error. 

So status is a function that does nothing and Jason is a function that does
nothing here. 

Why are they not doing anything? 

Because for this test I don't care. 

So I pass in this and I pass in this dummy next function here. 

Now this is an async function. 

We have the async keyword here and therefore it returns a promise automatically
and hence in the then block here. 

I want you to define my expectations. 

Now I know that we get something back here because I'm returning that saved
user. 

Now, by the way, if you're not liking this pattern of changing the controller
just so that we can test this. 

Of course, the alternative would be to simply test some other controller action
that actually needs that user object with its post and then simply call create
post and then that other controller action to and execute two controller actions
in the same test and only test something on the result of the second action. 

But here, I'll just beat this up and merge this into one controller action. 

So here I get my saved user and I expect that saved user. 

To have a property of posts that should be set. 

And I expect saved user posts. 

Do you? 

Have. 

A length. 

Of one. 

Because there should be one new post added to it. 

And thereafter we called none. 

Now let's give this a try. 

Let's run NPM test here. 

This will now take a while because of course, we have a couple of different
tests. 

Now, of course, I get an error here because I have an issue in my testing file. 

I'm importing the post model. 

But this of course, was incorrect. 

I'm actually not using the post model here. 

I need a defeat controller. 

But regarding the models, we still need to use user controller of course,
because I'm creating a user. 

So that's my mistake here. 

Let's quit that process and rerun NPM test thereafter so that now we don't have
an error here in the testing file. 

And now here, I'm getting an error. 

Target cannot be null or undefined, and that is stemming from our validation
here in the feed controller, as you can see. 

And we only have one test case in there. 

So it's this test case. 

So saved user seems to be null or undefined, even though I'm trying to return it
here where I store my saved user. 

And that actually still is an issue with my testing set up. 

I do define my response object with status and JSON functions. 

Now the tiny problem I have, if we watch closely, of course we're calling the
Jason method here, not on the response object but on the result of the status
method call. 

So for that to work back in a feed controller, we need to make sure that in this
function here for a status which we call first, we return this so that we return
the number reference at the entire object, which then has switched and has this
JSON function here. 

So now with this adjustment, let's run NPM test again. 

Let's see if we now succeed. 

And this looks better. 

It's now passing your cue for the feed controller. 

And if I would check for a length of zero here, for example, then it actually
should fail. 

So if I now let this run. 

Now you see it failed. 

And if we scroll up, we see it failed. 

It expected a ray with a length of one to have a length of zero, but got one so
correctly it failed and it doesn't fail. 

If I check for the correct length. 

Now, this is another example for testing here. 

The feed controller clearly as you can see. 

And now with that, we wrote quite some nice tests here. 

I hopefully gave you a good introduction to how testing works and how you
generally have to think about it. 

Now let me wrap this up, because I know that at this point it still can feel
entirely overwhelming and it doesn't have to be. 

---