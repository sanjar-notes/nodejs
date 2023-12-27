---
tags:
  - npm
  - npm-scripts
  - scripts
  - environment-variables
---
# 56. npm scripts
Created Sunday 5 February 2023 at 10:50 am

Docs - https://docs.npmjs.com/cli/v10/using-npm/scripts
## Why (have npm scripts)
An "npm script" is a convenient way to bundle common commands for use in a project. Examples - start the server, start the dev server, start test runner, lint all files etc.

- "npm scripts" are stored in the package.json file.
- They also ensure that everyone is using the same command with the same options. 
- They also help beginners/new-comers - they don't have to learn the command line tool or options.


## What (details)
npm scripts are not "scripts" in the general sense. They're more like "stored CLI aliases". 

They are **defined** under the "scripts" key in "package.json". Keys is the script name and value is the CLI command that will be run.

Example:
```json
// package.json sample
{
  "name": "my-custom-package-1",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "upper-case": "^2.0.2"
  }
}
```

npm scripts are **executed** using the command 
```bash
npm run <SCRIPT_NAME>
```
Note: The script name "start" is so common that one can omit "run" in this case, i.e. `npm start` and `npm run start` are the same thing.


## Passing arguments (optional)
Everything after `--` when using the script is placed directly after the script value before execution. Example:
```json
  "scripts": {
    "print": "echo",
    "ls": "ls"
  },
```
Doing `npm run print -- Hello` is equivalent to `echo Hello`
Doing `npm run print -- -l` is equivalent to `ls -l`

FIXME: there's no need for this `--`, appending stuff directly to "npm run <SCRIPT_NAME>" works out of the box?


## Access local packages commands
3rd party sometimes export commands, but these are not available in the terminal if the module is installed locally.

e.g. "nodemon" if installed locally, "nodemon" command in the terminal will still not work. But it *is made available inside a script*, i.e. npm injects all local dependencies of the project in the script's environment. Of course, global packages and all other system stuff is available as well.

Assume nodemon is only install locally:
```json
  "scripts": {
    "myNodemon": "nodemon --help",
    "nodemonx": "nodemon" // ok to name the same, but want to show that any name is fine
  },
```

```sh
nodemon app.js # ERROR, "nodemon" command not found

npm run myNodemon # Ok
npm run nodemonx -- app.js # OK
```

Note: if a module is installed both globally and locally, the local one will be preferred if used in npm scripts.


## Run npm script from anywhere
Suppose I am at `~`, and I wish to run a script for project at `~/my-work/my-app`.
This can be done in one go without `cd`, like so:
```sh
npm run COMMAND --prefix ~/my-work/my-app

# or in general
npm run COMMAND --prefix some-location
```

The following also works, identically
```sh
node some-location/index.js
```

Note: these two ways, and doing them from inside the folder behave the same (filename and dirname are also printed the same).
source - [StackOverflow](https://stackoverflow.com/questions/36172442/how-can-i-get-npm-start-at-a-different-directory)


## Access* package.json stuff in scripts/code
*The \* - only some built-in things can be accessed, but there is a user managed key available.*

See https://docs.npmjs.com/cli/v10/using-npm/scripts#packagejson-vars, [helpful article](https://dev.to/paulasantamaria/mastering-npm-scripts-2chd)

Note here that:
1. There are two modes here - you access variables inside scripts, or inside code. Mostly, the same thing works for both.
	1. Inside script - `$variableName`. Example: `echo $npm_package_name`
	2. Inside code - `process.env.variableName`. Example: `console.log(process.env.npm_package_name)`
2. There are a lot of hidden variables also, which may not be useful, so I'll not discuss them here. Example: "npm_node_execpath"
3. These variables are available only if code or script is run via `npm` command. Running via `node` command will not work, i.e. the variables will not exist.

### `npm_package_` default
3 values are available by default:
1. `npm_package_name` - `'myproject'`
2. `npm_package_version` - `'1.0.0'`
3. `npm_package_json` - path to package.json

### `npm_package_config_`
This is a user managed object, key being `config`. 
By default, it doesn't even exist. 

The keys you add to this object become accessible in underscore notation (instead of the usual dot). Nesting is allowed, and again, underscore will be added. 

All variable names and values are strings. BTW, this also means that the root, `npm_package_config`, by itself, isn't a valid variable.

```js
// package.json
...

 "config": {
    "my-var": "🐥Some value",
    "portx": "🐥1234"
  }
  
...
```

`npm_package_config_portx` and `npm_package_config_my-var` are both available now.

[Docs](https://docs.npmjs.com/cli/v10/configuring-npm/package-json#config)