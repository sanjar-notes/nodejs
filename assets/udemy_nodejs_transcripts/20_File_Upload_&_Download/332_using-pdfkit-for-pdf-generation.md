## 332. Using PDFKit for .pdf Generation

<strong><em>no description</em></strong>

Now that we learned how to save files and how to return them in different ways
statically as one big file or as a streamed response, let me show you a little
bonus so to say where we can create a pdf on the fly on the server, instead of
serving that hardcoded pdf here, let me create it on the fly instead. 

So I will delete my invoice here and instead when we get the invoice for an
order, I don't want to serve a file that already exists but I want to generate
that file based on the real order data. 

For that I first of all will still check if we have that order and if the user
is allowed to access it but of course this will now change, well actually the
name will be the same and I will store it in the same way but I now can't read
the file, I need to create it and how can we create a pdf? 

Well there are third party packages which we can use which make it a lot easier
and pdfkit is a very prominent or popular package for creating pdfs on a nodejs
server. 

I strongly recommend checking out their documentation to learn more about all
its many options because it's super powerful, it can do a lot of stuff, so
definitely worth having a look at this and we will use it to create a very
simple pdf in this course here. 

Now for documentation, it's important to know that this documentation uses
coffee script which is like a superset to javascript, it's not supported by
node, it's just a tooling for writing your code, it's compiled back to a normal
javascript and therefore this documentation can be a bit hard to read. 

In the end you could say something like this new pdf document, here we would
have curly braces after it, require would be using curly braces so some stuff
here looks a bit different but I will show you how to use it in this module, in
this lecture actually. 

Let's start by installing it, so I will simply run npm install --save pdfkit,
that's the name of the package, you'll also find these instructions on the
official page, npm install pdfkit and then we can start using it once it's
installed. 

So let me start that server again and up there in my shop.js controller file,
I'll import pdfkit by requiring pdfkit, so this package we just installed. 

Actually pdfkit exposes a pdf document constructor, so let's maybe name it like
this, so pdf document, the name is up to you but this is closer to what this
package really exposes. 

Now I want to create a new pdf document when we get an invoice at this point
here. 

So let's create a new pdf doc, whatever you want to name it by calling new pdf
document and that's what I meant, you need to add normal parentheses as we
always did for all constructors. 

So now we have a new pdf document. 

This actually also turns out to be a readable stream, therefore what we can do
here is we can use the pdf document and we can do two things. 

First of all we pipe this output into a writable file stream, so create write
stream is a function we can call on the file system package and to that we pass
a path where we want to write it to, the invoice path in my case and this
ensures that the pdf we generate here also gets stored on the server and not
just serve to the client. 

So we create that and of course I also want to return it to the client, so I
also pipe the output into my response, just as before, the response is a
writable read stream, pdf doc is a readable one so we can do that. 

Now we have this set up and now whatever we add to the document will be
forwarded into this file which gets generated on the fly and into our response. 

Now let's start simple and let's now use pdf doc and let's call the text method
which exists there, this allows us to add a single line of text into the pdf
document. 

So here let's add hello world maybe and then you have to call pdf doc to tell
node when you're done writing to that stream because you have to be done at some
point, right. 

So here you simply call end and when you call end, these writable streams for
creating the file and for sending the response will be closed so to say or will
know that you are done writing and therefore the file will be saved and the
response will be sent. 

And now with that saved, just make sure you also change your setup down there at
the bottom. 

I will keep the headers but I will not pipe any file because we now, well pipe
the file up there when we create it and I just need to make sure that I set my
response headers accordingly. 

Now with that if you save that and you click on that invoice link, you should
get a pdf with hello world in there and this pdf also can be found here. 

Now it might look a bit strange here but you can open it with a normal pdf
reader and it should look like a pdf. 

So this is how you can create a pdf on the fly, now in the next lecture let's
actually populate it with some order data. 

---