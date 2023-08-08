## 450. Deployment Preparations

<strong><em>no description</em></strong>

How do we then prepare the code for production? 

Now this obviously always depends on the kind of application you're building. 

In general, you want to use something which is called environment variables and
I will show you what this is in our concrete projects in this module, no
worries. 

Use environment variables instead of hardcoding certain values like API keys,
port numbers, passwords and so on into your code. 

Also make sure that if you are using some third party services like stripe, that
you use the production API keys and not the development keys, for example stripe
which we used gave us a testing API key while that is obviously what we want to
use as long as we test the application, as soon as we deploy it we want to use
the production ready API and that is something that also depends on the third
parties or on the third party APIs you might be using. 

Now we also might have some mechanisms to handle errors or to log something and
there we want to make sure that we reduce the error output details. 

We don't want to send sensitive info to our users, so if something fails, if
some error message is thrown, we want to make sure that it does contain as
little information as possible because the users of our website should of course
not get any insights into our source code. 

Now by default and in the way we build this project or these projects in this
course, we'll not have problems with that because if we use the default express
error handling middleware and the default errors and the custom errors we build
also don't contain any sensitive information, then we are fine but if you're
building an application where you create your own error objects, maybe with a
lot of data added to them, you should make sure to strip some of that data out
of these custom errors when you deploy your application or when you prepare your
application for deployment. 

Regarding the responses your application sends, you want to make sure that you
set secure response headers. 

There are some response headers, some headers you can add to any response which
don't hurt, which prevent the clients from doing certain things, certain things
and so on and therefore setting these headers won't hurt and I will show you in
this module how to easily set these headers and how to find out which headers
that are, so we'll implement some best practices there. 

Now in a typical node application, you might also be serving some assets, some
javascript, some css files and there, adding compression can be a good idea
because that will reduce your response size or therefore also your response time
because the client has to download less and most modern browsers and so on are
able to download compressed, so zipped assets and unzip them on the fly directly
in the browser, so this is not some fancy mechanism where you would have to do a
lot of manual coding, it's actually pretty straightforward and the browser does
a lot of the work for you. 

You also want to configure logging so that you are aware of what's happening on
your server. 

Since we're now not testing the server anymore but real users do interact with
it, we certainly want to log interactions into log files that we can look into
at any time we feel like it. 

So there, that is another thing we want to add so that we can stay up to date
about what's happening. 

And last but not least, ssl/tls, so encryption of data in transit is also
something we might want to look into. 

Thus far in this course we used the normal http server and therefore our
communication with the server was not encrypted, for testing this is obviously
fine, now for a production ready app, it's strongly recommended that you do
encrypt your connections and therefore I will also show you how to turn that on
in your node express application in this module. 

It's also worth mentioning that the last three points here, compression logging
and ssl are often handled by your hosting provider and I will talk about that
when we choose a hosting provider because often or typically, you want to use
some managed service where these things are also managed for you so that you
don't have to worry too much about that. 

I'll still show you how to enable it manually but it might be worth noting that
you probably don't have to do that when deploying your application. 

---