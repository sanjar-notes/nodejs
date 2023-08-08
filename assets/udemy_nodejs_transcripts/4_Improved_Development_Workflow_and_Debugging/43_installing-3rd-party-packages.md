## 43. Installing 3rd Party Packages

<strong><em>no description</em></strong>

So in the last lecture, we added a script to start our application and this is
nice to know that we have this scripting functionality. 

Now with such a package.json file available, so therefore with this being a
managed node project you could say, we can also do one other very important
thing, we can install third party packages because a typical node project looks
like that. 

You have your local project with your code obviously and you use a lot of core
node packages like the fs package or the http package we're already using but
often this does not suffice and in the next core section, we will install one
big third package actually because you typically have such dependencies third
party packages. 

So you want to use some functionalities some code which you didn't write on your
own but which is also not included into nodejs. 

Packages could help you with parsing incoming requests, validating user input,
anything of that kind. 

Now we will use express in the next lectures or in the next module to be
precise, body parser is another package we'll use throughout this course and
there are thousands of packages available that offer all kinds of utilities you
can add to your projects so that you don't have to reinvent the wheel. 

These packages are available through the npm repository, that is a cloud package
repository where all these packages live and you can conveniently install and
manage them via npm, remember that tool that shipped with node. 

And this is exactly what we will do now to install a first little utility
package that will speed up our development workflow. 

Because right now what we have to do is whenever we change our code, we have to
quit the development server with Control-C and restart it, right, so if we have
it running with npm start now, remember this is our new command to start the
server and I would change something here, like for example here I fixed that
/head right, whenever I do this I have to save this and for my change to have an
effect, I have to quit the server with Control-C and restart it. 

Now this is a bit cumbersome because we just want to be able to type and then
hit save and it should automatically restart and right, that would be a great
workflow during development and to achieve this, we have to install a third
party package that gives us just this functionality. 

Now how do we add such a third party package? 

We do that with the help of npm and there, we get the install command, so just
as we had run to run one of our scripts, install installs a third party package.


Now how do we install it? 

First of all we have to know the package name and if you're wondering well how
do I know the package name, well that comes with courses like this, experience
or by simply googling for certain problems which you want to have solved and all
of a sudden you find a thread where some package is mentioned. 

Now I can tell you for this auto-restart mechanism, there is a package called
nodemon, written like this. 

By the way you can always search for npm and then the package name if you know
that name and you will find an entry on npmjs.com. 

Now this is the package page basically where you find a description,
installation instructions, usage instructions, how to configure it because most
packages give you an easy way of using it and then always give you configuration
possibilities. 

You'll see how popular the package is, what's version it's using, if there is an
exernal little home page, where the source code can be found if it's open
source. 

So you find a bunch of stuff here, pretty useful, you also see how many versions
are existing and by default, you will always install the latest version by the
way but let's go back to installing it before we dive deeper into this whole npm
thing. 

So we want to install it and this command would install it but don't hit enter
yet, you can define how this should be installed because packages which you
install can be divided into development packages, so packages which mostly help
you during development and production dependencies, so packages that helps you
for the app as it's running on a server, for example nodemon would be a
development dependency because we only use it during the development process,
once we install our app on a real server we don't need it there. 

The real server which is running somewhere in the Internet of course shouldn't
restart and it also doesn't have to because we'll not change its code
dynamically. 

And you can basically tell npm which kind of dependency this is, this does not
make a huge difference and you can omit the setting but it helps you understand
which package is used for what. 

Now you do add this by adding --save-dev, if you had just save like this, this
would install it as a production dependency, so a package which we really use
and use in our code and work with and with this we're indicating that this only
adds something we used during development. 

There also is a third option by the way, -g, we'll not install it in this
project but globally on your machine so that you can use it anywhere. 

Now let's first of all install it with save dev, like this --save-dev. 

Now what this will do is it will download it from the npm repository and install
it into this project, so not globally on your machine but into this project. 

So now you see you get a report here that it finished successfully, what it did
and it gives you a couple of new things in your project. 

It gives you that node modules folder, the package log json file and it updated
the package.json file. 

There we see that the new dev dependency section was added and that stands for
development dependencies, as I said you can differentiate between different
dependencies, we'll see production dependencies later too and there you see that
nodemon was installed and which version was picked. 

Now regarding that character here, well this basically defines how this package
will be updated if you rerun just npm install, without defining an extra package
name because this command standalone will simply go through all your packages
mentioned in package.json and install them and it would automatically pick a
later version if available but more on npm and packages can also be found in a
separate module later in the course. 

So this is basically how we now install this and the question is where is it
installed? 

Well that is the node modules folder and actually that is a huge folder as you
can tell. 

The reason for this is that for one we got nodemon in there,  if we look for n,
we see it here. 

Now this is basically the source code of the package or the build version of the
package we installed and this package simply happens to have a couple of peer
dependencies, you can see them here and here. 

So we got a bunch of dependencies in there and these and their dependencies are
also installed, that is why you could end up with quite a big node modules
folder but you can always delete that node modules folder if you need to free up
space. 

Now you can't use that package but you can then rerun npm install if you start
working on that project again and it will re-install this package and all its
pure dependencies and therefore recreate the node modules folder, this is how
packages work in node projects. 

So you need that node modules folder while still using the packages but if
you're not working on the project, you can delete it if you want, if you need
the free space and then just remember to rerun npm install once you are working
on the project again. 

The package log json file by the way just stores the exact versions I installed
today so that if you share your project with others, they can actually get these
exact versions too instead of the latest versions but again, more on npm in a
separate module. 

---