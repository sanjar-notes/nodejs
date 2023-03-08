Skipping handlebars, not relevant at the moment.
- Handlebars is mostly HTML, unlike plug
- It's restrictive, in that no computation are allowed inside the template, including conditional ones. This is good - in the sense that all logic is present on the server code, not the template. But it's bad - in the way that the most trivial of things need to be done outside the template.
- It does have conditionals, and iteration constructs.