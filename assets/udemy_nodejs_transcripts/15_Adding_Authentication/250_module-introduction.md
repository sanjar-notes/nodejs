## 250. Module Introduction

<strong><em>no description</em></strong>

Now that we learned what sessions and cookies are and we had our dummy
authentication flow in place, let's dive into real authentication. 

This means that in this module, we'll add a functionality that allows users to
sign up, to sign in and we'll make sure that some resources can really only be
accessed by users who are signed in and that we're not just hiding the menu
options but that we really lock down access, I will also show you how to store
passwords securely and so on. 

So what exactly is inside of this module? 

Well first of all, we'll have a look at what exactly authentication is, how it
works in a node application or in a web application in general because this is
actually not limited to nodejs, authentication would be implemented like this in
a PHP app in the same way and in all the other languages too. 

We'll have a look at how we can store and use the credentials, so the email and
password with which the user signed up and I will dive into protecting routes,
that is what I meant with locking down access to make sure that users are only
able to access the routes they need to access and that we don't just hide the
menu options but that we really check the permissions on the server side. 

---