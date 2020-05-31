---
layout: post
title:  "React's useReducer in 3 minutes"
date:   2020-5-22
description: 'Make complex state simple with Hooks'
img: hook.jpg
tags: [programming, terminal, bash] # add tag
---
---

Hello and welcome back to my series on React Hooks! If you missed the first post on useContext, feel free to check that out [here](). As I mentioned in that article, I love Hooks! They feel like a simple and effective extension of React itself, and I tend to prefer writing functional components over class components anyway. Now, if you are using Hooks to manage relatively simple state, the useState hook works great. In fact, I have used useState for all my state in a React application before. However, if you end up working with complex state logic with multiple sub-values, then you may want to check out useReducer! This Hook allows you to specify multiple actions for setting your state in different ways depending on the context.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [What are Hooks?](#what-are-hooks)
- [Getting Started](#getting-started)
- [Add `useReducer`](#add-usereducer)
- [Update the form](#update-the-form)
- [Congrats!](#congrats)

## What are Hooks?

Hooks are a new addition to React which let you use state and other features in functional components. If you haven't used Hooks before, I would recommend first checking out the [docs](https://reactjs.org/docs/hooks-intro.html) to get familiar before diving in.

## Getting Started

We are going to be using useReducer to handle the state for a form with multiple inputs. To begin, lets go ahead and set up a basic form component:

```js
// ReducerForm.js
import React from 'react'

export default function ReducerForm() {

	return (
		<form>
			<label>
				First Name:
                <input
                    type='text'
                    value={}
                    onChange={() => {}}
                />
			</label>
            <label>
				Last Name:
                <input
                    type='text'
                    value={}
                    onChange={() => {}}
                />
			</label>
            <label>
				Bio:
                <textarea
                    value={}
                    onChange={() => {}}
                />
			</label>
            <label>
                Favorite Fruit
                <select
                    value={}
                    onChange={() => {}}
                >
                    <option value="pineapple">Pineapple 🍍</option>
                    <option value="lemon">Lemon 🍋</option>
                    <option selected value="coconut">Coconut 🥥</option>
                    <option value="mango">Mango 🥭</option>
                    <option value="strawberry">Strawberry 🍓</option>
                    <option value="grapes">Grapes 🍇</option>
                </select>
            </label>
			<input type='submit' value='Submit' />
		</form>
	)
}
```
As you can see, this form allows a user to enter their first and last name, a bio, and select their favorite fruit. The `value` and `onChange` properties are currently blank, but we will fill those in as we build out our state. Now, we can begin adding `useReducer`.

## Add `useReducer`

The first step is to import useReducer at the top of our file. once we do that, we want to create an instance of our state and dispatch. State is just hat it sounds like, our state for this instance, and dispatch is a function that we call to change that state. We can create these like so:

```javascript
import React, { useReducer } from 'react'

const [state, dispatch] = useReducer(formReducer, initialState)
```

As you can see, it is initialized with 2 values, a reducer and the initial state. Lets start with our initial state:

```js
const initialState = {
        firstName: '',
        lastName: '',
        bio: '',
        faveFruit: ''
    }
```

As you can see, our initial state is an object with keys for each input in our form, and all values are empty strings. Next, we need to create our reducer. If you have any experience with Redux, this will look familiar. It is essentially a switch statement, but each case is an option for handling an individual piece of our state.

```js
 const formReducer = (state, {type, payload}) => {

    switch (type) {
        case 'firstName':
            return {...state, firstName: payload}
        case 'lastName':
            return {...state, lastName: payload}
        case 'bio':
            return {...state, bio: payload}
        case 'faveFruit':
            return {...state, faveFruit: payload}
        default:
            throw new Error()
    }
}
```

The reducer normally takes two arguments, state and action. In the above example, I destructured action into type and payload. Type will be a string determining which case will be hit, and payload will be the value to set the new state to. Now, all that is left is to update our form to take advantage of our reducer!

## Update the form

To make our form controlled by storing all values in our state, we can dispatch actions to our reducer in the onChange functions. We also want to set the value of the input to that same state value. For the first name input, it will look like this:

```jsx
<label>
    First Name:
    <input
        type='text'
        value={state.firstName}
        onChange={(event) => dispatch({type: 'firstName', payload: event.target.value})}
    />
</label>
```

We one argument to the dispatch function, and object containing the type and payload. This object is known as the action, which we destructure in our formReducer function. Just like that, you now have a controlled form with state managed by useReducer! Lets go ahead and finish updating the rest of the form:

```js
import React, { useReducer } from 'react'

export default function ReducerForm() {

    const initialState = {
        firstName: '',
        lastName: '',
        bio: '',
        faveFruit: ''
    }

    const formReducer = (state, {type, payload}) => {

        switch (type) {
            case 'firstName':
                return {...state, firstName: payload}
            case 'lastName':
                return {...state, lastName: payload}
            case 'bio':
                return {...state, bio: payload}
            case 'faveFruit':
                return {...state, faveFruit: payload}
            default:
                throw new Error()
        }
    }

    const [state, dispatch] = useReducer(formReducer, initialState)

	return (
		<form>
			<label>
				First Name:
                <input
                    type='text'
                    value={state.firstName}
                    onChange={(e) => dispatch({type: 'firstName', payload: e.target.value})}
                />
			</label>
            <label>
				Last Name:
                <input
                    type='text'
                    value={state.lastName}
                    onChange={(event) => dispatch({type: 'lastName', payload: event.target.value})}
                />
			</label>
            <label>
				Bio:
                <textarea
                    value={state.bio}
                    onChange={(event) => dispatch({type: 'bio', payload: event.target.value})}
                />
			</label>
            <label>
                Favorite Fruit
                <select
                    value={state.faveFruit}
                    onChange={(event) => dispatch({type: 'faveFruit', payload: event.target.value})}
                >
                    <option value="pineapple">Pineapple 🍍</option>
                    <option value="lemon">Lemon 🍋</option>
                    <option selected value="coconut">Coconut 🥥</option>
                    <option value="mango">Mango 🥭</option>
                    <option value="strawberry">Strawberry 🍓</option>
                    <option value="grapes">Grapes 🍇</option>
                </select>
            </label>
			<input type='submit' value='Submit' />
		</form>
	)
}
```

## Congrats!

You now know how to use useReducer! If you have any further questions, I would hight recommend reading the docs, as React's documentation is outstanding. Good luck with your projects!
