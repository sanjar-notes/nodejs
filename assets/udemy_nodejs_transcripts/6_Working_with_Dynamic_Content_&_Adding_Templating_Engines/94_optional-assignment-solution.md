## 94. [OPTIONAL] Assignment Solution

<strong><em>no description</em></strong>

I'm in a new project here and I will start with NPR Minute and as before answer
everything with the default settings and then NPM install with DASH Safe Express
because we need that. 

And EJ's and I will also add body parser because I will need to parse that
incoming body. 

And that is an important step which you also learn about earlier in this course
hit enter and thereafter you can also of course install node mod and I will do
that with safe depth node on here so that I can add a script to restart the
server whenever I change my code. 

Speaking of that, let's add an app JS file to have a place to start our server
and our express application. 

And in the package adjacent file I will add a start script where I simply run
node app. 

JS Excuse me, not node but node mod of course, because I want to have all
restarting with that. 

Let's go into the app JS file and create a normal express app by importing
express y, I require express. 

And then you learned how this works. 

We can create an app with app and execute express as a function and simply call
app list and free 1000 to bring up that node server. 

This is a very minimal express application that doesn't do anything. 

Now I will have a couple of routes and you can create a routes folder for that. 

I will handle them in this app JS file, but I will create a views folder for my
templates. 

Now let's start by adding the routes. 

I'll add my routes like this. 

I will have to get routes. 

So two pages and one post route, the route which is triggered when I submit that
form. 

The first get route is for just slash. 

And there I want to render a view. 

Of course I want to render the page which holds the form I mentioned in the
assignment tasks. 

I will also have a slash users route and there I also get my rest request rest
next function. 

And here I will also render a view and this will be the view where I output the
entered usernames. 

Now, last but not least, here is a post route and you can name this however you
want. 

I'll name it add user. 

And in here I don't want to render a view. 

Instead I want to redirect. 

So here I will call, rest, redirect and redirect to just slash excuse me, to
slash users, which is where we can see the entered users. 

So this is my basic setup here. 

Now we need to add a templating engine. 

Now, I already installed edges, but I will show the solution for all three
engines you saw. 

So I will also add express handlebars and pug. 

And I will start with pie, just as I did in this module. 

So for that. 

Let's register this as a view engine by setting this global view engine variable
or setting in our app. 

And then I set this to pack, which works out of the box because Express supports
this out of the box. 

I get that views folder and that is the default. 

So the following setting can be omitted, but I'll still set my views to the
views folder so that Express knows where to find them. 

Now in the views folder I will now add my index dot pack file and you can name
this file however you want. 

This will basically be for my starting page and my users dot. 

Pike file. 

I will also add a layout folder and in there have my main layout pack. 

That name also is up to you. 

Now in main layout I will create a html five template already thanks to my ID
generated in the pack format and I strongly recommend using an ID that supports
emit and pack files like Visual Studio code that's out of the box. 

And now in there we got our nice document. 

We probably want to output the title dynamically here and we can do this with
the help of Pack, remember and Pack. 

This was the syntax for outputting a single value and it will output page title
here. 

This is some data I have to pass into my templates. 

Then of course. 

Now this is my basic setup, and you can add more, you can add styles, you can
add scripts, whatever you want. 

Now, one thing I will add here and that's the last thing, is a very basic
navigation here. 

And I will not even style it in a in any way. 

I will just have some navigation where I do have an anchor tag which leads to
just slash and I'll have another anchor tag which leads to users. 

And I will of course give these some text. 

So here I will have enter user. 

Then I want to have like a pipe separator between my two links here and I will
then have users here. 

So that's a very basic navigation obviously, and you can improve that with
styling if you want. 

This is the layout. 

Now let's go to the index pack file and there we could extend that layout with
the extents keyword. 

So here I will extend layouts and then main layout pack like this. 

Now we will automatically take this. 

I now just need to define a block in here and I will do this next to the header
with the block keyword for my content. 

So this is done in the main layout in index pack. 

We then also refer to that block content, define what should be inserted into
this block. 

And there I want to have a forum which leads to add user because remember that
is my post route which I target or which I want to target. 

