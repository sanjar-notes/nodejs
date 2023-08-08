## 282. Adding Logic to Update the Password

<strong><em>no description</em></strong>

We added a page that allows us to enter a new password. 

The new password view here and there. 

We will send a post request to slash new password. 

Now we need to add that root and controller action as a next step so that the
existing user password can be replaced with the new one. 

So back to the off controller. 

Let's add a new controller action the post new password action. 

And you guessed it, which arguments we have in that function here. 

And then in here, what do we need to do? 

Well, we need to extract the new password from request body password, and that
is request body password. 

Because in the new password view, I'm storing the password in a field named
password. 

And we'll need to extract that user ID here too. 

So that user ID is also something user ID is equal to request body user ID. 

We need that as well. 

I also still want to have that token because otherwise people could start
entering random tokens here and still reach that page and then maybe change
users on the back end by entering random user IDs in that hidden input field as
well. 

So I want to have that token and therefore a new password. 

I'll also add another hidden input field password token and output password
token here. 

So that is another field and I need to pass that token into my view. 

So that is something. 

Forget new password for this action here. 

I need to pass password token as a variable into the view and it will hold the
token I'm extracting from the URL here and that is the token we originally
generated. 

So this is not all the past and this is not also something I can extract here
the password token. 

Request body password token extracted from that password token field here. 

Okay. 

So now we got these three pieces of information in here. 

Now I want to reset my user. 

So I will again find one user in my database and I'll find the user where the
reset token is equal to the password token, where the reset token expiration is
again greater than. 

Date now. 

So the same logic as I did up here and where the ID. 

Is equal to my user ID. 

I'll then again add then and catch. 

Log any errors we might be facing here, and then I'll have my user debt fulfills
all these criterias. 

And then here. 

I want to assign a new password to the user. 

Now, obviously for that I'll again hash it because that doesn't change. 

It still should be hashed. 

So I'll again use decrypt. 

Hash pass in the new password and my number of salting rounds. 

12. 

And I will return this year and then add another, then block the hashed
password. 

Where I can stored it on the extracted user. 

However, the user is an argument in this function, but I need it here to be able
to access it in this function as well. 

I will create a new variable up there user or reset user. 

And it will store user in reset user. 

So in that variable, because that variable is defined in this function scope. 

So I can use it in this end in this function and now I can use reset user in
here too, and I can use it to call reset user and set the password equal to the
new hash password. 

And for the reset user, I will also set. 

Reset token equal to null and I will also set reset token expiration to null
here or not to null. 

Let's set it to undefined. 

So these fields here are not required anymore. 

They don't need to store any values anymore. 

Once I'm done, I can call save here and return that. 

And here I'll then have my result of that safe operation. 

And once we did save, I can now redirect the user back to the login page with
the new password. 

You could also send a number of mail confirming that reset if you wanted to. 

And now if you save this. 

Let's reload that password resetting page here. 

And let's add a new or enter a new password. 

Click update password and I get a page not found. 

Which makes sense obviously, because I have my new post route, but I need to
register it as a route. 

I have my action here, I should say. 

I need to register it as a route. 

So in the off JJ's file here, we need to add a new post request to new password
and execute of controller post new password there. 

That is important. 

Safe that. 

Then simply go back to the page where you have that token in the URL and to your
new password. 

Let's also quickly reload our users collection before we hit save and kind of
memorize the value. 

Here it ends with x. 

Y. 

W y. 

And Click Update Password. 

I'm on the login page and now if I reload my users collection, that password
here should change. 

And it does. 

And also the reset token and so on. 

It's gone. 

I also have no errors here, so it looks like password resetting was successful. 

We successfully assigned a new password. 

Now if we try going to reset. 

With some random token. 

Then this will not work and we're not doing proper error handling there. 

I'll have a whole module on that because we essentially fail to find a user for
that token. 

So this all works. 

We can't start changing values of random tokens of random users. 

So this will not work here. 

---