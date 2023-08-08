## 360. What are REST APIs and why do we use Them?

<strong><em>no description</em></strong>

Rest APIs are there to solve one problem you could say. 

Not every frontend user interface works with html pages or not every user
interface might want your server to generate, well the html code which
effectively is the user interface. 

Think about mobile apps, for example the Twitter app, these apps typically don't
work with server side rendered html code, they don't need a templating language
on the server to render the html code because you build these apps with Java for
Android or with swift objective C for iOS and you use a rich suite of pre-built
UI widgets, you use UI libraries provided by Apple, by Google and so on, you use
these libraries to build your user interfaces in the respective IDEs of these
programming languages like Android Studio for Android development. 

You build these user interfaces totally decoupled from your server, you don't
want html code because you can't really render it there. 

Obviously you have mobile browsers too, you have a browser on your mobile phone
and that will render html pages but all the apps you install through the App
Store most often don't use html to draw the interface but instead they build the
interface with the tools given to them by the, well by Apple, by Google and then
you only need to data to fill these user interfaces with life. 

Another example would be single page web apps. 

You might not have heard of these but the Udemy course player is actually a
great example for that. 

Here's an example, this is a course by me but of course this is the case for any
course. 

Watch this refresh icon at the top left corner as I now click around to course
content, Q&A and so on. 

Now all these parts here do re-render without the page reloading or the page
being refreshed and the reason for that is that this entire page is actually
rendered through browser side javascript, you can of course execute javascript
in the browser as you know and this javascript code can manipulate the dom, the
dom is simply the rendered html code. 

So what Udemy does here and what is very popular, not just on Udemy but on many
modern web applications is that you only fetch one initial html page that does
not really contain a lot of real html content but that does load all these
javascript script files and then these javascript scripts reach out to some
backend API, to a restful API and only fetch the data they need to work with to
then re-render the user interface. 

So if I click on Q&A, some javascript code would reach out to a Udemy server and
get me the Q&A items I want to display. 

If I click on course content, another script reaches out to the backend and
gives me these course items and if I click on one of them, then I might enter a
new area where another part of javascript takes over. 

So such web applications are very popular because they give us a mobile app like
feeling. 

We click around and we don't have to wait for a page refresh, we always stay on
the same page and only the data that gets rendered changes and therefore only
the data is exchanged behind the scenes, all the user interface rendering is
done through browser side javascript. 

So this is another kind of popular user interface of popular frontend you build
these days and I actually got a lot of courses on react, on angular, on vue
which are popular browser side javascript frameworks that you can use to build
such user interfaces. 

You also might not work on a particular frontend, maybe you are working on a
classic node application as we did thus far but you also have certain service
APIs that you might want to use, like the Google Maps API. 

So here it's not the frontend that requires us to build a rest API on our own
but this is another example for a case where you only need the data and no user
interface. 

You don't expect the Google Maps API to give you back the html code, you might
just be interested in some coordinates, something like this, so again you're
interested in the data. 

And that's the common theme here. 

We have a frontend or we have code that is decoupled from the backend or from a
certain backend logic like Google Maps and we only need to exchange the data
because we don't want to get any user interface, we don't want to get html code,
we build that on our own, we just have a backend that needs to serve us data and
that is a core idea or that is the core idea of building rest APIs because there
we need a different kind of response. 

And rest API or rest stands for representational state transfer and the simple
translation I like to use is that we transfer data instead of user interfaces. 

So instead of html, we just transfer data and we leave it to the client or to
the frontend, be that a mobile app, be that a single page application, we leave
it to that frontend to then do with this data whatever it wants to do. 

And thus far in the course, we always rendered the html page on the server and
that of course did not only include the data but also already the user
interface. 

And let me also highlight that this is not bad at all, it's a common pattern for
a lot of web applications but for other applications, you might want to build a
decoupled frontend or you might need to and then rest APIs are the solution. 

It's also important to highlight that only the response and the request data
changes but not the general server side logic. 

So everything you learned about validating, about reaching out to databases,
about handling files on the server, all these things don't change, you do that
in exactly the same way when building a rest API and that is really important to
me because often, rest APIs and traditional web apps where you render the views
on the server are seen as two totally different things. 

They are not, they only differ in the response and in the kind of data you
expect but they don't differ in what happens on the server besides the fact that
you don't render the view there and that is really important and this is also of
course why what you learned thus far is now not redundant, actually we'll reuse
99% of the knowledge, we'll only tune our data usage or our data handling and
the response a little bit. 

---