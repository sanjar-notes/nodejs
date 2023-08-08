## 57. Module Introduction

<strong><em>no description</em></strong>

You've now got an introduction to nodejs and how it works and how you can use it
to write basic nodejs programs but what you also already saw is that with nodejs
alone, you have to write a lot of code to deal with basic things like extracting
the body of an incoming request. 

Now typically you don't want to do that, you want to focus on your business
logic, the code that makes up your specific application, you don't want to work
or you don't want to care about standard tasks like handling incoming requests
or routing, so executing different code for different paths, different urls, you
don't want to do that and therefore we'll now have a look at expressjs. 

This is a framework you can install as a third party package into your node
project and as such, it basically helps you outsource some of that nitty-gritty
work, some of these details you don't want to care about, it gives you a rule
set in which you work and a lot of utility functions that help you write cleaner
code and focus on your core business. 

So what's inside this module then? 

We'll have a brief look at what expressjs is, I gave you a short introduction
already now but let's take a closer look. 

I'll then have a look at one important concept that pretty much defines
expressjs or that expressjs is built around, middleware and what this is of
course. 

We'll then have a look at how we can work with requests and responses with the
help of express in a way easier way than we did thus far and we'll also have a
look at routing and see how we can execute different code for different incoming
requests and paths or urls without having to write a bunch of if statements. 

And last but not least, I'll also show you how we can return html pages, so
files we prepared to our client instead of writing html code in nodejs as we did
us far which wasn't really that great. 

So let's dive into all of that in this module. 

---