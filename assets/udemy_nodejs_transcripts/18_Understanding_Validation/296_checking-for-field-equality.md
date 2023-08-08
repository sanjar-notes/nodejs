## 296. Checking For Field Equality

<strong><em>no description</em></strong>

With our basic validation in place, let's now find out how we can check for
equality in our passwords and for that, I of course want to check my confirm
password field, so in my sign up view, I'm talking about this field with the
name confirm password. 

So let's go back to auth.js to that route and let's add a new check for
something in the body of the request, so basically for the confirm password
field here. 

Now in there, I want to check if that is equal to my password and how can I
achieve this? 

Well I could do it by adding a custom validator here, that custom validator
which receives a value and where I then extract the request with this
destructuring syntax and if they're in there, I check if the value of confirm
password is equal to the value of request body password and this is why you
might need access to the request object because here I need to extract the
password, so this field value from the request body in my custom validator. 

And now I can check if they are equal or to be precise, if they are not equal
and if they are not equal, well then I want to throw a new error where I say
passwords have to match, like this and otherwise I return true. 

And this is how we could check for equality of two fields, I'm checking whether
my confirm password is equal to my other password. 

With that if I now save this and I do enter a valid email address, this one is
already taken but I'm not validating for this with this package so this should
be fine. 

I do enter a valid password and I do enter let's say another theoretically valid
password, though we're not checking for length or anything like that on confirm
password so anything would do it there. 

But the important thing is this is a password that differs from this one, you
can make this really clear by adding more characters. 

If I now hit sign up, I get passwords have to match, so this is now working. 

If on the other hand, I take an e-mail address but again that's not validated by
this package but then I try valid equal passwords, then I only get my e-mail
thing but the validation with that validation package succeeded. 

Now it's also worth noting that I did not add the other password validation like
isLength and isAlphanumeric to the confirm password even though that applies to
the confirm password too of course but why did I not add it? 

Because we're already checking it on this main password and then we're checking
for equality, so we implicitly have this check here on confirm password too. 

I don't care if confirm password is long enough because it has to equal that
password and that password is checked for its length,  so I got this in place
here and therefore I am protected against any errors on this site. 

So this is now how we could check for password or any field equality that you
might need in your application. 

---