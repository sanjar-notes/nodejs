## 452. Using Production API Keys

<strong><em>no description</em></strong>

Now I did mention on the slide that you also want to exchange testing keys for
production keys and in our case, that would be that stripe key we're using here
through environment variables which we do set in the nodemon and in the
package.json file. 

Now obviously that always depends on which kind of APIs or third party services
you are using. 

Maybe in your app, you use no service at all and therefore this is not an issue
for you, with stripe what you want to do is you want to click on that to switch
to public or to production ready data. 

Now you need to activate your account here to be able to do that as you see and
to activate your account, you have to fill out some information including some
payment information. 

And therefore I will not do that here but if you were to deploy this into
production, you need to fill that all out and once you fill that out, you will
be able to switch that toggle here here at the top and see your live data, your
production ready keys and you should use these keys in your code. 

So wherever you are using the test keys right now, you would have to replace
them with the production ready keys and that is just a stripe example, other
APIs you might be using might have a similar behavior. 

---