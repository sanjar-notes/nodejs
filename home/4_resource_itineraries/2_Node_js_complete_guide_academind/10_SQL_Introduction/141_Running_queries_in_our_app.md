# 141. Running queries in our app
Created Thursday 23 March 2023 at 11:58 pm

1. [Fetch all products](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/bc7c6077f8445f897134f2db595fd182ef88f49e)
2. [Fetch products by id](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/2c3e8b21fec17de849cd361607f04ffa93f3dda3) - **sanitized substitution** in `mysql2` - to prevent SQL injection attacks. Syntax is simple (`?` is the placeholder):
	```js
	// syntax
	db.execute('string containing one/many ?', [value1, value2, value3]);

	// example 1
	db.execute('SELECT ? FROM ?', ['*', 'products']);
	// evaluates to 'SELECT * FROM products'

	// example 2
	db.execute('SELECT * FROM ? WHERE ?=?', ['products', 'id', 2]);
	// evaluates to
	// 'SELECT * FROM products WHERE id=2'
	```
3. [Fetch all, fetch by Id inside Product model](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/de7c2239553ea6c0526532425d653e8a37ea13b0) - the app is partially broken due to this change. This is not a bug, it's meant to break.
4. [Add, delete products using SQL](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/94bfcba87b3fbb23548e339006db7a961beb3219) - again, the app is in broken state. Which is fine.
5. [Data Pre-population using SQL](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/c48e6224203a4f12ed4ff5a4cad95cb2b46478ab)

We'll update the remaining routes with SQL, and fix issues later. The goal was to demonstrate how to run raw SQL with in Node.js, with `mysql2`.