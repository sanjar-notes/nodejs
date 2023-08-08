## 368. Wrap Up

<strong><em>no description</em></strong>

That's it for the basics of rest APIs, we'll dive much deeper into rest APIs and
build a real project with the rest API in the next module. 

The core concept and ideas are that rest APIs are all about data, no user
interface logic is exchanged. 

Rest APIs are normal node servers though and that is really important to keep in
mind, we're not building a totally different kind of app all of a sudden, just
the data format and the way we send responses changes because now we simply
expose a couple of endpoints which is a combination of http methods and paths
but we did this before too, we just have more http methods available now and we
exchange data in the json format for both requests and responses, we don't
return html pages as the response anymore. 

Rest APIs are decoupled from the clients therefore, they are totally decoupled,
they don't share any connection history or store any connection history. 

Now when we have a look at the requests and responses, it is important to
understand that you should attach data for requests and responses in the json
format and that you should let the other end know by setting the content type
header. 

Expressjs does this automatically when using the json method, in the browser it
depends on which method you use, when using the fetch API as we did, we had to
set it manually, when you would use axios another common library in browser side
javascript for sending async requests, it would be done automatically. 

Cors errors are also something we had to look at, they occur when the API and
your client are sitting on different servers, different domains and they want to
exchange data. 

You fix them in quotation marks because they are a security mechanism but you
can bypass that on purpose by setting the right cors headers which basically
tell the client hey it's fine, I'm a public API, you may use my data. 

These are the basics. 

Now let's dive much deeper into that, use different http methods, add
authentication and so on by working on a real project. 

---