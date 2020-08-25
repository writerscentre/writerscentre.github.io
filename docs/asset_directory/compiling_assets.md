---
id: compiling_assets
title: Compiling Assets
sidebar_label: Compiling Assets
---

# Introduction

The Webpack config has been setup with an existing boiler plate to compile SASS and VueJS. 

## Installation & Setup

Before starting, make sure that you have the NPM and webpack dependencies installed in your machine.

```
node -v
npm -v

webpack -v
webpack-cli -v
```

When executing `webpack -v` and the command-line prompts you to install `webpack-cli`, then type *yes*. If ever you are stuck with installing `webpack-cli` even after verifying the installation or seeing an error message that `webpack-cli is not defined`, try installing it globally first then install it locally.

```
npm install -g --save-dev webpack-cli
npm install --save-dev webpack-cli
```

## Running Webpack

To run [Webpack](https://webpack.js.org/) tasks you will need to execute one of the NPM scripts that is included in the <span style='color: #00B4CD'>`package.json`</span> file inside the theme folder.

```
// Run Webpack tasks
npm run dev

// Run Webpack tasks and minify output
npm run production
```


### Watching Assets for changes

The `npm run watch` will continute to compile assets and will watch relevant files for changes. Webpack will then recompile assets for any changes detected.

```
npm run watch
```
