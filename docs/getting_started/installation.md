---
id: installation
title: Australian Writers' Centre Theme
sidebar_label: Installation
---

The site is designed for [Australian Writers' Centre](https://www.writerscentre.com.au/). This documentation will only show you how to install and extend the theme, it will not show you how to install wordpress. For wordpress installation please refer to this [documentation](https://wordpress.org/support/article/how-to-install-wordpress/) instead.


## System Requirements
The theme has a few system requirements. Please see the list below.

 - PHP >= 7.2
 - Wordpress >= 5.4
 - Composer >= 1.6.5
 - NodeJS >= 8.x
 - Yarn >= 1.5
 - Webpack >= 4.x
 - Webpack-cli >=3.3.x

## Installing the theme

_A wordpress should already be installed._

The theme utilizes [Composer](https://getcomposer.org/) for the backend packages and [NPM](https://www.npmjs.com/get-npm) / [Yarn](https://classic.yarnpkg.com/en/docs/install/#windows-stable) for Frontend packages.
clone a copy of the theme in github, then install all asset requirements of the theme. 

If the cli requested to install webpack-cli, type <b>yes</b>

```
npm run build
```


## Verifying Installation

Navigate through the themes folder by going to wp-content/themes/australian-writers-centre-theme. The directory will contain a file structure similar to this -- files inside the sub-directories are not included:

```
australian-writers-centre-theme (theme root directory)
├── .babelrc
├── .gitignore
├── 404.php
├── composer.json
├── composer.lock
├── functions.php
├── package.json
├── package-lock.json
├── page-reviews.php
├── page-search.php
├── screenshot.png
├── scripts.js
├── style.css
├── style-mobile.css
├── webpack.config.js
├── assets
│   ├── backend/
│   └── frontend/
├── lib
│   ├── Classes/
│   ├── Helpers/
│   ├── Shortcodes/
│   ├── helper_functions.php
│   └── index.php
├── src
│   ├── backend/
│   └── frontend/
├── template
└── woocommerce
      
```

