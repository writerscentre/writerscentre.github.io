---
id: asset_directory
title: The Assets Directory
sidebar_label: The Assets Directory
---
# Introduction

The site has two asset directories, the <span style='color: #00B4CD'>`assets`</span> and <span style='color: #FE2F4B'>`src`</span>. The <span style='color: #FE2F4B'>`assets`</span> directory contains all compiled scripts and styles. While the <span style='color: #FE2F4B'>`src`</span> directory contains all raw scripts and styles.

The site uses [webpack](https://webpack.js.org/) to compile assets, the webpack config is located under `wp-content/themes/<theme_directory>/webpack.config.js` 

## CSS

Before compiling your CSS, install your project's frontend dependency using [NPM](https://www.npmjs.org/)

```
npm install
```

Once the dependencies have been installed using <span style='color: #00B4CD'>`npm install`</span>, you can compile your SASS files to plain css using [webpack](https://webpack.js.org/). The `npm run build` command will process the instructions inside the webpack.config.js file. The compiled CSS will be placed inside the its designated folder under assets/<span style='color: #00B4CD'><frontend/backend></span>/css directory.

```
npm run build
```

The <span style='color: #00B4CD'>app.scss</span> under frontend or backend directories serves as an entry point for the <span style='color: #00B4CD'>webpack.config.js</span> to compile the css. the app.scss should contain all imports such as SASS variables, css components, objects, and etc.

## Javascript

All of the Javascript dependencies required by the website can be found in package.json under the theme directory. Since the way wordpress works is that all public files are contained inside the theme directory, we must navigate to `wp-content/themes/australian-writers-centre-theme`. Install the dependencies using [NPM](https://www.npmjs.org/)

```
npm install
```

Once the packages are installed, you can use npm run build dev-build command so that webpack can start compiling the Javascript. Webpack is a bundler that will execute the instructions given inside `webpack.config.js`

By Default, `webpack.config.js` compiles your app.scss SASS file that are located inside the frontend and backend directories of the source folder. While in Javascript, the `webpack.config.js` compiles the app.js inside the frontend and backend of the JS folder inside the source directory.
