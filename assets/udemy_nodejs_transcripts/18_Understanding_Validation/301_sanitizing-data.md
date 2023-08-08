## 301. Sanitizing Data

<strong><em>no description</em></strong>

Now we learned a lot about validation and providing a good user experience, now
sometimes you also want to sanitize user input. 

Now what does sanitising mean? 

For one on this validator page, so the package which is used behind the scenes,
you don't just find all these validators, you also find available sanitizers
here and there you also see what they do. 

For example what you can do is you can ensure that there is no excess whitespace
in a string passed by the user on the left or on the right, you can normalize an
e-mail which means it's converted to lowercase and things like that. 

So there are a couple of things you can do to make sure the data you get is not
just valid but also is stored in a uniform way, so without extra whitespace or
anything like that. 

So sanitising input is also something that makes sense to be done. 

Cross-site scripting attacks sanitation which is a security feature is by the
way something I'll cover in the security module of this course, so we'll focus
on the visual sanitization for now not on security relevant sanitising. 

So this is what you can also do, now how does sanitising input work though? 

Well you do it in one step with validating, so in the routes folder in the
auth.js file in our example, let's say the email here, I want to make sure that
it's stored in a normalized way, so lowercase not starting with an uppercase
character, no excess whitespace. 

Well I can do this by chaining another method after my validation logic and
there I can call normalize e-mail which is one of these built-in sanitizers
which I showed you. 

For the password we could trim it, so here we could trim the password to remove
excess whitespace. 

Of course we can do the same for the sign up here, besides our check here I also
want to normalize the email once I'm done with it, with sensitise, with
validating and for the password I want to trim excess whitespace. 

So again this is something which I can do here to sanitize user input and to see
the result of that, let me actually connect to my database real quick with the
help of compass, my visual user interface here and there in the users, I get a
bunch of users because I created some users throughout this module. 

Let me delete a couple of entries here really quick just to clean this up, well
actually delete them all and now let me create a new user, keep in mind I added
sanitization. 

Now if I enter test@test.com like this with an extra blank after this and I
enter my password here with an extra whitespace at the end, so our blank at the
end, then I do already get an error because for signing up, I do actually trm my
password here but I don't trim the confirming password, so I should trim this as
well otherwise the whitespace is removed here and indeed it is, this is one
character shorter. 

Now if I sign up, both passwords were changed and keep in mind the email started
with a capital character and also had an extra whitespace, if I now reload my
users, we see the email is stored with a lowercase t at the beginning and
without that extra whitespace at the beginning and this is now simply the case
because I sanitized the input. 

So sanitising data is also something which makes sense to ensure that your data
is stored in a uniform format and well that your email addresses look equal and
so on. 

---