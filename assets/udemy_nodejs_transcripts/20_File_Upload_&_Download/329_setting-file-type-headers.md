## 329. Setting File Type Headers

<strong><em>no description</em></strong>

We have our code for downloading a file and this file is now only available if
we are logged in. 

Now we can improve the way we return this however, we can pass some extra
information to the browser so that it uses a different file name and also with
the right extension. 

For this we'll set some headers, so we can use set header for that and first of
all we can set the content type to application/pdf because that is what it is
here, whoops, like this. 

Let's see what this does, if I save it like that and I now click this button,
now I open it in the browser. 

So this already changes the behavior, it already gives the browser some
information which allows the browser to handle this in a better way and for
pdfs, most browsers simply open them inline, so in the browser. 

So that's great but we can pass more information. 

We can also set another header and that is the contents-thisposition, this
allows us to define how this content should be served to the client. 

We can set this to inline to still tell the browser to open it inline for
example, so if I change it like this, nothing changes but we can also for
example add a file name here. 

So we can add semi-colon and then file name and set this equal to in double
quotation marks the file name you want to serve, so in my case it would be the
invoice name right. 

So we can also set file name equal to double quotation marks plus invoice name
plus closing double quotation mark contained between single quotation marks. 

If I now save this and I click this button, now we don't see a difference with
the file name when opening it inline because it's open in the browser anyways
but we can change inline to attachment for example. 

Now with that adjusted, if we click on invoice, the download menu opens again
and now here we have the proper file name with the proper extension and this is
how you can control how the browser should handle the incoming data. 

Should it automatically open it, should it instead let you download it? 

So I'll switch this back to inline but keep this file name here and now I have a
set up where only authenticated users can request this invoice. 

We can still improve that. 

---