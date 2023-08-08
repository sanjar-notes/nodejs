## 466. Why & How?

<strong><em>no description</em></strong>

I kind of answered why we want to test already, but I really want to make this
clear again, testing. 

So and with data, I mean, automated tests allows us to automatically test
everything and there is a star behind that because we only test what we define,
so only the tests we write. 

But in theory it allows you to test everything in your application after every
code adjustment, after every code change. 

Therefore, it's easy to detect breaking changes, even in places you might not
have expected to break upon your latest change. 

And with the automated tests, we ensure that we have predictable, clearly
defined testing steps. 

Our tests obviously always run in the exact same way since we define all the
steps in code, and that of course ensures that we can rely on the scenario
always being the same. 

If you're manually testing your app, you might think you're doing the same thing
as you did the last time, but in reality, you might not be doing that because
you forgot a step. 

So that is why you should test. 

How do you then set up your node project for testing? 

No matter what you're building with no charges. 

So no matter if you're building a page where you render views on the server, if
you are building a rest API or if you're building a GraphQL API, you want to run
tests automatically. 

So you want to run code that tests your code. 

And for that you typically need a couple of tools. 

You need a tool that executes your test code. 

Sounds pretty simple, but you need that and it should not only execute your
code, it should also give you a nice output that tells you whether your tests
all passed or if a test failed. 

So that is the first tool we need. 

The second tool then is one that does not just run our code, but that also
allows us to define certain conditions that have to be met. 

So we want to assert certain results. 

You want to find out if certain scenarios well succeeded, if tests succeeded. 

We wanted to find what success means in a certain test. 

So we want to validate the test outcome. 

Now for running the tests, there are different tools for all these steps, but
for running these tests, one popular framework is MOCA and we'll use MOCA in
this module here too. 

And for asserting the results and defining conditions. 

Chae is a popular choice and we'll use that in this module too. 

There are alternatives like Jest, but MOCA and GI are really popular, exist for
a long time. 

There are a lot of tutorials out there for you to dive deeper and therefore I
will also use them here. 

You're certainly not doing anything wrong when sticking to these tools. 

Now, as you will see throughout this module, there will also be one ever tool we
need when it comes to managing side effects or working with external
dependencies or certain complex scenarios. 

There we'll use Sinon, which is a tool that allows us to create steps or mocks,
and I will come back to what that is later. 

Now with that all out of the way, I'd say let's install our basic testing tools
and let's set up our testing environment and then also write our first test so
that we can gradually walk through our node application and see how we could
test it. 

---