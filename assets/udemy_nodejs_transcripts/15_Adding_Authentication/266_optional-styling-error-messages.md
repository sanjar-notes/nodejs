## 266. Optional: Styling Error Messages

<strong><em>no description</em></strong>

I'm outputting that error message, I just want to style it a little bit now and
for that I'll give it a css class and I'll simply name that user message and
then maybe user message --error using some BEM styling here, that's a css
styling convention or a convention of naming your classes. 

Doesn't matter too much, you can name this whatever you want in the end, I added
these two classes, one to have a general message look and then one for errors
because maybe we also want to be able to output success messages later. 

So with that, let me quickly add this to some css files and you can skip this
lecture if you want, in the next lecture you find the finished code attached
which you can use. 

In the main css, I'll quickly add this, let's say at the bottom of this file,
it's up to you right before the media query maybe, I have my user message,  so
this css class I just added here and let's say such a user message should use a
margin auto to be centered, get a width of 90% by default, I'll also set up some
styling in case I'm on a bigger screen, there user message will have a width of
let's say 30rem and then here I'll give it a border of one pixel solid and let's
use maybe some bluish color here, maybe not that blue, well basically which ever
blue color you want, maybe this one and a background color, I'll also use a blue
here, also a different blue, so some light bluish color here so the general info
message should have maybe some neutral color, so some blue like this and let's
see how that looks like. 

With it added, let me try entering an invalid email again, looks like that, well
not too pretty, that should be much lighter. 

I also want to have some padding in here, maybe 1rem and let's give it some
rounded corners as well and now with that, if we enter an invalid email that
looks much better. 

Ok so now this is my general info message, let's also maybe also center the text
if we want to and now let's give this an error version basically with --error,
that's the other class I added to this specific box in my login screen and there
I will change the border color to be red and the background should be a light
red, so let's start with red and then turn this into a light red and now if we
try this again, now it looks like this. 

Ok so this could be the error message we're outputting here, you could also turn
the text red if you want, so you could also say text color should be red here
maybe and reduce the padding maybe to .5, that could look a bit better, so an
invalid email or password, that looks good. 

Now I always have that stickaround now, reason for that is if I go back, error
message seems to be set to something even if we're not having a message in there
and that is something I'll check in the next lecture. 

---