---
id: add_to_cart
title: The Add to Cart Button Shortcode
sidebar_label: Add to Cart Button
---

# Description

> File location: lib\Shortcodes

**Class**: AWCAddtoCartButton

# Methods

## __Construct

The constructor class. This class adds the Class functions into the shortcode.

```
// Line 43
public function __construct()
    {
        add_shortcode('awc_add_to_cart_button', array($this, 'start'));
    }
```

## Start

The `start` method bootstraps the whole class as a shortcode

```
// Line 49
public function start($atts = [])
{
    $this->attributes = shortcode_atts([
        'id' => '',
        'text' => "Add to Cart",
        'color' => 'red'
    ], $atts);

    $this->helper = new CourseHelper();
    $this->cartStatus = new CourseCartHelper();

    return $this->render();
}
```

### Parameter

`$atts : array` The attributes that will be passed onto the shortcode. 

 **Accept**
 
 - *id* - The ID of the post or product
 - *text* - Text attribute that will override the default text "Add to Cart"
 - *color* - Color attribute that will override the default button color "Red", the colours can be seen in the AWC settings in the backend.
 

## Render

The `render` method creates the HTML that will be shown in the frontend of the shortcode. This will create a button that will have the functionality to add the product ID that was passed in the attribute into the woocommerce shopping cart.

```
// Line 63
public function render()
{

    // Get the button properties
    $id = $this->attributes['id'];
    $text = $this->attributes['text'];
    $color = $this->identifyColor($this->attributes['color']);

    // Attach product Data and Cross sell Data from woocommerce   
    $productData = htmlspecialchars(json_encode($this->helper->get_basic_product_data($id)), ENT_QUOTES, 'UTF-8');
    $crossSells = htmlspecialchars( json_encode($this->helper->get_cross_sells($id)), ENT_QUOTES, 'UTF-8');

    // Create the HTML frontend
    $html =
        "<button type='button' class='product-var-add-to-cart {$color}'
            data-product-data
            data-product-variation-id='{$id}'
            data-product-data='{$productData}'
            data-cross-sells='{$crossSells}'>
            <span>{$text}</span>
        </button>";


    return $html;
}
```

## IdentifyColor

This method identify and returns the color that should be added as a class to the rendered HTML.

```
// Line 86 
private function identifyColor( $color )
    {
       return "btn-{$color}";
    }
```

### Parameters

### Return Type

# Source

```
<?php

namespace AWC\Shortcodes;

use AWC\Helpers\CourseHelper;
use AWC\Helpers\CourseCartHelper;
use AWC\Classes\AWC_Data;
use WC_Product_Variable;
use WC_AJAX;
use WC_Product;
use Carbon\Carbon;
use AWC\Shortcodes\Base\ICourseShortcode;


class AWCAddtoCartButton extends ICourseShortcode
{

    /**
     * Attributes accepted by the shortcode
     *
     * @var array
     */
    private $attributes = [];

    /**
     * Helper class for Course list
     *
     * @var CourseHelper
     */
    private $helper;

    /**
     * Helper Class for Course Cart
     *
     * @var CourseCartHelper
     */
    private $cartStatus;


    /**
     * AWCVariationList constructor.
     */
    public function __construct()
    {
        add_shortcode('awc_add_to_cart_button', array($this, 'start'));
    }

    public function start($atts = [])
    {
        $this->attributes = shortcode_atts([
            'id' => '',
            'text' => "Add to Cart",
            'color' => 'red'
        ], $atts);

        $this->helper = new CourseHelper();
        $this->cartStatus = new CourseCartHelper();

        return $this->render();
    }

    public function render()
    {
        $id = $this->attributes['id'];
        $text = $this->attributes['text'];
        $color = $this->identifyColor($this->attributes['color']);

        $productData = htmlspecialchars(json_encode($this->helper->get_basic_product_data($id)), ENT_QUOTES, 'UTF-8');
        $crossSells = htmlspecialchars( json_encode($this->helper->get_cross_sells($id)), ENT_QUOTES, 'UTF-8');

        $html =
            "<button type='button' class='product-var-add-to-cart {$color}'
                data-product-data
                data-product-variation-id='{$id}'
                data-product-data='{$productData}'
                data-cross-sells='{$crossSells}'>
                <span>{$text}</span>
            </button>";


        return $html;
    }


    private function identifyColor( $color )
    {
       return "btn-{$color}";
    }

}
```

