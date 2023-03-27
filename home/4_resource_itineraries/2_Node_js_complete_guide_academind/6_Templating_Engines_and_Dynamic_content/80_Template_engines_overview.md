# 80. Template engines - overview
Created Sunday 5 March 2023 at 10:01 pm

## What's a templating engine.
I was right here, just read it - [78_Module_introduction](78_Module_introduction.md)
![](/assets/80_Template_engines_overview-image-1.png)


## Some popular templating engines
These differ in:
1. Syntax - DSL
2. Philosophy
3. Reuse-constructs
4. Layout, and styling constructs

Engines:
1. EJS - normal HTML for markup, DSL for JS code.
2. Pug (aka Jade) - uses a minimized version of HTML, hashtag-curly brace syntax for placeholders. Special constructs for control flow.
3. Handlebars - normal HTML for markup, double curly brace syntax for placeholder. Similar to EJS, but has less features and different philosophy.

![](/assets/80_Template_engines_overview-image-2.png)


## Installing a template engine
- Template engines are simple Node.js packages available through npm.
- Since template engines are needed at request time, they're installed as production dependencies.
- Most template engines can hook into the server lib/frwk, with almost no code needed.
- All the 3 mentioned here (EJS, Pug, Handlebars) are "Express.js compatible", i.e, they can be plugged in as an Express middleware using a single line.


## Connecting a template engine to the server lib/frwk
- `ejs`, `pug`. Has express.js support out of the box.
- `npm install ejs`
- For handlebars, use `express-handlebars` since it has built-in express support. FYI: the `handlebars` package is a general package for Node.js.

Note: templating engine, in principle, are not tied to a server lib/frwk. Thus, they do need some code to connect with the server lib/frwk in use. Since the packages discussed above already have support for Express, that code is just one line.
