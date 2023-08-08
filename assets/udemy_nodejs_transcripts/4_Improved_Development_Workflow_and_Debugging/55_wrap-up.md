## 55. Wrap Up

<strong><em>no description</em></strong>

Now in this module, we had a look at how we can have an easier time developing
or building nodejs applications I guess. 

And for this, we started with npm, the node package manager which allows us to
manage our project and mostly its dependencies but also which added this
package.json and gave us the opportunity of adding scripts there. 

So with npm init, you can initialize a new project, you basically add a
package.json with that command and then you saw that you can use scripts to
define shortcuts to commands you run all the time anyways. 

We also use npm to install third party packages though because node projects
typically don't just use the core modules for your own code but often you want
to pull in third party packages. 

Utility packages like nodemon as we did it here but also as you will see in the
next section, real big packages that we use in our production code, expressjs is
what we'll install there. 

You can install different kinds of dependencies which doesn't really make a
difference, you could use them all even without specifying any of these options
but it helps you keep track of which dependency you are using for what. 

--save and --save-dev allow you to differentiate between production and
development dependencies and global dependencies with -g can be run from within
the terminal without getting a command not found error. 

Speaking of errors, well in your code you often have errors, that is absolutely
normal and there are different types of errors you can have a look at. 

Syntax, runtime and logical errors are three categories of errors I identified. 

Syntax and runtime errors at least throw a hopefully helpful error message and
you should read these messages and look at the line numbers they give you
because that often helps you find out what went wrong and how to fix this. 

Logical errors often are more difficult to fix but you can fix them often with a
lot of testing and possibly the help of the debugger which you learned how to
use with the help of Visual Studio code in this section. 

Speaking of debugging, debugging can be a helpful process because you can use vs
code or debuggers of other IDEs that can be used with node to look into your
code whilst it's running and step through it step by step. 

You can analyze the variable values at runtime and you cannot just look into
them but you can also manipulate them as you learned, you do all that by setting
breakpoints so that you define when your code execution should stop and give you
an opportunity to look into the code. 

You can find more than one breakpoint at a time and you should manage them
cleverly, keep in mind how node code executes, that it's not line after line but
that it works with callbacks and is event driven and therefore if you want to
look into a callback, you have to add the breakpoint there and not right before
it. 

With all that, you hopefully get useful tools that help you build your nodejs
applications. 

---