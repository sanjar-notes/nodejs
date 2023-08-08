## 2. What is Node.js?

<strong><em><p>What is Node.js?&nbsp;That's the most important question in a Node course I'd argue and in this lecture, we'll explore what exactly NodeJS is and why it's amazing.</p></em></strong>

So let's dive into the most important question, what is nodejs? 

Nodejs is a javascript runtime and now what does this mean? 

You know javascript, it's a programming language you typically use in the
browser to manipulate your dom, to manipulate the page which was loaded in the
browser, for example to open a popup, a modal or add any kinds of effects
because Javascript is a language that runs in the browser that allows you to
interact with the page after it was loaded and it therefore is a crucial part
when it comes to building interactive user interfaces in the browser, so
whatever your users see. 

However javascript is not limited to that. 

Nodejs is a different version of javascript you could say, it is basically built
on javascript, it adds some features to it, is not capable of doing some other
things you can do with javascript in the browser, so it basically takes
javascript and puts it into a different environment. 

It allows you to run javascript code on the server you could say, in theory not
just on the server but on any machine though. 

So it basically allows you to run javascript not just in the browser but
anywhere else like a normal programming language, like normal programs on your
computer or some computer in the Internet effectively making it a great choice
for building web applications that run on servers which are just computers
running somewhere in the Internet. 

So in detail, this means that we can use nodejs to run javascript outside of the
browser, that is the core takeaway, now how does this work technically? 

Well nodejs uses v8 and v8 simply is the name of the javascript engine built by
Google that runs javascript in the browser, so back to the browser we now are. 

V8 is simply the name the creators gave their engine and what does an engine
mean? 

Well it simply means that engine takes javascript code, the code running in your
browser then or in node's case which builds up on v8, also the nodejs javascript
code, it takes that javascript code and compiles it to machine code and this is
what your browser does too, what v8 does in your browser. 

It does take your javascript code and compile it to machine code because that is
the code that runs ultimately on your computer and that can be handled
efficiently. 

Now this is done by v8, v8 itself is written in C++ but that doesn't really
matter too much for you, you don't need to write any C++ code to use javascript
or nodejs but nodejs basically takes that v8 codebase which is written in C++
and adds certain features like for example working with your local file system,
opening files, reading files, deleting files, these are all things which are not
possible in the browser, you can't access your local filesystem in the browser
for security reasons, so this is not supported. 

Nodejs adds these features to v8's engine you could say so that you can suddenly
do that. 

Now nodejs does not run in the browser so these restrictions still apply, there
you use vanilla v8, so v8 only without the nodejs extensions but if you then
install nodejs, you can use it to basically use that extended v8 version to run
javascript scripts on your computer which then suddenly can access these new
features because they don't run in the browser but are directly executed through
that nodejs runtime you could say. 

So this is how that works together and what nodejs does. 

It allows you to run javascript on your computer and it adds useful
functionalities to the javascript engine so that you can do more useful stuff
there than you can do with browser side javascript. 

Now one important note maybe on this point also is that of course some features
are also taken away. 

In the browser you use javascript to interact with the document object model, so
with the html elements on your page, if you just execute a javascript file
directly, you of course have no attached page and therefore these features are
missing. 

But this is a lot of theory, why don't we just have a look at this and see how
we can install and use nodejs and what it actually does for us. 

Let's do that in the next lecture. 

---