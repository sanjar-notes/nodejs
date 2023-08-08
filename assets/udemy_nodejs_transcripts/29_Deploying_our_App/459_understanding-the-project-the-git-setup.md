## 459. Understanding the Project & the Git Setup

<strong><em>no description</em></strong>

So I'm back on heroku and I created an account which is why I'm in my dashboard
now. 

If you haven't done that, definitely do so, click on sign up, create a new
account, enter your data and you should end up on a similar dashboard and have a
create new app button somewhere. 

Now when you click that, on heroku you can give your app a name and I'll name it
node complete udemy, the name is up to you of course. 

You can choose a region, I'll go with Europe because I'm located there but that
is up to you of course and you can then simply click on create app. 

Now with that clicked, you can now choose a couple of different things. 

First of all, we can ignore the pipeline feature, here deployment method will
use heroku git, now what is git? 

Git is a tool which is not part of heroku but used by heroku. 

Git is a version control system and as such, it's a tool which you can use, it's
totally optional but it helps a lot with saving and managing your source code. 

It allows you to work with so-called commits, branches and remote repositories
to name some of its most important features. 

Commits are basically snapshots of your code which you can take but when you can
always switch, so you can always go back to the older version of your code and
have a look at it and then go back to your most recent one or rollback to an
older commit, so this allows you to revert to older snapshots easily or well
safely add it to your code because you can always go back, now you can create
commits after you fix some bugs, after you add new features and so on. 

Branches also allow you to not just have one history of snapshots but multiple
histories for different versions of your code, so you could have a master branch
where your production ready code is in and then you want to fix bugs or add new
features in other branches so that your main code is untouched but when a new
feature done, you can do something which is called merging and merge the new
feature branch with your main branch so that you have one branch which you can
put back into production again but it allows you to work on different features
in different branches without affecting your main finished code for now and this
allows you to basically separate your development workflow from let's say, the
new feature or bug fixing to production workflow. 

Remote repositories, that simply means that your code is not only stored locally
as it is by default but that you can store it and its commit and branches in the
cloud and that of course means that you can protect against loss of local data
and you can also access your source code from different machines and share it
with other developers of course and you can also use that feature to deploy your
code automatically and that is what heroku does because you will essentially use
heroku as a remote repository which means when you push your code to that remote
repository, to heroku, it will then be taken by heroku and it will be put into
production and a server will be spun up based on it automatically. 

That is what git is and that is what heroku uses here. 

Now that means that you will need git and for that you can simply google for git
and then it's this link here, gitscm.com and there you can simply click
downloads and download it for your operating system. 

Simply download the installer for your operating system here and walk through
the steps presented there and thereafter, you'll have git installed. 

Now check the documentation in case you are facing any problems and also
attached to this video, you'll find some free links to get you started with git
in case you want to learn more about it. 

For the deployment only, you don't really need to become a git expert though,
you only need it installed. 

Once you did that, let's continue with the rest of the deployment process here. 

---