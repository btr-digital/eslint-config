# Bob the Robot ESLint config

Opinionated linting and formatting with ESLint and Prettier for browser JS+Node and/or Vue. Extends [eslint-config-airbnb-base](https://www.npmjs.com/package/eslint-config-airbnb-base).

> The setup is meant to be used with VSCode and requires the [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) extension.

## Usage

### 1. Browser/Node

Install `eslint` and the config:

```
npm i -D eslint @bobtherobot/eslint-config
```

Tell ESLint to use the config with `.eslintrc` (or whatever your eslint config file format is) in project root.
```
{
  "extends": [
    "@bobtherobot/eslint-config"
  ]
}
```

Tell VSCode to use ESlint for fixing and formatting on save. In your global settings, workspace settings or `.vscode/settings.json`:
```
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

### 2. Vue + Vetur

Vue + the VSCode extension [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur) requires a bit more finessing to make everything work.

Install `eslint`, config and `eslint-plugin-vue`:
```
npm i -D eslint @bobtherobot/eslint-config eslint-plugin-vue
```

Tell ESLint to use the Vue config with `.eslintrc` (or whatever your eslint config file format is) in project root. This extends the root config with Vue specific rules and utilizes the `eslint-plugin-vue` and its parser.
```
{
  "extends": [
    "@bobtherobot/eslint-config/vue"
  ]
}
```

Then we'll have to make Vetur let ESLint and Prettier do the validation and formatting of `.vue` files. Either in your VSCode global settings, workspace settings or project root `.vscode/settings.json`:
```
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "vetur.validation.template": false,
  "vetur.format.defaultFormatter.js": "none",
  "vetur.format.defaultFormatter.ts": "none"
}
```

## Notes

Against eslint config best practices this package uses dependencies instead of peerDependencies for everything except eslint itself and assumes that no conflicting versions are installed.

This is because NPM v6 (shipped in Node 14 LTS) does not install peerDependencies automatically and kind of defeats the purpose of an easy install config. NPM v7 (shipped in Node 16 LTS) will fix this issue and we will switch to peerDependencies once we transition fully to Node 16.

For further reading on the subject see this [eslint issue](https://github.com/eslint/eslint/issues/3458).

## Todo

- [ ] Major: Switch to peerDependencies
- [ ] Major: Separate Vue config into its own package