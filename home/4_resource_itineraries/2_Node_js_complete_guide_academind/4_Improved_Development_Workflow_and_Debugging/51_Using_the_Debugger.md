# 51. Using the Debugger
Created Sunday 19 February 2023 at 02:27 pm

VScode has a built in Node.js debugger. It's nice and easy to use. We'll be using that here.

## Starting the debugger
1. Add breakpoints in file(s)
2. Run the main file in debug mode. We can of course run a specific file, but most files either give an error or not useful independently.
   

## Using the debugger
- Controls
	- Pause, stop, restart
	- Resume
	- Next line (i.e. step over)
	- Step into, step out
- In debug mode:
	- Hover over tokens to see values
	- See variable values in the side-panel
	- See the stack
	- Add variables to 'watch' to see changes to selected variable


## Intermittent code
- We can run explicit code in the debug console. Writing to variables is allowed.
- Variable values can be changed by double clicking on them in the debug side-panel.


## Restarting the debugger automatically
We use "nodemon" to restart the app if any file is edited. 
1. Install "nodemon" globally.
2. Add this to the config (in "launch.json"):
```json
"restart": true,
"runtimeExecutable": "nodemon",
```

- Optionally, one can use the terminal instead of debug console. Set:
```json
 "console": "integratedTerminal"
```


## Further reading/help
1. Node.js docs - https://nodejs.org/en/docs/guides/debugging-getting-started/
2. VScode docs - https://code.visualstudio.com/docs/nodejs/nodejs-debugging