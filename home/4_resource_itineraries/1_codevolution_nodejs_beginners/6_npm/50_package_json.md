# 50. package.json
Created Friday 3 February 2023 at 10:53 am

## What
- "package.json" is npm's configuration file the npm package or project or app.
- It's both human and machine readable.
- It is stored at the root directory of the project. Or, a code project containing a "package.json" most probably means it's a Node.js project.


## Why
- A central place to configure and describe how to interact with and run the package
- It is primarily used by npm CLI
- Contains dependencies' names and versions.

- It's usually generated automatically by running the command `npm init` or `npm init -y` (avoid prompts and stick to the defaults) inside a directory.
- The file is automatically updated by the npm CLI when a package is added/removed/updated.