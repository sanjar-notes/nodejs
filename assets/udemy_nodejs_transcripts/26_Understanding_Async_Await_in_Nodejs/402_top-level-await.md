## 402. Top-level "await"

<strong><em>no description</em></strong>

Now, Max, from the future here in the last lecture we added async await and I
explained all about it. 

Now what I explained here is all correct. 

But there is one important addition I want to make here. 

Starting with version 14.3, which when I recorded this video was just released,
starting with that version of Node.js. 

You can actually use the a wait keyword also outside of asynchronous function. 

This is a feature called Top Level Await. 

You would be able to await a promise which you have here in the top level of
your script. 

So which is not inside of a function you can now also use await here. 

Previously this was not really possible. 

You always needed a async function around await. 

Now you can use a weight on the top level if you are using it instead of a
function. 

As we are doing it here though, you still should add async, so that hasn't
changed. 

It's just this extra addition that you could now also use await on the top
level. 

And I just found this important to mention because it is part of Node.js and it
is related to a single weight or to just a weight then I guess. 

---