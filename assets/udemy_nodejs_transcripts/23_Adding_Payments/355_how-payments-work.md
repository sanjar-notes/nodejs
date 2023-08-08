## 355. How Payments Work

<strong><em>no description</em></strong>

Let's first of all start with the payment process, how does this work? 

Well it's a pretty long process, we start by collecting the payment method, so
the credit card data typically. 

We then have to verify that, is the credit card data correct, is it expired, is
the number correct? 

We then have to charge it and after we charge it, we have to manage payments, so
that includes things like fraud protection, also managing disputes and so on. 

And last but not least, we of course have to process the order in our app, so in
our server side code, for example that we store it in the database there. 

Now all the payment related things here are pretty complex tasks, both from a
legal and a technical side and therefore typically you outsource them and by the
way, even very big companies outsource this. 

Stripe is a very popular company offering payment services, it offers a great
integration and it's super easy to add to any application as you will see in
this module. 

How does it work? 

Well we have our client and our server, so that is all the code we own and we
wrote and in the client, we'll collect credit card data. 

We'll do that with the help of stripe and we'll send it to the stripe servers
which are not owned by us but by that company to validate that input. 

Once it is valid, stripe will return a token to us which basically encodes or
which includes that credit card data and the confirmation that it is correct. 

We send that token to our server, so to our code and in our code, we create a
charge or we charge this payment method then with the help of stripe again. 

So we create a payment, an object, a charge object, we send that to stripe with
that token and with our price included and stripe will then do the actual
charging, do the actual managing and we will get a response once this is done
and then we can also continue with our code and edit this or store this in the
database and so on. 

So this is generally how that will work, now let me walk you through that step
by step. 

---