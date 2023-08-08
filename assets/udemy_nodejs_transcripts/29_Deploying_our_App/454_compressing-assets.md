## 454. Compressing Assets

<strong><em>no description</em></strong>

Now with response headers added, let's make sure we serve optimized assets and
for that, we can use another package. 

If you google for node compression, you'll find that expressjs compression
middleware package which makes it easy for you to add compression to your
application. 

It's actually super easy but you can learn all about the configurations you
could add if you wanted to here in this official documentation but if you want
to add it in a very simple and standardized way, you just run npm install --save
compression, like this, the package is called compression and after you
installed it, you go to your app.js file and there, just as we imported helmet,
we'll import compression by requiring it here and we then add it as a
middleware. 

So let's maybe add it right after helmet here by running compression as a
function as well. 

Now you can configure it as mentioned in the official docs but you can also just
run it like this. 

And now for that to see an effect, I'll comment this out and save and the node
server therefore reloads and now I open the network tab and I'll reload my page.


Now these are the size of the assets we're downloading, especially have a look
at main.css and main.js, obviously these are not super big but still this is the
size of assets as we download them by default. 

Now I'll comment that back in, that extra package and save it and now if I
reload that page, you will see that these assets got a bit smaller and obviously
this will matter more if you have more frontend assets in your application that
you need to serve. 

So this is compression in action and this is worth considering especially in
apps where you have a lot of css and javascript code you are serving to your
users or in general where a lot of files are served to your users, by the way
image files are not compressed here because that actually makes it longer to
load them but this is a nice addition. 

I also want to note that again, most hosting providers you might want to use
have some support of compression built in or might at least offer this
compression support which you can conveniently add there. 

So then they will compress assets on the fly and you don't have to do it with
your own middleware and then you actually shouldn't do it but in case your
hosting provider does not support it or you're building your own server, then
this is a nice middleware which you can add. 

---