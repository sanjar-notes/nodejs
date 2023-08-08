## 45. Using Nodemon for Autorestarts

<strong><em>no description</em></strong>

So for now we got that nodemon package installed and it will just work because
it automatically installed all the dependencies this package needs in turn. 

So how can we now use it? 

Nodemon is a utility tool and it allows us to run our application, our node
application through this package here which will run node apps.js in the end but
which will also watch our files for changes and restart the process for us if we
do change something. 

So we can simply change start here, so the node app.js command to nodemon app.js
and this will look for a nodemon tool which it will find in this project because
we installed it here. 

As a side note if you were to run nodemon app.js down there, you would get an
error that this command is not found because it's only installed in this project
and not globally on your machine but the terminal will try to find this
globally. 

Here it will work because this will look globally. 

So if you now run npm start, this will simply start the node server and output
some extra information and if you now go to your routes.js file and edit
something, let's just add an extra line and you save that file, you see it's
restarting. 

And this of course is very convenient because now, we dont have to spend time on
manually exiting and restarting, now is this done for us. 

---