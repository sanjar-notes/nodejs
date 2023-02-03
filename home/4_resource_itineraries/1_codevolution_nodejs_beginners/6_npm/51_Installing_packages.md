# 51. Installing packages
Created Friday 3 February 2023 at 11:11 am

## Choosing a good package from the registry
A few things to consider when choosing a package from the registry:
1. Popularity (downloads per week)
2. Last published (should be recent)
3. Is actively maintained (should be)
4. Issues (too many for a simple thing means not a good package)

---
To install a package from the registry, run the following command (inside the directory):
```bash
npm install myPackageName

# more patterns
npm install myPackage@x.y.z # installs version x.y.z
```
Packages installed this way are installed "locally", i.e. they are meant to be used only by the current project.

---
Locally installed packages are stored inside a folder named "node_modules" (this is done automatically).
- This folder contains raw source code used by the library.
- It's not meant to be version controlled. It's usually ignored using the `.gitignore` file.
- It should not be edited. If this is needed, something's probably wrong with the approach/solution.
- It can be regenerated anytime by running `npm install` (which installs all dependencies).

---
Packages can be installed globally by using the `-g` option, by running the following command (location does not matter here):
```bash
npm install myPackageName -g
```

However, packages installed this way are not accessible by default inside the Node.js REPL or scripts. To access these inside the REPL and scripts, the `NODE_PATH` environment variable needs to be set up. It's value is a list of paths Node.js will include at the time of module resolution  (i.e. finding the module). **If this is feels too complicated, just set the `NODE_PATH` to the output of `npm root -g`**.

---
NPM packages can be of three types based on CLI usage:
1. Only CLI - packages that are meant to be run as a command only, i.e. not meant to be imported in code.
2. No CLI - packages that are meant for imports only.
3. Both - package that can be used through the CLI and inside scripts. It's not necessary that functionality offered will be the same in both modes.

Packages to be used as a CLI are generally installed globally. Node.js automatically seeds a command with the package's name. Examples:
- create-react-app
- nodemon

---
Commonly used npm syntax:
```bash
npm list -g # show all globally installed packages
npm i myPackage # 'i' is an alias for 'install'
npm uninstall myPackage # remove the package from current project, -g is available
```