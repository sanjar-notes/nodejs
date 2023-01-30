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