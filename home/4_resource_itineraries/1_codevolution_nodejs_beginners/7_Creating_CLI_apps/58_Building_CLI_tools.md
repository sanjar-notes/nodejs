# 58. Building CLI tools
Created Sunday 5 February 2023 at 12:43 pm

Create a basic CLI tool using node and npm
Pass options to the CLI
Add interactivity to the CLI

Steps:
1. Add shebang to the start (main) file. This is to specify the interpreter that OS will use.
```js
#!/usr/bin/env node

console.log()
// JS code here, this is index.js
```
2. Add the command name as attributes of "bin" in package.json. Command name is key and main file name is value. This adds the command to the environment variable.
```json
{
	"bin": {
		"sanjarcode-pokedex": "index.js"
	}
}
```
3. The CLI tool can now be installed via the npm registry.
4. (Optional), to install the tool without publishing, run `npm install -g` from within the folder.

The command can now be used directly in the terminal.

Note: Like all other Node.js projects, we can install and use 3rd party modules.

[Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/2062dd8b3da1c86a3c97d56672d2f81f451584c1)