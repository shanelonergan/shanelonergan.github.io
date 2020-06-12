---
layout: post
title:  "Getting started with React without using Create React App"
date:   2020-6-12
description: 'Create a basic React app with no build tooling'
img: hook.jpg
tags: [programming, terminal, bash] # add tag
---
---

React is is one of the most popular JavaScript frameworks used today. When first learning React, many developers jump straight into using Create React App (CRA). Now, there is nothing wrong with this, and that is how I learned to use React myself. However, React has actually been designed so that you can use as little or as much of it as you need. If you jump straight to CRA, you are also getting many tools such as Webpack, ESLint, Babel, testing setups, and more. For a simple application, or a website that doesn't need to be a Single Page Application (SPA), using CRA may be a bit overkill. Luckily, we can add small parts of React to our project as we go, increasing what we use as our needs increase. In this post I will walk through adding React to existing HTML file, including support for JSX.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [What are Hooks?](#what-are-hooks)
- [Getting started](#getting-started)
- [Adding State](#adding-state)
- [Use the State](#use-the-state)
- [Congrats!](#congrats)

## What are Hooks?
