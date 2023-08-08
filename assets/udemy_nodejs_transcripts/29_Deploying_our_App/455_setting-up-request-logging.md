## 455. Setting Up Request Logging

<strong><em>no description</em></strong>

Now we had a look at compression and headers, now logging is also something that
matters. 

For that I'll quit my server and I'll install a new package with npm install
--save and that is called morgan and that is a package that makes logging
request data really simple. 

Now after adding it, I can, whoops, restart with npm run start dev, my nodemon
server and now to use morgan, I'll import it here in the app.js file, I'll
require morgan like this and now we can use it as a middleware, also before we
handle all the requests, so also maybe up here, we app use morgan and we execute
this as a function and pass the information on how to log this into this
function. 

Now you find more in the official docs, that simply defines which data is being
logged and how it's formatted, I'll go with combined and now if I save that and
I reload this page here, you'll find some logging data here in the console. 

You see detailed logging information about the incoming request that we had a
get request, which browser I used which operating system and so on. 

Now obviously we typically don't want to see that in the console when we deploy
our application instead some files would be nice and to log that to files, we
just have to add something here, we can create a new constant, the access log
stream, use the node file system which is a core module which we have to import
by requiring fs here and now with that, we can create a write stream with create
write stream and this allows us to then define a path best with path join, seen
from our current folder on to let's say access.log so that we will write the
logs into this file. 

We will add a configuration here where I set flags to a which means append, so
new data will be appended to that file and not overwrite the existing file but
add it at the end of the file so that we don't just have one log statement in
the file but we continuously add them to the file and now this write stream can
be used by morgan and we simply pass that stream to morgan in a second argument.


Here we can set a stream value in that object and we set that, whoops, not here
but in the morgan function here, so here we set the stream and we set that to
our access log stream here. 

And now this file stream will be used by morgan to log our requests and
therefore now if I reload this page, we don't have the log here but we have this
new access log file and in here, we see that log data and that is of course how
we would want to log that but also as mentioned on the slide, often logging is
done by our hosting providers so then this might not matter for you. 

If you want or have to do it manually though, this is a nice package where you
can of course configure more as you can see in their official docs which allows
you to log your request data to files so that you always know what's going on on
your server. 

---