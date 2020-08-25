---
id: sass
title: Working with Stylesheet
sidebar_label: Stylesheet
---

# Introduction

[SASS](https://sass-lang.com/) is a css pre-processor used for writing large and complex stylesheet. SASS contains features that don't exist in CSS. To give the site and sass a much more cleaner and easier way to navigate and manage the css files, we use [BEMIT](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/). It is based on the **block-element-modifier** naming convention and **ITCSS**, a proposed method in structuring stylesheets. 

## Frontend

The `frontend/sass` folder contains all files for the frontend. The `app.scss` is configured to be the entry point where the `webpack.config.js` file will compile into the app.css inside `assets/frontend/css`.

The app.scss is divided into several folders `components`, `elements`, `objects`, `tools`, `utilities`, `variables`.

### Variables Folder

The `variables` folder contains all variable that the site is using like the colors, fonts, breakpoints and etc. The variables will help out to standardize the css elements and values.

### Tools Folder

The `tools` folder contains all mixins and functions for the SASS files.

### Elements Folder

The `elements` folder contains all base html elements styles. This should contain the normalization css, compatibility, and base css.

### Objects Folder

The `objects` folder contains all class patterns for generic elements like the .button, .list-item, .heading, and themes.

### Components Folder

The `components` folder contains all rich design UI that are not available in html elements alone. This includes, modal class, login interface, etc.

### Utilities Folder

The `utilities` folder contains all helpers, hacks and other utility functions. most !important tags are common inside this folder as it should overwrite the existing CSS attribute. The css class should be preceded by an underscore ( _ ).   

```
//Examples

._m-t--10 // margin-top: 10px;

._bg-color--red //background-color: red

```


## Backend

The Backend folder contains all files for the backend. The `app.scss` is configured to be the entry point where the compiled asset will then be placed inside `assets/backend/css` folder.

