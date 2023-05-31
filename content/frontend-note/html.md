---
title: HTML
description: HTML
summary: "Updated by Fatma, May 25, 2023."
date: 25-05-2023
categories:
  - "Coding"
tags:
  - "html"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
comments: true
---

## Head element

```html
<head>
    <meta charset="UTF-8">
    <meta name="author" content="fatma">
    <meta name="description" content="Page description">
    <title>Title</title>
    <link rel="icon" href="icon.png" type="image/x-icon">
    <link rel="stylesheet" href="main.css" type="text/css">
</head>
```

## Text basics

```html
<!-- Comment -->
<abbr title="Content Delivery Network">CDN</abbr> <!-- To display details -->
```

## List types

```html
<!-- Unordered list -->
<ul>
  <li>Coffee</li>
</ul>

<!-- Ordered list -->
<ol>
  <li>Coffee</li>
</ol>

<!-- Description list -->
<dl>
  <dt>Coffee</dt>
  <dd>- black hot drink</dd>
  <dt>Milk</dt>
  <dd>- white cold drink</dd>
</dl> 
```

## Meta

- `viewport` tells the browser to adapt the content to the size of the device.
- `width=device-width, initial-scale=1` establishes a one-to-one relationship between CSS and device-independent pixels.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## Adding breakpoints

- A breakpoint displays different styles depending on characteristics of the device, like device width or device pixel density.

## Media queries

- We can apply different styles using media queries, giving us a completely responsive experience.

```html
<link rel="stylesheet"
      media="(min-width: 500px)"
      href="min-500px.css">
```

```html
<style>
  @media (min-width: 500px)
</style>
```
