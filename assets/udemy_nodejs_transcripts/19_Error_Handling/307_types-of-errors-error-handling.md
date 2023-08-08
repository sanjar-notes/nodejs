## 307. Types of Errors & Error Handling

<strong><em>no description</em></strong>

So how bad are errors? 

Now errors are not necessarily the end of your app, you can recover from the
errors, you can inform the user that something went wrong and that he should try
again for example, you just need to handle errors correctly that is the key
takeaway and there are different types of errors. 

We can have technical or network related errors where you have very little
influence on at least if you're not the system administrator, we have so-called
expected errors and this is not an official term, that is something I came up
with and I'll explain what this is in a second and we also have bugs or logical
errors in your code. 

Now for technical errors, our mongodb server might be down and therefore any
interaction with the database will fail. 

In such a case, there's not that much we can do, the best thing might be to show
some error page to the user to let the user know that something is wrong on our
end, that we are sorry and that we're working on fixing the issue. 

We also might want to behind the scenes send an e-mail to the administrator or
anything like that. 

We also have these expected errors as I like to call them. 

There are certain operations, let's say we are interacting with a file or with a
database that can fail, not very often and of course it's not really expected
for this to fail but that can happen. 

Maybe because there are too many simultaneous requests to a certain file,
anything like that. 

Here informing the user and giving the user the ability to retry might be a good
solution. 

For example the validation errors which we also implement in earlier module,
these would also be expected errors, users will input valid and invalid data and
for invalid data, we want to inform the user and give the user the chance of
retrying and of course we also have errors in our code where we interact with a
user object in a place where it just can't exist or at least not in all
circumstances. 

We should fix such errors during development, we should test our code and we
should fix such issues of course, these are not errors we should handle at
runtime, we should not show a message to the user because these errors are not
the users or the network's fault, they are our fault. 

So how can we work with the different types of errors then? 

We have to differentiate. 

There are errors where an error is thrown, an error is a technical object in a
node application. 

So there is a built in error object which we can throw that's also a javascript
language features, basically all programming languages have such a feature. 

We also can have scenarios where we can't continue with our code but there is no
technical error. 

An example would be that we try to log a user in but the email address does not
exist, this is not really a technical error, there is no error being thrown but
we know we can't continue and so we want to check for this scenario as well and
handle it appropriately. 

Now for the errors thrown part, we have certain tools we can use to test code
and catch potential errors so that we can handle them gracefully and for
synchronous code, that would be try catch blocks. 

For asynchronous code with promises, we have then and catch which you already
saw quite a lot throughout this course. 

In the end in both scenarios, we then have the choice if we want to directly
handle the error or if we use a mechanism built into express, a special error
handling middleware which we haven't used thus far which you can use to catch
errors and then return a response to the user and I'll show how this works in
this module of course. 

For this scenario that no error is thrown, well we just have to check values
with if checks for example and then we can decide whether we want to throw an
error, to kind of enter the left world here and then kick off that error
handling process or if we want to directly handle the error which is not a
technical error but where we simply add some code that can continue with the
missing input data for example. 

In all cases, we've got different ways of communicating with our users. 

We can return an error page, so a dedicated page that informs the user hey we
have a problem and that of course should be kind of the last resort because
there the user loses all his input, can't continue. 

We also can return the page which user was on and just give some error
information, that is what we did for validating for example, there we returned
the page the user was on, kept the input values and just added an error message.


Or we could redirect, for example if we try to access a page which we are not
authenticated to visit, then we can redirect the user. 

So these are the different tools we have, the different ways of working with
errors we have and now let's dive into our code and see what we're already using
and what we can use. 

---