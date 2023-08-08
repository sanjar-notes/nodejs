## 453. Setting Secure Response Headers with Helmet

<strong><em>no description</em></strong>

Now we already prepared some things for production, let me now dive into that
secure headers thing and for that, we'll use a third party package which is
called helmet and you can use it to secure your node express applications. 

Now you can dive into the official docs of this package to learn more about it
and in the end what this will do is this package will add certain headers to the
responses you sent back and it follows best practices for doing so, you'll see
which attack patterns or which security issues these are against which it
protects you by setting the right headers. 

So definitely check that out to learn more about these headers and why it
protects you against that, using the package is very easy though. 

In your project, you just run and install --save helmet and then this will be
downloaded and you can use it as you see here by simply including it as a
middleware and then it will automatically run on all incoming requests and
therefore also have a chance of adjusting the responses as you learned and it
will then set its headers. 

So you can simply go to your app.js file then and there, import helmet by
requiring it like this and then as a next step, you simply add this line here
after you initialized your express app, maybe in the place where we then also
set up all our other middleware down there. 

Here we can use app use helmet and execute this as a function, and this is it. 

Now with that, if I run npm run start:dev, my new script I added to use nodemon,
everything runs as before but now actually if I visit localhost 3000 here and I
hope my network tab and I reload this page, I can see that on this response, I
have a couple of headers being set and there are some special headers which were
added by helmet here and you can always check that by temporarily commenting out
helmet, we'll automatically restart since I'm using nodemon, we had 11 response
headers before, if I now reload this, we just have 6 because now some special
headers are missing. 

And that is something you should consider doing, read through the official docs
to learn all about the headers it is adding but it's definitely worth looking at
that and probably worth using that. 

---