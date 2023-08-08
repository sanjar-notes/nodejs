## 534. App Setup

<strong><em>no description</em></strong>

<v Instructor>Now, for that attached,</v> you find the application we built in
the last course section. 

However, with one difference. 

There is a new frontend-app folder in there, and, in there, you find a basic
React application which will be ready to talk to our Deno server. 

Now, I'm not writing this application from scratch with you because this course
is not about React. 

It's about node in the end, and now also about Deno, I guess. 

Therefore, you get this finished application, and in order to start and use it,
make sure that you open up a terminal, navigate it into this extracted folder
which you find attached, and then cd into the frontend-app folder. 

So, with this cd command, move into that frontend-app folder. 

And, in there, first of all, run npm install to install all the dependencies of
this provided project. 

This will then generate this node_modules folder in the frontend-app folder. 

Thereafter, run npm start, and this will now spin up a simple development server
for this front-end application, and that's important. 

This will now not start our Deno server, it will start a standalone
development-only server for this front-end application. 

It's essentially the same pattern we used in the REST API and GraphQL modules of
this course, if you remember that. 

Now, this should automatically open up a new tab on localhost:3000. 

If it didn't, you can simply do it manually. 

And here, you got this React application which will try to communicate to our
Deno server. 

Though, of course, at the moment, at least for me, this server is not up and
running, and, therefore, if we open up the developer tools, we see that we got
an error being printed here. 

We're not able to get results from the server, essentially, and therefore we're
not able to render any todos here. 

Well, that is something we can fix, of course. 

Keep that development React server running, and open a new terminal, so that you
got that other process still running, and now, in your main project folder, so
now longer in frontend-app, but in your main project folder, run your Deno app. 

For that, I'll cd into the deno folder, and then, with deno run --allow-net, I
can run the app.ts file. 

Now, this will spin up the Deno server, but now I get a address in use error. 

And the reason for that is that our Deno application here also wants to run on
port 3000, and that's where the React app runs already. 

The fix is simple. 

I'll switch Deno to port 8000, that's also a common development port, and
therefore now, if we rerun this command, it should compile and run this
successfully. 

If you now reload the application, you still get that error though. 

Now, the reason for that is that in the React application, we need to make one
tiny adjustment, and, for that, you don't need to know React, no worries. 

In the frontend-app source folder, under components, Todos.js, you'll find a
bunch of URLs, and they always point at localhost:3000. 

Change this to 8000 now because that's where our server is running on. 

So, change all those occurrences, and save that Todos.js file. 

This will now restart the React server, and you now can already see the
Middleware log at the bottom here, which means that a request reached our Deno
server. 

And indeed it did, but now we're getting a different error. 

We're getting a CORS error. 

And to fix that, we need to understand what CORS is. 

I did cover it before in the course. 

I'll give you a brief refresher here. 

And, once we understood that, we can fix it in our Deno application code. 

---