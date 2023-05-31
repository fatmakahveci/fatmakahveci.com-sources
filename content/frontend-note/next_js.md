---
title: Next.js
description: Next.js
summary: "Updated by Fatma, May 30, 2023."
date: 30-05-2023
categories:
  - "Coding"
tags:
  - "nextjs"
  - "react"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
comments: true
---

- `Next.js` is a web framework that gives you building blocks to create web applications.
- It handles the tooling and configuration needed for React.
- It provides additional structure, features, and optimizations for your app.

- **User Interface:** How users will consume and interact with your application
- **Routing:** How users navigate between different parts of your application
- **Data Fetching:** Where your data lives and how to get it
- **Rendering:** When and where you render static or dynamic content
- **Integrations:** What third-party services you use (CMS, auth, payments, etc) and how you connect to them
- **Infrastructure:** Where you deploy, store, and run your application code (Serverless, CDN, Edge, etc)
- **Performance:** How to optimize your application for end-users
- **Scalability:** How your application adapts as your team, data, and traffic grow
- **Developer Experience:** Your team's experience building and maintaining your application

## Document object model (DOM)

- `DOM` is an object representation of the HTML elements.
- It acts as a bridge between your code and the UI.
- It has a tree-like structure with parent and child relationships.
- With the DOM, we can use `JS` to interact with the objects and make changes to them.

## Pre-rendering

- `Next.js` has two forms of pre-rendering.
- You can create a hybrid app by using static generation for most pages and using server-side rendering for others.

### 1. Static generation

- The HTML is generated at build time and will be reused on each request.
- It is recommended whenever possible because your page can be built once and served by CDN, which makes it much faster than having a server render the page on every request.
- Marketing pages, blog posts, e-commerce product listings, documentation pages, etc. can use it.

### 2. Server-side rendering ([SSR](https://nextjs.org/docs/pages/building-your-application/rendering/server-side-rendering))

- If a page uses SSR, the HTML page is generated on each request.
- It will be slower than static generation, but the pre-rendered page will always be up-to-date.

## Pages

- A page is UI that is unique to a route.
- A page is always the leaf of the route subtree.
- `.js`, `.jsx` or `.ts` files can be used for pages.
- A `page.js` file is required to make a route segment publicly accessible.
- Pages are Server Components by default but can be set to a Client Component.
- Pages can fetch data. View the Data Fetching section for more information.

## Layouts

- A layout is UI that is shared between multiple pages.
- Any route segment can optionally define its own Layout. These layouts will be shared across all pages in that segment.
- `.js`, `.jsx` or `.ts` files can be used for layouts.
- A `layout.js` and `page.js` file can be defined in the same folder. The layout will wrap the page.

### Root Layout

- The `app` directory must include a root layout.
- The top-most layout is called the Root Layout. This required layout is shared across all pages in an application. Root layouts must contain `html` and `body` tags.
