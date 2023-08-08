## 54. Changing Variables in the Debug Console

<strong><em>no description</em></strong>

There's one more feature about the nodejs debugger which I also haven't shown
you yet but which I of course don't want to forget. 

If you start debugging here and here I just use the shortcut and you place a
breakpoint anywhere in your app and then do something to trigger that
breakpoint, I showed you that you can look into all these variables and that you
can look into them in the debug console without changing them. 

Well sometimes you might want to change them and that can be done by going to
the debug view here and then by simply typing in there. 

Now for example, the parsed body holds this string and you can't just change it
and now this will affect the runtime as you can see if you hover over this. 

So now if I just resume execution with my code which doesn't have a bug right
now and I go back to my explorer view here, then you will see that I stored
testing here which is the value I edited in the debugger. 

So you can actually manipulate the values there of the variables and so on if
you need to, you can do that because this of course allows you to make sure that
you can quickly test something. 

This is just another useful feature which I wanted to share with you since it
can help you with debugging your code, being able to manipulate some values
there. 

---