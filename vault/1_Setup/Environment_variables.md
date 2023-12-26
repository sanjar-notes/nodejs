---
tags:
  - env
  - environment-variables
---
# 1. Environment variables
Created Mon Dec 25, 2023 at 9:57 PM

## No library (native) method
### Set envs
There are two ways:
1. inline - `SECRET1=hello node app.js`. Multiple can be added too `SECRET1=hello SECRET_2=world node app.js`. Works with npm scripts too.
2. file. This is possible with a new feature (works on v20). You specify the .env file as an option. Don't add spaces around equal sign.
	```env
	SECRET1=hello
	SECRET2=world
	```
	File will be run like so `node --env-file=.env app.js`

### Get envs
The envs in both cases are injected into `process.env`. So `process.env.SECRET1` will get the value.


## With library
There's the [dotenv](https://www.npmjs.com/package/dotenv) library that's common.

### Set envs
Add to file
```env
SECRET1=hello
SECRET2=world
```

### Get envs
```js
const env = require("dotenv").config().parsed;
env.SECRET1 // 'hello;
```

There are more sophisticated libs that allow nested configs, type safety etc.