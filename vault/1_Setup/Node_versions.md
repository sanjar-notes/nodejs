# Node versions
Created Wed Dec 27, 2023 at 12:38 AM

Many projects have bad documentation or ways around what Node.js version they use, and how to load it.
But there's a simple explicit way to do both enforcement and convenience at once.

It involves making changes to 4 files - `.nvmrc`, `.npmrc`, `package.json` and terminal hook (`.zshrc` for example).

1. Enforcement - the app will raise errors for wrong versions during `npm install`. `.npmrc` and `package.json` do this, since any app is started by an npm script. This raises an error during `npm install` itself for wrong Node version, which is a good thing. See [StackOverflow](https://stackoverflow.com/a/61403989/11392807)

   `/.npmrc`

   ```sh
   engine-strict=true
   ```

   `/package.json`. See [engines property on npmjs](https://docs.npmjs.com/cli/v10/configuring-npm/package-json#engines)

   ```json
    "engines": {
        "node": "<=16"
    },
    // supports range like so `>=0.10.3 <15`
    // optionally, even `npm` version can be specified
   ```

2. Convenience

   1. Manual load - Add `.nvmrc` with the node version (by running `node -v > .nvmrc`), then manually do `nvm use` inside the directory. Don't have to remember "x" in `nvm use x`, good.

      `/.nvmrc` and (for safety/other [environments](https://stackoverflow.com/questions/27425852/what-uses-respects-the-node-version-file)) `/.node-version` file

      ```json
      v16.20.2
      ```

   2. Auto load - remembering and doing `nvm use` for each new terminal is lame. So, add `.nvmrc` to the project as usual, and also add a function that loads the node version. Fully automatic. See [Deeper shell integration](https://github.com/nvm-sh/nvm?tab=readme-ov-file#deeper-shell-integration)

      `~/.zshrc`

      ```sh
      # for ZSH: Add to .zshrc https://github.com/nvm-sh/nvm?tab=readme-ov-file#zsh
      # for bash: Add to .bashrc https://github.com/nvm-sh/nvm?tab=readme-ov-file#bash
      # optionally can do
      ```

Notes and gotchas:
- Set global default: `nvm` has a bad UI. To set global default, one has to run `nvm use alias default _version_`
- Use specific node version (temporarily - for terminal session) - `nvm use _version_`
- On mac, make sure to run `brew uninstall node`. Homebrew node messes up with nvm global default - it just takes over the default.

## PS
Time to take [asdf](https://asdf-vm.com/) seriously?