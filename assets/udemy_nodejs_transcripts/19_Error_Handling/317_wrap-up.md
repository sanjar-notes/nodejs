## 317. Wrap Up

<strong><em>no description</em></strong>

That's it for this module. 

We had a look at the different types of errors and how to handle them. 

You can differentiate between a couple of different errors, there are technical
errors where you get this error object and where some place in your application
throws an error with the throw keyword and you can do that on your own or some
package or express or node itself does this and you can handle these errors with
try catch or with then and catch in a promise for example and there are expected
errors. 

These are errors which are not technically errors, there is no error being
thrown, at least not necessarily but there you could be dealing with invalid
user input and invalid email or some file access that should work most of the
time but might fail occasionally. 

Depending on how you treat that, if you throw an error or not, you might still
need try catch or then catch here as well but you could also just use an if
check to see does that e-mail address exist in the database, so normally if
check could do there. 

And if you want to throw an error or if you want to forward an error in then or
catch, you learned that you can use that global express error handling
middleware of which you can have multiple which are then executed step by step,
you can use that and express will automatically call it whenever you next an
error or you throw an error in synchronous code. 

We also had a brief look at status codes and it is a good practice or it is
definitely something you should consider, that you set the right status codes on
your responses so that you don't always return 200 codes but that you instead
let the browser know about certain issues and that will become more important
later in the rest API section of this course when the browser gains more power,
when more UI logic is executed in the browser. 

And you've got different types of status codes, you can have success codes, the
2x codes, redirects, client side errors and server side errors and you should
look at all these codes and see which code is best set for your scenario, your
use case. 

Important as I mentioned, when you set a status code, this does not mean that
the app crashed or that the response is incomplete, it's simply an extra piece
of information you pass to the browser. 

---