---
title: CSS
description: CSS
summary: "Updated by Fatma, May 31, 2023."
date: 31-05-2023
categories:
  - "Coding"
tags:
  - "css"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
comments: true
---

- A `viewport` represents the area in computer graphics being currently viewsed.
- `milisecond`
- `radian`
- `frequency`
- `resolution`
- `vh`:= 1/100 height
  - 1vh of ...x800 => 1x800/100 = 8 pixels
- `vw`:= 1/100 width
  - 1vw of 1280x... => 1x1280/100 = 17,8 pixels
- `vmin`:= 1/100 min(height, width)
  - 1vmin of 1280x800 => 1*800/100 = 8 pixels
- `vmax`:= 1/100 max(height, width)
  - 1vmax of 1280x800 => 1x1280/100 = 12,8 pixels

## Box model

- A box is everything displayed by CSS.
- Behaviour of a box changes depending on its `display` value, set dimensions, and its content.

- There are two ways of sizing in CSS:
  - _Extrinsic sizing_ determines sizes based on the context of an element, without regard for its contents. e.g. `<div></div>` has the width of 100% of its parent.
  
  ```css
  .style {
    width: 100px;
  }
  ```

  - _Intrinsic sizing_ means that the sizing of an element depends on its content size. The browser arranges based on the box's content size. e.g.
    - `min-content` means that it's equal to the width of the element's content longest word.
    - `max-content` means that it's equal to the width of the content.
    - `min-content <= fit-content <= max-content`

  ```css
  h1 {
    width: min-content;
  }
  ```

- When content is too big for the box it is in, we call this `overflow`. You can manage how an element handles overflow content, using the overflow property.
- Scrollbar will occupy space if `overflow: auto` or `overflow: scroll` set.
- Boxes are made up of distinct box model areas:
  1. **Margin box** is the space around the box. `outline` and `box-shadow` occupy the space. `margin` defines it.
  2. **Border box** surrounds the padding box. `border` occupies space.
  3. **Padding box** surrounds the content box. `padding` creates it.
  4. **Content box** is the area that the content lives in.

## Cascade and specificity

## Flexbox

## Grid

## z-index

## `container` vs. `wrapper`

- `container` contains more than one element.
- `wrapper` wraps around a single object to provide more functionality and interface to it.

```html
<body class="Site">
  <header></header>
  <main class="Site-content"></main>
  <footer></footer>
</body>
```

```css
.Site {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}
.Site-content {
  flex: 1;
}
```

## Selectors

### Universal selector

- It matches any element.

```css
* { style properties }
```

### Type selector

- A _type selector_ matches an HTML element directly.
- Type selectors can be namespaced when using `@namespace`.
  - `namespace` can be used to restrict the `universal`, `type`, and `attribute` selectors to only select elements within that namespace.

```css
element { style properties }
```

### Class selector

- It matches any element that has that class applied to it.

```css
.class-name { style properties }
```

### ID selector

- An HTML element with an `id` attribute should be the only element on a page with that ID value.

```css
#id_value { style properties }
```

### Attribute selector

- It matches elements based on the presence or value of a given attribute.

```css
a[title] {
  color: purple;
}
a[href="https://example.org"] {
  font-size: 2em;
}
```

### Grouping selector

- A selector doesn't have to match only a single element.

```css
element, element {
  style properties
}
```

## Pseudo-class

- It selects elements that are in a specific state.

- `:first-child`
- `last-child`
- `:invalid`

```css
article p:first-child {
    font-size: 120%;
    font-weight: bold;
}  
```

```html
<article>
    <p>First paragraph</p> <!-- p:first-child -->
    <p>Second paragraph</p>
</article>
```

## Pseudo-element

- It lets you style a specific part of the selected element(s). [Ref](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
- `::before` and `::after` are common.

```css
/* The first line of every <p> element. */
p::first-line {
  style properties
}
```
