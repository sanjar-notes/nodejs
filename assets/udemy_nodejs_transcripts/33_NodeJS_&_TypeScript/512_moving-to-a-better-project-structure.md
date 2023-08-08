## 512. Moving to a Better Project Structure

<strong><em>no description</em></strong>

<v Instructor>With that, we're finished with the code.</v> But I'm not 100%
happy about the folder structure. 

For one, I only have a routes folder, I don't have a controllers folder, for
example. 

Now, obviously, you can split it up. 

You can add a controllers folder, and put those controller functions here into
that folder, just as we did it in other parts of the course. 

I just kept it all in one file here because it's really just a basic dummy API
with very little code. 

So, I think using one file is fine, but you can absolutely use a controllers
folder with a controller file. 

The more important thing, or the more annoying thing for me here is that we
always have these JavaScript files next to the TypeScript files. 

And the problem with that is that our actual source code in which we as
developer work is just the TypeScript code. 

So therefore, we have the extra files next to our source code and we shouldn't
work in those extra JavaScript files. 

You shouldn't change that code. 

You should only work in the TypeScript files. 

And therefore, I wanna ensure that the compiled files end up in a different
place. 

And to achieve this, we can go to the tsconfig.json file and there, we have the
outDir configuration, which I'll now comment in here. 

This allows you to set a directory where the generated JavaScript files will be
stored in. 

And here, I will specify /dist as a directory. 

This will create a new dist sub-folder, and all of our compiled files will end
up in that folder. 

With that change made, if I now run tsc, you see that we get this dist folder,
and in dir, we got the same folder structure as outside of it, but now in dir,
we only got our JavaScript files. 

And if I now delete the other JavaScript files outside of the dist folder to
only have my TypeScript source code there, if I rerun tsc, you see they're not
appearing again. 

They're really only in the dist folder. 

So, that's great. 

Now, the dist folder holds our finished Node app, which we can run with the Node
executable. 

And our source code is outside of that. 

Maybe you also want a separate source folder in which you store your source code
though, to have a clear separation of input and output. 

And that's something I'll do here. 

For that I'll add a source, a src folder and move my models folder, my routes
folder, and the app.ts file into that source folder here, just like that. 

I'll keep the rest of the project structure as it is. 

And now in tsconfig.json, we can set up our rootDir which specifies the root
directory of input files. 

And I wanna set that to /src to make it clear that that's the folder that
contains our TypeScript code. 

And then the outDir is the folder where the compiled code should end up in. 

So, now if I run tsc, that still works, and it's now taking the source code from
inside the source folder to generate the dist folder. 

And if I delete dist, that folder is of course regenerated, which proves that
everything works. 

Now important, we're always executing the code into dist folder because Node.js
is not capable of running TypeScript code like this. 

We only work in the source folder though, and then we compile it to JavaScript
to have our executable code. 

---