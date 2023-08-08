## 471. Using Stubs

<strong><em>no description</em></strong>

To solve that issue that we had. 

We have an external dependency with some method. 

Well, to solve that, we can use marks or steps, which means we essentially
replace this verified method with a simpler method. 

Now, how can we do that? 

Well, first of all, let's import JWT here by requiring JSON Web token. 

And what we can do now is in here, we can, of course, call, JWT, verify and set
as equal to a new function. 

That simply returns an object where we have the user ID field, which is a C, for
example. 

So what we're doing now is we're overwriting the actual verify method that this
package has. 

We're overwriting it and the way module imports work in Node.js, if we overwrite
it here, this will be the case in the middleware when it runs too, because we
have one global package, so to say, which is used here. 

So we overwrite this with our own function. 

Now, if I run NPM test, our own function gets executed and that will return a
user ID in that object it gives us, and therefore it will, first of all, not
throw an error. 

And it also gives us a way of pulling out our user ID. 

And so now if I run my tests, this will still fail. 

But now it fails because we expect it to have a property user ID, but actually
we don't. 

We only have an object with a get method because we only have this object. 

We don't have a user ID and now we can look into our code and see, oh yeah,
maybe we should add this code again to make sure we do store that user ID in the
request object. 

And now if we re execute NPM test we have for passing tests and that is because
we actually replaced the built in verify method and that is a common way of
handling such cases. 

However, instead of manually overwriting it like this, there is a more elegant
way because this has a huge downside. 

Which downside does this approach have? 

It becomes evident if I cut this test you just wrote and I put it in front of
the test we had before that this is the test where it should throw an error. 

If we have an invalid token, please note that before all tests passed so we did
get an error for an invalid token here. 

However, we're then overwriting verify to basically never throw an error. 

So now after I switch the order of tests, I actually have a problem with my last
test because this does not throw an error anymore. 

Why? 

Because in this test I globale replaced the verify method here. 

That, of course, is not ideal. 

It's good for this test to succeed. 

But it means, of course, that if I have any other test that needs the original
Verify method, it now has no chance of getting that because we replaced it here.


And therefore, instead of manually stopping or marking functionalities and
replacing them, it's good to use packages that also allow you to restore the
original setup. 

For that, we'll install that extra package, which I mentioned earlier already
with NPM, install dash dash save death and its name is Sinon. 

Sign in is a package that allows us to create a so called step, which is a
replacement for the original function, where we can easily restore the original
function. 

Though to use that, we simply import Sinon by requiring well, sign in here at
the top of our testing file where we need it, and then in the place where I want
to replace verify instead of manually replacing it like this, I call Sinon step
and I pass in the object where I have the method I want to replace that is JWT. 

And of course the official sign and docs are the place to learn all about this
package and all the different ways of using it. 

So here for setup I pass on the object which has the method I want to replace
and then as a string the method name. 

Right. 

So I have two arguments here. 

JWT is the object that has the method. 

Verify is the actual method. 

Now sign and will replace that and by default it replaces it with an empty
function. 

That doesn't do anything special. 

Though that's not entirely true. 

It actually will do things like registering function calls and so on, so that
you can also test for things like Has this function be called no matter what it
executes? 

So now as a next step with that being stepped. 

We can actually reach out to JWT Verify, which now is a startup and there we can
call returns. 

And this is now a method that was added by CNN. 

So now verify is in the end, an object you could say that cannot be executed,
but that also can be configured and returns allows us to configure what this
function should return. 

And here it should return a JavaScript object with a user ID key, which could be
a, b, c. 

Now whenever we call JWT, Verify will actually call that stuff. 

And the great thing is after checking our expectation here, we can now call JWT,
Verify, Restore and this will now restore the original function. 

That's the big difference to our own setup, where we replaced this on our own. 

Because now if I run NPM test again, all tests pass again because I actually
restore the original function after this test where I needed a different
behavior. 

Now, just for completeness sake, of course, we can now also test if request has
a property. 

User ID with a certain value. 

That's an optional second argument you can pass to that property, to that
property method. 

So we want to make sure that the value is ABC. 

Of course, that's kind of a redundant test because we define the value here. 

So of course it is that value, but it could rule out that we, for example,
manipulated this here and added user ID here in front of this to concatenate a
string, because now this would fail and we would detect bugs like that and it
would only succeed if I get rid of that and really store or store the raw user
ID now everything passes. 

So that is something. 

And as I mentioned, this stub also registers things like function calls. 

So if you want to find out if this has been called at all. 

So if the verify method has been called, you can call expect JWT Verify called. 

To be true, for example. 

Now if you run this. 

It succeeds because the Verify method has been called in our off middleware. 

And if we now, for example, comment this out and we set decoded token to just an
object where we have a user ID, well then our, our tests would normally still
succeed, but we do actually get an error here because we expect that false to be
true. 

Well, we expect that because now. 

This check here whether verify has been called gives us false, but we expect it
to be true. 

But indeed it has never been called. 

So now we could fix such an error here. 

Of course that was a made up example, but it is easy to imagine scenarios where
you have code, where you change something and suddenly you have an extra if
check which has a tiny bug and some method that should be called doesn't get
called anymore because you don't make it into that if check. 

Well, this allows you so this here allows you to detect such cases. 

So this is how you use steps you can replace built in methods with empty methods
in case you don't care about the return value and what they do, or you define
what they should return and you can then find out whether they have been called.


You can use that return value you set up. 

So you have a very powerful way of replacing some external methods and still
restore everything once you're done so that our tests that might need the
original functionality still work correctly. 

---