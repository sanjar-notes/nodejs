## 331. Streaming Data vs Preloading Data

<strong><em>no description</em></strong>

So we added authorization to our download option here. 

Now that's not all we can improve, we can also improve the way we are serving
that file because right now, I'm simply reading that file and once I read it, I
return it. 

Now for small files this is probably fine but you should be aware of one
important fact, if you read a file like this, node will first of all access that
file, read the entire content into memory and then return it with the response. 

This means that for bigger files, this will take very long before a response is
sent and your memory on the server might actually overflow at some point for
many incoming requests because it has to read all the data into memory which of
course is limited. 

So reading file data into memory to serve it as a response is not really a good
practice, for tiny files it might be ok but for bigger files, it certainly is
not, instead you should be streaming your response data and that is what I will
do now. 

So I'll comment out this code where I read my file and instead here, I will now
start streaming it. 

For that I'll create a new constant, I'll name it file and I will use the file
system and create a read stream because I want to read some data in. 

Now I want to read in data at a specific path and the path hasn't changed, it's
the invoice path, so now I have to read read stream and node will be able to use
that to read in the file step by step in different chunks. 

I will then take my response code here where I set the headers, I still do that
on the response object and then here, I will use that file read stream and call
the pipe method to forward the data that is read in with that stream to my
response because the response object is a writable stream actually and you can
use readable streams to pipe their output into a writable stream, not every
object is a writable stream but the response happens to be one. 

So we can pipe our readable stream, the file stream into the response and that
means that the response will be streamed to the browser and will contain the
data and the data will basically be downloaded by the browser step by step and
for large files, this is a huge advantage because node never has to pre-load all
the data into memory but just streams it to the client on the fly and the most
it has to store is one chunk of data. 

Again we're back to the streams and the buffers, the chunks are what we work
with, the buffers basically gives us access to these chunks and here we don't
wait for all the chunks to come together and concatenate them into one object,
instead we forward them to the browser which then is also able to concatenate
the incoming data pieces into the final file. 

So with this setup here, let's try this again, click on orders, click on the
invoice and again we see the invoice as before but now this is actually streamed
data created with that create read stream thing which is the recommended way of
getting your file data especially for bigger files. 

---