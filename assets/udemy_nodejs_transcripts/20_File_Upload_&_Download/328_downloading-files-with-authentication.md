## 328. Downloading Files with Authentication

<strong><em>no description</em></strong>

So serving images statically is fine but we don't want to serve only images or
only public files, I want to serve an invoice and that invoice should only be
available to me. 

Now for that, let's start with a dummy invoice and I'll create a new folder for
that, I'll name it invoices. 

You could of course put all images and invoices and so on into a parent folder,
like data to not have them all as root level folders, that might be something
you want to do. 

I'll move the invoices in there, images is kind of like a special case but my
private data should be maybe somewhere else, so I'll put it into the data folder
which was redundant until now, now it's not anymore and I prepared a simple pdf
which I'll move in there. 

Now this is a really simple pdf, you can write it on your own, it's just holding
some text looking like this. 

So here is my invoice, that is the pdf file I'm serving now, later we'll also
generate this dynamically, now we won't, now I just want to show you how to
serve that. 

Now obviously, we could make our invoices folder here statically accessible but
that's not what I want to do. 

Now first of all let me work on the orders view to make sure we have a link to
get that invoice. 

So for each order, this list item here which we have, let's maybe add a dash in
the list item and in there, let's add an anchor tag which says invoice and then
it should be pointing at the invoice. 

So now if I reload this page we have invoice here as a link, now I want to be
able to click this and download the invoice, how can we do that? 

Well since I want to handle this privately, I need to set up my own route for
working with invoices because that will then allow me to check for things like
is the user authenticated and so on. 

So let me go to the routes folder and in there under shop because this is a
customer feature, not admin related, under shop here I'll add a new route,
orders and then maybe invoice ID or order ID maybe because the invoice let's say
will have a name of that order ID ultimately, we could name this file
differently, we can name it invoice and then let me quickly look up my order ID
to make this all work correctly. 

Got a bunch of orders in there but this is my latest order which I just placed,
so let's grab that text ID here and add that to the invoice name here, maybe
after a dash we have the order ID, something like this. 

So this is my invoice and I'm getting the order ID in this route, I should be
protected, authenticated to see tha, so I'll protect this route and then I'll
use my shop controller and there, I get invoice controller action which I have
yet to add. 

So that's why it crashed here because I don't have that action yet. 

In the shop controller at the bottom maybe, let's export get invoice here and
that will be our default middleware function with request response and next and
in here, I now want to return that file. 

First of all, I need the invoice ID for that, the order ID, excuse me, order ID
will be a request and then it's encoded in the url, so it's params and then
order ID, that is what I specified here in my routes file, order ID that's the
name and therefore I have to retrieve it by that name in my controller, so order
ID here. 

Now I have that order ID, the file name or the invoice name we'll be looking
therefore will be invoice- and then my order ID and then .pdf right, that is the
format in which all our invoices are stored let's say. 

So now we need to retrieve that file and we can retrieve files with nodes file
system. 

We use that before in the course already, so let's start using it again,  let's
import it, file system by requiring file system, this is a core node module if
you remember, you don't need to install a package it's already included in node
and the file system allows you to do things like read files which sounds like a
thing that makes sense here. 

So let's use the file system and read a file, we know it will be found in the
data folder, now the path here should be constructed with the path core module
so that it works on all operating systems. 

So let's also import path by requiring path, another core node module, the path
module and let's construct that path to the invoice, so here I'll have my
invoice path and I'll create it with path join and I'll be looking for the data
folder,  that's the first element, then the invoices folder and then the invoice
name, the file name. 

So this is the path which I want to read, so I'll pass that invoice path to read
file, read file then gives me a callback, so a function which it will execute
once it's done reading that file, so here I will either get an error or the
data. 

Now data will be in the form of a buffer. 

Now of course we should check if we have an error and if that is the case, well
then we simply next it so that the default error handling function can take over
otherwise if we don't have an error, here I'll return by the way so that the
other code won't execute. 

So if we don't have an error, then data should be my my file right, so then I
can call res send which is a function provided by the express middleware, my
data. 

Now theoretically that should be the file, now let's see if that works and to
make it work, we have to use this route in our anchor tag. 

So in orders.ejs, in this anchor tag we'll be looking for /orders/ and now we
need to output something dynamic with ejs and that is the order ID because
that's what we're looking for in the route, so the order ID is simply order_id
which we use up there already. 

So let's output that here,  let's save that and reload that page and now let's
click this invoice here and I do get my download option here. 

Let me save that and try to open that file and indeed, it should open as a pdf
or you should be able to open it as a pdf but of course it was not the most
convenient way of downloading this. 

We had a strange filename right, this strange cryptic name, we don't have the
pdf extension and all of that. 

So we can certainly improve that, let's do that in the next lecture. 

---