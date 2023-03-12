# 99. Adding models
Created Sunday 12 March 2023 at 07:37 pm

/somewhat-rough

The data of our app is currently stored in a controller. This is not ideal, since a model may be used by many controllers. Note - not having the DB is not the issue I'm talking about, I'm talking about coupling of unrelated parts of code, which is not desirable. **We should create a dedicated model file**.

---

The structure of a single product is quite simple - an object with a string attribute called "title".

A model should also have functions to:
1. save, delete, edit the model instance. 
2. get, delete and query the whole collection (here - a simple array) of models. 

Code (for this project):
- Since the a model (i.e. model instance) has properties ("title") and methods, we can use the `class` keyword available in modern JS. This is better than other methods like constructor-closure.
- The collection functions should be usable without creating a model instance - i.e. they should be static keyword. Modern JS does have the `static` keyword that can be used for this.
- Model file and the `class` name, by convention, start with capital letters.

[Code - add Product model](https://github.com/exemplar-codes/mvc-basics-exploration-expressjs/commit/d930ada68f7b481da6f41318811d6b1b4e22a16c)

Code (generally):
- The model contains the database connection logic, and this part should be abstracted in the app code - i.e. controllers should not have to worry about DB connection, etc.
- We didn't have an `id` or any other unique identifier (aka "primary key" in DB jargon) here. This is usually not an issue, since the database program assigns this automatically.

Note: 
- Since we don't have a database, the collection (i.e. array of objects) is stored outside the model. Of course, the static functions do refer to this outside array, which is fine.