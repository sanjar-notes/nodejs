## 485. What is a Build Tool?

<strong><em>no description</em></strong>

Now that we briefly walked through npm and what we use it for, let's bring
something back into our memory. 

Nodejs in this course was primarily used to spin up a web server and write code
that runs on the server side and that is indeed the main thing you do with
nodejs when you write your own nodejs apps. 

But we have to remember that theoretically you can run any javascript code with
nodejs and specifically you can also interact with your local file system, you
can read and write files after all and that opens us a new door, a new
opportunity. 

We could use nodejs to execute utility scripts that for example parse certain
files, manipulate the content and output the manipulated content back into the
original file or into a new file and that is the idea behind so-called build
tools and that is something nodejs also is capable of being used for. 

And it's important pointing out here that when we talk about build tooling and
build workflows, we mostly talk about frontend web development, like for example
with our react application here. 

This react application is not a nodejs app but still we use a package.json file
and we use npm to install packages. 

These packages are all holding code that runs in the browser though and in the
end, the code we write here in the source folder will also end up in the browser
but let me point out that the way we write it here would not run in browsers, at
least not in all browsers. 

For example we are splitting our javascript code here across multiple files and
we're using es module import syntax for merging these files together. 

Now this does not natively work in all browsers, only in very modern browsers
and therefore this is indeed not the code that will end up in the browser. 

This is the code we work with but we use a build tool, a build workflow which is
started during development with npm start and for production with npm run build,
this build workflow will take our code and kind of merge it together and
transform it into code that runs in older browsers too and that is also minified
and optimized because that's also important. 

We use build tools to optimize our code, we might write code that looks like
this and that is indeed how our code looks like in the react I just showed you. 

But as I mentioned, this does not run in all browsers and even if it would, it
would be very large in the browser since all the code has to be downloaded by
your users before it runs and that's different on the server, there the code
sits on the server and that's it, in the browser the code has to be downloaded
and therefore you want to keep it as small as possible so that your app and your
javascript code in the browser starts as quickly as possible. 

Therefore we want to end up with optimized code and the idea here is that we
also have code that is not only too big but that is using next gen features,
like here the spread operator or arrow functions and we want to convert this to
code that runs an older browsers too and that is like an example optimized code
which is shorter, we use less characters and therefore the code is shorter and
it also does not use next generation javascript features. 

And that is the idea and as I mentioned, it's primarily important for frontend
development because there, not all browsers support the next features and we
want to keep our code as small as possible, that does not really matter that
much on the server side. 

So that is the idea and that is what we can use node and npm for because if we
go back to our react project, we want to convert that code into optimized
version and if you run npm run build in your project here, you actually start
such a production workflow which means now it's creating an optimized production
bundle and this is all done by npm which started the script and by node. 

And here it completed and now indeed if we look into this build folder, this now
holds our app code, so the code we wrote in source but in an optimized way. 

There in the static folder, we have javascript code and if we look into that,
this in the end is our code, just minified a lot and therefore it's pretty hard
to read but it's our code and this code is not just very condensed and only
contains current gen javascript logic, so logic that runs in older browsers too.


This is of course not the code we would like to write, it's very hard to dig
through that but it is the code we want to output and we use npm and node to
transform our code. 

That's the idea behind build tooling and now let's have a closer look at how npm
and node can help us with that. 

---