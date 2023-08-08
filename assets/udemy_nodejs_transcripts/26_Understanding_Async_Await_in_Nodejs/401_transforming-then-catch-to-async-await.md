## 401. Transforming "Then Catch" to "Async Await"

<strong><em>no description</em></strong>

So now that we had a brief look at how asynchronous code can be identified and
what is important about asynchronous code and that you can use callbacks and
promises to handle asynchronous code, now that we learned all that, let me
introduce you to async await. 

To use that, you first of all have to prepend the async keyword in front of a
function, like this arrow function here, so this function where you plan to use
the await keyword, so where you want to use these two keywords, they always are
used together, async in front of the function and then you can tweak this
syntax, you can write this syntax almost as if it would run synchronously. 

You can get your count, a new constant or variable you create by awaiting post
find count documents and then you would get rid of this then block here, you
would instead continue here or you directly store your total items here to be
precise, you can get rid of this line now and you get rid of this return
statement and instead you continue with the next line, post find limit, this
gives you back a list of posts, so what you currently have in that then block
and you again write it like this, post await, post find and then this whole
statement that in the end would be followed by a then block. 

If you now get rid of the then block like this, let's comment out catch because
that is something we'll care about in a second and now if I reformat this, this
is our adjusted code, this is using async await and this now looks like the
normal javascript code we write but behind the scenes, async await takes your
code and transforms it into the old then-like structure we used. 

So it uses then behind the scenes, we just can't see it and we have this more
convenient way of writing our asynchronous code. 

Now I haven't used this in this course thus far because I think that if you're
relatively new to javascript or node, this can quickly lead you to think that
this works just like the other code langs and indeed it doesn't. 

Always keep in mind, await just does some behind the scenes transformation of
your code, it takes your code and adds then after it gets the result of that
operation and then stores it in total items and then moves onto the next line,
executes that inside of that then block it creates here implicitly, so basically
the exact same code we had before, this is done by async await behind the
scenes. 

But if you know, if you understand this, then this can be a syntax you might
prefer, you don't have to, you can absolutely use the other one with then and
catch but you might prefer this one. 

Now back to catching, how do we handle errors now? 

Well since this now runs almost like asynchronous code, we use try and catch. 

So we try something, we try some code, this code here to be precise and we then
catch an error, like this which we then handle in there with the code we
previously had inside of catch, like this and therefore you still have to next
an error here because keep in mind, behind the scenes this gets converted to
then and catch as we used it before. 

But now with that, we have transformed this first snippet where we used promises
to async await and we can see that. 

If I now save that and I go back to my running application, let me quickly log
in and open the developer tools to see if we get any errors and I currently got
no posts so I'll quickly create one, a test post. 

We'll take that duck again, this is just a test, let me hit accept here and this
looks good. 

Now if I refresh, we definitely fetched a post and this still works. 

So all that code still works, we also get no error here on the backend and now
we transform this to async await. 

---