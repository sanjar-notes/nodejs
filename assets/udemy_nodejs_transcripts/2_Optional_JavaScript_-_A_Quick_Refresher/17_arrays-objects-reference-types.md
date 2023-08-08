## 17. Arrays, Objects & Reference Types

<strong><em>no description</em></strong>

Now. 

What did we learn about objects and arrays? 

There's one common misconception I sometimes see in the Q&amp;A section. 

Please check out that video I linked earlier in this article where I talk about
primitive and referenced types and JavaScript because that is a crucial concept.


Objects and arrays are so called reference types and you'll learn all about that
and what that is in the linked video. 

So I'm not going to re-explain it here. 

They are reference types and therefore when I store an array in a constant
hobbies, I can still edit disarray without violating the restriction that
constants must not change. 

Let me prove that to you. 

If I comment that out and I add a new line here and I use another method to push
method which allows me to add a new element to the existing array. 

So this will not return a new array. 

It will add it to the existing array. 

And here I will add programming. 

Now if I now console log hobbies after pushing. 

And I run note pledges. 

You see, that is the output. 

And we get no error about editing this constant. 

The reason for that is that reference types only store an address pointing at
the place in memory where that array is stored and that pointer. 

This address has not changed by us adding a new element. 

So the thing stored in this constant is just this pointer, just this address,
and this has not changed. 

Therefore our constant value has not changed. 

The thing it's pointing at has changed, but that totally does not matter here. 

And this is something you have to understand so that you don't wonder what's
going on. 

When we do edit in quotation marks a constant value. 

We're not really editing the thing that is stored in a constant. 

We're only editing the thing that constant thing is pointing at. 

---