## 345. Wrap Up

<strong><em>no description</em></strong>

So now we added pagination to our application and of course you can now tweak
this adjusted to your needs, change the items per page you want to display for
example, if you switch that to two and you reload, you won't find items on page
4 but you will find items on page 1 and now you got all that logic in place that
should allow you to display the data you want to display and to not fetch all
the data in one go. 

And it's important for you to understand that since find uses a cursor, it does
only retrieve the items you need. 

Count documents does not retrieve all, it only counts them which is faster than
retrieving them and skip and limit also manage or are managed by mongodb in a
way that you only transfer the items over the wire which you really need, so
this is not doing some server side filtering of the data, it really filters it
on the database server already. 

So this is how you can add pagination to your node express application. 

---