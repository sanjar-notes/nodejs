# 56. npm scripts
Created Sunday 5 February 2023 at 10:50 am

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
Everything after `--` when running the script is placed directly after the script value before execution. Example:
```json
  "scripts": {
    "print": "echo",
    "ls": "ls"
  },
```
Doing `npm run print -- Hello` is equivalent to `echo Hello`
Doing `npm run print -- -l` is equivalent to `ls -l`

FIXME: there's no need for this `--`, appending stuff directly to "npm run <SCRIPT_NAME>" works out of the box?


## Using commands exposed by 3rd-party  modules
3rd party sometimes export commands, but these are not available in the terminal if the module is installed locally.

e.g. "nodemon" if installed locally doesn't work using the "nodemon" command in the terminal. This can be solved by creating a script that calls the command, and it'll work.

In other words, npm scripts *do* have access to commands exposed by local 3rd party modules.

Assume nodemon is only install locally:
```json
  "scripts": {
    "myNodemon": "nodemon"
  },
```

```sh
nodemon app.js # ERROR, "nodemon" command not found

npm run myNodemon app.js # OK
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
source - [StackOverflow](https://stackoverflow.com/questions/36172442/how-can-i-get-npm-start-at-a-different-directory)