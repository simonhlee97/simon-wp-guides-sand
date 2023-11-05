---
title: Custom Queries
date: 2023-11-05
tags:
  - custom-queries
---
This post is about custom queries.
<!-- excerpt -->

## What is a "custom query"?

## When will I need it?

## Example

```php
$latestEvents = new WP_Query(array(
  'posts_per_page' => 2,
  'post_type' => 'event'
));

```