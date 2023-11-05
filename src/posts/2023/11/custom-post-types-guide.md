---
title: Custom Post Types Guide
date: 2023-11-06
tags:
  - custom-post-type
---
This is a quick "getting started" guide to custom post types, for developers who are new to creating themes and custom post types.
<!-- excerpt -->

You could create an action in your *functions.php* file, but if your CMS user(s) were to switch the theme, then that custom post type would no longer be accessible. Similarly, you could create a small plugin, but that could also be deactivated in the WP Admin.

Best practice would be to register your custom post types in a folder called "must use plugins", which live in their own dedicated folder, and are automatically activated. They cannot be deactivated from the WP Admin.

## Step 1 Register Custom Post Types

Create a folder called "mu-plugins". It should sit alongside your project's "plugins", "themes", "upgrade", etc directories. Then add a new file called (e.g.) "my-custom-post-types.php". Copy & paste the following code to that file.

```php
<?php

function my_custom_post_types() {
  register_post_type('event', array(
    'public' => true,
    'rewrite' => array('slug' => 'events'),
    'has_archive' => true,
    'show_in_rest' => true, # switches from Classic Editor to Block Editor
    'labels' => array(
      'name' => 'Events',
      'add_new_item' => 'Add New Event',
      'edit_item' => 'Edit Event',
      'all_items' => 'All Events',
      'singular_name' => 'Event'
    ),
    'menu_icon' => 'dashicons-hammer'
  ));
}
add_action('init', 'my_custom_post_types');
```

Visit the [WordPress docs](https://developer.wordpress.org/reference/functions/register_post_type/) to see a list of all the parameters that can be used with `register_post_type()`. 

## Step 2 Displaying Custom Post Types

You'll have to create a [custom query](/posts/2023/11/custom-queries) to display custom post types in your web page.


```php
$latestEvents = new WP_Query(array(
  'posts_per_page' => 2,
  'post_type' => 'event'
));

while($latestEvents -> have_posts()) {
  $latestEvents->the_post();
}
```