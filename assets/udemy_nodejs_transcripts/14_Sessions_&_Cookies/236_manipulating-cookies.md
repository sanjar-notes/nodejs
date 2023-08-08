## 236. Manipulating Cookies

<strong><em>no description</em></strong>

So in the last lecture I showed you how you can set a cookie and some a bit too
complex way of extracting that cookie. 

Now if you want to extract cookies by the way, there also are third party
packages which can help you with that but our approach has another flaw. 

Well obviously since I can access my cookies that easily in the developer tools,
I can easily change them, I can go here and manipulate the value, for example if
I set it to false and I reload, I'm actually still logged in because false is
sent as text and text is always treated as true but we can simply add a
comparison here and see if that value is equal to true, so to the text true here
and now if I reload here, I'm not logged in anymore. 

If I change it back to true though and I do reload, I am. 

So the issue here is we can manipulate that from inside the browser and
obviously you don't want to allow the users of your website to login by simply
manipulating some cookie value. 

So whilst it is certainly interesting to store some data in the client side,
especially things that are related to tracking users, advertisements tracking
and so on, whilst this is interesting, sensitive data should not be stored in
the browser because users can edit them as you see, we can edit our logged in
cookie. 

So whilst cookies are generally a good thing for storing data across requests,
it might not be the best approach in all scenarios and that is exactly something
where sessions can help us with. 

However before we dive into sessions, let me quickly explain you some other
fields you can configure about a cookie which will also highlight when a cookie
does make sense to be used before we then dive into the scenario where it's not
the best tool. 

---