---
id: base_shortcode
title: The Shortcode Base Class
sidebar_label: Shortcode Base Class
---
# Description

> File location: lib\Shortcodes\Base

**Class**: Shorcode_Interface

**Type**: Abstract

The Abstract class of the shortcode. This class will provide extendable functions for the shortcode.

# Methods

## Start

The abstract method for `start`.

```
//Line 15
abstract public function start($atts = []);
```

### Parameters

`$atts : array` The attribute that will be passed onto the shortcode


### Return Type
String | HTML

---

## Render

The abstract method for `render`.

```
//Line 20
abstract public function render();
```

### Return Type
String | HTML


## ProcessID

This method processes the ID that is passed inside the `$atts` property. It checks whether the passed ID is a single or multiple IDs. It returns an array of ID that has been checked for existence inside WP or the ID itself.
```
//Line 26
public function processID( $id )
```

### Parameters

`$id : int | array` Post or a product ID


#### Return Type
int | array

---

## Exists

This method checks the existence of the ID that has been passed inside the ProcessID method. if the ID does not exists, it deletes the ID inside the the array so that it will not be included later on in processing the whole shortcode.

```
public function exists( $id)
     {
         $IDs = explode(',', $id);
         $ctr = 0;
         foreach($IDs as $ID){
             if( ! get_post_status( $ID ) ) {
                 array_splice($IDs, $ctr, 1);
             }
             $ctr++;
         }
         return $IDs;
     }
```

### Parameters

$atts : array


#### Return Type
String

---

# Source

```
<?php

namespace AWC\Shortcodes\Base;

use AWC\Shortcodes\Base\Shortcode_interface;

abstract class ShortcodeBase implements Shortcode_interface{

    /**
     * @param array $atts
     * @return mixed
     */
    abstract public function start($atts = []);

    /**
     * @return mixed
     */
    abstract public function render();

    /**
     * @param $id
     * @return array
     */
     public function processID($id)
     {
         return (strpos($id, ',') !== false)
             ? $this->exists($id)
             : $id ;
     }

    /**
     * Check existence of ID in wordpress
     *
     * @param $id
     * @return array
     */
     public function exists( $id)
     {
         $IDs = explode(',', $id);

         $ctr = 0;
         foreach($IDs as $ID){

             if( ! get_post_status( $ID ) ) {
                 array_splice($IDs, $ctr, 1);
             }

             $ctr++;
         }

         return $IDs;
     }
}

```
