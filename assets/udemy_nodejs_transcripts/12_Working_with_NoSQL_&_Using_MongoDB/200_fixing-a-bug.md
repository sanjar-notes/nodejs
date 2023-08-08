## 200. Fixing a Bug

<strong><em>no description</em></strong>

So everything works but when clicking add to cart, it would be nice if we don't
get stuck here, so something seems to be wrong. 

If we have a look at post cart, well the thing is we never send a response here,
 we do add our product to a cart but that's it. 

Now in the old code, we redirected to /cart and that is what we should do here
too, so instead of returning this result which doesn't matter, no one's
interested here, I just want to call res redirect here or not here but here and
then I guess we can return this to see the result of that operation here if we
wanted to but the important part is that we redirect at some point. 

With that, now if I click add to cart here, I'm redirected to the cart page,
awesome. 

Now let's make sure we can delete cart items. 

As always feel free to try this on your own, in the next lecture and thereafter,
we'll do this together. 

---