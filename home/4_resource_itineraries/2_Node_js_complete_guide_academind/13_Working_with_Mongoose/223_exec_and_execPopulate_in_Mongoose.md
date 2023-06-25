# 223. `exec` and `execPopulate` in Mongoose
Created Friday 19 May 2023 at 11:50 pm

Note - `exec` is not needed generally. It's used only when query building is complex or calls have to be optimized (number of calls, or amount of data wise). Using `exec` from the get-go may be a sign of bad code.


### What is `exec`
By default, the query methods (`find*`), or query helper methods (`.populate`, `.select`) all return a "Mongoose query object" - which is just the query built to be executed, i.e. the DB trip is still not made. Example:
```js
Book.findById(23); // no trip made
Book.findById(23).populate('author'); // no trip made
```

**This is helpful since it allows creation of chains and makes sure only 1 final DB call is made**

To actually end the query and trigger the DB call, a function called `exec` needs to be called. There are 3 ways to use it
```js
Book.findById(23).exec().then(book => {}); // #1 explicit

Book.findById(23).then(book => {}); // #1 implicit, using .then()

const book = await Book.findById(23); // #3 implicit, using await


// # in the implicit cases, exec is called internally due to .then and await - the promise handling constructs
```

This is the main use of `exec` - marking end of query being built and triggering the DB call.


### More about `exec` (help from the Web)
FIXME - need to recheck this (when I code it), especially the breaking down chained query part

1. Main use - end queries being build and trigger DB call. Already seen.
2. Usage - Breaking down query chain into multiple statements.
	```js
	// case 1 - single statement
	const bookDetail = await Book.findById(23).populate('author');
	// await is enough, exec not needed


	// case 2 - break down query into multiple statements
	const bookMiniQuery = Book.findById(23); // a query object
	const bookDetail = await bookMiniQuery.populate('author').exec();
	// continuing the query


	// equivalents
	const bookDetail = await bookMiniQuery.populate('author'); // implicit exec
	bookMini.populate('author').then(bookDetail => {});
	```
3. Usage - Building queries on top of already fetched documents, as opposed to the usual "query object". This works only if `.lean` is not used.
	```js
	const bookDetail = await Book.findById(23).populate('author');
	// await is enough, exec not needed

	
	const bookMini = await Book.findById(23); // document
	const bookDetail = await bookMini.populate('author').exec();
	// needed here because bookMini is a document, not a query object
	
	// equivalents
	const bookDetail = await bookMini.populate('author'); // implicit exec
	bookMini.populate('author').then(bookDetail => {});
	```
4. `exec` is idempotent - doing `exec` with `await`, `.then` will not result in an error. Also calling `.exec()` repeatedly is fine too. Mongoose is smart enough to ignore the extraneous `.exec` (whether implicit or explicit) and does not create extra DB calls.
5. `execPopulate` - `.execPopulate(arg)` is short for `.populate(arg).exec()`
6. Implicit nature - if one is using `then` or `await` and using a single query chain, there's no need to use `exec`.