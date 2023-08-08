## 275. Potential Limitation for Large Scale Apps

<strong><em>no description</em></strong>

So in this module I showed you how to send mails with nodemailer and in this
case, the sendgrid third party service. 

Now one thing I also want to highlight is the way we send that an e-mail here
works for our app and it's good that we don't block the redirect but that we
redirect and send the mail at the same time because if you have an application
with a lot of requests and you would wait for the email to be sent before you
redirect, you might slow down your application because you're sending a lot of
e-mails. 

Now depending on the size of your app and now we're talking about really huge
apps, you could also look into totally different approaches where you have some
server side scripts running every x hours or every x minutes that send e-mails
to newly signed up users. 

Now this will only matter from a certain scale of app on and there you have
different problems anyways but I just want to highlight that you should strongly
consider not using this in a blocking way because if you wait for this to be
finished, this can be slow and you have to evaluate if it's worth waiting for
this or if your user can continue even without that mail being delivered. 

Now with that, you learn how to send mails, not that difficult as you can tell. 

Now let's use that knowledge in the next module and enhance our authentication
process or our authentication features we offer. 

---