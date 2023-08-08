## 462. Deploying APIs

<strong><em>no description</em></strong>

Now we got a running application. 

Now that is how we deploy our application to heroku, heroku is just one possible
hosting provider so definitely explore alternatives, check out the documentation
for your favorite hosting provider to learn the exact steps on how to get your
code onto it and which additional configuration you might need to do, that
always differs a bit but it never differs that you need to get your code onto
that server there and spin up your node server and pass your environment
variables, that is always the same, so check out the docs for your favorite
hosting provider. 

Now this of course was our shop application, it was not the rest API and not the
graphql API but there, I will not show you specific deployment videos because
actually deploying these does not differ. 

There we still have a normal node server right, a node express application so we
can deploy it in exactly the same way. 

The only thing that will differ is that we can't really click open app anymore,
well we can but then on the starting page, we'll not see much because there are
no server side rendered views, instead we'll have an API running where we can
send requests to and will then be our frontend application or our mobile
application where we have to adjust the url to send the request to our now
running hosted application and not to localhost anymore. 

So there in your application, you'll have to exchange your urls here and use
your hosted domain and not localhost but that is the only thing and then the
frontend app or the mobile app is deployed differently anyways. 

A mobile app is sent to your users through the app stores, a frontend
application as this one built with react typically is deployed as a static web
application and that is something you can learn in my react, angular and so on
courses. 

You simply build this project with the build script you can find in
package.json, in this case it would be npm run build and this will then spit out
a new folder with all the built and optimized code and more on that in the
respective courses on these frameworks, why that is required and so on, you
learned all about that there. 

And then you would take that code, in this case in the build folder and ship
that to a static web post like for example AWS S3 and then serve your app on a
totally different server than your node application is running on because as you
learned many times in this course, there is no strong relation between your node
API and your frontend mobile app, whatever it is. 

So that is how you would deploy that. 

---