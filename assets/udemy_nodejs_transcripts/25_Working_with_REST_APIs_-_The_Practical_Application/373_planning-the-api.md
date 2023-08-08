## 373. Planning the API

<strong><em>no description</em></strong>

So let's analyze this react application to find out which rest API endpoints we
want to provide. 

Now you don't need to know react for that, no worries. 

The app.js file is essentially our entry file where our react application starts
or where it basically starts rendering the first screens and there we also have
some logic on which we'll have to work on later. 

For example for logging users in, we'll later have to insert a real url here
that allows us to do that and the same for signing up and so on. 

Now in the pages folder, you'll find a feed folder and there the feed.js file is
what's responsible for this page with the new post button and so on. 

There we also have a couple of routes, for example here where we fetch the
status of the currently logged in user but then also additional routes for
loading existing posts, here where I want to reach some url that serves up some
posts but also later down, hooks or methods where we can edit the user status,
where we can also add new posts or edit existing posts, we'll do this in the
finish edit handler and where we can delete posts, something we'll do in the
delete post handler. 

There you already see I have a couple of fetch methods set up but the url is
always missing and that is something we'll have to do of course, we'll have to
add our own url and make sure that this works or that we have the respective
endpoints for that. 

On the single post screen here, we load a single post if we click on it and
there indeed, we also want to reach out to the backend and fetch data for that
single post. 

So in short, which endpoints will we need and now I switch back to my rest API
which we started building in the last course module, you also find this snapshot
attached to this video. 

There I already got a route for getting all posts and for creating a new post,
that is great, we will also need routes for getting a single post, for editing a
single post, for deleting a single post and we'll also need routes for logging a
user in, signing users up, so creating new users, for viewing the status of a
user and for editing the status of a user. 

These are the routes we will need and with that, let's start working on that and
let's implement them step by step. 

We already got a route to get posts and to create a new post which does not
sound like the worst start, let's maybe continue with these so that we can start
implementing the appropriate code in our react application to get posts and to
create posts. 

---