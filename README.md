
## @shaggytools/

# template-typescript-npm

A boilerplate/starter template to **code** in [Typescript](https://www.typescriptlang.org/), **unit test** with [Jest](https://jestjs.io/), generate **documentation** with [JSDoc](https://github.com/jsdoc/jsdoc), build a **universal package** with [Rollup](https://rollupjs.org/guide/en/) and **publish** your package to [npm](https://www.npmjs.com/) / [yarn](https://www.yarnpkg.com/) for use anywhere (CommonJs, UMD, AMD, IIFE, ESModule, CDN, browser script, etc.)

> INFO: This template was developed and tested on `Node v12.14.0`, `NPM v6.11.3`, and `Yarn v1.21.1`

# Prerequisites

- [ ] Install [Node](https://nodejs.org/en/)

- [ ] Install [Yarn](https://yarnpkg.com/lang/en/) - an alternative to NPM and used in this template's scripts.

- [ ] Optional - Install [NVM](https://github.com/nvm-sh/nvm) - to switch between different node versions.

- [ ] It is recommended to use the [Visual Studio Code](https://code.visualstudio.com/) editor to develop your package.

- [ ] It is also recommended to install the [Live Server - Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) to be able to test live versions of your modules locally in the browser before publishing to NPM and Yarn.

---

# Setup - *REQUIRED*

---

## 1. Clone this template and install dev dependencies

```node
// Clone this repository:
git clone https://github.com/ShaggyTech/template-typescript-npm.git

// Change into the template directory
cd template-typescript-npm

//Install all of the development dependencies listed in the package.json with:
yarn install

```

## 2. Edit the package.json file

1. Change the `"name"` field to what you want your NPM / Yarn package name to be.
   - This package uses an npm organization as the first part of the name (@shaggytools/) but not all packages do.

2. Change the `"libraryName"` to the global variable name you want to use when importing and using the package in a browser script. Ex: `myModuleName.function()`.  
   - The `rollup.config.ts` file uses this field to determine the library name output in the various bundles.
   - You might also want to change the various .html and .ts files in the `/tests/` folder to use this new name in the script imports.  These html files are simply there to show you how the various modules can be imported and used in the browser.

3. Customize the following fields to your desired values:
   - `"version"`: start at 1.0.0 or 0.0.1, etc.
   - `"description"`: short description of your package
   - `"repository.url"`: your git remote repository
   - `"author"`: your name, email, etc.
   - `"bugs.url"`: where users can report bugs
   - `"homepage"`: can be documentation homepage (gh-pages) or github link, etc.
   - `"keywords"`: an array of keywords to help find your package in searches

## 3. Edit this ./README.md File

This README file, that you are currently reading, will serve as the `index.html` of the [documentation](https://www.shaggytech.com/template-typescript-npm/index.html), as well as the [npmjs.com](https://www.npmjs.com/package/@shaggytools/template-typescript-npm), [yarnpkg.com](https://yarnpkg.com/en/package/@shaggytools/template-typescript-npm), and [source code](https://github.com/shaggytech/template-typescript-npm) homepages.  Therefore, you must complete the following steps:

**1.**
Bookmark the [live documentation](https://www.shaggytech.com/template-typescript-npm/index.html) version of this README for future reference as you are about to heavily edit or delete the contents of this file and may need it in the future. You can also rename or move the file if you prefer to save a local copy.

**2.**

- _EITHER_ Heavily edit and modify this README file to suit your package needs.
- _OR_ Delete the contents of this file and start over with your package info.
- _OR_ Rename this file to something else so you can still reference it later, and create a new root `./README.md` file with your desired package info.

**3. Optional**
You can change the homepage of the documentation by changing `module.exports.opts.readme` in the JSDoc config file: `./jsdoc.js`

## 4. Add npm/yarn credentials

1. Ensure you've setup your `package.json` as described above.

2. Folow the steps listed [HERE](https://yarnpkg.com/lang/en/docs/publishing-a-package/) to get setup for publishing your package.

## 5. _CONGRATS!_

**You're all setup for local development and publishing and NPM package! Additional optional setup steps, commands, etc. are below:**

---

## Some commands to get you started with local development (more listed below in the commands/scripts section)

- `yarn build` - will output the *production* rollup build to the `/dist` folder.  This is the folder that will be used as the source for our NPM/Yarn package.  This script will be automatically run before the `yarn release` script.

- `yarn watch` - will simultaneously run TSC, Rollup, JSDoc, and Jest in watch modes, watching for changes in the `./src`, `./docs`, `./docsSrc` and `/tests` folders, with all outputs going to the `./dev` folder.

## Optional Additional Setup

Some additional setup steps you may want to perform.

### Clean the ./docs folder for a fresh start on documentation

`yarn docs:clean`

### Edit Configuration Files

Some files at the root project level are configuration files for various packages used in this template.  I encourage you to open these up and at least skim through them.  Play around and see how the process and build is affected when changing or adding config options.

| Package    | Config File       | Description                                                        | Prod | Dev |
|------------|-------------------|--------------------------------------------------------------------|:----:|:---:|
| Rollup     | rollup.config.ts  | Uses process.env.ROLLUP_WATCH = 'true' or 'false' to switch output location and other options |   X  |  x  |
| Typescript | tsconfig.json     | Used for production builds                                         |   x  |     |
| Typescript | tsconfig.dev.json | Used for development builds                                        |      |  x  |
| JSDoc      | jsdoc.js | Uses process.env.JSDOC_ENV = 'development' or 'production' to switch output location and other options    |   x  |  x  |
| Jest       | jest.config.js    | Testing during development  |      |  x  |
| Babel      | .babelrc          | Used to transpile code in production and development               |   x  |  x  |
| ESLint     | .eslintrc.js      | Used by our code editor to enforce code standards and styling      |      |  x  |
| Prettier   | .prettierrc       | Used by our code editor (VS Code) for styling our code |      |  x  |

---
---

# Development scripts

---

There are more scripts in the `./package.json` file than are listed here but these are the frequently used ones. Add your own or modify the existing ones if needed.

All of these commands are to be run in the terminal from the root project directory, and can be found in the `./package.json` file.  You can also substitute `npm add` for `yarn` in the commands if you prefer to use NPM.

---

## `yarn build`

This script will output the *production* Rollup build to the `/dist` folder.

- Run *before*  `yarn release`

---

## `yarn build:docs`

This script builds the **production** documentation via JSDoc.  

- Utilizes `process.env.JSDOC_ENV` with 'production' or 'development' values

- First cleans all files from the `./docs` folder, then

- Outputs documentation files to `./docs/`.

- See `./jsdoc.js` to adjust the options, output, plugins, templates, etc.

---

## `yarn build:docsDev`

This script will build the **development** version of the documentation via JSDoc

- Utilizes `process.env.JSDOC_ENV` with 'production' or 'development' values

- Outputs documentation files to `./dev/docs/`

- See `./jsdoc.js` to adjust the documentation options, output, plugins, template, etc.

---

## `yarn build:rollup`

This script will build the **production** version of the final npm package, via Rollup and output to `./dist/`.

---

## `yarn build:rollupDev`

This script will build the **development** version of the final npm package, via Rollup and output to `./dev/dist/`.

---

## `yarn clean`

This script will clean all files from the `./dist/` and `./dev/` folders.

---

## `yarn clean:dist`

This script will clean all files from the `./dist/` folder.

---

## `yarn cleanDev`

This script will clean all files from the `./dev/` folder.

---

## `yarn release`

- will do the following, in listed order, to publish your package:
  - clean the `/dist/` folder
  - run `yarn build` script
  - run `yarn publish` script
  - ask for a new version number
  - publish the contents of the `./dist/` folder to both NPM and Yarn, using the value of `package.json.name` and the new version number
  - run `git push --tags` to update your repository with a commit tagged with the newest version

---

## `yarn watch`

This script will run the `watchAll.js` script located in the root `bin` directory and allow you to more easily watch all portions of the development process, reloading with file changes each time.

- Outputs development files to relevant sub-directories of the `./dev/` directory.
- will simultaneously run TSC, Rollup, JSDoc, and Jest in watch modes, watching for changes in the `./src`, `./docs`, `./docsSrc` and `/tests` folders, with all outputs going to the `./dev` folder.
- Under the hood this command runs the `watchAll.js` file found in the `/bin` folder. Feel free to modify that file if you want to adjust/add/remove any of the commands that are run concurrently.

> NOTE:
This command is CPU intensive and may be slow on older PCs. You may be better off either removing a few of the commands from the `bin/watchAll.js` script, or running the individual watch scripts (`watch:docs` `watch:test` `watch:rollup` `watch:tsc`) themselves, in separate windows, as needed.

> NOTE:
You won't be able to use Jest keyboard commands in this main watch mode, use `watch:test` if you need finer control in Jest watch mode.

---
---

# Project Structure

---

`!` - denotes a folder + sub-folders ignored by git (see `.gitignore` file) and not included when committing and pushing to a remote repository. You can safely delete or clear these folders before *committing and pushing to a remote repository*.

`*` - denotes a folder + sub-folders ignored when publishing to NPM/Yarn with `yarn release`. You can safely delete or clear these folders before *publishing your package*.

## Overview

```markdown
## Folder Structure

bin/

  <!*>
  dev/
    coverage/
      - code coverage output files from Jest

    dist/
      - development rollup build, mirrors root /dist folder structure

    docs/
      - production documentation build with JSDoc, considered part of source code.

    package.json
      - copy of the root package.json file,
      - simulates a final package so you can import directly from the ./dev folder

  <!>
  dist/
    - browser/
      - IIFE
      - minified
      - single file

    - cjs/
      - CommonJs/Node)
      - code-split
      - module

    - module/
      - ESM Module
      - ES2015+
      - code-split
      - module

    - types/
      - Typescript `.d.ts` type definition files
      - auto populated from your ./src code

    - bundle.min.js
      - UMD (universal bundle)
      - browser and node
      - minified
      - single file

    - bundle.min.js.gz
      - UMD
      - Universal Bundle, browser and node
      - minified
      - gzipped

  docs/

  docsSrc/
    - static/
    - tutorials/

  src/
    - __tests__/ (test files ending with .test.ts)
    - index.ts (main entry)
    - ... more source code

  tests/
    - browser/
      - simulated browser imports in .html files
    - node/
      - simulated CommonJs imports in .ts files

  README.md
    - home page of the documentation page and npmjs.com package

  package.json
    - scripts and package settings

  + various package configuration files

```

---

## Directories

`!` - denotes a folder + sub-folders ignored by git (see `.gitignore` file) and not included when committing and pushing to a remote repository. You can safely delete or clear these folders before *committing and pushing to a remote repository*.

`*` - denotes a folder + sub-folders ignored when publishing to NPM/Yarn with `yarn release`. You can safely delete or clear these folders before *publishing your package*.

---

### `./bin/`

A directory containing node helper scripts used in `package.json` scripts.

---

### < ! * > `./dev/`

A directory which contains all of the output when running any of the development scripts in `package.json`

- Directory will not be created until the first time you run a development script that outputs here.

- Not included in the source code repository nor in the published package code

- Clear all folder contents via `yarn cleanDev`

---

### < ! > `./dist/`

A directory which contains all of the output from `yarn build` script in `package.json`.

This is also the directory that will be uploaded to NPM/Yarn when you publish your package with `yarn publish`.

- Directory will not be created until the first time you run the `build` script.

- Not included in the source code repository.

- Clear folder contents via `yarn clean:dist`

---

### `./docs/`

A directory containing the output from `yarn build:docs`

Github can automatically update your documentation site every time you push changes to this folder to your remote repository. Set this folder as the gh-pages source in your repository settings:

[See this Github help article for more information](https://help.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

- Clear folder contents via `yarn docs:clean`

---

### `./docsSrc/`

A directory containing static assets, tutorials, and anything else you would like to include when building the documentation files.

---

### `./src/`

A directory containing all source code typescript files as well as unit tests located in `__tests__` sub directories.

---

### `./tests/`

A directory containing tests that check various ways of importing the module.

---
---

# Documenting your code

---

This template utilizes the NPM module [JSDoc](https://github.com/jsdoc/jsdoc) in order to document your code.

I encourage you to read through the JSDoc [documentation](https://devdocs.io/jsdoc/) if you're not familiar with how to document your code.

> NOTE: It is recommended to preview a *development* version of the documentation first before building the production docs.  Although, this is effectively the same thing as watching/building the *production* version, it was thought to be a better practice if we separate *development* and *production* versions of the documentation builds.  As the `./docs/` folder is part of the source code and is used by gh-pages for live production documentation, we only want to rebuild docs in that folder when we're ready to commit production docs to source.  It might be prudent to go so far as to build and commit the production docs in a separate commit, after committing other souce code files.

## Documentation during Development

**Using VS Code and the Live-Server plugin to see documentation output live during the development stage**

Using [Visual Studio Code](https://code.visualstudio.com/) and the associated [LiveServer](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) plugin you can utilize the following scripts to setup live documentation changes.

- `yarn watch` or `yarn watch:docs`

This will output documentation build files to the `./dev/docs/` directory.

If you then *right click* on the `index.html` file and select `Open With Live Server`, this will open a new browser window. Any changes you make to files located in the `./src/` and `./docsSrc/` directories will trigger the docs to get rebuilt and the changes reflected live in the browser window that was opened with Live Server.

Once you are satisfied with your changes, continue to the next section below to see how you can use Github-Pages to serve a live version of your documentation.

## Production Documentation

**Setup gh-pages to serve your live documentation from remote repository:**

Github can use the `docs` folder in your remote github repository to serve a live version of the JSDoc build files in that folder.  

This means you can update the 'production' documentation by simply building new documentation files in the local `./docs` folder and pushing the changes to your remote repository, whereafter the live 'production' documentation website should be updated within several minutes.  Follow these steps to get it going:

> **IMPORTANT!** -  If you haven't moved, modified, or renamed this very ./readme.md file, YOU HAVE NOT COMPLETED SETUP and should do so now before proceeding with the following steps. The Setup section can be found at the top of this document.

1. Make sure you have followed all steps in the 'Setup' section at the top of this file.  It's important that your `./package.json` and `./README.md` files have been setup for your specific package/project.

2. Set the `docs` folder as the gh-pages source in your repository settings. [See this Github help article for more information](https://help.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

3. Make changes to your documentation, in either the `./src/` or `./docsSrc/` directories.

4. Run `yarn build:docs` to generate new documentation in the `./docs/` directory.

5. Run `git commit -m "commit message here"`

6. Run `git push` to update the remote repository, and new changes to documentation will be live within several minutes.

**See [HERE](https://www.shaggytech.com/template-typescript-npm/index.html) for an example of the live documentation for this template package.**

---
---

# Testing your code (unit testing) with Jest

---

This template utilizes the NPM module [Jest](https://jestjs.io/) in order to test the code you write.

I encourage you to read through the Jest [Documentation](https://jestjs.io/docs/en/getting-started) if you're not familiar with how to test your code.

## Testing scripts included in this template

`yarn watch:test`

Runs Jest in watch mode with the --onlyChanged option flag, this will limit tests to only files that have changed since the most recent git commit.

`yarn test`

Runs all tests once.

`yarn watch`

Runs Jest in watch mode with the --onlyChanged option flag, concurrently with other dev watch scripts. Note that you won't be able to enter any commands to control jest, use 'yarn watch:test' if you need to enter jest commands:

---
---

# Building your package

---

This template utilizes the NPM module [Rollup](https://rollupjs.org/guide/en/) and various associated plugins in order to package your module into multiple formats (the 'universal' part of this template).

I encourage you to read through the Rollup [Documentation](https://) if you're not familiar with how to bundle your code.

The build outputs to `./dist/` and is controlled via the `rollup.config.ts` config file. 

By default this template is setup to output the following formats: `Default:UMD(Universal` - `CJS(CommonJS/Node)`  `ESM(ES Module)`  `IIFE(Browser)`. This and other options can be changed in the rollup config file.

A `types` folder is also output into `./dist/`, which will contain all of the Typescript type definition files (.d.ts) for your package. Change the output location in the `tsconfig.json` and/or `tsconfig.dev.json` Typesrcipt config files.

## Development Build

`yarn build:dev` or `yarn watch` or `yarn watch:rollup`

Will build the package with Rollup and output everything to `./dev/dist/`. A copy of the `./package.json` file will also be placed in the root of `./dev/` folder.

## Production Build

`yarn build`

Will build the package with Rollup and output everything to `./dist/`. The contents of that folder are what gets uploaded to NPM and Yarn when you publish your package.

---
---

# Publishing your package to NPM and YarnPkg

---

## Setup

> IMPORTANT:
**Make sure you have followed all of the steps in the Setup section of this document before proceeding!**

- Folow the steps listed [HERE](https://yarnpkg.com/lang/en/docs/publishing-a-package/) to get setup and ready to publish your package.  You will need to be logged in to NPM with your credentials to be able to publish a package.

- Make sure you've setup your root `package.json` file

- Make sure you've setup your root `README.md` file

## Release

It is advised that you commit and push all of your source code to your remote repository before running the `release` script. If done correctly, the last 2 commits in your remote repo, after publishing, should be `<vX.X.X>` and then `<new source code commit>`.

This is a final step and the version number you choose is permanent, once published it cannot be changed.  If you mess up or need to change something after publishing, you will have to bump the version (x.x.+1) by running `yarn release` again.

We recommend using the [yarn pack](https://yarnpkg.com/lang/en/docs/cli/pack/) or [yarn link](https://yarnpkg.com/lang/en/docs/cli/link/) commands to test local development before publishing.

You can also use the files found in the root `tests/` folder to test your Rollup output is correctly imported in various different scenarios before publishing.

**`yarn pack`** creates gzipped NPM package file

- creates a gzipped file identical to what will be uploaded to NPM as the final package contents. Use this to ensure you're uploading what you think you are to NPM, upon release.

**`yarn release`** to **publish** your package.

- This script will run `yarn build` before attempting to publish your package.
- You will be prompted to enter a new version number before publishing is completed. Once entered, the package.json "version" field will be changed to reflect the new version, saved, and git committed.
- After successfully publishing the package, `git push --tags` is run to push a commit to remote source with the new version as the commit name.

---
---
