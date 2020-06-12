---
layout: post
title:  "Getting started with React without using Create React App"
date:   2020-6-12
description: 'Create a basic React app with no build tooling'
img: hook.jpg
tags: [programming, terminal, bash] # add tag
---
---

React is is one of the most popular JavaScript frameworks used today. When first learning React, many developers jump straight into using Create React App (CRA). Now, there is nothing wrong with this, and that is how I learned to use React myself. However, React has actually been designed so that you can use as little or as much of it as you need. If you jump straight to CRA, you are also getting many tools such as Webpack, ESLint, Babel, testing setups, and more. For a simple application, or a website that doesn't need to be a Single Page Application (SPA), using CRA may be a bit overkill. Luckily, we can add small parts of React to our project as we go, increasing what we use as our needs increase. In this post I will walk through creating a React app from scratch, including support for JSX.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Overview](#overview)
- [Part 1: HTML](#part-1-html)
- [Part 2: Add React](#part-2-add-react)

## Overview

For our code examples, we will be expanding on the Like Button example used in the React documentation. Our goal is to render a like button or dislike button based on whether or not it has been liked yet. To do this, we will use a functional component, the useState hook, JSX, and Babel for JXK Preprocessing. If you haven't used any of these tools before, feel free to check out the documentation, but don't be afraid to just dive in!

## Part 1: HTML

To get started, lets build out out HTML skeleton. In your directory, create a file called index.html, and fill that with an HTML skeleton. In the body, all we will need at first is a single div with the id of `like-button-container`. I am also going to add a header for display purposes.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>React without CRA</title>
  </head>
  <body>

    <h2>React without Create React App</h2>

    <div id="like_button_container"></div>

  </body>
</html>

```

## Part 2: Add React

We are going to add React through script tags. To do that, add the following lines of code right before the closing `</body>` tag. The first two load React into our project, and the last one will load the component that we will build in the next step.

```html
<!-- ... other HTML ... -->

        <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
        <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>

        <!-- Load our React component. -->
        <script src="LikeButton.js"></script>
    </body>
```

**Note:** If you are deploying your  application, make sure to replace "development.js" with "production.min.js".
