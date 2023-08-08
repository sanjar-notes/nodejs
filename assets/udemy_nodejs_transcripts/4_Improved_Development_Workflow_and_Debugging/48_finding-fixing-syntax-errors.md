## 48. Finding & Fixing Syntax Errors

<strong><em>no description</em></strong>

Syntax errors can be very annoying but most of the time, they're not that hard
to fix. 

Let's add a simple syntax error, here in app.js let's simply remove the t in
const, now all of a sudden, this is an invalid keyword, it doesn't exist, it's
not a keyword and we already get some help in the IDE which is showing us
something is wrong here. 

Now if we hover over this, we see that a semi-colon is expected and actually
this is not that helpful and this is simply because visual studio code thinks so
that this is a variable and since we have a variable in the same line, we should
close this with a semi-colon and now it actually doesn't show an error. 

But let's save this and let's try running our app with npm start without that
semi-colon we added. 

And you will see, it right away crashes and in there we see unexpected
identifier const server. 

So in the end, whilst it doesn't clearly tell us that we forgot the t here
because it's not smart enough to understand that this is the error here, we
still see that the error seems to be stemming from this line and in such cases,
as dumb as it sounds, you should simply take a closer look at this line and see
what could be wrong there and you should quickly be able to see I forgot a t
here. 

So these are syntax errors, other errors would be that you maybe go to the
routes.js file and let's say you forget a closing curly brace here. 

Now again visual studio code does complain and does show an error over there, 
if we jump there we see at the end that the closing curly brace is expected. 

Now it's not expected at this point where it's showing this message but it's
expected somewhere in the file and whilst it can be cumbersome, you should then
check your block statements like this if statement and see if there are all
closed correctly. 

In visual studio code, you also get some help because if you click next to such
a curly brace, you'll see that this line gets highlighted and it actually shows
you where it thinks that this is getting closed and this is far too much at the
bottom here for example. 

Again if you run this, you will see that it crashes and there, you also see
unexpected token and it points us at routes.js . 

and then you see the line number too. 

So here it points us at line 52 and it basically shows us the same place as
visual studio code which is the wrong place but in such a case here, you should
really take the IDE help, see that error message and then go through your file
and see hmm where could I be missing a character or where do I have an extra
closing curly brace or something like that and eventually you should be able to
find this error and therefore of course fix it. 

So syntax errors should always result in an error message and then that can
sometimes be hard to find them, often it's like a typo, a mistyped variable name
of a variable that therefore doesn't exist or missing or extra characters but
you can find them and it just takes some time to go through your file. 

---