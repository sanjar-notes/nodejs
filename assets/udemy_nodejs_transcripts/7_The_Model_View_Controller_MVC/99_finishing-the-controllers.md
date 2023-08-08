## 99. Finishing the Controllers

<strong><em>no description</em></strong>

We added our products controller in the last lecture, now let's also make sure
we handle the 404 route with a controller. 

In theory this is of course is not required, it's totally optional but it's a
good practice. 

So definitely pause the video here and try this on your own before we then do
that together, make sure to decide which controller you want to use, a new one
or the existing products controller and how you would extract the 404, here is
the 404 page logic into that controller and connect the existing route to it,
good luck. 

Were you successful? 

Let's try that out and for that, let's first of all identify where we are
rendering that 404 route and that is in the app.js file here at the bottom. 

Now we can absolutely leave that code here, it's very simple and there's nothing
wrong with it but to be in line with our other code, I also want to put that
into a controller. 

Now it's clearly not related to products because we can have many features on
our page and every path can fail or the user can enter any random path, so
instead I'll create a new controller here and you can name this however you
want, you can name it 404.js, I'll name it error.js and in there, I will export
a function with exports and then I'll name it get 404 page or you get 404 to be
in line with get products which I have in the other controller and now I will
cut that function here, this middleware function from app.js and in error.js,
this is what I will store here in get 404. 

This is my function where I return the 404 page and with this I just have to go
back to app.js and in there, I will simply import my controller, so const error
controller is imported by going to the controllers folder and there to the
error.js file and we can now take that error controller here and down there on
app use, I will simply put error controller get 404, just like this as a
reference to this function. 

And now this is also in line with the other routes and with the other products
controller. 

So this is now the controller being added and with that we get views and
controllers. 

Let's move on to the model next. 

---