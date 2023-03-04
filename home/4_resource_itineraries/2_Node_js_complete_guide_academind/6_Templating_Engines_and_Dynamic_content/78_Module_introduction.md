# 78. Module Introduction
Created Sunday 5 March 2023 at 01:38 am

## Situation
Currently, we are sending "static" HTML files and assets. This is not realistic since websites usually need to show different pages depending upon the user data.

This means that even if a page is similar in look and feel for different users (i.e. page has a common UI template), the data displayed on the page is different (based on user data).

## A solution - template engine
A template engine is a tool that helps the servers generate the pages to be sent dynamically. The template engine is essentially a function that takes 2 arguments - a template file (with keys) and user data (with corresponding keys) and spits out the HTML file. This file is sent as the response. This is also known as server side rendering.

<details>
  <summary>What I know (or think I now) about template engines</summary>
  <ul>
    <li>
      Templates are usually written in a DSL. The DSL and the template engine
      are mostly coupled and made by the same team.
    </li>
    <li>
      Templates have *placeholder* constructs were data and also code in a
      programming language may be written.
    </li>
    <li>
      The placeholder should evaluate to a render-able type like strings,
      number, characters.
    </li>
  </ul>
</details>

---
In this module, we'll be learning about:
1. Managing dynamic content (without a database, for now)
2. Using some templating engines - Pug, Handlebars and EJS
   
[Initial code - server app with static HTML and assets](https://github.com/exemplar-codes/templating-engines-w-express-js/commit/591b2acf09cb6d83fd434e20bc367f65136e5463)
We'll build up and learn upon this.