## 71. Returning a 404 Page

<strong><em>no description</em></strong>

Were you successful? 

Let's add it together. 

I'll add a new html file in views and I'll name it 404.html but the name is
totally up to you, well it has to be a html file of course. 

I'll then create a new html5 skeleton with the help of visual studio code here
and then here I'll name this Page Not Found, that sounds like a fitting title
and now you can get of course really creative here, I will in the end just add
an h1 tag where I say Page Not Found, obviously you can add more content here if
you want. 

Now I want to return this html file whenever we make it into this middleware and
therefore again, I should send a file here but obviously I want to construct the
path with the help of the path module to make it work on all operating systems,
so require the path here and then go down there, send and don't send but send a
file and that file will use a path which we construct here with their name and
now here's a gotcha, we already are in the project folder here because we're in
app.js, so we don't need to go up a level here because we already are in the
root folder. 

Instead here we can go right away into the views folder and then serve the
404.html file, like this, we also still want to set this status code because we
still have a 404 error. 

If you now save this and you enter any random route that doesn't exist, you
should see that page not found being served and you see that 404 error being
sent back too. 

So this is now working too and and this is now a way better, well way of serving
this all but styling would also be nice, wouldn't it? 

So let's work on this over the next lectures. 

---