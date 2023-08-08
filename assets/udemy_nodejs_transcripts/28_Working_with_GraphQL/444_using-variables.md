## 444. Using Variables

<strong><em>no description</em></strong>

Now finally before we leave that module, there's one thing we can optimize now
because there is one thing which I did in a way that is ok to do that will work
but that is not recommended doing and that we can do better. 

Whenever we pass a dynamic value to our GraphQL queries as we are for example
doing it here where I do have a page, we currently do use the interpolation
syntax here where I use this dollar sign curly brace thing to inject or
interpolate a value into my string literal. 

Now this absolutely does work but this is indeed not the recommended way of
adding variables into our GraphQL query, there is a better way. 

Maybe you also remember that for mutations, we had to add mutation here but for
queries, we didn't have to add query here and indeed if you would have added a
query like this, we would have gotten an error. 

Well now I will add it because now I will also add something else, I'll give
this query a name, a name that does not really make a difference, it does not
make it behave differently, it will help in error messages for example but that
name then also allows us to do something else. 

So here we are of course getting all posts, so here I'll name this fetch posts
and you can give this any name you want, so this here is totally up to you. 

Now with this name assigned, I can add parentheses after this name to define
which variables this query will use and we create such a variable here with a
dollar sign but then no curly braces and then the name of the variable you want
to use and that name is again up to you, I'll name it page but you could have
named it current page, whatever you want. 

This will be of type integer, so you assign a GraphQL type again here and this
is really important to understand, this is GraphQL syntax here, this will be
parsed on the server, this is not javascript code that runs in the client. 

This will only tell our GraphQL server that we have a query which will use an
internal variable. 

Now that I'm saying internal, the question of course is where do we use that
$page? 

Well we use it in the place where we do have a dynamic, a variable value and
that would be here where we currently inject our value. 

Now I use my $page here and this name here has to match this name and it has to
start with dollar sign and now GraphQL knows ok this part here is dynamic, it
might change and it will be an integer because we're defining this here, so now
the only question is how do we get our page variable here in javascript into our
$page variable here in GraphQL and for that, we add a second property to that
query object we're creating here. 

Thus far I only have the query expression, now after that I'll add a comma and
I'll add a second property which are my variables and this has to be named
variables, just as this here had to be named query. 

This now is the query expression and variables now is an object where we can
assign values to the variables we pass into our query here. 

So here I have $page, here it then should be just page without the dollar sign
and then my javascript variable or value, so I could pass one here to always use
the first page or in my case, I do have that page constant or variable here in
javascript now, so this is the value I want to assign here. 

Now I have page two times but the first page refers to the internal variable
used in the GraphQL query and the second page after the colon refers to my
javascript variable, just to make this clear. 

And now with that let's save this and let's reload our application or first of
all let's quickly log in there because I was logged out and now here you see I
get my post, now if I add another duck here and I then add one more item so that
we do have pagination going on, then after reloading, we can indeed see that
this works as before, I can switch between my two pages and I simply have two
cups in there. 

By the way maybe you notice that we didn't get that next and previous link after
we created our item, our new item and that is something we can fix too but for
now let's focus on the variables and there in our frontend code, this is how we
use variables and technically it works just as before but this is the more
elegant, the better way of using variables in your GraphQL queries. 

So now we can replace that in all our queries, for example in this mutation. 

There I also use string interpolation to get my value in there, better would be
to give this a name, update user status or anything like that and then define
which variable we need in here, that would be the let's say user status, again
this name is up to you and then the GraphQL type of that which will be a string.


Then here without the double quotation marks because we define it to be a
string, you add user status like this and then again, you add a second variable
to that GraphQL query object where you add that variables key where you now
assign a value to that variable you defined here without the dollar sign and
then the value you want to store there and in this case this would be this state
status just as before. 

Now if I continue, here in the next query where I do edit or create a post,
there I also give this a name, create new post seems like a fitting name here
and there we'll have a couple of variables which is no problem, we can of course
have more than one, we'll have the title which is a string, we'll have the
content which is a string and we'll have the image url which is also a string. 

And now just as before, we use these values in here, so title, content and of
course also the image url and now we just need to add that second argument here,
the variables, so that we can store our title and you might remember, this was
post data title, then the content was post data content and the image url, well
that is our image url variable in javascript or the constant which I am creating
here. 

Now when we edit a post, update existing post could be a name we assign to that
and there we also have some variables and there we will need our post ID let's
say which is an ID, we then also have our title which is a string, we then have
our content which is a string and now just as before I'll copy that value
because I'll need it in a second but then I'll replace this here with post ID,
I'll replace the rest in a second too, let me first of all add my variables
below that and then here, we have that post ID which is the value I just cut out
and then here we have the post data title and the post data content. 

