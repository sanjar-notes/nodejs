## 483. Using npm

<strong><em>no description</em></strong>

Let's first of all understand npm a bit better, it's node's package manager as
you learned and in the end it's a cli, a command line interface. 

We always used it from the command line from the terminal by running npm and
then some command, mostly npm install in this course. 

The idea behind packages or tools like npm and every programming language has a
similar concept you could say is that we might have some isolated functionality,
some code that we wrote or that we came up with that does something useful,
let's say it generates a random number. 

Now we can use that in our web application but maybe we want to use it in other
applications as well because this isolated functionality does not depend on our
business logic in the project we're creating or maybe we want to share it with
the public. 

Well if we want to share it internally or externally, we can put it into a
package with the help of npm. 

You can use npm not just to install packages but also to create and share
packages through that npm repository which is a cloud service where you don't
have to pay for where you can host packages you created and this is also a
service where you will in the end fetch packages from with the npm install
command. 

So in this repository which is managed globally, you'll find thousands of
packages obviously and if you now have some node project, you can use any of
that, you can use any of those packages with the npm install command through
that cli and that is how you add packages to your project, no matter if that is
a package shared by you and you can also have private repositories or private
packages on npm by the way, that is something you do have to pay for but you can
always use public packages and share packages with the public. 

That's the idea behind npm, now let's have a closer look at the official npm
repository page and the available commands we can use. 

You can visit npmjs.com, that is the official page of npm and there you can
search for packages, for example we could search for express here which is of
course a package we used, the express framework and then you see all kinds of
packages that kind of were found for that, maybe packages that use express,
maybe also of course the express package itself. 

And if you click on that, you find some quick docs, you see the versions that
were released here so here you can see the different versions you could install
through npm, you can target a specific version by the way by going to your
terminal and there with npm install, you can choose the package and then an @
sign and then a specific version number, for example we could choose 4.16.3 by
typing for 4.16.3 and now we would install that version into our project. 

If we select no version, the latest one is picked by default, that's just a
little side note. 

So we can see that version history, we can see which other packages this package
relies on and these packages will be installed for you automatically when you
install expressjs . 

So these will also end up in node modules as will the dependencies of these
packages and that is why you quickly end up with a big node modules folder by
the way because you have a lot of dependencies of dependencies of dependencies. 

You also see other things like the official home page, the github repository, so
the repository where you can find the source code for this package and so on. 

So this is really useful, now if you want to learn more about the npm command
though, so what else you can run besides install or how you can configure
install for example with --save versus --save dev to install a production or a
development dependency, if you want to learn more about that, the official docs
are of course the right place. 

There if you dive in, you can learn way more about npm and diving deeply into
that would really be beyond the scope of this course because npm creating and
managing packages, that is a topic on its own not closely related to nodejs the
language, just an additional feature you get for free, so here you can learn way
more about that and here on this page if you scroll down a bit further, you'll
also see all available commands you could run and then if you click on one of
them, for example uninstall, you also see how you may use it. 

So here you see detailed instructions on how you may configure it, for example
that you can run it in global mode to install a package on your system and not
just in a project or that you can of course also install it with the --save flag
save dev or save prod which is the same as just --save in the end, so there you
see all the ways of configuring that or running that command in different ways
and if you want to learn way more about that and for most cases, you just need
npm install --save or --save dev or -g but if you want to learn way more, of
course these official docs are the place to go. 

It is worth pointing out that you also can get help here locally, when you type
npm help here, you also get instructions on the available commands you may run
and you can also get help on a specific command. 

So if I run npm install --help here or just -h, then I see how I may run this
command and also which options I have to add additional flags. 

However these are just the common options, not all options, for the full docs of
course, you should dive into the official documentation here. 

The commands you can run here especially installing are one powerful thing npm
allows you to do, you can add any package you want to your project. 

Another important feature is that if you click on using npm here, you can run
scripts with npm and that generally is related to that package.json file you get
when you put a project under control of npm which you do with help of the npm
init command, we also use that in that course. 

That will ask you a couple of questions and then give you a package.json file
which you can use to configure a project and there you can not only keep a list
of your dependencies, you can also add certain scripts and you can run these
scripts either with npm start to run the start script or npm run and then any
script name you configured in there and that is very powerful especially when it
comes to using npm and nodejs to build projects. 

It is something I can best show in the react application we worked with in this
course. 

Here I am in that application and there if we had a look at that package.json
file, you see that scripts area and there you see a couple of scripts which you
can run, for example start with npm start but that's a special case, all other
scripts with npm run and then for example, build or eject and then these scripts
are executed. 

Now these scripts actually use a third party package, so a dependency which was
installed, react scripts we see it here in the dependencies list and then that
dependency holds the code that will actually do something and that is the next
step I will come back to with nodejs being able to run on your machine and not
being limited to spinning up a web server. 

---