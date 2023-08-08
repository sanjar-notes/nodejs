## 97. What is the MVC?

<strong><em>no description</em></strong>

So what does mvc stand for or what is it? 

It's all about a separation of concerns, so making sure that different parts of
your code do different things and you clearly know which part is responsible for
what. 

MVC stands for model view controller so we work with models, views and
controllers and actually for example views, that is something you already know,
we already got views in our project, right. 

Models are basically objects or is a part of your code that is responsible for
representing your data in your code and allowing you to work with your data, so
things like saving data, fetching data to or from a file or even if it's just in
memory as we're currently doing it, this should be handled by models. 

The views are responsible for what the user sees in the end, they are
responsible for rendering the right content in our html documents and sending
that back to the user, so they are decoupled from your application code and are
just having some light or minor integrations regarding the data we inject into
our templating engine to generate these views. 

And the controllers are now the connection point between the models and your
views because since the views shouldn't care about the application logic and the
models do care about how to save and fetch data and so on, the controllers are
the thing working with the models, saving that data or triggering that save
process and so on and also the part where they then pass that data that was
fetched to your views for example. 

So the controller is the middleman, it contains the in-between logic. 

Now in case you're also wondering how routes fit into this picture, well routes
are basically the things which define upon which path for which http method
which controller code should execute and as I just said, the controller is then
the thing defining with which model to work and which view to render. 

This is the pattern and in an app with express or built with express as we are
doing it which heavily relies on this middleware concept, the controllers are
also kind of split up across middleware functions or some of the logic might be
separated and moved into another middleware function but we'll see all of that
and we'll get there step by step. 

For now, let's simply move back to our project and implement an mvc pattern
there. 

---