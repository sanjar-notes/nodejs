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