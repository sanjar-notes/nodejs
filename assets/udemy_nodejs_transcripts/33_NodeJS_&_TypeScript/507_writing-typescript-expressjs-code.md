## 507. Writing TypeScript Express.js Code

<strong><em>no description</em></strong>

<v Instructor>With the basics out of the way,</v> let's turn this into a very
basic REST API. 

For that, I'll actually add a routes folder again, and in there have my basic
routes and now let's say we're building a very simple to do app REST API. 

Certainly not the most exciting thing we can build, but a great practice for
Node Express and TypeScript. 

So here I have my todos.ts file, and in there I now import, express from
'express', to then create that router here by calling express router right? 

That's what you'll learn throughout this course. 

Well, actually now with this new import syntax, we can actually also change it
slightly and import router like that, between curly braces from 'express' and
then just call it like this. 

So instead of importing the entire express object and then extracting what we
want, this is a import syntax which automatically only imports what we need. 

So again, a little advantage we gain by using TypeScript, because this arguably
is shorter than what we had to write before. 

Now when we wanna export something we also now don't have to do module exports
equal router, but instead we can just export default router. 

And this will export router as the default export in this file. 

The default export then simply is what we can import an app.ts with todosRoutes
from './routes/todos'; This import syntax will always pick the default export of
a file and you can name it here however you want, this doesn't have to be the
name you used for exporting, it can be a different name, as you see here. 

We can then of course, as before, use our todosRoutes as middleware with the use
method. 

And now back in the route's file we can register the routes we need. 

So here we can add a get route. 

Let's say with the pop slash, that should just fetch all todos. 

So we got the request, the response and this next function and we can work with
that here. 

And now what's really nice, is that again we get auto completion on all those
things. 

TypeScript knows the types of this request parameters, of the response parameter
and of the next parameter. 

It knows which kind of data we get there, and hence it's able to support us and
therefore the IDE is able to support us when we work with those values. 

So for example here for getting data, we might wanna return our todos. 

So let's say we're managing the todos here, simply in such a constant and
therefore only in memory, because it's just a dummy example here. 

Then we could simply call response, status 200, json and there simply return our
todos on a todos property in that object which we're sending back. 

Now here we're now getting a complaint by TypeScript in the IDE, and we would
also get this if we tried to compile this code. 

And that is that. 

The variable todos is implicitly of type any array and its true, we're not
specifying which kind of data will end up in this array eventually. 

And that's something we wanna do. 

As I explained in the previous lectures as well because this allows us to write
cleaner code where we avoid mistakes by passing an incomplete data for example. 

We can avoid such mistakes by making it very clear which kind of data we want
here. 

So lets implement this and continue with the entire REST API in the next
lectures. 

---