## 505. Node & TypeScript: Setup

<strong><em>no description</em></strong>

<v Instructor>Now, with the TypeScript basics</v> out of the way, let's see how
we could utilize TypeScript in a simple Node Express application. 

And for that, I cleared my folder again, and I'll initialize my TypeScript
compiler there with tsc --init to create this tsconfig file again, and I'll run
npm init to basically turn this into a new npm controlled project where we then
can install dependencies. 

I'll confirm all these defaults here, and that gives me an empty package JSON
file. 

Now, I wanna create a basic Node Express application, let's say a basic Node
Express rest API, but with TypeScript instead of with JavaScript. 

And for this now, besides creating these configuration files here, of course we
wanna install Express, with npm install --save express, we install the Express
package which we also used before in the course. 

We can also install with npm install --save the body-parser package to parse
incoming request bodies. 

Now, with all of that installed, we could write a regular Node Express
application as we did at multiple times throughout this course. 

We can add a app.js file, and in there, you know that we can import Express by
requiring express like this, and we can create our app by calling the express
function, and on app, we can then listen on a port, and then we can register our
middleware, our different routes, we can parse incoming request bodies, we can
do all of that. 

But I now don't want to do it like that, instead now the goal is to write some
TypeScript code. 

And since we now learned all those core essentials about TypeScript in the last
lectures, let's convert this to a TypeScript application and let me show you how
we can build a basic rest API with TypeScript. 

---