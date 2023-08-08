## 457. Setting Up a SSL Server

<strong><em>no description</em></strong>

Now last but not least before we then really ship our application to a server,
to a hosting provider, I want to have a look at ssl/tls and tls is simply the
newer version of that, ssl is the term more people know however. 

Both is about securing your data that is sent from a client to the server
because when we communicate between client server, we typically exchange data. 

Now we can have an attacker, third party who's eavesdropping on that data, this
is technically possible, of course not super trivial but possible and therefore
this attacker could read your data which you're sending from the client to the
server which is of course a problem if we're talking about credit card data or
anything like that. 

Hence we want to protect that data and we do that with ssl/tls encryption. 

Now once such encryption is in place, eavesdropping is not possible anymore
because while the data is unreadable as long as it is in transit and it will be
decrypted on the server. 

Now to enable that encryption and to be able to decrypt it, we work with a
public private key pair, both is known to the server. 

Now that public key is as the name suggests, not something we have to protect,
the private key is however, the private key will ever only be known by the
server because the private key will later be important for decrypting the data,
the public key will be used for encrypting. 

Now in ssl certificate, we bind that public key to the server identity, the
identity is simply something like the domain, the admin email address, you set
that data when you create a certificate. 

That ssl certificate therefore connects a public key and a server and sends that
to the client, to the browser so that the client also is aware of the public key
and knows that it belongs to that server. 

Now typically you will use a certificate authority for that, though you can
create your own ssl certificates too and we'll do that in this module but when
you create your own keys, then the browser does not actually trust you that the
information in there is correct and that is when you get informations or
warnings like hey this page uses ssl but doesn't seem to be secure, do you
really want to visit it. 

Hence in production, you would use a ssl certificate provided by a known
certificate authority which the browser trusts and therefore you have a real
secure and trusted protection. 

Nonetheless the way it works always is the same, we have that public key, part
of that certificate, certificate ideally is not created by you but by a trusted
authority, we will create it here on our own though because that will be free,
that public key is then received by the client through that certificate and now
the client can encrypt the data which it sends to the server and the server can
decrypt the data with that private key and only that private key can decrypt
that data and this is how that works and how that secures your data in transit. 

Now let me show you how this works in practice, now to set up a ssl connection
on your own server with your own certificate, again you should get one from an
authority once you deploy that to production but for testing this, we can
definitely play around with our own one, we need to create a certificate and we
do it with a command named open ssl. 

On Mac and Linux, you have that available by default, on Windows you don't but
there you can find it by googling for open ssl windows and then that second link
here, this binaries link leads you to a page where you can take the first link
to ssl pro web and there when you scroll down, you'll find installers that
install this open ssl tool on Windows too, so that you can follow along with the
commands I'm about to run on Windows as well. 

Choose your version here, install it and once you have installed it, you can run
open ssl rec-nodes-new-x509-keyout server.key-out server.cert and this will give
you that private key and the public key packaged up in a certificate. 

Now once you hit enter, you will be asked a couple of questions and there make
sure to choose valid values though that does not really matter too much but the
idea here is that you connect your identity, the identity of your application to
your public key though again your own self-signed certificate will not be
accepted by browsers anyways, for production you should not use that option. 

Still let's fill it out with some truthy values and one important value is this
common name, you must set this to localhost otherwise the certificate will not
work because this has to be set to your domain. 

So if you were to use your self-signed certificate on the server you deploy your
app to and you host this app on example.com, then then you would have to set
this to example.com. 

Again typically you request a certificate for your domain by some authority and
then they will do this for you but if you create your own one, use the domain
your app is running on and locally, that is localhost and this certificate will
be denied and will not be accepted if you set this to another value. 

Now after you did all that, you'll find two new files in your folder, server
cert which is the certificate and server key which is the private key. 

Now the private key will always stay on your server, the certificate is what we
send to the client in the end. 

Now to use that, in app.js I first of all have to import a new node module and
that is the https module which allows us to spin up an https server. 

Thus far, we directly or indirectly through app listen used http,  now we'll use
https. 

To use that, I need to read in my files and I will do that up here. 

I will read in my private key by using the node file system package which you
need to make sure you import in this file here, you need that file system
package and there, you can read a file synchronously. 

Now this will block code execution until the file is read and you learned that
typically, this is not what you want to do but here I actually don't want to
continue with starting the server unless I have read that file in. 

So here I will read that file synchronously and the file I want to read is
server.key, so my private key file. 

I'll also add another constant which I'll name certificate and that will be fs
read file sync and then of course it's my server.cert file. 

Now with these two files read in, we can scroll down to the place where we start
the server with app listen and now I'll not use app listen any more but I'll use
https, this new package we just imported and there, create server to create a
https server. 

This now needs two arguments, the first one configures the server and here we
have to point it at our private key and the certificate and the second argument
will be our request handler, in our case our express application. 

So the second argument will be our app, the first argument will be a javascript
object where you need to set two things, you need to set the key key and you set
that to that private key constant we created a second ago and you also need to
set the cert key which you set to that certificate constant we created a second
ago and then we listen on that server. 

Now with that, if you run npm start, it will start your server but now using ssl
encryption and if we now go back to our application and we reload localhost
3000, this will fail because by default it uses http, if I use https localhost
3000, it will fail because the browser does not accept that custom or that
self-signed certificate as you learned but if you click on advanced here, you
can proceed to localhost and now again, the browser does warn us because it does
not like our self-signed certificate but technically we are now using ssl
protection. 

And this is how you enable it but just as with logging and compression,
typically you would set this up differently, you would let your hosting provider
set this up because technically the hosting provider often also has its own
servers in front of yours and the servers of the hosting provider then use ssl
and the traffic between your app and the in-between servers does use http
because it's blocked or it's not available to the public anyways and the hosting
providers front servers would implement this logic. 

So you wouldn't write that code on your own and indeed here, I will fallback to
my old code where I just had app listen because we'll need that later when we
deploy it because we will let our hosting provider manage ssl but if you ever
need to do it manually, this is how you do start a node server in https mode. 

---