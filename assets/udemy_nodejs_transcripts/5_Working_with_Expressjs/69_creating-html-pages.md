## 69. Creating HTML Pages

<strong><em>no description</em></strong>

So now that we had a very close look at that whole express middleware thing and
how routing works in express and how we can use that to our advantage, how we
can filter routes and so on, let's actually start working on what we serve to
the user. 

Thus far it has always been some dummy html content but you're probably not in
the course to just learn how to build dummy html content, so let's return some
real html files to the user that also don't look like crap. 

For this I'll create a new folder in my project and I'll name it views, now that
name is up to you, you can also name that folder whatever you want but in that
course, we will slowly go towards a MVC, a model view controller structure and I
will explain what this is a little bit later. 

One part of it is that we manage our views, so what we serve to the user in one
place of our application in the views folder here. 

Now the views will just be a bunch of html files here though. 

So I'll create a new file and that will be my shop.html file, it's a file I want
to serve for users visiting just slash and I also want to have my add product
file here. 

So I'll add add-product.html, later by the way in case you already know the
concept of templating engines, we'll use these two so that we can dynamically
add content into the html files but for now, let's just start with these files. 

So let's start here in add-product.html and now here's one important note, if
you're not interested in writing that html code, you can skip this lecture now
and find the finished html code attached to this and the next lecture. 

So if you want to skip, you can do that and just follow along in the next
lecture where I will provide that finished html code otherwise let's now create
it together. 

So in this add-product.html file, I'll now create a new html5 skeleton and
visual studio code helps you with that,  as you saw if you just type html5, it
should open this pop-up, if it doesn't you can force it by typing or by hitting
control and space and then navigate to html5 with the arrow keys and hit enter
and it gives you this nice skeleton which basically defines a basic, well html
skeleton. 

Now here I'll change the title to add product and in the body, there I now want
to have my form. 

I don't just want to have the form in there though, I also want to have some
navigation bar that allows me to switch to my shop.html page, to the slash route
and the other way around. 

So here I will first of all add a header and in that header, I'll add a nav bar
and in that nav bar, I'll add an unordered list with list items which are links
where I go to slash, so this is just my shop and then another list item, add
product which will be /add product. 

This is the page we're on here but I always want to show both options, obviously
you can write the html code that fits your needs. 

So this is the header, it will be pretty unstyled for now, we'll add styling too
and now let's add a main section too, so this is also a normal html element
which holds or which should hold the content of our page here. 

And there I want to have my form with the action that is also add product,
remember here we're then targeting this post route and in there or there, I will
add my post method and I will now also add my input here, the input of type text
with a name of title and I will add my button of type submit here which I'll
label add product. 

Now we will add more to this form later because a product is obviously not just
made up of a title but for now, this will do. 

We got our form in here, let's now copy that entire html code and paste it into
the shop.html file and there of course in the main section, I don't want to have
a form instead a h1 tag my products and below that later in the course, we will
render all the products. 

So here we will have a list of all the products and right now we don't have that
but we'll get there once we learn how to manage data on the server and so on. 

Now the rest of the page can stay the same for both pages and again as I
mentioned, styling is missing. 

Let's now move onto the next lecture where the goal will be to serve these html
pages before we then work on the styling. 

---