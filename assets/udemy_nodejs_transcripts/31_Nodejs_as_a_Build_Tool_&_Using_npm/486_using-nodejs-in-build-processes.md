## 486. Using Node.js in Build Processes

<strong><em>no description</em></strong>

So we want to end up with optimized code and again this is mostly important for
frontend projects. 

Npm is useful because we can install packages, we can manage this project with
our package.json file and we can of course install packages that run in the
browser too. 

It's our duty as a developer to ensure that we don't try to install expressjs
into this project because we couldn't use any functionality from expressjs in
the browser but we know as a frontend developer which packages we can use and we
want to use, we find that out with research and so on and then we can install
these packages and we can import them in our files with a slightly different
syntax, that just happens to be primarily used frontend development import
export syntax with that es module style because that is actually the style that
is supported in modern browsers too and then this is done by npm. 

We install the packages and now we also want to start a script with npm. 

Now npm's work is over and nodejs takes over, the react scripts package here,
let's look into that. 

And for that we can look into our node modules folder, run npm install in case
you don't have that because that will install all dependencies that are listed
in your package.json file and now in node modules, let's search for that react
scripts package and you can see by the list that is very long, that all packages
have a lot of dependencies which in turn have dependencies which is why we end
up with a lot of packages being installed here. 

Now I'm in the react area though and there, I find react scripts. 

Now there we also have a package.json file because if you share a package you
also need that, you need to add some extra information to the package.json file
then and you can learn all about creating and sharing packages in the official
npm docs if you're interested and there you will also find like the entry point
that is executed which is in the bin folder, the react scripts js code here. 

This is in the end the code that will be executed and now here's something
important, this code well in the end be executed by nodejs because the idea
behind build workflows is of course that it runs on your computer before you
deploy your optimized code, so before you upload your optimized code to some
server. 

So this code will not run in the browser or anything like that, this code will
run on your local machine and therefore it will be executed by nodejs. 

This is also the case because in the end this code will kickstart, other scripts
will kickstart other code and it will kickstart code that will also work with
your local file system. 

For example in the scripts folder, we find the build.js file and there, we will
see what else it does and now this is actually a very complex build workflow, in
the end this uses a tool called webpack which is used heavily in frontend
development to orchestrate your build workflow and to compile your different
files and unlock next gen features and make sure that you can handle the
features correctly, again by using also some other tools like babel but that
would lead too far here. 

The idea is here we are using nodejs, we can also tell that we are by the fact
that we now have a different import export syntax and we are loading different
packages here, we're running them and some of these packages will in the end
also pick up our files, so our local source code we have written here in the
source folder. 

We'll parse them and we'll transform the content in there, pull all of them
together because we don't want to have multiple files in the end but only very
few files with one main file, we'll pull all that code together and then also
rewrite our code in a way that also runs in older browsers and this is all done
by a couple of packages which are used behind the scenes here, which are
installed by npm and then the code in that packages is executed through nodejs. 

And that was a lot of talking about that but I really want to get that into your
heads because it's so important that you understand that you can use nodejs to
execute any javascript code which uses nodejs features of course on your machine
and that it's therefore also used to run utility scripts and you could also
write your own utility script that like calculates your taxes but here, the
utility scripts actually take our source code and then transform it as defined
by the packages we use because we don't want to write all that build tooling
code on our own. 

And that is another important area where you can use nodejs and if you want to
dive into that area, actually a lot of the knowledge you learned in this course,
like for example when it comes to work with files will be useful but you will
also have to pick up new skills because you need to know all the ins and outs
about working with files, managing large chunks of data efficiently and so on. 

You don't need to create a web servers or anything like that, you don't need to
validate user input and that of course was the main topic of this course but
this is a different area of nodejs that you can also dive into if you are
interested and especially npm is something that is worth having a look at,
having a look at the commands you got there so that you throughly understand
what you can use npm for and if you want to learn how to distribute your own
packages for example, the getting started guide there also teaches you that, how
to publish and update packages and so on. 

So check these resources out if that's interesting to you, I found it important
to mention that this also exists and is important area where nodejs and npm are
being used. 

---