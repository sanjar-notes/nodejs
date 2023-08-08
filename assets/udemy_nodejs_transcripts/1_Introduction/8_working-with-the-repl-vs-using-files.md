## 8. Working with the REPL vs Using Files

<strong><em><p>When writing Node code, you got two main options:&nbsp;Files which you execute or the REPL. This lecture explains + explores both alternatives.</p></em></strong>

Now before we finally dive into the javascript refresher or optionally in case
you skip that, into the nodejs basics, let me dive into two different ways of
executing your node code. 

One way of executing it which I briefly mentioned earlier in this module is the
repl. 

Repl stands for read, reading user input, eval, evaluating user input, print,
outputting a result and l, loop for returning and waiting for new input and the
repl is what you use if you just type node into your terminal. 

Here I am in the terminal or on Windows this would be your command prompt and
there if you just type node with node installed, you are now in the repl which
you can identify by the fact that you now don't have that full path of your
computer name at the beginning but just that greater than sign and there you can
execute node commands like console log, two plus two or also writing,
interacting with files. 

You can import the file system there just as we did it previously in our file
and then we can use that to write a file synchronously and so on, so that will
all work here and this is of course an environment where we don't store our code
in files but we write our node application with every line. 

The lines don't work independent from each other, so I can now use the file
system package for example now that I imported it one line earlier but once I
quit out of this process with control c, I'm done. 

This is not saved anywhere, this is not a file I can execute again and this
therefore is a great playground. 

The alternative to running codes is that you execute files as we did it before
and as we will basically do it for the rest of the course, this is the
alternative to using the repl. 

When you execute files, the advantage of course is and that is why we use it for
real apps, that we write our code in advance and we can always execute it and
when we build a real app, we want to save our code of course in files which we
can then deploy in the end which we could share with other developers and where
we can also pause our work and pick up later and where we never lose the code we
write. 

But the repl is a great playground because we can use that to run some commands,
to try out certain things because we execute code as we write it and therefore
these are the two ways of running your node code, obviously we'll go with the
store code in files approach in this course but whenever I say repl, I'm
referring to this direct input way which I can recommend for trying out some
features but not for writing real applications, that is not what you would do. 

I just wanted to get these two ways out of the way, we'll focus on the left one
here and with that, let's dive into writing some code with the next modules. 

---