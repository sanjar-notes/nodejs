## 425. Adding Input Validation

<strong><em>no description</em></strong>

Now we added our first mutation and a mutation of course also means that we
store data in the database. 

When something like this happens, we want to ensure that the data we store is
valid and previously in the rest API and also in the normal node express
application where we render views, we use express validator for that and we
added that as a middleware on our routes. 

With graphql, this is not an option because we only have one route, this one,
this is the only endpoint we have and we certainly don't want to validate all
requests in exactly the same way. 

So to change that and to adjust it to our needs, we want to move validation into
our resolvers. 

There we have our endpoints and there is the place where we can now validate our
incoming request data. 

To do validation there, I'll install a new package with npm install and then
--save and that is called validator and that by the way is the package which
express validator used behind the scenes, we can use that directly in our code
now. 

So in my resolvers file, I will import that validator object provided by the
validator package and now in create user, we can add some validation logic with
simple if statements. 

For example I can check if I don't have a valid email, so not validator and then
isEmail and you got the same rules as with express validator because as I
mentioned, it builds up on this validator package and then I check if user input
email is not an email address and if that is the case, then I want to store that
error. 

So I'll create my own errors array here and that's just one way of handling
this, you could find a different pattern of course and I will push a new error
onto this array and for me here and that again is only my implementation, an
error will be an object where I have a message, for example e-mail is invalid. 

Now let's say we don't just want to validate the e-mail, we also want to check
whether our password is there and if it's too short. 

So if validator is empty user input password, then we have a problem because
then we got no values for the password or we also have a problem if it's not
empty but if the length is not long enough. 

So if the length for the password is not fitting the criteria we specify in the
second argument to isLength which is an object where we can set a min and max
key and I'll set min to 5. 

So if we enter a password that is empty or not long enough, so if it is not long
enough, we need to add an exclamation mark here, then we make it into this if
statement here and then we also have a problem and there I also want to push an
error onto my errors array and there I'll add a message of password too short. 

Now this is just one way of implementing this, now after having all these if
checks, I can check if my errors array has a length that is greater than zero
which means I do have errors and if I do, I'll create my own new error object
where I throw invalid input or where I report invalid input and now I throw that
error. 

Now let's give that a try. 

If I now try to add an email address which is not an e-mail address and I hit
play here, I indeed see my invalid input message and that is how we can add
validation. 

What if we now want to pass more data with our error message here? 

---