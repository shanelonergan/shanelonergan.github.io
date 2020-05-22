---
layout: post
title: 'React's useContext in 3 minutes'
date: 2020-5-22
description: 'Access your state anywhere with a convenient hook'
img: hook.jpg
tags: [programming, terminal, bash] # add tag
---

---

Hooks are my personal favorite way to manage state in a React application. I prefer functional components over class components most of the time, and Hooks feel like a simple and effective extension of react itself. Now, if you are anything like me, you have probably found yourself endlessly passing state down as props until you feel like you are descending into madness. Luckily, there is a solution! `useContext` is a Hook which allows you to pass data throughout the competent tree without having to manually pass down props on each individual level.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [What are Hooks?](#what-are-hooks)
- [Getting started](#getting-started)
- [Create Context](#create-context)
- [Context Provider](#context-provider)

## What are Hooks?

Hooks are a new addition to React which let you use state and other features in functional components. If you have'nt used Hooks before, I would recommend first checking out the [docs](https://reactjs.org/docs/hooks-intro.html) to get familiar before diving in.

## Getting started

Lets say we have a logged-in user's information, and we want that information to available to us in any component. Below is a mock-up of a user object we received from our imaginary server:

```js
const user = {
    id: 1,
    name: "Shane",
    bio: "bio",
}
```

One important thing to note is that `useContext` is a Hook that only lets you access your context. You will need to set up that context using a few other React features.

## Create Context

The first step is create an instance of context for our application using `createContext`. For our purposed we will be writing all of our code in one file, but I have typically seen context declared in its own file, such as `UserContext.js`.

```javascript react
import React from 'react';

const UserContext = React.createContext(null)
```

## Context Provider

Next, we need to wrap all our components which will be accessing the context in a Context Provider. True to its name, this component provides the context to all of its children. Whenever the context data changes, it will pass down the changes and trigger a re-render.

```javascript react
import React from 'react';

const UserContext = React.createContext(null)

const App = () => (
    <UserConext.Provider>
        <NavBar />
        <Main />
    </UserConext.Provider>
)
```

Now both the NavBar and Main, as well as any children, will have access to the User Context.
