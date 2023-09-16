# Adding controllers
Created Sunday 12 March 2023 at 07:36 pm

/not-exhaustive - coz wasting time on getting to a definition for controllers, right now is a waste of time

## What controllers to make
Controllers can be grouped in many ways, choose what's easy and scalable. Example:
1. One controller per route.
2. One controller per model action
Note: controllers are named as plural, e.g. "products". Models are named singular, e.g. just "product".


## Implementing controllers
- Start with a [new project](https://github.com/exemplar-codes/mvc-basics-exploration-expressjs)
- Add controllers - [start](https://github.com/exemplar-codes/mvc-basics-exploration-expressjs/commit/d38d7b158058fd255911e83a5dd32bbdf44ccb72) to [finish](https://github.com/exemplar-codes/mvc-basics-exploration-expressjs/commit/939b74e949c24d70db272c587ccc55a817616705)


## 7 actions (Rails inspired) - optional
Ruby on Rails has 7 general kinds of actions. These apply per exposed model. [Link](https://guides.rubyonrails.org/routing.html#crud-verbs-and-actions)

| Action  | HTTP verb | Path             | Comment                                      | Used in API server |
| ------- | --------- | ---------------- | -------------------------------------------- | ------------------ |
| index   | GET       | /photos          | display a list of all photos                 | yes                |
| show    | GET       | /photos/:id      | display a specific photo                     | yes                |
| create  | POST      | /photos          | create a new photo                           | yes                |
| update  | PATCH/PUT | /photos/:id      | update a specific photo                      | yes                |
| destroy | DELETE    | /photos/:id      | delete a specific photo                      | yes                |
| new     | GET       | /photos/new      | return an HTML form for creating a new photo | no                 |
| edit    | GET       | /photos/:id/edit | return an HTML form for editing a photo      | no                 |