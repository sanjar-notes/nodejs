## 361. Accessing Data with REST APIs

<strong><em>no description</em></strong>

So now that we know what a rest API generally is or which problem it solves, let
me give you a big picture of how it works. 

We have a client in the server and the client is a mobile app or our single page
application, on the server we build our API. 

So here we build an API for these apps we might be building and one advantage by
the way is that we can use one and the same API for multiple clients. 

So we might be building a web app and a mobile app, not that uncommon these
days, most companies have mobile apps and web apps but we can use one and the
same API because both apps, mobile and web app use the same data of course, they
might present it differently and that is what I was talking about, about the
user interface being handled by the frontend, by the client. 

They might present it differently but they work with the same data, so that is
our API we might be building or we have any kind of app including our
traditional web app which just needs a service API or we might be building our
own service API, maybe to also sell our service. 

Maybe we're building a stock API where any application which we might not even
know is able to query data from and we just sell access to that API and that is
our business model. 

So in all these cases, we obviously exchange something and this something we
exchange is data as I mentioned before, only the data not the user interface. 

And that of course leads us to one important question, in which format do we
exchange that data? 

We learned about html thus far but there are different kinds of data we could
attach to a request and a response. 

We can send plain text for example, we could send xml or we could send json and
there are other formats too but these are some well-known formats. 

Html of course look something like this so we can send html code and this is
what we did thus far in the course. 

When we rendered an ejs view, what we essentially did is we sent html code to
the browser because the view was rendered on the server and the result of that
rendering process simply was a html page, simply was html code, so this is how
we could send data. 

Html code contains both the data and the structure of course, the html elements,
the css styles we might be adding, that all adds structure and design and what
is between the html elements is our data. 

So therefore this also contains our user interface, it defines how our user
interface should look like. 

Now the problem is of course that if we just want the data, we got all the
overhead html content, it's unnecessarily difficult to parse because even though
the html elements are of course kind of defined and regulated, how we use them
and how we well structure our document is not really enforced onto us, so its
unnecessarily difficult to parse if we just need the data. 

We can of course send plain text, the thing here is this is only data of course,
there is no structure, there is no design element added and therefore, we make
no UI and that is user interface of course, we make no UI assumptions. 

Still if you want to transfer data like this, it's unnecessarily difficult to
parse because text is easy to understand for humans but for computers, it isn't,
there is no clear pattern in the text and therefore this is not really a great
way of exchanging data. 

Xml looks a lot like html and actually html is a special kind of xml you could
say, the difference is xml allows you to use any tags and this of course allows
you to transfer data and it's also not making any UI assumptions because it's
not parsable by the browser, the xml elements are totally made up by you. 

The good thing is it's easier to read by machines than plain text, you can also
of course define clear structures there but you will need a special xml parser
because traversing through an xml node tree is kind of challenging, not
impossible to solve but you need a special parser and all these elements of
course add some overhead to the data you transfer, so there's a lot of extra
text that is only required to read your data that is not really your core data
though. 

The last data format and you might already guess it, that will be our winner is
json. 

Looks like this and we already use that in the course when I had a look at
asynchronous requests couple of modules ago. 

And now this also is just the data, it makes no UI assumptions and it's also
machine readable. 

The good thing is it's a bit more concise than xml and it can easily be
converted to javascript and that is of course a huge plus when working with
nodejs on the server but also with well javascript in the browser which happens
to be our only programming language we can use there. 

So therefore this is our winner data format, json is our winner data format if
we just want to transfer data and it's the most common format in any API you are
communicating with these days. 

All the other formats are not as great for transmitting data as json is,
therefore this is what we will use but it's important for you to understand why
we use it and I hope this became clear. 

---