So add user like this and then also set the method to post, make sure to use a
comma here to separate these two attributes and in the form also keep this very
simple add the input of type text and also add a button of type submit. 

And on the button I'll put some text where I say add user. 

So this is a very basic setup for the index pack file and I'll copy that over to
the user's pack file where I for now will simply output users in each one tag. 

Now with all these files added, let's go back to app JS and in here. 

Let's make sure we render the appropriate views. 

So for just slash, I want to render the index file here and I will inject an
object which then in turn holds the data I want to inject into my view. 

And right now I don't output anything except for the page title in the layout. 

So we should make sure that we set this page title here and here. 

You can set it to add user or whatever you want. 

And for the users page here I will output the user's pack file and remember that
you omit the file extension here and I will also pass in a page title here so
that this can be used for the layout for this page. 

And there I'll just say users. 

Okay. 

So with all that prepared, let's run NPM start and see if that works. 

If you now enter localhost 3000, you should see this page and you can also go to
users here. 

So my navigation works and if I now enter some user here, I'm forwarded to the
user's page. 

So this is working. 

Let's now make sure we manage that data and output our users array. 

And for that I will follow the temporary approach I showed you in this module
already. 

I will create a new constant users, which is an array and I will work with that
array here. 

And keep in mind that this data is shared across requests and across users of
your page. 

So not really something you would use in production for saving any data that
well shouldn't be shared. 

So here users is now the array which I'll use. 

Whoops. 

Not here though in the post route of course. 

So here users and I want to push a new user onto it. 

Now important. 

We want to use the value the user enters into the form and for that we need to
do adjustments. 

The first one is that an index pack for the input we need to assign a name. 

This is required so that the auto generated request has a key value pair where
the key is the name by which we then can extract the entered value. 

So here name will be username. 

You can take any name you want here. 

With that added in the post drought. 

Here we can. 

Extract it, but to extract it, we need to do one other thing and that is we need
to import the body parser. 

So let's import body parser here by requiring it from the body parser package
like this. 

Remember, we did install the body parser here. 

And let's register it as a middleware. 

And we did this early in the course, too. 

You simply execute body parts as a function, and to avoid warnings, you need to
pass in a configuration object where you set extended to false. 

With this set up, we got some logic or some help that will parse the incoming
data for us. 

And now here we can push a new object where we set the name of the user equal to
request. 

And then there is this special body property which holds the parsed body. 

And then there we will have a username key because username is the name we gave
our input here. 

Now if that this user should get saved and that array, we now just need to
output it here in our users page. 

And for that let's simply add a new property to the object we're passing to the
template, so to say. 

And let's also name this users. 

You can give this any name you want though, and it will refer to users. 

So this can be confusing the value here. 

This user is part after the colon. 

That is our array here. 

The array where we add an element in the post root users here is simply the key
by which we'll be able to use that data in the template. 

So now we can go into the user's template and use it and therefore here maybe
below the H1 tag, I'll add an unordered list and in that list I now want to loop
through all my users. 

We do that with the special each keyword, and then we define a variable name
which holds the extracted user for each iteration. 

You can name this user or whatever we want. 

And then simply in users and users here of course, has to match the name. 

You gave your data here, so before the colon. 

Now we are in a loop here and we can output a list item where I simply print
user name and there should be a dot name because in the post route we add a user
as an object where the entered user name is stored in a name property. 

So with all that out of the way, I have an error yet. 

Body parts are you are ll encoded. 

Is the function you have to execute. 

Not body parts or itself is the function. 

But body parts are dot you are ll encoded. 

A little bit of oversight. 

You're on my side, so make sure you get this right. 

That is also the same syntax we used before in this course. 

And now with that, let's go to the entry user page and I'll enter Christian
here. 

And click add user and we see user name here. 

Yeah, which of course makes sense because if I want to output something dynamic
and not just text, I have to wrap it in my output, add value syntax with hash
tag and then curly braces. 

So this is the correct syntax in the user spec file. 

And with that now if I reload this page, I see Christian and if I add more
values here, we also see that. 

