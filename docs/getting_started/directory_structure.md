---
id: directory_structure
title: Directory Structure
sidebar_label: Directory Structure
---

# Introduction

The directory structure for the theme.


## The Root Directory

### The Library Directory

The <span style='color: #00B4CD'>`lib`</span> directory contains the extended core code of the website. almost all shortcode, helper classes and etc will be in this directory.


### The Assets Directory

The <span style='color: #00B4CD'>`assets`</span> directory contains all the compiled assets such as the CSS, and Javascript. Assets are separated by a sub-directory - `frontend` and `backend`.

### The Source Directory

The <span style='color: #00B4CD'>`src`</span> directory contains all raw, uncompiled assets such as SASS, Javascripts, and VueJS components. Assets are separated by a sub-directory - `frontend` and `backend`, and folders inside are separated by Javascript folder and Sass folder.

### The Woocommerce Directory

The <span style='color: #00B4CD'>`woocommerce`</span> directory contains the overwritten templates of [Woocommerce](https://woocommerce.com/). This is suggested way to extend or overwrite the existing template of woocommerce templates which can be found in the plugins directory.

### The Vendor Directory

The <span style='color: #00B4CD'>`vendor`</span> directory contains your [Composer](https://getcomposer.org/) dependencies.

### The Node Moduless Directory

The <span style='color: #00B4CD'>`node_modules`</span> directory contains your [NPM](https://www.npmjs.com/) dependencies.

## The Library Directory
