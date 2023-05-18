# Setting up MongoDB
Created Friday 19 May 2023 at 01:10 am

## Installing MongoDB (the database)
- We can install MongoDB locally.
- However, we'll use a cloud environment - from the official MongoDB website. This will be helpful if we wish to deploy our app. MongoDB has a good enough free tier, this is sufficient for the course.


## Cloud setup
- Sign in
- Create a user, and a cluster. Make sure the user has both read and write permissions.
- Check IP whitelist etc, and add your PC's IP address. We'll need to do this for exploring MongoDB in our Node.js apps locally.


## Local (project) setup
- Install the mongoDB driver, by running `npm install mongodb`
- Creating a connection. Copy the SRV address, and add in the password (use an [env variable](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/226967b78f8741422a48e901144ea69cc60470cf))
	```js
	// file /util/database.js
	const mongodb = require('mongodb');
	const MongoClient = mongodb.MongoClient;

	const mongoConnect = callback => {
	  MongoClient.connect(
	    'mongodb+srv://maximilian:9u4biljMQc4jjqbe@cluster0-ntrwp.mongodb.net/test?retryWrites=true'
	  )// Copied from the site (SRV address)
	    .then(client => {
	      console.log('Connected!');
	      callback(client);
	    })
	    .catch(err => {
	      console.log(err);
	    });
	};
	
	module.exports = mongoConnect; // is a function
	```
- Use the connection code in main app file (`app.js`)
	```js
	const mongoConnect = require('./util/database.js')

	// express code

	// start express from inside the mongoConnect callback
	mongoConnect((client) => {
		console.log(client);
		app.listen(3000);
	});
	```

[Code till here](https://github.com/exemplar-codes/online-shop-with-nosql-mongodb/commit/a3b84f8383ce314699f83539f86e89dde6dfa767)