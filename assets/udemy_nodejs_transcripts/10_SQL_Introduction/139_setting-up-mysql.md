## 139. Setting Up MySQL

<strong><em>no description</em></strong>

Now to work with SQL, we need a SQL based database and I'll go for MySQL because
you can install and use that for free, at least in the basic version which does
suffice for this course. 

You can visit MySQL.com to download and install it and there simply click on
downloads and scroll down, we don't need the enterprise edition here instead
we'll go for the community edition which is the free one, click on downloads
there too and now what we will need is the MySQL community server and we'll also
need the workbench. 

Now you can also download a combined installer, especially here for Windows you
should choose the MySQL on Windows Installer in tools which allows you to set up
everything in one go but you can also click on MySQL community server here
simply and this should give you a download which allows you to install all these
things in one go anyways. 

So let's choose the MySQL community server here, always dive into the
installation instructions in case you're facing any problems on your system and
then if you scroll down, select your operating system here, the one you plan on
using, so for Windows you can then also download this general installer which
allows you to pick the programs you need, for MacOS we simply can go for this
first download, the DMG archive and then once you click there you don't have to
log in, you can simply choose no thanks just start my download to well start the
download. 

Now this can take a while because it's quite a big file, on Windows you have the
choice between downloading a web-based installer which is smaller but downloads
what you need to during the installation or a complete installer which downloads
everything in advance. 

Once your download is done, simply execute the downloaded file so the windows
installer or this Mac DMG archive. 

Here I'm asked to well continue through the installation wizard and I will do
that, agree to the license, leave the default installation path, click on
customize here though to choose what to install and make sure that you do
install the MySQL server here. 

If you're running this installer on Windows, you should have a different
installer where you can choose to install the MySQL server but then also in one
go, install the MySQL workbench, so make sure you select both for installation
and click install here and now on both operating systems, this should install
it. 

Now once installation is done, a configuration process should start
automatically. 

There you should make sure that during this configuration process, you do choose
the legacy password encryption which sounds insecure but which is perfectly fine
and the newer version simply is not supported by the node SQL package we're
using yet. 

So choose the legacy password encryption and choose next, you also have to
choose a password for your root user and you can also leave start MySQL server
once installation is complete checked or check it if it is unchecked and click
finish. 

On Windows, simply leave all the other settings as they are and click through
them and by the end, it should be done and it should then also start a MySQL
server for you with the setup you chose here in the configuration steps. 

Now once installation is complete, on Windows if you also installed the MySQL
workbench, you're done, on Mac or Linux, you're not done yet, instead you should
go back to your previous page where you chose MySQL community server and there
also install the MySQL workbench. 

The workbench basically is a client, a visual client we can use to connect to
our database to inspect it and play around with it outside of our node
application which simply makes debugging and developing a bit easier. 

So choose the MySQL workbench here and there you also can choose your operating
system, now again on Windows if you used that general installer, you already
have it. 

Download that file here, again you don't need to log in, just start to download
and wait for the download to finish so that you can again execute the, well
executable once it is done. 

Finish the installation process as instructed by the installer and once you're
done with that, you should be all good. 

You can now test your setup by starting the MySQL workbench you just installed
and then there, you should already see your MySQL instance running. 

If that is not the case, have a look at the attached document where I describe
some common issues or in general give you some links on how to make this work
and how to bring this up, you just need to make sure that your MySQL server is
running and during installation, you had a choice to check that it should always
start with your system, on Mac you can also open your system preferences and
there you should have the MySQL option where you can also stop and start the
server. 

To connect to the database, simply click on that instance and now enter that
root password you assigned during the installation. 

This should now allow you to connect to your SQL server instance like this, then
once you enter the password you should be connected to your database system. 

And right now this is what you have, basically an empty window and we won't work
too much in that, we'll of course work with our database from inside our node
application but this will allow us to conveniently look into our database from
time to time and see what is stored and one thing we can do already is we can go
down to schemas here which can be translated with database here you could say
and there, we can define a new schema, so a new database with which we'll work
and I'll name it node complete, you can name this whatever you want and you can
also leave the other settings here and then on the bottom right and I know it's
small here, unfortunately you't zoom in, you can click apply. 

Now this will create a new database you can say with which we can interact
later, you can leave all the default settings and simply click apply here and
now you should see that node complete thing which has a couple of tables or none
right now but where you can then later connect to and store your data in the
tables that will be created here. 

So with that, we can continue and we can now move on with our code and start
interacting with MySQL from inside our node application. 

---