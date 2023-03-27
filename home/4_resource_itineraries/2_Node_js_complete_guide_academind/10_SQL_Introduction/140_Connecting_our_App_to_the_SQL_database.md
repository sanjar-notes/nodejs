# 140. Connecting our App to the SQL database
Created Wednesday 22 March 2023 at 01:37 am

#### Note
- This is not specific to an "app". This page is a general method to connect any Node.js code (script, app etc) to the SQL database (software) running (independently) on the machine.
- Yes, MySQL (or any other database software) keeps running independent of the Node.js code. It's generally never stopped.

## mysql2
- This is the "database driver" - i.e. a package with code that helps us communicate with the database.
- Practically, it allows us to run raw SQL queries in our Node.js code.
- The basic idea is to obtain a "connection" object using the package. This "connection" is used for all interaction with the database, as well as closing the connection.
- This code to connect to the database is usually kept separate from the application code, in a utility file (like the path utility we have [now](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/tree/d18ab604acb9ac5509949d9e185ccaf6f3a2ba14/util)).


## Connecting to the database
There are two ways to do this:
1. Create a "connection" - the smallest possible *claim* of DB resources established between a user (i.e. a backend server app) and a database (technically database server).
	- A connection is usually ended by the client after they are done with their *queries*, i.e. it's not a one query construct - just that it's meant to be limited.
	- This has the limitation of being sequential (one query at a time - one has to wait for query response before another can be sent) queries against the DB.
	- The request for a connection may be rejected, due to high load on the server.
	- This is a low resource, high overhead, high risk type of DB resource claim.
		- Low resource - small amount of DB resources allocated
		- High overhead - establishing a connection, i.e. calculating and allocating resources on the DB has some overhead, and of course network (request/response wait) overhead, which may become significant if connections are opened and closed multiple times. This is especially relevant if there's high load on the DB.
		- High risk - because connections requests may be rejected by the DB.
2. Create a so called "connection pool" - a size configurable, guaranteed *claim* of DB resources established between a user (i.e. a backend server app) and a database.
	- A pool consists of multiple guaranteed connections, all established at once. The DB is guaranteed to provide query service even under high load, since a pool marks resources for the given client/user (i.e. backend server app).
	- Using a pool has the advantage of being able to do parallel queries with the database (assuming they're sufficiently independent). This is because each connection is Independent from others (in a pool or otherwise).
		- Maximum number of parallel queries is equal to the set number of connections (they are guaranteed ones of course).
	- This is a high resource, low overhead, low risk kind of DB resource claim
		- High resource - since a pool request usually consists of many guaranteed collections.
		- Low overhead - since all connections in the resource are allocated at once, it doesn't have the overhead of network requests, calculation, estimation (FIXME) that is done here?) on the DB.
		- Low risk - since connections in a pool are *guaranteed* to be respected by the DB, even under high load.

Note:
- Connections, even if from the same client, are Independent from each other (weather in a pool or now, though pool connections have guaranteed priority). And most databases (MySQL, for example) can process many connections at once.
- Of course, a client can request multiple connections, as well as multiple pools. Assuming no hard limits are triggered.
- FIXME maybe - the concept of pool vs connections seemed a little fishy. I consulted ChatGPT to learn the difference, i.e. **guarantee + multiplicity** in case of a pool.

Code for obtaining a pool:
```js
const mysql = require("mysql2");
const pool = mysql.createPool({
  host: "localhost",
  user: "root",
  database: "node-complete",
  password: 'my-password',
});

module.exports = pool.promise();
```

---
### Running SQL queries
For that first create a table, using MySQL Workbench.

### Create a table
1. Go to 'node-complete' schema we created (in the left sidebar), and create a table named "products".
2. Add fields of the table
	1. Add "id", of type "INT". It should also be a primary key (PK), should be Not Null (NN), Unique (UN), unsigned (UN), auto-incrementing (AI). Leave others unchecked.
	2. Add "title", type "VARCHAR(255)". Not null.
	3. Add "price", type "DOUBLE". Not null.
	4. Add "description", type "TEXT" (a little bigger than VARCHAR). Should be Not Null.
	5. Add "imageUrl", type "VARCHAR(255)". Not null.
3. Click on apply. This shows a preview of the SQL query that will be run. Proceed.

### Add some products
1. In the left sidebar, go to the database, the table, and click the rightmost icon.
2. Add values in the first row. ID is optional (it will be assigned automatically if not specified). Click apply.

![](/assets/140_Connecting_our_App_to_the_SQL_database-image-1.png)

### Node.js code
```js
const db = require("./database");

(async () => {
  try {
    const response = await db.execute("SELECT * FROM products");

    const resultRows = response[0];
    console.log(resultRows); // array, with each element as object form of the row.
  } catch (error) {
    console.log(error);
  }
})();
```
The first element in the output is an array of resultant rows.

[Code - creating connectionPool, executing queries](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/65d8d045c5bacd9699215eaf7f1a7b5bba231b46)
