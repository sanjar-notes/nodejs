## 324. Filtering Files by Mimetype

<strong><em>no description</em></strong>

Now we added our multer configuration to rename our file and to control the
storage place in detail, now we can also add a filter to multer to only allow
certain kinds of files and for that 2D object where we configure multer, I can
add the file filter function here. 

Now I'll again create in a separate const up there to make it easier to read,
file filter will simply be a function, I'll use an arrow function here where I
get the request, some file data and a callback which I have to call and in
there, we should call the callback with null as an error and true if we want to
accept that file so if it should be stored or false if we don't want to store
that file. 

Now how can we determine whether we want to store it? 

Well we can write any logic we want here, now I will check if the file mime type
is equal to an image/png or if the file mime type is equal to image/jpg or if
the file mime type is equal to image/jpeg with an e. 

If any of that is true, so if I have a file which is of that type, then I will
accept that so I will call the callback with true as a second value otherwise
I'll call the callback with false as a second value which means I'll not accept
that file. 

And now we can use that file filter and pass it as a value for file filter in
our options here and with that set up, we got some logic here that should filter
out invalid files. 

So if I go back now and I submit a form here with let's say my boat.png, I
succeed here, well I get an error here but I succeed because it stores the file
but if I try to submit a different value, let's say I'll pick a pdf here. 

You can use any pdf, any non-image file, then you see I only get undefined here
and that undefined is stemming from my admin controller from this line, so then
multer did not store anything and this is how we can filter out files. 

Now I will remove all these files up there and I'll also clean up my database
soon because right now we're not really storing the data appropriately and that
is the next step we should do of course. 

---