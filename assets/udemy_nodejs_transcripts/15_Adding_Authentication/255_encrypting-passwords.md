## 255. Encrypting Passwords

<strong><em>no description</em></strong>

We did add a basic authentication flow or a signup flow in the last lecture but
we have one huge security flaw in our current approach. 

Do you know which flaw that is? 

Well we can see it in this line when we store a password. 

We're storing the password in plain text and we can see that here in compass,
this is the password I entered and it's stored in plain text. 

Now this is not how you should do it because if your database gets compromised
which of course we want to avoid but if it happens or if some employee of your
company has the rights to look into it, your user passwords are fully exposed. 

So what we should do is we should encrypt that password, we should hash it in a
way that is not reversible, where people cannot construct the password from, so
that even if you get access to the database, you might be able to see the e-mail
but you're not able to see the password, the real password that belongs to the
e-mail. 

This is something you should implement and this is something we will implement
now and for this we'll install another package. 

So I'll quit my server with Control C and install that package with npm install
--save and the name of the package is bcryptjs, written like this. 

This is a package that helps us with encryption and that will help us with
encrypting the password. 

Now once this was installed, we can restart our server with npm start and now in
the auth controller here, we can use bcrypt, so here I will add an import at the
top and I'll name it bcrypt, the name is up to you and I'll require bcryptjs,
like this, so the package we just installed. 

With it installed, let's head over to post sign up here and here instead of
storing the password like this, I will store a hash password. 

For this right before I create my user, I'll use the bcrypt package which I
installed and which I imported here and I will call the hash method. 

The hash method as a first value takes the string which you want to hash, so in
our case the password, so we'll pass the password here. 

The second argument then is the salt value, now this is simply specifying how
many rounds of hashing will be applied you could say and the higher the value,
the longer it will take but the more secure that will be, currently a value of
12 is accepted as highly secure. 

Now this will generate a hash password but this is an asynchronous task and
therefore this actually gives us back a promise. 

So I will return this so that I can chain another then call, a then block where
I will get my hashed password as an argument once it's done, so this function
here will be called once the hashing is done and therefore the user creation
will go into this then block and there I have the hashed password available and
the hashed password is what I'll store here. 

And with that, we dramatically improve the performance because now if I do sign
up again, first of all let's use a different e-mail otherwise it should fail, we
can test this in a second too. 

So I use a different e-mail, if I sign up now and I look into my collection,
this is the new user and this is of course not the password I entered, this is
the hashed value and the important thing is you can't reconstruct the password I
use, you can't decrypt this. 

This is also the reason why we don't encrypt the e-mail because we won't be able
to decrypt this, I will still show you how we can then find out if the user
entered a correct password but we can't decrypt it, so if we need to send
messages to that e-mail, that would not work if we encrypt the e-mail as well
because we could not revert that. 

So we need to store the e-mail like this but the password is secured, it's not
readable. 

So this is how we should store it and now I will get rid of my other user but
not before testing whether that works. 

So if I try to create a user with that same email again, I'm redirected to sign
up. 

So I don't see an error message because I didn't add anything that would show
such a message but it seems to fail here, that is good so for now, we can't
create a new user with the same credentials. 

Let's now get rid of this one with the insecure password and continue with the
one with the secure password. 

---