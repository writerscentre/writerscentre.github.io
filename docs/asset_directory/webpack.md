---
id: webpack
title: Webpack
sidebar_label: Webpack
---

# Introduction

[Webpack](https://webpack.js.org/) is a module bundler designed to bundle files for the frontend, it offers features like minimizing, versioning of Javascript files.


## The Webpack config

`webpack.config.js` is a configuration file of [Webpack](https://webpack.js.org/), the file is located inside the theme folder `wp_config/themes/australian-writers-centre-theme`. The config is necessary for processing webpack.

### Entry point

The `entry` setting is the entry point where to start the bundling process.

```
  entry:  {
    //Website Frontend Sass and Javascript files
    
    'frontend/css/app': './src/frontend/sass/app.scss',
    'frontend/js/app': './src/frontend/js/app.js',

    //Website Backend Sass and Javascript files
    
    'backend/css/app': './src/backend/sass/app.scss',
    'backend/js/app': './src/backend/js/app.js',
  }
```

### Output

The `output` setting contains the set of options that will instruct webpack on where to output or write the compiled assets. 

```
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, './assets')
    },
```

### Module

The `module` settings determine on how the project should be compiled.

```
module: {
   rules:[    
        { // sass / scss loader for webpack
           test: /\.(sass|scss)$/,
           use: ExtractTextPlugin.extract({
             fallback: 'style-loader',
             use: [ 'css-loader', 'sass-loader' ]
           })
        },
   ]
}
```


