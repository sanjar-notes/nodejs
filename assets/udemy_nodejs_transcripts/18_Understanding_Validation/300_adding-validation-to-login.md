## 300. Adding Validation to Login

<strong><em>no description</em></strong>

So we've worked in the user experience, now let's also work on the user
experience of logging in because right now if I login, well I don't get any
highlights here and if I do login like this and my password has to be valid,
then my old data is lost. 

Now of course this is a great challenge for you so feel free to pause the video
and try this on your own, you have to basically do what we did before though
there is a little extra twist which I'll also show you of course. 

So here's your chance to pause the video, we'll do it together thereafter. 

Were you successful? 

Now let's try this together and we start in the auth controller but now in post
login of course because that is, whoops, up there where we do gather validation
results for the login screen. 

Now if I render this response with this error code which you don't have to set
as you saw but which is a good practice to set to be very clear about what went
wrong, if you do all that, then of course you can also pass some old input on
this route here. 

So old input here would contain the e-mail which we extract up here, there and
of course the password which we extract and pass that in a keys named email and
password back to the view, you can also set your validation errors if you want
and set that to errors array, like this basically as we did it for the sign up
route. 

There's just one difference, we also have some errors that stem from us entering
an invalid e-mail or password, so basically when we try to log a user in for
which we don't have an entry in the database or where the password does not
match. 

Now in such cases since I don't use my validation logic here and since I
redirect, to make sure that we treat this in a uniform way, we should also
return our rendering here because in the end we have an invalid input here as
well, the error message then just is this error message and hence we don't need
to flash it anymore so we can get rid of that flashing. 

The old input is definitely something we want to keep here as well and
validation errors, well there we have to add some objects with param and that in
this case it could be param email and param password if you want to make sure
you don't show what exactly led to the error but of course you could also just
leave that out and kind of only give out that message, keep the old values but
don't mark anything as red, simply do not give away what exactly failed if you
wanted to do that. 

So here I'll just return an error message and the old input and now I will copy
that again and down there where I also redirect with my error message, well I
basically do it in the same way as up here and yes you could refactor this in
some way. 

But now with that, if we save that we just have to work a little bit on the
login screen and on the login screen, we of course want to pre-populate these
fields with their old values again and we do this as you saw with the help of
ejs by using old input email here and then the same for the password, here old
email password. 

So these two fields, setting the value attribute on these two inputs, that is
what we need to do here to return this old or use this old data and in the
controller we just have to make sure that we set this old data. 

We also need to make sure that for the first time we load this with get login,
we also set the old input, in this case here to an object where the email is an
empty string and the password is an empty string and I'll set validation errors
here to an empty array, so that we don't get an error regarding this not being
found when it's first rendered. 

And now if I reload this page or if I go to login page again, this works and now
if I try to login like this, I get an error but the old data is kept and now if
I enter a valid password but one which is invalid, then you see we also keep the
old values. 

Now we can also add the red borders if we want to by reusing that code from
signup.ejs, there I use that code for setting a css class and I do the same on
the login.ejs page. 

So there let me split all these fields up and then add the class here, look for
email in this case since I'm on the e-mail input here and of course let's do the
same for the password down there. 

Let's split that, add the class and here password is actually correct already. 

So now with that, one last check. 

If I do enter just invalid credentials in the sense of no user is found for
this, then nothing is marked as red but if I enter something invalid like this
where the password is too short, well then I do give it that red border and this
is the setup I'm using here. 

Obviously you can adjust this to your requirements. 

---