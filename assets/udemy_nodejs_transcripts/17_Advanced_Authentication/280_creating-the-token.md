## 280. Creating the Token

<strong><em>no description</em></strong>

So let's give this a try, this reset mechanism. 

And for that, we first of all need to make sure that our newly added controller
actions can be reached. 

So we added a get reset root. 

Now we also need to add a post reset root so that this reset password button
actually works. 

So let's add this root and execute post reset that action we worked on. 

And with that on the reset password page. 

Let's first of all, try out an incorrect URL, an email, one which does not exist
in the database. 

And we get this message, which is great. 

Now use a real email which you used for signing up and click Reset Password. 

Now you should be redirected back and if you check your emails there, you should
have a password reset email with a link. 

If you click that link, you should end up on a page not found error, but you
will see that we are on reset and then some token. 

And that token can also be seen in your user collection here. 

This is the password reset token which we stored. 

So now we just need to add some logic to add this root, extract that token,
validate whether we have a user for that token and then offer a form that allows
the user to set a new password. 

Let's work on that next. 

---