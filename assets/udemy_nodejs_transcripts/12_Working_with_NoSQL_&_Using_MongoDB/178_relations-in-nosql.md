## 178. Relations in NoSQL

<strong><em>no description</em></strong>

So we know how we store data and I mentioned that this gives you more
flexibility, also regarding the storage of relations between different data. 

Now in NoSQL it would be pretty normal to have something like this, here are
three collections and we have some duplicate data in there, we have a users
collection which holds all the details about a user but then we might have some
copy of that data or of a part of that data in an embedded or nested document in
another document in another collection. 

So instead of just matching by ID as you do it in the SQL world, here you can
also depict a relation by embedding data into other documents. 

You could embedded the ID which points at another document so that you still
have to merge two documents manually and you will indeed have to do that pretty
manually but you can also just take the information that is important for you in
the context of another document. 

Let's say here, some user data for the orders and you copy that into the orders
and then you have that data right there whenever you fetch all orders without
you having to fetch all orders, then look for the fitting users and fetch them
too and this is part of what makes NoSQL and especially mongodb so fast and
efficient. 

It really is built to make sure that you query your data in the format you need
it, that you store the data in the format you need it, that you don't have to do
a lot of merging and so on but that you can really fetch data in the format you
need it without having to combine multiple collections behind the scenes on the
server. 

That being said, you can still do that, nested and embedded documents are one
alternative for depicting relations, references are another one. 

So here's the embedded document example where the address is part of our
customer document, so instead of having two collections, customers and addresses
and then matching by ID, here we put the address right into the customer. 

There also are cases where you would have a lot of data duplication and where
you need to work with that data a lot and hence it would change a lot and you
would have to manually update it in all duplicate places, where using embedded
documents is not ideal. 

So for example if you have some favorite books for every customer, well you
would have lots of data duplication because a lot of customers might have the
same favorite books and these books might then change a lot, maybe there is a
new edition published and you would have to go to all customers who have these
books as favorites and update the entries for each customer. 

In such a scenario it would be easier to still go with two collections and only
store the references to the books in a customers documents and then manually
merge that with the books which are managed in a different collection. 

And over time you'll get a feeling for which approach you want to follow, I'll
show you some examples in this course and have a look at this complete mongodb
course I did mention which drives much deeper into that and shows you way more
examples that can be helpful to you. 

So this is the idea here though, we can embed or we can use references, whatever
fits the purpose a bit better and with that, we know how mongodb generally
works, that we have the important thing of not having a schema hence we have
more flexibility, no structure is required and we have fewer data relations
because we can relate by embedding. 

We can still build relations manually with references as you saw but you should
always know if that is the best approach right now or if you can use an embedded
document with too much work. 

So these are NoSQL characteristics and therefore the mongodb characteristics and
these are also part of the reason why mongodb is so popular because of the speed
and the flexibility it gives you. 

---