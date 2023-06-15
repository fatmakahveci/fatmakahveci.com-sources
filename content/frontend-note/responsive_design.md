---
title: Responsive design
description: Responsive design
summary: "Updated by Fatma, Jun 08, 2023."
date: 08-06-2023
categories:
  - "Coding"
tags:
  - "user interface"
  - "css"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
comments: true
---

- Three criteria for responsive design:
  1. Fluid grids
  2. Fluid media
  3. Media queries

## Liquid layouts

- It refers to a design approach where the elements on a web page sized using relative units rather than fixed units, allowing the content to dynamically adjust and adapt to different screen sizes and resolutions.

## Adaptive layouts

- Using CSS media queries, you can give people the layout that's closest to their browser width.

## A `meta` element for `viewport`

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## Media queries

- You can adapt your designs to different screen sizes using `CSS` media queries.
- `@media` keyword initiates media queries.

- Media queries work fine when you're applying changes to a few elements.

```css
@media (min-aspect-ratio: 16/9) {}
@media (max-aspect-ratio: 16/9) {}
@media (aspect-ratio: 16/9) {}

@media (orientation: portrait) {}
@media (orientation: landscape) {}

@media (min-resolution: 300dpi) {}
@media (max-resolution: 300dpi) {}
@media (resolution: 300dpi) {}

@media (update: fast) {
  a {
    transition-duration: 0.4s;
    transition-property: transform;
  }
  a:hover {
    transform: scale(150%);
  }
}
```

### Target different types of output

```css
body {
  color: black;
  background-color: grey;
}
@media print {
  body {
    background-color: transparent;
  }
}
```

#### Query conditions

- The `CSS` is applied only if the media
- The syntax for the media queries:= `@media type and (feature)`

```css
@media all and (orientation: landscape) {}
/* OR (orientation: portrait) */
```

### Adjust styles based on viewport size

```css
@media (min-width: 400px) {}
/* OR (max-width: 400px)*/
/* OR (min-width: 50em) and (max-width: 60em)*/
```

### Choose breakpoints based on the content

- `column-count` divides the text into two columns from that point on.

```css
@media (min-width: 50em) {
  article {
    column-count: 2;
  }
}
```

## Identify page language

```html
<html lang="en">
/* <html lang="en-us" */
```

## Identify a linked document's language

```html
<a href="/path/to/german/version" hreflang="de">German version</a>
```

## Hyphens

- It specifies how words should be hyphenated when text wraps across multiple lines.

```css
hyphens: none;
hyphens: manual;
hyphens: auto;
```

## CSS logical properties

- `block-start` represents the starting edge of a block-level element.
- `block-end` represents the ending edge of a block-level element.
- `inline-start` represents the starting edge of an inline-level element.
- `inline-end` represents the ending edge of an inline-level element.

```css
.example-element {
  block-start: 10px;
  block-end: 20px;
  inline-start: 5px;
  inline-end: 15px;
}
```

## Macro layouts

- They describe the page-wide organization of your interface.
- The single-column default ordering is what smaller screens will get.

## Grid

- CSS grid is an excellent tool for applying a layout to your page.
- A common layout in web design is a header, sidebar, body, and footer layout.

- A grid item is an item which is a direct child of the grid container.

```css
.container {
  display: grid;
  grid-template-columns: 5em 100px 30%;
  grid-template-rows: 200px auto;
  gap: 10px;
}
```

```html
<div class="container">
  <div class="item"></div>
  <div class="item"></div>
</div>
```

## Intrinsic sizing

- `min-content`:= as narrow as the longest word in the track.
- `max-content`:= as wide enough for all of the content to display in one long unbroken string.
- `fit-content()`:= once the track reaches the size that you pass into the function, the content starts to wrap.

## Flexbox

- `flex-direction` has the following properties:
  - `row`
  - `row-reverse`
  - `column`
  - `column-reverse`

- **Main axis** is set by `flex-direction`.
- **Cross axis** runs in the other direction to the main axis.

- Flex items move as a group on the main axis.
- You can move items individually or as a group.

```css
.container {
  display: flex;
}
```

```html
<div class="container" id="container">
  <div></div>
</.div>
```

## UI patterns

- Some interface elements may need to look quite different depending on the context they're viewed in.

## Typography

- The text will be resizable if you mix in a relative unit—like `em`, `rem` or `ch`.

```css
html {
  font-size: calc(0.75rem + 1.5vw);
}

article {
  max-inline-size: 66ch; // |ads..asd|
  line-height: 1.65;
}
blockquote {
  max-inline-size: 45ch;
  line-height: 2;
}

@font-face {
  font-family: Roboto;
  src: url('/fonts/roboto-regular.woff2') format('woff2');
}
```

---

- [Ref](https://web.dev/learn/design/)