So this is now working and this is the solution with Puck. 

Now in the next step I'll delete this and re implement it with handlebars to
implement this with handlebars, I'll keep that folder structure and I'll also
keep the files around for reference. 

But now I will register handlebars as the engine and for handlebars you'll learn
that you need to import it. 

So let's add that import here by requiring express handlebars and that we need
to register this as an engine. 

So with app engine we can register that and now you can register it as well as a
shortcut basically, which you already want to use as a file extension. 

And there I will execute express handlebars as a function and now we can use HBS
as our view engine here, and we can create HBS files which will be handled by
render. 

Now the general logic then is the same as for PAC. 

Of course, just a syntax differs. 

So let's create user start HBS and index dot HBS and also our main layout HBS. 

Now maybe you'll remember that for the layout we had to pass some configuration
to the Express HBS function here. 

We had to set the default layout to Main. 

Layout here. 

The layout directory can be set but doesn't have to be set actually because
we're using the views layouts folder, which is the default folder it will look
in. 

But then we also need to set extension name to HBS. 

If we're not using the default of handlebars and we're not using that, we're
using HBS with that set up. 

This should all work and now we can create an HTML five skeleton in the layout
here. 

Now the documents title is something we want to output dynamically. 

Just as with PAC and for handlebars. 

Remember we had to double curly brace syntax so here we can again output date
page title and this will now pull that from the data we're passing into the
template. 

Now handlebars was a bit less flexible than Park was. 

We could not define blocks here. 

Instead, in the layout we have triple curly braces and then body in there, and
this will serve as the single hook we can use where all the other content will
be injected into. 

So if this set up, we can still set up a header just as we did it in Puck. 

So above that rendering hook. 

Here, I'll add a header in which I'll then. 

Just as I did it here at two links. 

So I'll have an anchor tag which leads leads to enter user and then I'll have
like a pipe symbol and another anchor tag which leads to users like that. 

And of course, as before, you can tweak this style, this whatever you want, this
is the layout and it will automatically be used because we set it as the default
layout and all the other part we enter into our our HBS files will then be
injected here into this body hook. 

So now in index HBS, which holds that form, I simply do add that form which
leads to add user and sends a post request. 

And in there I now want to have my input of type text with a name of username. 

And that is important of course, because we're trying to extract that username
here and add a button which is of type submit to submitted form and send that
request where I say add user. 

Now that is set up just as we set it up in Pug. 

Let's now move on to the users page and there we have H one and H one tag and
then an unordered list. 

So let's recreate it here. 

Users unordered list. 

And now I want to add or output my list. 

That also reminds me of a thing I forgot in pack the conditional output. 

Right. 

Well, let me quickly show you that the conditional output and pack would simply
work by adding if. 

And then let's check if users length greater zero. 

If that is the case, we render that if that's not the case else we render no
users found. 

Sorry for that little interruption. 

This is how we would render if statements in pack with that. 

Back to HBS there. 

I don't want to forget this. 

So let's start with the if statement. 

Remember block statements. 

So statements that wrap HTML code, use a hash tag if or hash tag else syntax
here. 

So here it's a if statement and then you can't have conditions like user's
length. 

Greater zero handlebars doesn't support this. 

Instead, we need some value like has users which we actually set up in our node
express code. 

So for this route, the users route we need to pass in this additional field has
users which holds the result of that check where I see users or check users
length and see if users length is greater than zero. 

So the result here is true or false and will be stored in has users and has
users is then be forwarded or injected into our template. 

And therefore we can now use that code. 

And then you also need to close that block, by the way, like this. 

So now anything between the opening and closing statement here is rendered
conditionally, and that will be the unordered list where I now need another
block statement to output my list of users again with the double curly braces
and then hashtag each. 

That is what you use for a loop. 

And then here I simply loop through my users users because that is the key I am
passing into my template here. 

So now I'm looping for that and we need to close that block to like this. 

And now the question just is, how do I access my user? 

Well, I want to output a list item and I do output my value then with the normal
output of value syntax with double curly braces. 

And in there, the individual value for each iteration of this loop is stored in
the this keyword. 

