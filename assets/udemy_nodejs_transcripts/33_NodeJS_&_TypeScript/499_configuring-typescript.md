## 499. Configuring TypeScript

<strong><em>no description</em></strong>

<v Instructor>Now, I will not dive into</v> all possible types we have. 

Instead I wanna focus on a couple of core features. 

Therefore, as a next step, let's add some configuration to this project. 

So that they can briefly walk you through some Core Settings, especially one
Core Setting. 

We can add a Configuration file, which will then be taken into account by the
TypeScript compiler to this project by running tsc--init. 

This adds a tsconfig.json file, which has quite a lot of options you can set. 

Now, you can read through these comments here. 

I do talk about the options in greater detail. 

In my Understanding TypeScript Course. 

Here, I will leave most options as they are, so I will not comment them in, but
I wanna talk about this "Strict" option because that is important. 

"Strict" mode is generally encouraged. 

It means that certain things are not allowed, which normally would be allowed in
TypeScript. 

And we see this in app.ts file just by adding this configuration. 

I now get an error here that this is possibly 'null' This is one "strict" mode
feature. 

We have this "strictNullCheck" which is turned on. 

All those checks here are turned on. 

If "strict" is set to true, alternatively, you comment out to this line and just
comment in the features you want down there. 

So, they're all set to true when setting "Strict" to true. 

And one of these features ensures that you're not calling something on something
else, which might be "null". 

And here indeed, we select the 'button', but of course, TypeScript can't know,
whether that 'button' actually exists. 

it does not check our HTML code. 

So therefore this could be 'null' if we don't find a 'button', if we have no
buttonElement. 

Now to work around this, we have two options. 

We can add some code here where we check. 

If buttonElement is Truthy and move that code into that if check. 

Now we know that if this code runs buttonElement, can't be null. 

Because if it would be null, it would be falsy and we wouldn't make it into this
if check. 

Alternatively, we know that there will be a button. 

Just as we know that these elements here are HTMLInputElements. 

In such cases, we can add an exclamation mark here. 

This simply means the statement in front of it. 

The expression in front of it, could theoretically be 'null', but we know that
it isn't. 

So, please TypeScript ignored that 'null' case and take the other value. 

in this case, take HTMLButtonElement as the only value. 

This is important. 

And that's something I wanted to show you here. 

One other thing that wouldn't be allowed with Strict mode is that you omit the
type of one parameter for example, now it complains that this parameter
implicitly has the 'any' the type. 

There is an 'any' type which you cannot sign, and that's also is fine. 

But that's a very generic fallback type. 

It basically carries no extra type information. 

Any kind of value is allowed here. 

And therefore, this is really just a type you should know. 

If you have no idea, which kind of data you can expect, if you do know it
better, it is recommended that you are as clear as possible, in this case that
you simply define that you want a number. 

But even if you don't know it, if you set this to any it's okay. 

But not setting 'any' type, that's not something the "Strict" mode allows. 

Because then does this implicitly 'any', but it looks like you simply forgot to
look into this argument and you should at least explicitly set 'any' to make it
very clear that you don't know better, or that you indeed want to allow any kind
of value here. 

So, explicit 'any' is allowed implicit 'any' isn't, and it's even better, if you
set the specific type you are expecting. 

now important, As soon as you added that tsconfig.json file, Once you run the
types of compiler, you can still select the file, but then the tsconfig.json
configuration will not be taken into account. 

Instead, as soon as you do have such a tsconfig.json file, just run tsc like
this, and it will compile all types of files in the folder, whilst taking the
Config File into account. 

So, only if you don't point at a specific file, the configuration file will be
taken into account. 

And all types of files in the folder will be configured. 

You can still target the file if you want to. 

Then the configuration file is ignored for the types of compilation though. 

The IDE always picks up to config.json file. 

So the IDE support is always provided. 

No matter how you then compile it. 

---