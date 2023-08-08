## 339. Adding Pagination Links

<strong><em>no description</em></strong>

Here's our shop and I created three products behind the scenes, so you can of
course create any three products on one or more user accounts, doesn't matter,
in the end you will have three products. 

Now obviously we can absolutely display these three products like this, nothing
wrong with that. 

But let's say we have hundreds of products, we would not want to display all
these products on one page, instead we'd like to split them across multiple
pages and then somewhere on the page, often at the bottom, we'd have some
controls to go to page one, page two, the next or the previous page and that is
exactly what I want to implement here, pagination. 

Now you can certainly find some third party packages that can help you with that
and these would be fine to use but I will show you how to implement that from
scratch on your own because that is obviously how you learn the most. 

So back in our project, how can we implement pagination? 

Well typically, you handle this as I said by adding some controls which always
leads to the same path. 

so always /products or slash nothing but then you add a query parameter,
remember query parameters are these parameters you add after a questionmark
which allow you to specify optional data and there you could specify something
like page equals one to load the first page or page equals two to load the
second page and you would change these query parameters with these controls you
add. 

Let me show you what I mean. 

I will go into my views folder and let's work on that slash, so on that root
route, so that index.ejs file here and there at the bottom beneath my products
but inside of that first if block, so where I know that I have some products, in
there I'll add a new section. 

I'll give it a class of pagination because this will be the section where I
manage the pagination and my idea is to have a link here which says 1 for Page 1
and 2 for Page 2 and here I would go to slash and have page equal to one let's
say and here, page equal to two. 

So here I would set a query parameter to value one or respectively, to value
two. 

If I save this and reload, we can see that on the left here, now let's change
the styling real quick. 

So for that, I'll go into my public folder, css and there the main css file and
I'll scroll all the way to the bottom right before that media query, I'll add
pagination so that class I added to the section and I'll set text align to
center and I'll also style my links. 

This is of course totally optional but I will style my anchor tags in there to
have no text decoration, so to not be underlined. 

I'll give them a color of let's say my green which I'm using in this project, I
will also add some padding of let's say .5rem and give them a border of one
pixel solid and that same green color and also some margin of 1rem left and
right, something like this. 

If I now save that, I have these buttons here. 

Now one more thing, on the whole pagination section, I'll add a margin top of
2rem and I also want to make sure my buttons have some hover style, so
pagination a hover and pagination a active sets these styles when I hover over
them or when I click on them and there, I will set a background of this green
color and change the text color to white. 

Now this is all optional, I just want to have some stylings here for my buttons.


So now we have these buttons and if I click one of them, you can see the url
changes, it's the same path, just slash nothing but I have an optional parameter
in there. 

Now with that set up here, let's now see how we can work with that parameter on
the backend to control the data we are fetching. 

---