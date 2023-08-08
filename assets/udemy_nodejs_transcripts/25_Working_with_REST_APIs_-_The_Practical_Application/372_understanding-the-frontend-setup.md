## 372. Understanding the Frontend Setup

<strong><em>no description</em></strong>

Attached to this video, you find a new project and this is now not a nodejs
project, instead this is now a reactjs project. 

Reactjs is a frontend javascript framework, it runs in the browser and it allows
you to create such a single page application which I mentioned in the last
course module. 

You can simply download the attached project, extract it into a new folder and
then navigate into that folder in a terminal or simply open that folder in an
IDE like visual studio code and then inside of that extracted project, run npm
install to install all the dependencies of that project. 

Now I mentioned that this is not a nodejs project, why do we need to run npm
install then? 

Because it's pretty common that we manage any dependencies in javascript
projects even for browser side projects with npm, with the node package manager.


The packages I'm installing here are only packages that are getting used in the
browser though, there are no node express or anything like that packages beneath
them. 

Indeed if you have a look at the package.json file, you'll only find react
related packages here which do run in the browser. 

So don't be confused by the fact that we're using npm, these packages here still
only run in the browser and we're just using npm to install these packages
because in modern front end development, you have very complex setups, you have
very complex package dependencies and using a package manager like npm can speed
that up. 

Now once you ran all of that, you can run npm start to start a development
server which is now actually a nodejs server serving your application but it's
not related to the node server we will build, it's not related to our backend,
this is only a dummy development server which simply serves the build version of
our frontend application, so it serves a simple html file which you can actually
see in the public folder, this one which does not have a lot of content which is
what I mentioned earlier or in the last module actually that single page
applications have very trivial html files but we have some hooks here which are
used by the react application which is built in the source folder, there is the
source code and that will be mounted onto these hooks here automatically in the
browser which leads to an application like this. 

You will see an error by default when you first start this up, we'll fix the
error throughout the module and there, you will see this interface and this
interface is now fully rendered through reactjs . 

If you inspect the source code, so if you view the page source, you will find
the html page I just showed you with these hooks and then a couple of script
imports at the bottom and if you inspect the dom though, you will see way more
html elements and these are all rendered dynamically by react, so by the browser
side javascript framework and if you want to learn more about react, I get a
whole course on that of course so check that out. 

We'll not write react code here, almost all the code we'll work with is already
prepared by me, we'll just have to tweak some things as we create our rest API
but this is the frontend we'll use together with our rest API and the idea of
course is that you get a feeling for how frontend and backend, so the react app
and the rest API are decoupled and can still work together now. 

So this is the project we'll work with, it's a very simple social network blog
messaging like application, we can have our users status which you can update
here, we can create new posts here, we can later also edit and delete posts and
we'll later also add authentication. 

Right now nothing is working because I got no backend attached, this is also the
reason why we have an error message right at the start but we will get rid of
that throughout this module of course. 

So this is the frontend and this is now the frontend I want to connect to my
backend. 

So let's now see which kind of restful API endpoints this frontend could need
before we then start implementing them step by step. 

---