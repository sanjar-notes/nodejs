# 52. Dependencies
Created Friday 3 February 2023 at 11:33 am

"dependencies" inside "package.json" is an object containing external package name as key and version number as values.

It has many uses:
1. Setup - for setting up existing project again. npm installs all packages listed in "dependencies" with the correct version
2. Specify version of package - a package may or may not support the project's code in the future. Specifying the version makes sure the project works even if the package is updated by the maintainer.
3. 