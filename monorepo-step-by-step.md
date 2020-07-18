# How to create monorepo step-by-step?

This is monorepo built with `lerna` and `redux`. _Note:_ any following command starting with `npx` is to explicitly run with `npm` (can be applied to both Mac and Windows).

## 1. Initial Setup

### Setup project with `lerna`

`npm i -D lerna`

_Output_

```
root
+ --- node_modules (all necessary packages are installed)
+ --- package-lock.json
```

### Initialize `lerna` configuration

`lerna init` or `npx lerna init`

_Output_

```
root
+ --- node_modules
+ --- packages
+ --- lerna.json
| --- package-lock.json
| --- package.json
```

## 2. Create components and apps

To start, go to **packages** folder: `cd packages`

### Create a React _app_

`npx create-react-app [app-name]`

This will create package with dependency on `react-scripts`

_Output_

```
root
+ --- node_modules
+ --- packages
|     + --- [app-name]
|           + --- node_modules
|           + --- public
|           + --- src
|           | --- .gitignore
|           | --- package.json
|           | --- README.md
|           | --- yarn lock
+ --- lerna.json
| --- package-lock.json
| --- package.json
```

### Create a React _component_

`lerna create @eog/[component-name] -y` or `npx lerna create @eog/[component-name] -y`

_Output_

```
root
+ --- node_modules
+ --- packages
|     + --- [app-name]
|           + --- node_modules
|           + --- public
|           + --- src
|           | --- .gitignore
|           | --- package.json
|           | --- README.md
|           | --- yarn lock
|     + --- [component-name]
|           + --- __tests__
|           + --- lib
|           | --- package.json
|           | --- README.md
+ --- lerna.json
| --- package-lock.json
| --- package.json
```

**Note**: move following dependencies from `dependencies` section to `peerDependencies` in `package.json` file.

- `react`
- `react-dom`

## 3. Dependencies

- If execute following commands at **root** level, it will add third party package dependency to all `packages`
- If execute following commands at **package** level, it will add third party package dependency to that `package` (either `app` or `component`) only

### Third party packages

`lerna add [package-name]@[version]` or `npx lerna add [package-name]@[version]`

### Local packages (link)

`lerna add @eog/[component-name]` or `npx lerna add @eog/[component-name]`

## 4. Add `redux`

`lerna add redux` or `npx lerna add redux`

**Note**: move this dependency from `dependencies` section to `peerDependencies` in `package.json` file on React _component_ ONLY.

## 5. Add `react-redux`

`lerna add react-redux` or `npx lerna add react-redux`

**Note**: move this dependency from `dependencies` section to `peerDependencies` in `package.json` file on React _component_ ONLY.

## 6. Add `redux-saga`

`lerna add redux-saga` or `npx lerna add redux-saga`

**Note**: move this dependency from `dependencies` section to `peerDependencies` in `package.json` file on React _component_ ONLY.

## 7. Setup `reducer`, `middleware` and `store`

TBD

# Useful commands

## 1. `lerna`

### Clean up

This command will delete all `node_modules` from all `packages`
`npx lerna clean -y`

### Bootstrap

This command will install all dependency packages for all `packages`
`npx lerna bootstrap`

### Bootstrap with `--hoist`

This command will install all dependency packages for all `packages` and hoist to `root` level
`npx lerna clean -y && npx lerna bootstrap --hoist`

### Clean and Bootstrap together

I love this command the most, it does everything in the right manner after clone a git repo built with `lerna`
`npx lerna clean -y && npx lerna bootstrap`

## 2. `yarn`

### Find dependency of a package

This command can be used to detect circular reference also.
`yarn why [package-name]`

### Clear cache

This command will clean up all `yarn` cache globally
`yarn cache clean`

## 3. `babel`

Couple things to remember:

- `.babelrc` should present only at `root` or `component` folders to build/transpile
- All `babel` dependency packages should be added to `devDependencies` section in `package.json` inside `component` folder to avoid over-install onto other packages

# React-Redus

- All `reducers` must be combined into `rootReducer`
- All `sagas` must be `run` before they can listen to any `action`
- All `middlewares` must be grouped together into an array before calling `applyMiddleware()`

# Troubleshoot

## Version conflict

If you have version conflict, do following things:

- Run `npx lerna clean -y` at `root` level to clean up `node-modules`. _Note:_ this is applied for repo having `lerna` only.
- Delete `yarn.lock` (if exists) and `package-lock.json` (if exists) from all `packages`
- Run `npx lerna bootstrap` to re-install all dependency packages for all `packages`.

## Invalid Hook Call Warning

If you have this issue (with `lerna` project only), please ensure that following dependencies on **React Component** package are listed under `peerDependencies` section, NOT `dependencies` section in `package.json`.

- `react`
- `react-dom`

## Could not find “store” in either the context or props of “Connect(App)”

If you have this issue (with `lerna` project only), please ensure that following dependencies on **React Component** package are listed under `peerDependencies` section, NOT `dependencies` section in `package.json`.

- `react-redux`
- `redux`
- `redux-saga`

# References

- [Setup project with Lerna](https://michalzalecki.com/solve-code-sharing-and-setup-project-with-lerna-and-monorepo/)
- [CRA Universal](https://github.com/antonybudianto/cra-universal)
- [React-Redux Boilerplate](https://github.com/flexdinesh/react-redux-boilerplate)
