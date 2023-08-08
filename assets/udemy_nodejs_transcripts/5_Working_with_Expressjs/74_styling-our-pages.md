## 74. Styling our Pages

<strong><em>no description</em></strong>

Our html pages look pretty boring and obviously this is no css course, I got one
if you want to learn more about css though but that's just a little side note
but this is no css course but still, it's important to understand how you can
serve css in your node apps too because typically, you have css and also
javascript code in your apps. 

Now let's start simple, I'm on the slash page here, so on shop.html and let's
add some styling here with good old style tags in the head section and this is
not the way we'll keep it, this is just so that we can work on it and
auto-update this because importing an external style file wouldn't work at the
moment to spoil the fun already. 

Now as before, you can skip this lecture if you don't want to write the style
together with me and you'll find it attached to the next lecture, otherwise
let's do this together. 

So let's start styling this and let's start with the header. 

Now I won't target the element directly instead this will be my main navigation
or my main header, let's give it a class, main header header, this will be the
main header nav and if you're wondering about the strange css class name, I'm
using a styling system named bem, more on that can be learned in that css course
I mentioned or of course you can google css bem, it's a certain way of naming
your classes to avoid double class names basically, here I'll have my main
header, whoops, header item list and here I'll have my main header items like
this and you can of course name this however you want. 

So these are a bunch of css classes that should help us with styling, now let's
start with the header. 

The header should have a width of 100% to take the full width of the page and
let's say it should have a height of 56 pixels or if you want to work in rem
which has certain advantages, we could also go with 3.5rem. 

Now let's also give it a nice background color and here you're really free, I'll
not stick to red but now I can hover over this and use this nice color picker
and pick any color you want, now I'll try to pick a nice yellow golden-ish
orange color, something like this maybe, if you click on rgb it will also
convert this to a hex code so let's use that and of course the class is not
header but main header. 

And now if I save this and go back and reload, we got that, looks better. 

Now there is some padding in the body so let's actually define that we want to
have no padding and no margin, I think it's a margin, that we don't want to have
that, let's add this, looks almost better. 

We still got some margin here at the top, this is coming from our list in here
though, that some margin call isn't doing its job here, now let's also get rid
of that. 

By now also styling our main header item list. 

So let's copy that, add a class here, set the list style to none and remove any
margin and padding we might have here, that looks better. 

Now obviously the items are not looking nice, for this I will actually change
the display here to flex to use flexbox for the list and then style our items
here a bit, on these items for now I'll remove all margin and padding they might
have, reload. 

Now thanks to flexbox they're sitting next to each other, now let's also style
our links in there. 

So main header item, any nested anchor tag should have no text decoration and a
color of white maybe, looks a bit better. 

Now  vertical centering would also be nice and for that I'll go back to the main
header, excuse me, back to the main header nav here, let's add a class for that
too. 

And here I'll first of all use a height of 100% because this is a child element
of the main header and therefore it should take all its height and this will
also be display flex now and we can center items vertically with align items
centered now. 

With this if I save that and reload this page, now this is centered, now let's
add some padding to our main header. 

For this let's go here, add a padding, top and bottom I don't need padding but
left and right maybe 1.5rem, something like this, on mobile phone also still ok
I'd say. 

Let's also change the global font by the way so in the body I'll set the font
family to sans-serif for now, looks a bit nicer than the serif font I think and
now I want to have some space in-between my navigation items there so let's
actually go to the main header item and let's add a margin to the left and right
of 1rem, like that and for now, this will do. 

Now little hovering effect for the links maybe, so let's also go here, main
header item hover and main header item active and let's also define a rule which
would apply if the anchor has an active class attached to it and there I want to
set the color to well we have this nice little yellow touch here, so we could go
into the blue-ish direction here, maybe like this purple-ish color, let's let's
see how that looks like. 

Not too shabby, so let's go with that and now since we have that active class
rule here on shop.html where this link is active, we can actually add the active
class here and you will learn how to set that dynamically later in the course
too of course. 

So now this is active, now for the main section let's also style this. 

Here I will define a general rule for main that I want to have a padding of
let's say 1rem in all directions and now this is the style I want to go with. 

