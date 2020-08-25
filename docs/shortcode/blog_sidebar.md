---
id: blog_sidebar
title: The Blog Sidebar Shortcode
sidebar_label: Blog Sidebar
---
# Description

> File location: lib\Shortcodes

**Class**: AWCBlogSidebarWidgetBase

# Methods

## __Construct

The constructor class. This class adds the Class functions into the shortcode.

```
// Line 55
public function __construct()
```

## Start

The `start` method bootstraps the whole class as a shortcode

```
// Line 60
public function start($atts = [])
    {
        $this->attributes = shortcode_atts([
            'categories' => '',
            'limit' => '',
            'id' => '',
        ], $atts);

        $this->id = $this->processID($this->attributes['id']);
        $this->limit = $this->attributes['limit'];
        $this->categories = $this->attributes['categories'];

        $this->helper = new CourseHelper();

        $this->courses = $this->getCourses();

        return $this->render();
    }
```

### Parameter

`$atts : array` The attributes that will be passed onto the shortcode. 

 **Accept**
 
 - *$id* - The ID of the post or product
 - *limit* - 
 - *categories* - 
 

### Return Type
String 

# Source

```
<?php

namespace AWC\Shortcodes;

use AWC\Helpers\CourseHelper;
use Carbon\Carbon;
use AWC\Shortcodes\Base\ShortcodeBase;

class AWCBlogSidebarWidget extends ShortcodeBase
{
    /**
     * ID of the product
     *
     * @var int|array
     */
    private $id;

    /**
     * Collection of attributes passed to the shortcode
     *
     * @var array
     */
    private $attributes = [];

    /**
     * Collection of courses that was retrieved based on the arguments passed
     *
     * @var array | object
     */
    private $courses;

    /**
     * Number of products to get
     *
     * @var int
     */
    private $limit;

    /**
     * Taxonomy in getting the product list: categories
     *
     * @var string
     */
    private $categories;


    /**
     * Helper Class for Courses
     *
     * @var CourseHelper
     */
    private $helper;

    public function __construct()
    {
        add_shortcode('awc_sidebar_products', array($this, 'start'));
    }

    public function start($atts = [])
    {
        $this->attributes = shortcode_atts([
            'categories' => '',
            'hubs' => '',
            'limit' => '',
            'order' => '',
            'orderby' => 'ASC',
            'id' => '',
        ], $atts);

        $this->id = $this->processID($this->attributes['id']);
        $this->limit = $this->attributes['limit'];
        $this->categories = $this->attributes['categories'];

        $this->helper = new CourseHelper();

        $this->courses = $this->getCourses();

        return $this->render();
    }

    /**
     * Method to save all course collection under the private "courses" variable,
     * this allows us to loop in courses easily based on the given parameters.
     *
     * @return array|false|\WC_Product|null
     */
    public function getCourses()
    {
        $courses = [];

        if( !is_null($this->id)){
            //Check if IDs are in groups or just a single ID.
            if( is_array($this->id ) ){
                foreach ($this->id as $id) {
                    $courses[] = wc_get_product($id);
                }
                return $courses;

            } else {
                return [wc_get_product($this->id)];
            }
        }

        if (!is_null($this->limit) || $this->limit <> "") {
            return wc_get_products($this->getQueryArgs());
        }
    }

    /**
     * Renders the frontend of the shortcode
     *
     * @return string
     */
    public function render()
    {
        $ohtml = "<div class='awc-blog-sidebar'>";
        $ehtml = "</div>";
        $html = "";

        //Loop in thru all courses
        foreach($this->courses as $course){

            //Check if the product is a variation or a simple product;
            $id = $course->variation_id <> "" ? $course->variation_id : $course->id;
            $parentCourse = wc_get_product($course->id);

            $is_displayed = get_post_meta($id,'_is_displayed_product')[0];

            if($is_displayed == "yes"){
                if($parentCourse <> "") {
                    $title = $parentCourse->get_title();
                    $image = get_the_post_thumbnail_url($course->id) <> ""
                        ? get_the_post_thumbnail_url($course->id)
                        : wc_placeholder_img_src();

                    if($course->variation_id <> ""){
                        $startDate = get_post_meta($id,'_start_date')[0] <> ""
                            ? Carbon::createFromFormat('l j F Y', get_post_meta($id,'_start_date')[0])->format('j F Y')
                            : get_post_meta($id,'_not_a_start_date')[0];
                    } else {
                        $startDate = get_post_meta($course->id,'variable-product-start-date')[0] <> ""
                            ? date('j F Y', strtotime( get_post_meta($course->id,'variable-product-start-date')[0]))
                            : get_post_meta($id,'_not_a_start_date')[0];
                    }

                    $shortStatus = get_post_meta($id, '_short_status')[0];

                    $permalink = get_permalink($course->id);
                    $price = $this->helper->getPrice($id);
                    $location = $course->variation_id <> "" ? get_post(get_post_meta($id, '_location')[0])->post_title : get_post(get_post_meta($id, 'location')[0])->post_title;

                    $html .= "
                    <a href='{$permalink}' class='awc-blog-sidebar__widget awc-blog-widget__{$id}' data-product-id='{$id}'>
                        <div class='awc-blog-sidebar__widget__image'>
                            <img src='{$image}' alt=''>
                        </div>
                        <div class='awc-blog-sidebar__widget__content'>
                            <div class='details'>
                                <p class='title'>{$title}</p>
                            </div>
                           
                            <div class='start-date'>
                                <p class='start-date'>Starts {$startDate}</p>
                            </div>

                        </div>
                    </a>
                ";
                }
            }
        }

        return $ohtml . $html . $ehtml;
    }

    /**
     * Return a fixed Args for WC_Get_products
     *
     * @return array
     */
    private function getQueryArgs()
    {
        return [
            'limit' => $this->limit,
            'include' => $this->id,
            'category' => $this->categories

        ];
    }
}
```