So I can say this name because again, this is the property where the entered
user name will be stored in here. 

So now I got this set up. 

Now I also want to render a LS case here. 

So let me also add else just like this. 

And here I simply say no users found. 

So this is now the handlebars set up. 

Let's see if it works. 

If I reload this page, I see no user found. 

If I enter hands here, I see hands. 

And if I enter Helena, here I see Helena. 

So this is not working again. 

And this is the solution with handlebars, with our tiny addition of how it is
solved with pack for the if statement. 

With Handlebars and puck out of the way. 

Let's solve this a third time with Aegis. 

And for this in Atreus, we need to change the app engine. 

I'll copy out that HBS engine. 

Then we could leave that. 

It doesn't hurt if we define this. 

I'll just not use it because I'll use edges for this. 

We don't need to define the engine because EJ's is a package which is supported
out of the box. 

You just need to make sure you installed edges. 

But we did this and now we just need to create our Edge's files so users dot
Edge's and indexed on Edge's now Edge's dozens of port layouts but it supports
partials or includes, if you remember, so we can create a new folder name. 

It includes you could name it differently. 

And now let's see what is shared. 

Well, if we have a look at the layouts we used before, basically this entire
part here is shared and the end of the document is shared. 

So this is the only part which is not shared across pages. 

Well, therefore it includes we can again add a hat to Edge's file and maybe an
end to Edge's file. 

And then we can take this part from the HBS file all above body and add this to
head edges. 

Obviously, we need to replace that syntax here with Edge's syntax, and if you
remember that was smaller, then percentage equals page title to output a value
in place. 

And of course all the for the end of our template, we copy the closing body and
HTML tag and add this to end as well. 

And with this added here, we can now go on to index edges and start by including
the head for this. 

You added the normal Edge's tag, but then with a minus to add an escaped HTML
code and there we use to include keyword and go to includes and then head
Edge's. 

And we can already do that for the body of the document too. 

So includes and has like that. 

Now in between comes the content of this page, which is this form which I can
just copy from the handlebars page. 

It doesn't contain any special syntax which we would have to change. 

We can copy that entire code and move it over to users edges. 

But of course, in there we output something different. 

We first of all have our H1 tag where we say users, but then I want to output if
statement and in one branch of the if statement my loop now if statement is
written by using a normal edge's tag with neither a minus nor equal sign, but
just like this. 

And then I check if users length is greater than zero, I also add an opening
curly brace and once I'm done with the block of HTML code, I add another Edge's
tag with a closing curly brace. 

And in between we have our HTML code. 

Now that HTML code is this unordered list which I can just copy from the HBS
file. 

Let's move it in there. 

But of course, this looping syntax has to change. 

There we again use edges to simply create a for loop, and now you can again use
a for off loop, as we did in this module. 

I will mix it up and use a for each loop. 

Still a normal JavaScript function for each tags a function. 

You can also use an arrow function here which gets the user injected
automatically, and that should be users for each, by the way. 

So that function here which you pass to for each, is executed for you by
JavaScript. 

For each iteration it gives you the user you're currently looking at. 

Then I have that arrow next generation JavaScript and the opening curly brace. 

And once we're done here again, I have my Edge's text and here I have to close
that curly brace and that record here from for each we have to close that to and
you can add this semicolon but you don't need to. 

Now in here to output that I have my equal syntax here so the please output this
inline syntax and there I refer to user. 

So this user I get passed into this function for every iteration and then name. 

Now before we see if that works, let's also add a else statement here. 

So after this closing curly brace of the if statement, I'll add Al's open a new
curly brace and close that eventually to once we're done. 

And in that Alex BLOCK, I will simply say no users found like this. 

So now we should, in theory, have everything we need. 

Let's reload this page. 

No users found. 

And let's enter hands again. 

And this is looking pretty good. 

And of course, it should also work if we add another user. 

So this is now the assignment solved with edges. 

So now you saw all these templating engines in action. 

Again, you hopefully got a bit more used to them. 

And I can only encourage you to, of course, keep on practicing with them in your
own projects. 

---