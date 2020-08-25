---
id: shortcode_interface
title: The Shortcode Interface
sidebar_label: Shortcode Interface
---
# Description

> File location: lib\Shortcodes\Base

**Class**: Shorcode_Interface

**Type**: Interface

The interface class of the shortcode. This class will force the development to inherit the base classes for creating a shortcode.


# Methods

## Start

```
// Line 8
public function start(); : String
```

### Parameters

`$atts : array` The attribute that will be passed onto the shortcode

### Return Type
String | HTML

## Render

```
//Line 10
public function render() : String | HTML
```

### Return Type
String | HTML

# Source

```
<php

namespace AWC\Shortcodes\Base;

interface Shortcode_Interface {


    public function start($atts=[]);

    public function render();


}
```