Now let's also of course work on the admin add product styling here and we can
simply copy the entire style object from the shop.html file in the
add-product.html file and this will already get us pretty far. 

Now one thing we should change in add product, we should of course add all these
classes, so we can basically copy that header and later we will also learn how
to reuse it across files by the way. 

So let's copy that header, by the way that auto-formatting I'm doing
occasionally can be set up in the preferences by going to the keyboard shortcuts
and searching for format document, this is the shortcut I am using here but
that's just a side note. 

So here we now also have to change the active class, it's not on the shop link
here but of course it should go onto the add product link and with that if I now
reload this page, looks way better. 

Now let's work on the form here too and for this, I want to go to my form, give
it a class of product form maybe, the name is up to you, add a little div with
which I give a class of form control and in that div, I'll insert this input
here and I'll also add a label for the title, put title as a label on it, give
that input the ID title so that it matches the label for accessibility reasons
simply and now let's style this too. 

For this I'll use my form control, so this class I added to this rounding div
and here, I want to make sure that a label as well as an input which is nested
in a form control uses a display of type block so that it takes the full
available width and I also want to style the input then, so the input here
should have a border of one pixel solid and then I will reuse that yellow color
we used for the header. 

The font should be inherited so that it uses the default font family and so on
and I'll give it a little border radius of like two pixels maybe, let's see how
that looks like or the radius. 

If I now reload this, doesn't look too bad, let's now also work on the button. 

For this I will set up a generic button style here for now,  inherit the default
font, give it a border of one pixel solid and this light gray a background of
white maybe, let's maybe give it a black border here simply and a border radius
of three pixels. 

Now let's see how that looks like, it's ok but let's reuse the yellow color here
actually and let's also give the text that yellow color. 

Additionally I want to make sure that we assign the pointer cursor to get this
hand cursor when hovering over it and last but not least, I want to have some
spacing but with my form control div and the button. 

So on the form control itself, I'll add some margin to top and bottom of let's
say 1rem and 0 left and right so that this looks like that and I think for the
button, maybe you want to go with the purple color since that should be easier
to read and let's also assign a hover and an active state for that button and
when it is active, I just want to set the background color to purple and the
text color to white then. 

So now it looks like this and this doesn't look too shabby, we can go with that
I guess, we can always work on this and we will continue to work on this
throughout the course but for now this is good. 

Let's now center the entire form and for that I assigned the product form class
to the form. 

So here I want to give this a width of let's say 30rem, a max width of 100% or
of 90% in case we're on a mobile view, give it a margin of auto, this will
automatically center it horizontally and now just make sure that the input and
so on take the available space so let's reduce this 20 actually, I think 30 is a
bit too much and on the form control for laying an input I'll give it a width of
100%. 

and now this looks much better. 

Now I'm not happy with the white text here now that I think about it so let's
actually go to the header and change the white link text to black, let's see how
that looks like, yeah I think I prefer that so let's actually take that and also
add it to shop.html so that we have the black color there too and I think the
purple could be a little bit darker. 

So let's now also go to the hovering and active style here and make this a
darker purple and replace the purple in all occurrences with that color style. 

I'm using a multi-select feature of the IDE here to do that quickly, I can of
course also search and replace to do that, reload, yeah I think that is a bit
better. 

Now you can always tweak this to your needs, it's not a css course here. 

I just want to have some basic styling that we can use. 

So this is the style with which we'll go from now on and which we'll of course
continue to tweak. 

Now one thing we should also do now, let's copy that style from the shop.html
file and put it into the 404.html file here because there, I also want to take
the header and copy that into there because I don't just want to have the page
not found thing, I also want to show the header. 

So that now if I do enter some route which does not exist, like this, we also
got the header there and we can at least leave that route, though we can't
because I obviously got an error in the url, that should be admin flash add
product. 

Now let's fix that everywhere here including our form of course, like that and
now if I reload, we can navigate around just fine here and try adding a book,
that seems to work. 

And with that, we get the styling in there, we get the basic html markup but of
course regarding the styling, the issue is that it's all in our html files. 

It would be nice to have some external files for that, wouldn't it? 

---