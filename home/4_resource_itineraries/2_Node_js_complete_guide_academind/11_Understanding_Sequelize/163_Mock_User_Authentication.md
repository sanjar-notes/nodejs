# 163. Mock User Authentication
Created Sunday 23 April 2023 at 10:19 am

A very simple and useful way to defer user authentication is to assume the authentication "PASSES" for each request. Example - add a middleware that sets the user with Id = 1 as the authenticated user, like so - [code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/8d1dd904baa13090bf1acfefef045f388473a836
):
```js
const User = require('..something'); // Sequelize model

app.use((req, res, next) => {
	req.user = await User.findByPk(1);
	next();	
})
```
Note, the convention way to store user data for the duration of the request is to store it inside `req.user`. A more general construct for storing data to be used by upcoming middlewares is to add attributes to `req.locals`.

At an endpoint, the code will be something like this
```js
router.get((req, res, next) => {
	const user = req.user;
	const products = await user.findAllProducts({});

	render(..something);
})
```