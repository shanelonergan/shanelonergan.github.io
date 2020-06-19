---
layout: post
title: 'How to add animations on scroll in React'
date: 2020-4-24
description: 'Add a little flair to your React app using AOS'
img: grommet.png
tags: [programming, terminal, bash] # add tag
---

---

Scroll animations are one of my favorite style features to add to a website. They are a feature that, while relatively simple to add, can make your website feel much more slick and interactive. In this blog post, I am going to walk through adding scroll animations to a React application using the [AOS](https://github.com/michalsnik/aos) library.

## What is AOS?

AOS is an open source animate-on-scroll library made by [Michał Sajnóg](https://michalsnik.github.io/aos/). It was created to optimize performance by using all CSS for the animations themselves, and reserving JavaScript to handle the logic. It was made to be easy-to-use by providing HTML data attributes which you can add to any HTML element or React component, and is highly customizable. You can learn more by checking out the [website](https://michalsnik.github.io/aos/), [GitHub](https://github.com/michalsnik/aos), and codesandbox demos.

## Install AOS

The first step is to install AOS in you app using your preferred package manager. For the purposes of this post, we will be using npm. To do so, run the following command:

```bash
npm install --save aos@nex
```

Next, we need to import aos in our root file (likely `App.js`). This will require two imports, one for the CSS and one for the JavaScript:

```js
import AOS from 'aos';
import 'aos/dist/aos.css';
```

Now, we just need to initialize AOS. To do so, we can simply run `AOS.init()` inside of our root component. However, you can also pass the `.init()` function an optional settings object to customize the functionality to your liking. This settings object is described in the documentation, but for our purposes the default settings work just fine!

## Using AOS

Now we are ready to animate any pice of a component we want to! To do so, set your desired animation using the `data-aos` attribute like so:

```js
const divList = () => {
    return (
        // ... a bunch of divs
        <div
            data-aos='fade-up'
        >
            <p>I am animated!</p>
        </div>
    )
}
```

The library comes with a bunch of default animations, such as `fade`, `flip-up`, `slide-down`, `zoom-in`, etc. A full list of animations can be found [here](https://github.com/michalsnik/aos#animations).
