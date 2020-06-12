---
layout: post
title:  "React's useState in 4 minutes"
date:   2020-6-5
description: 'React state made easy using Hooks'
img: hook.jpg
tags: [programming, terminal, bash] # add tag
---
---

Hello and welcome back to my series on React Hooks! If you missed the first post on useContext, feel free to check that out [here](https://shanelonergan.github.io/react-use-reducer/). As I mentioned in that article, I love Hooks! They feel like a simple and effective extension of React itself, and I tend to prefer writing functional components over class components anyway. Previously, if a component needed to use state, you had to write it as a class component. Then, in order to access the state, you had to write out clumsy lines such as `this.state.user.name`. With Hooks, this process is much simpler. In this post I will walk you through the Hook that lays the foundation for all others, `useState`.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [What are Hooks?](#what-are-hooks)
- [Getting started](#getting-started)
- [Adding State](#adding-state)
- [Use the State](#use-the-state)
- [Congrats!](#congrats)

## What are Hooks?

Hooks are a new addition to React which let you use state and other features in functional components. If you haven't used Hooks before, I would recommend first checking out the [docs](https://reactjs.org/docs/hooks-intro.html) to get familiar before diving in.

## Getting started

For our example, we are going to make a input where a user can enter text, and that text will be displayed as a header at the top of the page. This will introduce the useState hook, and also apply it to a controlled form. This tutorial will be working from a starter app created using [Create React App](https://create-react-app.dev/), but you can also follow along in any existing React application.

Let's begin by setting up our component. We will create an input, where the user will enter their text, and then a header where we will eventually display that text.

```js
// App.js
import React from 'react'

function App() {
    return (
        <div className='App'>
            <h1>Header Text</h1>
            <div>
                <input
                    type="text"
                    name="header-input"
                />
            </div>
        </div>
    )
}

export default App
```

## Adding State

Now lets add our state! The first step is to import the useState hook at the top of our component. Once we do that, we can create a new state instance by calling useState:

```js
// App.js
import React, { useState } from 'react'

function App() {
    const [headerText, setHeaderText] = useState('Header Text')

    // ...
    )
}
```

If you haven't used destructuring before, this syntax may look a bit strange. We are creating a variable and setting it equal to the return value of the function `useState`. This function returns an array with two values: the first is the state, and the second is a function you can call to update that state. So instead of having to do something like `stateArray[0]` to access the state, we can use array destructuring. This create two variables we can give descriptive names, helping our code be more readable and clear. The `useState` function also accepts an argument, which is the initial value of our state. Here, we are setting it to the placeholder string 'Header Text', but you could set it to any string you like.

## Use the State

Now, all we need to do to utilize that state is set the value of our `h1` tag to `headerText`, do the same with the input value, and create a function to handle the user's input. This function will use `setHeaderText` to update the state to that input.

```js
function App() {
    const [headerText, setHeaderText] = useState('Header Text')

    return (
        <div className='App'>
            <h1>{headerText}</h1>
            <div>
                <input
                    type="text"
                    name="header-input"
                    value={headerText}
                    onChange={(event) => setHeaderText(event.target.value)}
                />
            </div>
        </div>
    )
}
```

## Congrats!

You now know how to implement the `useState` Hook! If you are coding along, the result should look something like this:

![gif](https://gph.is/g/ZWrOgMD)

Thank you so much for reading, and good luck with your projects!
