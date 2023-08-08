## 465. What is Testing?

<strong><em>no description</em></strong>

What exactly is testing? 

Well, we're writing our code, obviously. 

That is what we did throughout this course. 

And we manually tested this code with that. 

I mean, we simply visited the page. 

We send requests to our API. 

Now, the big advantage of this approach is, of course, that we can see our page,
we can really see the page as our users will see them. 

We can interact with our API as any developer would interact with it, and
therefore manual testing is super important. 

But there also is a downside. 

It's easy to forget to test something. 

It's easy to only test some parts. 

And especially when you make changes to your code, it's easy to break something
in some place of your app, which you might not think you're breaking and you're
not testing it explicitly, and therefore you introduce a bug which you only find
later or maybe never at all. 

That, of course, is the downside, and it's pretty hard to test every possible
feature and every possible combination of steps in your application after every
tiny change you make. 

And that is where automated testing comes into play. 

Automated code testing means that we write code that tests our code. 

So we define steps that are executed, we define certain scenarios that are
tested, and we automatically run these tests on every change or after every
important change we made so we can run them whenever we want. 

We can even put them into our deployment process and run them right before our
app gets deployed and Dad will throw an error at us whenever some of our tests
fail. 

And we can then look into these tests and find out why they failed and fix them.


The big advantage of automated testing, therefore, of course, is that we can
cover all core features and we can define all possible scenarios you want to
test and therefore really make sure that we don't introduce breaking changes. 

But of course there are downsides to automated testing too. 

If you write the wrong tests, then you might have a good feeling because all
your tests are passing, but maybe you're just testing for the wrong things, for
the wrong scenarios. 

Additionally, well, you only test what you define and it's also hard to test the
user interface, so you might not really see what your users see. 

So it's a combination of both manual testing, which we did throughout the course
and which you naturally do, and automated testing what you'll learn about in
this module. 

---