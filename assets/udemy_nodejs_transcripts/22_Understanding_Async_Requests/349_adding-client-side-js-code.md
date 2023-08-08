## 349. Adding Client Side JS Code

<strong><em>no description</em></strong>

In our course project on the admin products page where we can delete products, I
want to implement this delete function differently. 

Right now when I would click delete, I would simply well delete that, send that
request to the server and get back a new version of that page essentially where
this product is then missing and we can see that of course on our server side. 

If we have a look at our admin controller and we have a look at the post delete
product action, this action here, then we see that we, well we also extract some
incoming data of course and then we work with the data to delete the image
belonging to that product and then the product itself and by the end, we
redirect back to admin products which is a route which will return a new html
page. 

Now don't get me wrong, there is nothing wrong with this set up and you can
absolutely use it but maybe it would be a great user experience if we would
never have to leave that page, if we wouldn't reload that page but if we click
delete, we send that information that we want to get rid of that item to the
server behind the scenes, the server can then still do its thing and once we're
done, the server will respond just with some json data, so some success message
or anything like that and once we get that message in our browser, we can delete
this dom element, so we can delete this article here. 

We could do all that with client side javascript, so with javascript running in
the browser and some help by our server side here and that is a so-called
asynchronous javascript request or this will use so-called asynchronous
javascript requests. 

Now the logic on the server won't change too much but the way we expose our
route changes a little bit and we'll have to add some logic on our client side,
so let's do that now. 

And for that, I'll first of all go to my public.js folder and I'll create a new
file there, the admin.js file, now you can name it however you want. 

Important, this is javascript code that will now not run on the server but that
will run in the client, so in the browser. 

I will import this javascript file into my products page here. 

So there let's say below the bottom here, below our footer, I will import a
script with script source and you have to close the script tag like this and
then I will import js admin.js. 

So I will import that javascript file from the js folder which is in a public
folder which is served statically. 

Now this script will execute on this products.ejs file and if we load it at the
end of this file, we make sure that the entire dom has been rendered and parsed
by the time we execute our javascript code. 

So now we can go back to admin.js and add some logic in there, now which logic
do I want to add? 

Well I want to react to a click on this delete button here and therefore first
of all, this button should not be of type submit anymore, i should be of type
button instead. 

Actually I will remove this entire form because this form was required for
sending a request through the browser, sending a request with this xwww url form
encoded data. 

Now I'll not do it like this anymore, I will get rid of that instead and
instead, I will now gather that data here manually. 

So I will listen to a click to that button and then I will gather the product ID
and the csrf token manually through the help of my client side javascript. 

Now with the form removed, I'll go back to admin.js and here, I now want to get
access to all these delete buttons, listen to a click on them and then do
something when they get clicked. 

Now for that, I'll define a function, admin.js delete product, here I'm using
next gen code but this is code that will run in the browser, all modern browsers
support the syntax but of course if browser side javascript is new for you, you
should take a dedicated course on that, this course will not focus on that but
here I'll have a function where for now, I will simply execute clicked. 

Now this delete product function is a function I can use from inside my ejs and
therefore html file, on that button I can add onClick and simply say delete
product, so this function here, delete product like this, execute that function
when we click on that button. 

If we now save that and we reload this page here and I open the browser
developer tools, if I click on delete, you should see clicked here. 

Now it's not deleteing the product anymore because we deleted that form, right. 

So now I'm reacting to a click and now the next thing will be that we have to
find out which ID and csrf token we have. 

For that back in the admin.js file, when we click I want to get access to the
field next to the button, I want to get access to the csrf token and as I
mentioned, to the product ID. 

Now how do I get access to the surrounding elements? 

Well in products.ejs, we can pass this to delete product. 

This is a special keyword and in the context here, it will refer to the element
on which we clicked, so to the button. 

Now since I get this, in admin.ejs, I can access to the button since I now
receive this as an argument and I can prove to you that this is the button by
simply logging it. 

If we reload the page and I click delete, we see the button being logged here
and here it would be that button. 

So now we have access to the button and with that we can easily get access to
the surrounding inputs. 

I can simply access the parent node of my button which will simply be, well the
element around my button, so in this case this div here and I can find my inputs
in there, the input with the name product ID and the input with the name csrf,
_csrf. 

I can do so by using the query selector on the parent node and here, I'll use
the attribute selector to find name equal product ID. 

Now let me log this to the console to see if it works. 

If I now reload my page and I go to the console log, now I get that input ID
being logged, that hidden input ID. 

Now from that input, I can of course also extract the value which is then just
the product ID itself and not the entire dom element. 

So with .value added, now I just get the ID and for the other product, I get
well the other ID. 

So now I have a way of getting that, let's store that, prod ID in a constant and
then let me also store the csrf token and here I will simply repeat that code,
access the element with a name of _csrf and extract the value. 

And now with these two pieces of information, we can now send our asynchronous
requests to the server, for that of course, we need a fitting route and so on. 

So let's work on that next. 

---