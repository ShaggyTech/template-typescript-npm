
## @shaggytools/

# template-typescript-npm

A boilerplate/starter template to **code** in [Typescript](https://www.typescriptlang.org/), **unit test** with [Jest](https://jestjs.io/), generate **documentation** with [JSDoc](https://github.com/jsdoc/jsdoc), build a **universal package** with [Rollup](https://rollupjs.org/guide/en/) and **publish** your package to [npm](https://www.npmjs.com/) / [yarn](https://www.yarnpkg.com/) for use anywhere (CommonJs, UMD, AMD, IIFE, ESModule, CDN, browser script, etc.)

# Getting Started

INFO: This template was developed and tested on `Node v12.14.0`, `NPM v6.11.3`, and `Yarn v1.21.1`

## Prerequisites

- [ ] Install [Node](https://nodejs.org/en/)

- [ ] Install [Yarn](https://yarnpkg.com/lang/en/) - an alternative to NPM and used in this template's scripts.

- [ ] Optional - Install [NVM](https://github.com/nvm-sh/nvm) - to switch between different node versions.

- [ ] It is recommended to use the [Visual Studio Code](https://code.visualstudio.com/) editor to develop your package.

- [ ] It is also recommended to install the [Live Server - Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) to be able to test live versions of your modules locally in the browser before publishing to NPM and Yarn.

## Setup

 Clone this repository:
 `git clone https://github.com/ShaggyTech/template-typescript-npm.git`

 Change into the template directory
 `cd template-typescript-npm`

Install all of the development dependencies listed in the package.json with:
  `yarn install`

Change the "name" field in the `package.json` file to what you want your NPM / Yarn package name to be. This package uses an npm organization as the first part of the name (@shaggytools/) but not all packages do.

Folow the steps listed [HERE](https://yarnpkg.com/lang/en/docs/publishing-a-package/) to get setup for publishing your package, make sure you've setup your package "name" field as described above, this will be the published name of your package.

Open up `package.json` and change the "libraryName" field to whatever you want to call your library when using it in a browser.  The `rollup.config.ts` file uses this field to determine the library name output in the various bundles. You might also want to change the various .html files in the `/tests/` folder to use this new name in the script imports.  These html files are simply there to show you how the various modules can be imported and used in the browser.

Some of the root level files are configuration files for various packages used in this template.  I encourage you to open these up and at least skim through them.  Play around and see how the build is affected when changing or adding config options.

| Package    | Config File       | Description                                                        | Prod | Dev |
|------------|-------------------|--------------------------------------------------------------------|:----:|:---:|
| Rollup     | rollup.config.ts  | Uses process.env.ROLLUP_WATCH to determine dev or production modes |   X  |  x  |
| Typescript | tsconfig.json     | Used for production builds                                         |   x  |     |
|            | tsconfig.dev.json | Used for development builds                                        |      |  x  |
| JSDoc      | jsdoc.json        | Production Documentation                                           |   x  |     |
|            | jsdoc.dev.json    | Development Documentation                                          |      |  x  |
| Jest       | jest.config.js    | Testing configuration                                              |      |  x  |
| Babel      | .babelrc          | Used to transpile code in production and development               |   x  |  x  |
| ESLint     | .eslintrc.js      | Used by our code editor to enforce code standards and styling      |      |  x  |
| Prettier   | .prettierrc       | Used by our code editor (VS Code)                                  |      |  x  |

  ---

Some commands to get you started with local development (more below in the commands section):

- `yarn build` - will output the *production* rollup build to the `/dist` folder.

- `yarn watch` - will simultaneously run TSC, Rollup, JSDoc, and Jest in watch modes, watching for changes in the `/src` and `/tests` folders, with all outputs going to the `/dev` folder. Under the hood this command runs the `watchAll.js` file found in the `/bin` folder. Feel free to modify the file if you want to adjust/add/remove any of the commands that are run concurrently.  This command is CPU intensive. You may be better off either removing some of the commands from the watchAll script, or running the individual watch scripts. (`watch:docs` `watch:test` `watch:rollup` `watch:tsc`) in separate windows.

# Project Structure

`!` - denotes a folder + sub-folders ignored by git (see `.gitignore` file) and not included when committing and pushing to a remote repository. You can safely delete or clear these folders before committing/pushing to a remote repository.

`*` - denotes a folder + sub-folders ignored when publishing to NPM/Yarn. You can safely delete or clear these folders before publishing your package.

```
bin/

!* dev/

- coverage/

- dist/

- docs/

- package.json

! dist/

- browser/

- cjs/

- module/

- types/

- bundle.min.js

docs/

docsSrc/

- static

- tutorials

src/

- __tests__/

- index.js

...

tests/

- browser/

- node/

- ...various project config files

```

### ./bin

A directory containing node helper scripts used in `package.json` scripts.

### ./dev

A directory which contains all of the output when running any of the development scripts in `package.json`

- Directory will not be created until the first time you run a development script that outputs here.

- Not included in the source code repository nor in the published package code

- Clear all folder contents via `yarn cleanDev`

### ./dist

A directory which contains all of the output from `yarn build` script in `package.json`.

This is also the directory that will be uploaded to NPM/Yarn when you publish your package with `yarn publish`.

- Directory will not be created until the first time you run the `build` script.

- Not included in the source code repository.

- Clear folder contents via `yarn clean:dist`

### ./docs

A directory containing the output from `yarn build:docs`

Github can automatically update your documentation site every time you push changes to this folder to your remote repository. Set this folder as the gh-pages source in your repository settings:

[See this Github help article for more information](https://help.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

- Clear folder contents via `yarn docs:clean`

### ./docsSrc

A directory containing static assets, tutorials, and anything else you would like to include when building the documentation files.

### ./src

A directory containing all source code typescript files as well as unit tests located in `__tests__` sub directories.

### ./tests

A directory containing tests that check various ways of importing the module.

# Frequently used Scripts/Commands

All of these commands are to be run in the terminal from the root project directory, and can be found in the root `./package.json` file.

## `yarn build`

This script will output the *production* Rollup build to the `/dist` folder.

- Run *before*  `yarn release`

## `yarn build:docs`

This script builds the **production** documentation via JSDoc.  

- First cleans all files from the `./docs` folder, then

- Outputs documentation files to `./docs/`.

- See `./jsdoc.json` to adjust the options, output, plugins, templates, etc.

## `yarn build:docsDev`

This script will build the **development** version of the documentation via JSDoc

- Outputs documentation files to `./dev/docs/`

- See `./jsdoc.dev.json` to adjust the documentation options, output, plugins, template, etc.

## `yarn build:rollup`

This script will build the **production** version of the final npm package, via Rollup and output to the `./dist/` directory.

## `yarn build:rollupDev`

This script will build the **development** version of the final npm package, via Rollup and output to the `./dev/dist/` directory.

## `yarn clean`

This script will clean all files from the `./dist/` and `./dev/`.

## `yarn clean:dist`

This script will clean all files from the `./dist/`directory.

## `yarn cleanDev`

This script will clean all files from the `./dev/` directory.

## `yarn release`

This script will run the commands `yarn build` then `yarn publish` and will ask for a new version before publishing your package to NPM and Yarn.

- Publishes the package based on any files located in the `./dist/` folder.

## `yarn watch`

This script will run the `watchAll.js` script located in the root `bin` directory and allow you to more easily watch all portions of the development process, reloading with file changes each time.

- Outputs development files to relevant sub-directories of the `./dev/` directory.

NOTE: This is CPU intensive and might slow down your development process on an older PC. You can run individual watch scripts via `watch:tsc`, `watch:test`, `watch:rollup`, or`watch:docs`

# Documenting your code

This template utilizes the NPM module [JSDoc](https://github.com/jsdoc/jsdoc) in order to document your code.

I encourage you to read through the JSDoc [documentation](https://devdocs.io/jsdoc/) if you're not familiar with how to document your code.

#### Development Documentation - Using VS Code and the Live-Server plugin to see documentation output live during the development stage:

Using [Visual Studio Code](https://code.visualstudio.com/) and the associated [LiveServer](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) plugin you can utilize the following scripts to setup live documentation changes.

- `yarn watch` or `yarn watch:docs`

This will output documentation build files to the `./dev/docs/` directory.

If you then *right click* on the `index.html` file and select `Open With Live Server`, this will open a new browser window. Any changes you make to files located in the `./src/` and `./docsSrc/` directories will trigger the docs to get rebuilt and the changes reflected live in the browser window that was opened with Live Server.

Once you are satisfied with your changes, continue to the next section below to see how you can use Github-Pages to serve a live version of your documentation.

#### Production Documentation - Live Documentation via Github-Pages

Github can automatically update a live version of your documentation website whenever you push changes to the `docs` folder of your remote repository.

1. Set the `docs` folder as the gh-pages source in your repository settings: [See this Github help article for more information](https://help.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

2. Make changes to your documentation, in either the `./src/` or `./docsSrc/` directories. It is recommended to preview a development version of the documentation first before building the production docs, although this is effectively the same thing and may not be needed.

3. Run `yarn build:docs` to generate new documentation in the `./docs/` directory.

4. Run `git commit -m "commit message here"`

5. Run `git push` to update the remote repository, and new changes to documentation will be live within several minutes.

# Testing your code (unit testing) with Jest

This template utilizes the NPM module [Jest](https://jestjs.io/) in order to test the code you write.

I encourage you to read through the Jest [Documentation](https://jestjs.io/docs/en/getting-started) if you're not familiar with how to test your code.

#### Testing scripts included in this template

`yarn watch:test`

Runs Jest in watch mode with the --onlyChanged option flag, this will limit tests to only files that have changed since the most recent git commit.

`yarn test`

Runs all tests once.

`yarn watch`

Runs Jest in watch mode with the --onlyChanged option flag, concurrently with other dev watch scripts. Note that you won't be able to enter any commands to control jest, use 'yarn watch:test' if you need to enter jest commands:

# Building your package

This template utilizes the NPM module [Rollup](https://rollupjs.org/guide/en/) and various associated plugins in order to package your module into multiple formats (the 'universal' part of this template).

I encourage you to read through the Rollup [Documentation](https://) if you're not familiar with how to test your code.

The build outputs to `./dist/` and is controlled via the `rollup.config.ts` config file. By default this template is setup to output the following formats: `Default:UMD(Universal` - `CJS(CommonJS/Node)`  `ESM(ES Module)`  `IIFE(Browser)`. This and other options can be changed in the config file.

A `types` folder is also output into the `./dist/` directory which will contain the Typescript type definition files (.d.ts) for your package.

#### Development Build

`yarn build:dev` or `yarn watch` or `yarn watch:rollup`

Will build the package with Rollup and output everything to `./dev/dist`. A copy of the `./package.json` file will also be placed in the `./dev/` folder.

#### Production Build

`yarn build`

Will build the package with Rollup and output everything to `./dist/`. The contents of that folder are what gets uploaded to NPM and Yarn when you run `yarn release`.

# Publishing your package to NPM and YarnPkg

You can use the `yarn release` script to use publish your package. This script will run `yarn build` before attempting to publish your package. You will be prompted to enter a new version number before publishing is completed.
