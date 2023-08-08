## 272. How Does Sending Emails Work?

<strong><em>no description</em></strong>

So how does sending mails work? 

Well we obviously get our node server with our code and we get our user and we
want to send an email to that user. 

Now it's super important to understand and a common misconception that node and
expressjs, these are language or frameworks runtimes that we use for writing our
server side logic but with nodejs, you can't trivially create a mailing server. 

Handling mails is totally different to handling incoming requests and responses,
it's a totally different technology, something totally different happens behind
the scenes. 

Therefore in reality, you will very likely never implement your own mail server
because that is a very complex task, creating a mail server that is capable of
handling thousands or one hundred thousands of e-mails at the same time, sending
them and so on, security, all that stuff is highly complex, so in reality you
typically use third party mail servers for that and that is exactly what we will
do in this module too but I will show you how to interact with such a service to
send that e-mail through that service. 

And by the way all major web applications you might be interacting with
including Udemy don't have their own mail servers, they are using third party
providers like AWS or whatever it is for sending e-mails, so that is exactly
what we will do in this module too. 

---