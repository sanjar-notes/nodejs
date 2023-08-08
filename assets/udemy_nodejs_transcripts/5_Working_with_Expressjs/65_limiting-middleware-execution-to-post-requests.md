## 65. Limiting Middleware Execution to POST Requests

<strong><em>no description</em></strong>

We're able to parse incoming request bodies with the help of the body parser
package which is pretty neat but right now as I mentioned, this middleware
always executes, not just for post requests but also for get requests, what can
we do regarding that? 

Well instead of app use, we can also use app get. 

This is basically app use, it has the same syntax as app use, we can use a path
or don't use a path but it only will fire for incoming get requests, so this is
another form of filtering besides filtering for the path, app get allows us to
filter for get requests and on the same page, we also got app post to filter for
incoming post requests and just by changing this word, this middleware will now
only trigger for incoming post requests with this path and not for get requests.


So if I save this and I go to /product, you see I get hello from express, so I
don't end up here even though I entered /product but it was a get request but if
I send a post request through that form I have on add product, if I do this
here, book too, you see we get this output, so we clearly made it into this
middleware due to our filtering. 

So this is another way of using that middleware function, instead of use which
will work with all http methods, we can also use get or post to filter for
these. 

And additionally you also have delete, patch and put which are other http works
which we'll use later in the course because we can't really use them from a
normal html document. 

---