## 445. Fixing a Pagination Bug

<strong><em>no description</em></strong>

Now there's one thing you also might have noticed. 

When we only have two posts, so we have no pagination because we don't have
enough posts to have a second page and I add a new value like a duck here, then
this duck will show up but we don't get that next button. 

There is a little bug here which is easy to fix, has nothing to with nodejs but
it is really easy to get rid of. 

In our finish edit handler here, when we go down to the code where we create
that new post and we then add it to our existing posts, it's this else block
here which is interesting to us where we in the end make sure that we only
render two items at a time and that we add our new post at the beginning of the
list. 

Now here what I need to do is I need to make sure that I do increase the amount
of total posts. 

In our state in react here where we manage how many posts we have on that page,
I do set total posts here to a different amount of posts when I fetch all posts
where I get that total posts information. 

Well when adding a new element, I know that total posts will simply be the old
total posts plus one. 

So I will add a new variable here, right below updated posts and that's updated
total posts and that will be previous state total posts and that is a bit of
react logic here but this first of all takes the old status and now when I do go
into that else block which is the case when I am not editing but when I am
adding, then I want to set updated total posts plus one, with the plus plus
syntax I increment that by 1 and then here in the return statement I'll set the
total posts equal to updated total posts. 

And with this change in place, if I now quickly delete my duck again so that I'm
back to two items and I do add my duck so that I go up to three items again, now
you see that next button and you can use it of course because now we're managing
the total post correctly too. 

So that's just a little adjustment, has nothing to do with node or graphql but
since I spotted that bug, I of course also want to get rid of it. 

And with that we moved our entire rest API over to graphql and I hope you see
the power graphql gives you by being more flexible regarding the data you fetch
from the backend and therefore your frontend development can move faster because
your backend gives you the entire bandwidth of data you might be interested in. 

---