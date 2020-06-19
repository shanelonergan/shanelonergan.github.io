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

## Table of Contents
- [Table of Contents](#table-of-contents)
- [What is AOS?](#what-is-aos)
- [Install AOS](#install-aos)
- [Using AOS](#using-aos)
  - [Adding an animation](#adding-an-animation)
  - [Customize the animation](#customize-the-animation)
    - [Offset](#offset)
    - [Delay](#delay)
    - [Duration](#duration)
    - [Mirror](#mirror)
    - [Once](#once)
    - [Anchor Placement](#anchor-placement)
    - [Easing](#easing)
  - [Further Customizations](#further-customizations)
- [Congrats!](#congrats)


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

### Adding an animation

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

### Customize the animation

You can adjust the behavior of the animation by adding more `data-aos` attributes. Here are some examples:

#### Offset

```html
<div
    data-aos-offset='200'
>
</div>
```

Offset changes the distance (in pixels) from the original animation trigger point. This will essentially wait to trigger the animation until you scroll past the desired offset point. The default value is 120px.

#### Delay

```html
<div
    data-aos-delay='50'
>
</div>
```

Delay controls the amount of time (in ms) that will elapse after scrolling past the trigger point before the animation will trigger. The default value is 0ms, and you can increase in increments of 50ms.

#### Duration

```html
<div
    data-aos-duration='100'
>
</div>
```

Duration controls the amount of time (in ms) that the animation will take to run. This will essentially increase or decrease the speed of the animation. The default value is 400ms, and increments in 50ms intervals.

#### Mirror

```html
<div
    data-aos-mirror='true'
>
</div>
```

Mirror affects whether or not the elements should animate again on their way out of the viewport. The default value is false.

#### Once

```html
<div
    data-aos-once='true'
>
</div>
```

Once decides whether an animation should happen only one time, or every time an element is scrolled past. The default value is false.

#### Anchor Placement

```html
<div
    data-aos-anchor-placement='top-center'
>
</div>
```

Anchor placement defines which part of the element should trigger the animation. The default is `top-bottom`, and a full list of options can be found [here](https://github.com/michalsnik/aos#animations).

#### Easing

```html
<div
    data-aos-anchor-easing='ease-in-out'
>
</div>
```

Easing determines which easing function the animation should follow. Easing functions determine the rate of change for the speed of the animation over time. This [website](https://easings.net/) helps visualize some of the more complicated easings using graphs. A full list of easing options can be found [here](https://github.com/michalsnik/aos#animations).

### Further Customizations

AOS also allows you to add custom animations and easings, as well as integrate external animation libraries. To learn more bout these advanced features, feel free to check out the [docs](https://github.com/michalsnik/aos#recipes).

## Congrats!

You can now add awesome on-scroll animations to your React applications! Thank you for reading, and best of luck with your projects!
