## 518. Deno Setup

<strong><em>no description</em></strong>

<v Narrator>So let's get started with Deno.</v> And what better way to get
started than to write our first very simple Deno program. 

For that visit deno.land, yes, that is a valid URL. 

And there, you will be able to learn more about Deno, but you will also learn
more about it in this course. 

Of course, most importantly, you will find installation instructions for
different environments and also using different approaches. 

Now you can, of course use any of the approaches being listed here depending on
your operating system and what you want to do. 

And if you click on this Deno installing here, you also will again find a nice
overview of all possible ways of installing Deno. 

Now we might be getting different installation options in the future. 

For the moment, I will use one of those options. 

On Mac and Linux, you can simply copy this command here into the default
terminal. 

On Windows you can copy this command here into the windows PowerShell. 

So not the normal Command Prompt you got on your operating system, but the
PowerShell. 

Which is already pre-installed in which you can launch as a program on Windows. 

Since I'm on a Mac, I'm going to use this command. 

So I'll just paste this here into my terminal, this curl command and hit Enter. 

And this will download this install script, download Deno and install Deno on my
machine. 

Now, what you'll see is that once this finishes successfully, that I won't be
able to run Deno. 

Normally there should be a Deno command, which you can execute by just typing
Deno in your terminal or a Command Prompt. 

But if I do that, I get command not found. 

But actually I get the fix here as well. 

After the installation, that I should manually add the directory to your Home
bash profile or similar. 

These two entries to be precise. 

You can just copy and paste these entries. 

And again, depending on the point of time you're watching this and on the
operating system you're on, the exact instructions you are seeing here might
differ. 

Simply follow the instructions you are seeing here. 

In my case, I should add these two instructions to my bash profile, which is
basically a configuration file for your whole system, which tells your operating
system which commands are available in the Command Prompt, so to say. 

Now, since I'm on Mac OS Catalina, I don't need the bash profile. 

You only need that if you have a Mac version, a smaller or older than Catalina. 

If you have Catalina, you should look into your users folder for a .zprofile
file. 

If you're not seeing that, make sure you're showing hidden files. 

Then you can just edit this and in case you don't have it, you can simply create
such a .zprofile file. 

And I'm going to edit it with TextEdit. 

And in there, the file might look different for you, but in there, the only
important thing is that at the end you add these lines you saw in the Command
Prompt. 

So that's what I'm doing here. 

And with that, save that file, close it and open a new terminal. 

So close the terminal and open a new one. 

And once you do that, you should be able to run Deno and it does not give you an
error, but instead entered this interactive mode here. 

Now let's explore this and what we can do with Deno in the next lecture. 

So now this was Mac OS, now for Windows, I'm going to grab this command for the
PowerShell and just open up the PowerShell, which is a default tool on Windows. 

And in there, I'll just copy it in and hit Enter. 

And this is now going to basically send the request to Deno's servers and also
run an installation script to install Deno on our system. 

So let's wait for this to finish. 

And once this finished, unlike on Mac OS, I'm not even prompted here to do
anything else, and you probably aren't either. 

And therefore we can just go ahead and type the Deno command right away and it
should work here instead of the PowerShell. 

So that's how easy it is to set up Deno on Windows. 

And before that also on Mac OS. 

With that done, you should have Deno installed, and if you now restart the
terminal or the Command Prompt or PowerShell, you are able to run Deno just like
this. 

This is now a globally available command. 

And if you run it, you enter the Deno rappel. 

Now, you know the rappel from Node.js. 

If you run Node, you enter the Node rappel, and there you can execute basic Node
code. 

You can use it as a basic calculator and you can quit it with control C or
control D. 

And for Deno, it's the same. 

You enter the Deno rappel here. 

You can execute basic Deno code. 

You can use it as a basic calculator and you can quit it with control D or by
running Close. 

Now, the idea is the same. 

This is really just a nice playground, or to try out some things in reality,
you're going to write JavaScript code or TypeScript code with Deno, and you can
then run those code files with the Deno executable. 

That's how you would run most of the code when working with Deno. 

Now, speaking of that, let's maybe write some first Deno code so that we get an
idea for how it works and also so that we can gradually dive into the
differences compared to Node. 

---