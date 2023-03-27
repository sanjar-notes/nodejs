# 150. What is Sequelize: an ORM
Created Friday 24 March 2023 at 02:07 am

Sequelize is an ORM (Object Relation Mapper) library for Node.js. It supports TypeScript too.

## Motivations (to use an ORM - my guess)
1. No need to write SQL
2. SQL entities are converted into objects, and vice versa, automatically.
3. Stay within the primary programming language - i.e. JS (Node.js).


## What an ORM does (my guess)
1. **Converts** database entities (record, table, databases) to objects, and vice versa. By objects, I mean objects of the primary app (backend app) language   - JS (Node.js), Python, Ruby etc.
2. Provides **convenience functions for CRUD** operations.
3. Provides an **abstraction over table relations**, thereby eliminating* the need for managing/thinking about PK, FK etc.
	- This is the concept of "associations".
4. Provides a way to have **life-cycle functions** for database entities (records, tables, databases), and runs them properly.
	- e.g. if all books should have an author, and an author 'A' gets deleted, so will  (automatically) all books which have 'A' as author. This is a "destroy" lifecycle function. There could similar ones for update, create or even read.
	- Another important type of lifecycle function are validations. The ORM runs these during addition of rows (or other DB entities) to see if they fit the schema and other custom validation logic.
	- Life-cycle functions are *"events"*, essentially . They are run properly by the ORM at the correct time.
1. Provides other commonly used functions - like DDL ops.
	- Provides functions, code to connect to popular databases, or accepts drivers as plugins.
	- e.g. automatically choosing the best MySQL type that'll be equivalent to JavaScript's `String`.
	- e.g. create a table from a schema defined in a JS file.
2. Is a way to do **scripting** on a database with a regular programming language.
	- e.g. a Python script to do maintenance tasks as a DB admin.
	- e.g. changing the database on schema changes. This is the concept of *"migrations"*. Due to ease of scripting (FIXME: due to this?), some frameworks even support automatic migrations (in most cases).

Note (my guess):
- All this can be done without an ORM, i.e. using raw SQL too, but it'd be very hard and time consuming - both from a development POV and from a learning POV.
- The schema for a table, is generally saved as a `class`. This file/class is called the model. Custom functions can be added to the model, of course.


## What is an ORM
*I won't try to give an exact definition (it may not even exist).*

An ORM is primarily intended to act as a *bridge* between the database and the app's programming language via objects in it (the app's language).

Practically, ORMs provide a lot of other functionality too, as mentioned previously.


## Example
![](/assets/149_What_is_an_ORM-image-1.png)
