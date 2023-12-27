# 61. process variable
Created Wed Dec 27, 2023 at 10:57 PM

[Docs](https://nodejs.org/dist/latest-v20.x/docs/api/process.html#process)

This is globally available variable. It has many useful functions and data.

- `process.platform` - one of `darwin`, `linux`, `win32`, `android`
- `process.pid` - returns the PID of the process (self).
- `process.argv` - an array of strings containing CLI args passed when the Node.js process was launched. First value is path to node, i.e. nothing is removed.
- `process.debugPort` - port used by debugger, assuming it is enabled.
- `process.env` - environment variables from OS as well as any inline ones.
    
- `process.exit()` - exit the script. As opposed to `return`, which finishes current module execution, but the complete program keeps running.
- `process.cpuUsage()` - object with CPU time in milliseconds. Example: output `{ user: 38579, system: 6986 }`. If a previous output is passed as argument, shows a diff reading. [Docs](https://nodejs.org/dist/latest-v20.x/docs/api/process.html#processcpuusagepreviousvalue)