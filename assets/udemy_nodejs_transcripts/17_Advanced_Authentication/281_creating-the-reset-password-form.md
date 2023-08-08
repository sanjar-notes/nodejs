## 281. Creating the Reset Password Form

<strong><em>no description</em></strong>

So we got a token. 

Let's now add a form which allows the user to enter a new password. 

And for that I will go into my views folder again, the all folder there. 

New passwords or however you want to name this and they're all use my log in
each s page copy all that content into here. 

And then let's just maybe grab our password field here, remove the email for
sure. 

You can't add a new email. 

Re-enable the button to update password, you need to see a xref token. 

The action here should be maybe new password. 

Whatever you want a post request to new password. 

Reset password does not make any sense here, so let's remove that link. 

And now we got a prepared new password page. 

Now we want to load that. 

So we need a controller action. 

Exports get new password maybe, but we again have the free arguments we all know
and love. 

And in there let's render a view. 

So I'll just copy that surrender method and I want to render my off new dash
password view. 

Path is new. 

Oops. 

New. 

Passwords and here the title can be new password. 

I also will add my code for extracting a potential error message if I should
work with one. 

So now I have my get new password action. 

Obviously, I don't just want to render that view here though. 

I also want to check whether I find a user for that token which I receive here,
because this will be the page we load for this page where we do have a token in
the URL. 

So let's retrieve that token, first of all. 

By request from request params token. 

Let's say we'll need to add a root later that encodes the token in a token field
in our parameters. 

And then I'll find one user where this token fits. 

Now, since our tokens are generated in a random non gas able way, you can't also
enter random tokens and start editing passwords of other users. 

And even if you could, you would not know the fitting email addresses. 

So here I'll find a token with the reset token field, which we added here, reset
token. 

So I'm looking for reset token being equal to the token I have here. 

And we want to make sure that it's still valid from a date perspective so that
the document I find does not just fulfill this criteria, but another one too. 

I add more criteria with comma that the reset token expiration is still well
higher than the current date. 

For that, I can use a special operator wrapped in curly braces dollar sign GTI
stands for a greater than and I can simply compare if it's greater than now. 

So the current date and time only if the token matches and the token expiration
is still greater than now. 

So the token expiration is in the future. 

Only then I have the user I want to find. 

So here I'll add then and catch. 

Log, any errors I might be getting. 

And in the then block I get the user for whom we want to reset the password. 

So it's here inside of that then block that. 

I want to render my new password view and I want to pass my user ID to that view
so that I can include it in the post request where we will update the password. 

So here I will include user ID. 

To string, maybe to convert it from an object ID to a real string. 

So now we render new password, and on the new password page I will duplicate my
hidden C as our F token field because I'll also have a user ID field now which
is also hidden where I output that user ID I'm passing into the view. 

So this input is new with that hidden user ID and it will output that user ID. 

We'll need that for the post request where we want to save our new password. 

Okay. 

So with that, let's go to our roots, to the off roots here and let's add a new
get root here to get new password root where I will use to get new password
controller action. 

Now, it's not just new password, by the way, or it will not be new password at
all. 

It will be reset, but then there will be a token. 

So the URL is reset and then a dynamic parameter, the token parameter, and it
has to be named token here because in that get new password off controller, I am
looking for token in my parents. 

So token here which I'm looking for in request. 

Params means I have to name it token here as well. 

And with that let's go back and reload this page. 

And now I'm on that update password page, which is looking good. 

Now in the next lecture, let's add the logic to update that password. 

---