## 80. Templating Engines - An Overview

<strong><em>no description</em></strong>

I already mentioned at the beginning of this module that for putting dynamic
content into our html pages, we would use something called templating engines. 

Templating engines work like this, we got a html-ish template and with that I
mean that you typically write some code, some file that contains a lot of html,
your html structure and markup, your style and javascript imports, all of that
is typically included but you have some blanks in there, some placeholders. 

And then you have your node express content in your app, like our dummy array,
our products array we're currently using and you've got a templating engine
which understands a certain syntax for which it scans your html-ish template and
where it then replaces placeholders or certain snippets depending on the engine
you're using with real html content but that content, this html content it uses
there is generated on the fly, on the server by the templating engine taking
that dynamic content into account. 

So for example you could output anun ordered list with list items for the data
you have in your node express app with the help of the templating engine and in
the end, the result will be dynamically, on the fly generated html file which is
then sent back to your users. 

So the users never see the template, they never see the placeholders, all that
happens on the server, they just get a normal html page but it's not hardcoded
by you as it currently is in our project but instead, it's generated on the fly.


Now we got a couple of different available templating engines and actually, you
get even more options than I'll show you here, at the end of this module, you'll
find some useful links to dive deeper into them and learn about more
alternatives. 

The three options I want to present to you are the three most popular ones,
we've got ejs, pug formerly named jade and handlebars. 

Now these are free templating engines that use a different syntax and different
set of features, different philosophies that you can use to well create these
templates, inject your dynamic content and get html files out of them. 

Here's a brief, a very brief look at how their syntax looks like but I will also
present all three of them in this module. 

Ejs looks something like this, you write normal html markup but then you also
add like this smaller than percentage sign and then sometimes an equal sign,
sometimes not depending on what you're doing, you will see that in this module
and then the dynamic content you want to output. 

So if we had some name variable being injected into our template and you will
learn how that injection works, if we got that then the value of our name
variable would be output there and we would send back an html file with a
paragraph tags and the value that was stored in name between them. 

Pug uses a different syntax, it doesn't use real html, it replaces this with a
minimized version or a minimal version and then it also allows you to output
dynamic content with this syntax, the hashtag curly brace syntax for example. 

Handlebars in turn uses html again but then you have the double curly brace
placeholders for the dynamic content, so similar to ejs, actually handlebars has
a bit less features available you could say or it follows a different philosophy
but it's closer to ejs, pug is the well the outlier here which also uses a
different html syntax. 

So a short summary would be ejs, normal html and then actually you got these
placeholders which allow you to just use plain javascript in them actually, so
you can also write if statements, for loops. 

Pug use as a minimal html version and a custom template language which is
extensible but generally offers only a set of things, of operations you can do
but if statements and lists would be included, iterations would be included. 

Handlebars uses normal html but also a custom template language with a limited
set of features, again including common things like if statements or lists. 

So these are three popular templating engines, now let's briefly dive into them,
how we install them and how we use them before we then pick the favorite for
this course and stick to that favorite and again at the end of this module,
you'll find more resources on all these engines. 

---