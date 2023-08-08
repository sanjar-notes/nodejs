## 256. Adding a Tiny Code Improvement

<strong><em>no description</em></strong>

One quick word about my current set up here by the way, since I return my
redirect to signup here and we do this in a then block, this will actually
redirect, this is correct but it will still execute the next then block, this is
how promises work. 

So this code execution in this function does finish because I return but the
overall code execution does not and therefore we reached the next then block
even if we redirect and that is why we get this password is required error when
we use an existing email because we reached this then block and the function in
there but hashed password will be undefined here because since we return after
redirecting, we never execute the hash function so we reach this function
without the hashed password and this is why we get this error. 

So the result is the same but if you want to avoid this, what you can do is you
can take that code and actually chain it in here, so I have a nested promise
instead of one promise chain with multiple then blocks, we will end after this
then block if we redirect, there only is the catch block here for catching
errors of which we don't have one and then the server then blocks here are only
executed if we make it into the hashing mode. 

That is a tiny improvement that logically makes more sense here. 

---