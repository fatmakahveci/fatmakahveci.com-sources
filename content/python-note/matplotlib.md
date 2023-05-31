---
title: matplotlib
description: matplotlib
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
- The most popular python plotting and 2D data visualization library

## Install

`pip install matplotlib`

## Import

`import matplotlib.pyplot as plt`

## pyplot

- common plotting functions
- It mimics the behaviour of MATLAB.
- `fig, ax = plt.subplots()` creates a figure containing a single axes.
- `ax.plot(${array_variable_1}`, `${array_variable_2})` plots the data on the axes.

### 1. Figure

- It is the whole figure. It keeps track of all the child `Axes`.

```python
fig = plt.figure() # an empty figure with no Axes
fig, ax = plt.subplots() # a figure with a single Axes
fig, axs = plt.subplots(2, 2) # a figure with a 2x2 grid of Axes
```

### 2. Axes

- It is the plot. It is the region of the image with the data space.

```python
axes.Axes.set_xlim()
axes.Axes.set_ylim()
axes.Axes.set_title()
axes.Axes.set_x_label()
axes.Axes.set_y_label()
```

## Bring matplotlib to the browser: mpld3

`pip install mpld3`

[`fig_to_html()`](https://mpld3.github.io/modules/API.html#mpld3.fig_to_html) This is the core routine which takes a figure and constructs a string of HTML and JavaScript which can be embedded in any webpage.

[`save_html()`](https://mpld3.github.io/modules/API.html#mpld3.save_html) Save a figure to a stand-alone HTML file.
