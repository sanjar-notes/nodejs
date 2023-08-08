## 85. Adding a Layout

<strong><em>no description</em></strong>

You probably do notice that we do repeat a base structure in all our files here
and of course it's a bit annoying that we manually have to do that, for example
this base setup and also the import of main css as well as the header is part of
every single page and therefore it's a bit cumbersome if we manually have to
repeat this setup or this import all the time, so what can we do regarding that?


We can create a so-called layout. 

For this I'll create a new subfolder in views which I'll name layouts in case we
might have multiple ones and I'll add a main layout.pug file. 

Now I'll take my add or my shop.pug file or maybe 404 which is the most minimal
one and copy that file content into main layout. 

Now of course we get some elements in here which are dynamic now, which depend
on the page I want to use  and the question is how can we reuse this skeleton
anyways. 

Well we can extend this layout from inside our other pug views and we can
actually define some placeholders, some hooks in this layout where other views
can then enter their content. 

For example here in the links, we get a base layout which looks like this but in
other views that should extend this layout, they might use this layout and add
more links in this place. 

We can define such a hook by adding the block keyword which pug understands and
then defining any name of our choice, styles for example. 

Now we will be able to add more styles from inside other files here and I will
show you how to add this in a second. 

I also want to remove that active link here, by the way also in the 404.pug file
because I have no assumption about what's active and I will show you how to
dynamically set this in a second too. 

Now the content below the header also is dynamic and here I again will reserve a
block, so a hook which I'll name content and the name again is up to you. 

So now we get this basic layout with two hooks we can dynamically enter content
into from inside our other files. 

Now let's start with the 404.pug page here, there I will just copy that content
that matters to me and remove the entire rest and we can now extend the layout
by adding the extends keyword which pug understands and now we just need to
point at the layout. 

For that we have the layouts folder and we want to use the main layout file in
there, we have to add .pug here too. 

So now we're telling pug that we want to extend this and now we just have to
tell it what to render in that content and maybe also in that styles hook we
defined. 

For styles I don't need any special setting here but for the content block, I
want to enter my own custom content and I do this by again typing block content
but now since I extend a layout, this will not define a hook but actually allow
me to add content in that layout and then indent it here, I define what should
be injected into the content block in the layout, so in this place. 

With that if I save that and I enter some random path which doesn't exist, I
still get page not found but now behind the scenes, this actually uses my layout
and we can of course do the same on the other pages, like add product. 

There let's also for now keep the other content so that we can copy and paste
content over into our new layout, so we extend main layout pointing at the
layout file and here I will add something to the content but also into my styles
block and we do that by simply typing block styles here and then indent it, we
add what we want to add and these are these two lines because these are the two
style imports which are not part of the default layout. 

So let's add them here in the styles block and then we have the other block, the
content block, this one where I want to enter my own content. 

So for that, I will copy the entire part in the main section here or the entire
main section actually, like this, cut it and move it over and replace this h1
tag here and make sure the indentation is correct and now we can remove the
entire rest here and we should now have a file that does extend our layout and
therefore still looks the way it look before but now it uses this way more
concise approach which also ensures that if we ever change something to the
layout, we don't have to change it in all the files but only in that main layout
file and the other files since they extend it will automatically get it. 

So let's save this, let's go to add product and this looks good. 

Styling is good so all these styles are imported as you can see and it looks
like before almost. 

We got this active class missing, we don't see that the add product link is the
active one and that makes sense because in the main layout, we make no
assumption what is active. 

So the question is, how can we dynamically set this? 

---