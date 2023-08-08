## 313. Updating the App

<strong><em>no description</em></strong>

We had a closer look at error handling, now let me remove that code here where I
create a duplicate ID so that it works again. 

I hope you got an idea of how error handling can work and how we can use that
central error handling function or our own logic which we have in place all the
time where we check for the existence of a product and redirect otherwise and so
on. 

So we get a bunch of code already in our application where we do handle a
certain situations which we want to avoid of course and you can always be more
creative and handle them in a better way. 

For example here and get added product, if I don't find a product, I redirect to
the starting page. 

Now you can of course enhance this and you could redirect back to the admin
products page and flash a message onto that page which you then output in the
ejs template to give the user more information on what went wrong, I'm not doing
this here to not spend a lot of time on working on the UI only but these are all
things you can do. 

What I want you to takeaway here is that you have measures or that you have
tools for handling errors and one of the most important tool is to at least
handle all these catch blocks here correctly and therefore I will do that and
replace it with my catch block where I throw that error or where I forward this
error here because this allows me to at least centrally handle them with a 500
page, if I do nothing else, this is better than nothing. 

So I'll use that on all my catch blocks here, also in auth.js, there not for
this one here but for this one, I'll also add this catch block, the same for
this one, basically for all the catch blocks where I just log something to the
console, there I want to forward to the 500 page. 

Here as well and you can call that anywhere of course, not just inside the next
block whenever you create an error object and you next it and you avoid any code
being executed after this by returning next with the error, whenever you do
that, you end up in your express error handling function. 

And just because it's really important, this is just one way of handling this,
you also have all the other if checks and so on which we added, so this is just
my last resort here that I always do at least that if everything else fails. 

And now we should have an application which is a little bit more hardened or at
least shows some message to the user when something fails instead of just doing
well nothing basically as we did before because you want to avoid situations
where the app just crashes and you don't even tell the user, it's better to have
some code in place that at least returns an error page. 

And now with all these changes here, you should be able to still click around
and use that application as you did before, you can also delete for example, so
that all works. 

But now we got proper error handling in place for scenarios where something does
go wrong. 

---