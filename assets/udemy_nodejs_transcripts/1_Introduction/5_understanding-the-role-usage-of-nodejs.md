## 5. Understanding the Role & Usage of Node.js

<strong><em><p>Node.js can be used for a broad variety of things - web servers being the most prominent use-case probably. In this lecture, you'll get an overview of the different things NodeJS&nbsp;can be used for.</p></em></strong>

So you hopefully got a first picture of what nodejs is and why you use it and
what you use it for. 

Now typically and also what we will do in this course, you use nodejs to run it
on a server to write server side code and for that, we have to have a look at
the full picture. 

We have our users using a client computer with a browser, their mobile phone
with a browser, even mobile apps and we will come back to how nodejs can
communicate with these later in the course too but for now let's stick to the
traditional browser picture. 

We get our users using the browser and there we can use html, css and
javascript, javascript in the browser to create webpages, right. 

Now they visit a page, mypage.com and they send a request to do so, for example
by entering a url in the browser, a request is sent to that url. 

Now there, this server comes into play. 

We got our server, some computer running in the Internet which has the IP
associated with that domain which is automatically resolved for us and on that
server, we then want to execute some code that does something with the incoming
request and returns a response, often but not necessarily always as you will
learn, this response is a html page which the browser then in turn can display. 

By the way, it is not necessarily just html, it's also things like css files or
javascript files with javascript code for the browser, not for the server. 

Now on the server, we typically do tasks that we can't or don't want to do from
inside the browser for performance or security reasons. 

We connect to databases for example to fetch and store data. 

We do user authentication which we obviously can only do on a place the user
can't access to make it more secure and avoid it being hacked. 

We do it for input validation to see if a user entered a correct e-mail address,
the browser can always be tricked, users can even edit their browser side code. 

You can open the developer tools and start working on that page you're on but
the server is of course sheltered from that, the user can't access it. 

And in general, we have our business logic on the server. 

Everything our user shouldn't see which takes too much time to run in the
browser, where we obviously want to deliver a fast user experience or anything
of that kind and that is where we use nodejs. 

So also javascript code but this time, not on the browser but on the server and
this is where we use the many features nodejs gives us and this is how we
indirectly allow our users to work with the server through that request response
pattern, the direct access is not available. 

So this is how we will use nodejs in this course also, we will use it to write
code on the server that returns data our users, our clients can work with. 

Now one important side note at this point of time, nodejs is not limited to
running code on a server, it's a javascript runtime and you even saw a first
demo which did not do anything where we needed a browser right, we didn't spin
up a server there, we didn't do anything which we would have reached through a
browser. 

We'll do that a lot throughout the course but we haven't done it thus far
because it's just a javascript runtime, we can execute any javascript code with
nodejs and often that is code that runs on a server and is executed upon
incoming requests but you also often use nodejs for other code, for example for
local utility scripts or build tools. 

If you worked with let's say react or angular or vue or anything of that kind,
you actually used nodejs indirectly a lot for all the build processes these
languages or frameworks needed because nodejs is a great tool for writing
utility scripts. 

You have access to the file system so you can write and read and manipulate
files and this allows you to do a lot of utility stuff on your computer that is
never exposed to the public and I just want you to know that and I'll even have
a section this course where I dive a little bit more in such build tools and non
server side language usages of nodejs. 

In general and that is the most popular thing you do with nodejs though, you use
it in the context of web development and server side code. 

So you use it to run a server and actually and that is an important difference
to PHP for example, with nodejs you don't just write the code that is running on
your server, you also write the server yourself, so the code that takes the
incoming requests and routes them to your well other code. 

In PHP, you have extra tools like apache or nginx which run the servers which
listen to incoming requests and then execute your php code, here nodejs does
both. 

It does that listening and it then also does whatever you want to do in your
code, so that's important and that's something you'll see in action soon. 

We also use it or we therefore also use it to run all our business logic, so not
just to listen to incoming requests but to then work with the requests data,
work with files, work with databases, all that fun stuff  nodejs is capable of
and we'll do all that in this course obviously. 

And we also handle the response side not just incoming requests, you will also
learn how you use nodejs to send back data to your clients, be that html pages, 
html pages with dynamic content or data only in the format of json or xml or
even files. 

So this is what we use nodejs and what we will dive heavily into in this course.


Alternatives to nodejs would be things like Python, also with frameworks like
flask or Django or PHP with frameworks like laravel maybe or standalone vanilla
PHP of course and more, asp.net, Ruby on Rails, all that stuff, these basically
are all replacements for nodejs or nodejs can be a replacement for them and
there is no clear winner. 

All these languages are capable of doing the same kind of stuff and of course
they differ in some technical regards but in general, it's great to have that
broad variety. 

The huge advantage or one huge advantage of nodejs is that it uses Javascript, a
language which you need so much in modern web development for all the frontend,
for some build tools and if you then can also use it on the server side, you
don't need to learn a bunch of different languages, you can use one and the same
language and then use that for your server side code too. 

This is why nodejs is a great language to learn, you get so much efficiency out
of it, it's also a highly performant and popular language. 

There are so many jobs out there for nodejs, there never was a better time to
learn it. 

It's used in so many environments, also for a lot of cutting edge stuff but in
general, nodejs is a great solution, it's trending, it's fast, it's efficient
and it makes sure that you only need to learn one language to write all the code
you need in a modern web application. 

---