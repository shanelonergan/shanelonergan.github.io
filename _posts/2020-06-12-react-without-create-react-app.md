---
layout: post
title:  "Getting started with React without using Create React App"
date:   2020-6-12
description: 'Create a basic React app with no build tooling'
img: react.png
tags: [programming, terminal, bash] # add tag
---
---

React is is one of the most popular JavaScript frameworks used today. When first learning React, many developers jump straight into using Create React App (CRA). Now, there is nothing wrong with this, and that is how I learned to use React myself. However, React has actually been designed so that you can use as little or as much of it as you need. If you jump straight to CRA, you are also getting many tools such as Webpack, ESLint, Babel, testing setups, and more. For a simple application, or a website that doesn't need to be a Single Page Application (SPA), using CRA may be a bit overkill. Luckily, we can add small parts of React to our project as we go, increasing what we use as our needs increase. In this post I will walk through creating a React app from scratch, including support for JSX.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Overview](#overview)
- [Part 1: HTML](#part-1-html)
- [Part 2: Add React](#part-2-add-react)
- [Part 3: Create our React Component](#part-3-create-our-react-component)
- [Part 4: Add Babel](#part-4-add-babel)
- [Congrats!](#congrats)

## Overview

For our code examples, we will be expanding on the Like Button example used in the React documentation. Our goal is to render a like button or dislike button based on whether or not it has been liked yet. To do this, we will use a functional component, the useState hook, JSX, and Babel for JXK Preprocessing. If you haven't used any of these tools before, feel free to check out the documentation, but don't be afraid to just dive in!

## Part 1: HTML

To get started, lets build out out HTML skeleton. In your directory, create a file called index.html, and fill that with an HTML skeleton. In the body, all we will need at first is a single div with the id of `like_button_container`. I am also going to add a header for display purposes.

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

## Part 3: Create our React Component

Create a folder in your directory called `src`, and inside that folder add a file called` LikeButton.js`. In that file, we are going to define a functional component which has two outputs, depending on the `liked` state. First, lets create an empty component, and add state using `useEffect`. If you haven't used this before, it is a React Hook which allows us to utilize state in functional components.

```js
// src/LikeButton.js
const LikeButton = () => {
	const [liked, setLiked] = React.useState(false)

	return <button onClick={() => setLiked(true)}>Like</button>
}
```

In the above, useState gives us tow variables: `liked` and `setLiked`. `liked` is our state, ad we set the default value to false. `setLiked` is functionally equivalent to `setState`; it is a function which lets us change the value of `liked`. Our component returns a button with an onClick function which sets the state of `liked` to true.

Next, we want to change what this component renders when `liked` is true! To do that, we can create a conditional which, when `liked` is true, returns a sentence letting the user know they liked it, and a button to unlike.

```js
// src/LikeButton.js
const LikeButton = () => {
	const [liked, setLiked] = React.useState(false)

	if (liked) {
		return (
			<div>
				<p>You liked this.</p>
				<div>
					<button onClick={() => setLiked(false)}>Unlike</button>
				</div>
			</div>
			)
	}

	return <button onClick={() => setLiked(true)}>Like</button>
}
```

Finally, we need to append this component to our page! To do so, we will find our div with the id `like_button_container` using `document.querySelector`, and then append our component using `ReactDOM.render`. Our final component should look like this:

```js
const LikeButton = () => {
	const [liked, setLiked] = React.useState(false)

	if (liked) {
		return (
			<div>
				<p>You liked this.</p>
				<div>
					<button onClick={() => setLiked(false)}>Unlike</button>
				</div>
			</div>
			)
	}

	return <button onClick={() => setLiked(true)}>Like</button>
}

let domContainer = document.querySelector('#like_button_container')
ReactDOM.render(<LikeButton />, domContainer)

```

Note that we are using JSX in our component. JSX is a tool which allows us to use HTML syntax in our JavaScript code. However, this isn't supported in our application yet, as the browser isn''t able to read JSX. To remedy this, we will add a JSX preprocessor which will compile our code into a file readable by the browser.

## Part 4: Add Babel

In order to add Babel as our JSX preprocessor, we first need to make sure we have Node installed. You can do that by following downloading it [here](https://nodejs.org/en/download/).

Next, we need to initialize our project with NPM. To do so, run the following commands:

```bash
npm init -y
npm install babel-cli@6 babel-preset-react-app@3
```

This should create `package.json` and `package-lock.json` files in your directory, and well as a `node_modules` folder.

> **Tip:** If you are using git for version control, I would recommend adding `node_modules` to your `.gitignore` file.

Once you have completed the above, go ahead and run the following command in your terminal:

```bash
npx babel --watch src --out-dir . --presets react-app/prod
```

This command will not finish; it is watching your files in the `src` folder for JSX, and compiling it into plain JavaScript. You should see a new file called `LikeButton.js` appear in your directory. This is different than the one in the `src` folder, as it contained the newly compiled version of our component. If you recall, this is the file that we linked to in out script tag in `index.html`.

Babel also gives us access to modern JavaScript features such as classes, destructuring, arrow functions, and more, without having to worry about browser compatibility! It is a really awesome tool, and you can learn more about it in the [documentation](https://babeljs.io/docs/en/babel-cli/).

## Congrats!

You now know how to set up a basic React app using just React and Babel! Thank you so much for reading, I hope you found this post helpful. Good luck with your projects!
