## 404. Wrap Up

<strong><em>no description</em></strong>

So we are using async await everywhere now and there's one important thing I
want to highlight here. 

For all these mongoose operations which is the primary thing where we use async
await, you have to understand that mongoose actually with operations like count
documents or find does not return a real promise but a promise-like object where
you can use then and catch and also async await, that is supported by mongoose
even though behind the scenes it's not a real promise. 

Doesn't matter too much for you to be honest because you use async and await in
exactly the same way you would use it on a real promise but I also don't want to
hide that fact from you. 

You could use a real promise by chaining exec after all these mongoose
operations, so after find, after count documents. 

If you do that, then you get back a real promise, we don't really need that here
because, well that promise-like object behaves in exactly the way we want. 

You do have a real promise with the bcrypt library though, when we hash our
password, here we get a real promise and as you can see, well you see nothing,
you see no difference in the way we use await and you also had no difference you
previously used then and catch. 

So that is what I mean, you don't need to care too much about that, I still did
want to mention it. 

More importantly, I want you to take away that async await is a nice alternative
to using then and catch. 

It's not better, it's not faster, behind the scenes it's basically the same
code. 

It can be more readable to you but you must never forget that these still are
asynchronous steps, the javascript code execution behavior doesn't change
because of that. 

It does not block execution,  it simply wraps all the code after an await
statement in the then block you would have to write otherwise, so this runs
inside of the implicit then block this statement creates, this is how you have
to think about that. 

So never forget that these are asynchronous operations because that is really
important to understand. 

And you can absolutely go with the then and catch block we used before, so with
the old promise style if you prefer that, I like it for teaching because it's
clearer that we have some operation to wait for and that the line after that
would execute first, here this is less clear but if you are aware of how async
code works, this can simply be a nicer syntax to look at and it's up to you
which syntax you'll use. 

For the rest of the course, I'll write new promises or I'll stick to that async
and await syntax for my node application, for the react application I'll leave
the code as it is with then and catch. 

You could use async and await there too but again this is no react course so I
will leave it there as it is, for node we'll go with async await. 

---