So here we use the title, there we use the dollar sign content not wrapped in
double quotation marks and we also have the image url up there which is also a
string, so we should also of course use the image url here and now we need to
assign values to these variables down there too. 

So we have the title which is post data title, we have the content which is post
data content and we have the image url which is image url. 

Always remember, the first part here so the key name in our variables object
refers to the variables we defined here without the dollar sign, the second part
after the colon, so the value of our key value pairs here refers to the value we
want to pass into that variable. 

Time for a little save to just check if that is all working. 

So now if we create a new post, another duck because as you can tell by now
ducks are lovely animals, it's still lovely, if I accept that, then we seem to
have an issue here so that did not work and the problem we have here can be
found when I inspect my GraphQL request which fails. 

There I get some errors and we see that all my variables here of type string
expected a type string which is required and that of course is my mistake here. 

We should add an exclamation mark here because if we have a look at our backend
and our schema here and we have a look at our mutations there, then we can see
that create user has user input data and create post has post input data and
that is what we working on and that input data, the post input data indeed does
require all these strings. 

The page previously was optional, there we had no exclamation mark which is why
I did get no such error before. 

For the status by the way, we would also get an error because the status as you
can tell also has a required string and that is really important and therefore
good that this slipped through. 

The types you assign in your frontend for your variables have to match the types
in your backend schema. 

So here for example in create new post, all my strings here are required and for
update existing post, well there for update post, we also have the same type of
data and a required ID, so we should make sure that we add that exclamation mark
after all these values here because they are required in our schema, they have
to be required in our frontend too. 

So let's add this also on update status. 

So after this change, let me go back, let's try this again with another duck,
entering some dummy value here and now this is looking better. 

Now let me edit this by removing the exclamation mark and there I still get an
error, image url was not provided. 

Let me quickly have a look at what's wrong there, if we go to our update
existing post, I do have my image url here and on the backend in update post, I
also do require it there but indeed the problem I have here is that the image
url is not always set when we don't choose a new image, right. 

And you might remember that indeed on our backend, we have a check in update
post where we see if that is undefined as a text, so I should at least pass that
text in to go through that check. 

So what I'll do is if my image url cannot be set here, I'll set it to a string
undefined which is not the same as the default value, of the type undefined and
with that, if we now reload and I tried it again, now that works because now
we're setting this to a value we are checking for in the backend for the use
case that we don't have a new image and then we'll keep the old image here. 

With that back in the frontend, this is taking good shape, the other queries in
feed.js are all right. 

In the single post.js file there though, here I also have a query where I inject
a value when I get a single post, so here I'll give this a name by adding query
and the name, fetch single post and there, I expect to have a post ID which will
be of type ID and that is required because that is required in our backend
schema, here in our post query we do require that ID and then here, I can also
assign that here and as you learn add a second element to that GraphQL query
object. 

The variables property where I then set post ID equal to post ID, so to this
post ID which I'm extracting here. 

And now with that if I save this and I go back and click view, this still works
without issues. 

Now with that, let's also go to app.js in our frontend code because there we do
sign users up and in and here, we also inject values into our query. 

Now just as before, we should name these queries and use that different
approach, so here I'll name that user login and I do get an e-mail which is of
type string and which is required and I do get my password which is of type
string and required. 

And then here where I have auth data email and auth data password, I can use
e-mail, so $email and $password and we add that new variables object here as a
property to the GraphQL query and that email will be auth data email and
password will be auth data password just as before but now with that more
elegant syntax. 

And last but not least when we sign up, so when we create new users, then I'll
also give this mutation a name, create new user, whatever you want and here,
again I expect a couple of values. 

I expect an email which is a string and which is required, I expect a name which
is a string and which is required and you can always check your backend schema
to learn what is required and what is not and here our user input data is what
we have to pass to the backend. 

So last but not least here I also have my password which is a required string
and then I'll just quickly copy that because now I will replace these values
with my GraphQL variable equivalence, so $email, $name and of course here,
$password and then again add that variables object and pass email which is auth
data sign up form email value, pass the name which is auth data sign up form
name value and pass the password which is auth data sign up form password value
just as before. 

And with that, we should have replaced all injected values in our application
with new values. 

Now let me quickly sign up with a new user here, now let me also quickly login
with that user and that also works and with that, we got everything in place. 

I can't delete that obviously because I'm not the user who created it, I would
have to login with the correct user for that. 

So with that, everything is working the way it should and now we have a GraphQL
API that uses that new variable syntax which is the recommended way of passing
dynamic values into your queries. 

---