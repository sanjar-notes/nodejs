# 34. HTML templates
Created Monday 30 January 2023 at 02:30 pm

Sending HTML "as is" is fine. A server that does this is called a "static server".

But this is not enough. It is very common to have a page which has some dynamic part, depending on whose making the request or some other criteria. Example - a profile page, that greets the user. Assuming we know who the user each, we should display their name.

Such a server is called a "dynamic server".

---
One simple way to create a dynamic server is to have a "template" or "skeleton" HTML file which has placeholders for the dynamic parts. We can replace these placeholders with data before sending the HTML.

Here's a basic dynamic server with a template HTML file containing a single placeholder "{{name}}"". 
[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/f024b46b376893c3be766e3a26b4fa0b231b9eb8)
```js
(req, res) => {
  res.writeHead(200, { "Content-Type": "text/html" });

  const greetingName = "Sanjar"; // or get from DB, or external API
  // using readFileSync just to keep things simple
  let htmlFileContents = fs.readFileSync("./index.html", "utf-8");
  htmlFileContents = htmlFileContents.replace("{{name}}", greetingName);
  
  res.end(htmlFileContents);
}
```

---
Injecting dynamic data using string replacement is fine. But this doesn't scale:
1. There could be collisions with placeholders.
2. What if we want to add a list of things dynamically, string interpolation would be too much work, i.e. we would have to write the nested HTML for the element too.
3. The page content and the server code are tightly coupled.
4. What if we really want to display some characters that occur in the placeholder as is?

A good solution for these problems is to use a "web template engine". A template engine is a tool that:
1. Defines a [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) for viewable content.
2. Defines "programming" constructs like loops, conditionals that can be used for viewable content.
3. Has some server-side plugin that can be used to interface with the DSL. i.e. connect JavaScript (programming language) to the DSL ("view definition language"?).

Examples - [Pug - JavaScript](https://pugjs.org/api/getting-started.html), [Jinja - Python](https://en.wikipedia.org/wiki/Jinja_(template_engine)), [ERB - Ruby on Rails](https://guides.rubyonrails.org/layouts_and_rendering.html).