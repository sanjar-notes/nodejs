## 491. More on ES Modules

<strong><em>no description</em></strong>

<v Instructor>Now the new import export syntax</v> becomes interesting once we
use some node J-S globals. 

Now what do I mean by that? 

Let me show you. 

I'm sending back the content of my my page html file and I'm doing this by
reading it in with the file system. 

We can absolutely do that, it works as you can tell, but we could also send back
the file in a different way. 

The response object exposed by express also has a send file method and this
one's a file which it should send back. 

The thing just is if you just specify the file name like this it will not work. 

Then I'll restart the server and I reload here you see I get an error that the
path must be absolute in the end. 

Now we learned how we can build an absolute path throughout this course because
we had various places in our code where we needed such an absolute path. 

We can import path from path so from the path core module and then we construct
such a absolute path by calling path join and then we concatenate the different
path segments. 

We typically start with dirname here and then any folder into which we might
wanna go. 

In this case we have no such folder and then the file name which we wanna work
with if we need a file name. 

In this case we do so this would be the place where we now add my page html but
the key thing is that we have dirname first which is basically the path to the
current working directory so to your directory here in which your app files lie
and path join then constructs one long absolute path from this path and this
path so it in the end combines both path segments into one long absolute path. 

The problem with that if we run it is that if I now reload I get dirname is not
defined. 

Now dirname underscore underscore dirname of course was a global variable reused
multiple times throughout the course and it just worked. 

With the modern ES module syntax, it does not work anymore because there are no
globals anymore with this syntax. 

So these global variables like dirname or file name which you could use with the
other import export syntax with the require function, that does not exist here
anymore. 

Now of course this is you could say a known issue and if you search for dirname
in the ES module's documentation here you see that indeed these variables are
not available here but you also see a workaround, how you can still get your
dirname back. 

What we need is more imports from core node modules and then we can construct
our own dirname variable in the end based on this special pseudo global variable
we can access you could say so let's do that. 

Let's first of all add those two imports here to our file. 

Here I'm importing dirname from path and actually as you can see this is a named
import. 

Now we already do import something from path and we'll be importing the end to
this entire path object which exposes all its methods. 

Alternatively it just turns out that the path module does two things. 

It exports the entire path object so that we can import it like this basically
as a default but alternatively it also exports all the methods we can call on
path as standalone named functions. 

So I could also just import join from here and then also dirname in addition. 

Alternatively I could have also imported path and some named import side by side
with this syntax. 

So first your default import and then separated with a comma the named imports
this would all be possible. 

And to show you this syntax I'll stick to this approach here. 

Then I also import from the URL module and now we can construct our own
variables by copying this code. 

Now what does this code do? 

Import dot meta dot URL is basically a globally available variable you could say
which gives you the path to this file name. 

So to the response handler J-S file name and the file URL to path function just
converts that URL to a path with which the path package then is able to work. 

And the dirname function provided by the path package just takes such a path to
the current file to basically give you the path to the current folder in which
this file sits and with that we rebuilt our dirname variable now not available
globally but rebuildable with this approach. 

And hence if we save that and restart the application now we can reload this
page and we now send back a file with the send file method. 

Now why did I show you this? 

Because it's important to be aware of the fact that those global variables which
you can use with the other import export syntax are not available with this new
syntax but that you also understand how you can rebuild them and still use them.


And that's the modern E-S modules import export syntax. 

As I mentioned multiple times using it is 100% optional. 

It is the syntax you know from browser side applications though from modern
client side apps therefore. 

So hence you might feel inclined to also using here a node. 

Sticking to the other syntax which I used through the majority of this course is
of course fine though. 

There is a reason why I used that other syntax and the reason is that this new
syntax as I also mentioned already is experimental at the moment as the node
team says itself in the official docs and that the vast majority of node
projects out there will use that other syntax. 

So if you're joining a team working on some node project you need to be aware of
that other syntax. 

Nonetheless this modern syntax is also pretty nice and it's not too difficult to
switch to it as you can tell. 

---