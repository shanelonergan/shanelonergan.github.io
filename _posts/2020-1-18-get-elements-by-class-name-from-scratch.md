---
layout: post
title:  "Building JavaScript From Scratch"
date:   2020-1-19
description: 'Part 1: document.getElementsByClassName'
img: getElementsByClassName.png
tags: [programming, terminal, bash] # add tag
---
---

I am currently diving into my first job search as a software engineer, and recently had a mock technical interview. The interview was done in JavaScript, and consisted of two questions. The first was a fairly standard algorithm question, but the second was quite interesting: I was asked to build the `document.getElementByClassName` method from scratch, as if it didn't exist. I found it enlightening to build out a method that I had used so many times before, and improved my understanding of both DOM manipulation and Javascript as a whole. In this article I will walk you through the solution I came up with.;

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Goal](#goal)
- [Example](#example)
- [Plan](#plan)
- [Code](#code)
  - [Step 1: Set up the main function](#step-1-set-up-the-main-function)
  - [Step 2: Write the recursive helper function](#step-2-write-the-recursive-helper-function)
  - [Step 3: Put it all together](#step-3-put-it-all-together)
  - [Step 4: Add to the HTML Element prototype](#step-4-add-to-the-html-element-prototype)
- [References](#references)

## Goal

The goal is to create a functionally equivalent version of [`document.getElementByClassName`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName). In order to do this, our new function needs to have to following features:

1. Can be called on any HTML element
2. Takes one argument, a string, containing any number of class names.
3. Returns all elements that match all the class names passed in.
4. Returns only elements that are children of the element the function was called on

## Example

```html
<html>
<body>
    <div class='parent'>
        <p class='hello'>hello world 1</p>
        <p class='hello'>hello world 2</p>
        <p class='hello'>hello world 3</p>
        <p class='hello'>hello world 4</p>
    </div>
</body>
</html>
```

```javascript
const parent = document.getElementsByClassName('parent')
// =>    <div class='parent'></div>

const helloWorlds = document.getElementsByClassName('hello')
// => [  <p class='hello'>hello world 1</p>,
//       <p class='hello'>hello world 2</p>,
//       <p class='hello'>hello world 3</p>,
//       <p class='hello'>hello world 4</p>  ]
```

## Plan

First, we need to create a conceptual plan for our function:

1. Create an array to store all the elements that are a match.
2. Check all direct descendants of the main element for the class name
   1. if any do, add them to the array
3. Check all of those children's children the same way
4. Repeat until there are no more children

Based on this plan, we will need to create a recursive helper function, or a function that calls itself within its own definition, to check all elements beneath the primary. We will call this helper function within the main function. The return value of the main function should be an array of elements, which we will declare as an empty array at the top, and add elements to as we move along.

Now that we have a solid plan, let's get coding!

## Code

### Step 1: Set up the main function

Here we will define our main function. In the body, we will define two variables: `elements`, an array into which all elements with matching class names will be added; `firstChildren`, all the children of the element the function is called on. For the latter, we can take advantage of JavaScript's [`.children()`](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children) method, which returns an [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection) containing all child elements of the node upon which it is called. This HTMLCollection can be treated like an array.

```js
function getElementsByClassName2(classNameStr) {

   const elements = [] // the array we will add matching elements to
   const firstChildren = this.children // all the children of the element the function is called on

   return elements
}
```

### Step 2: Write the recursive helper function

A [recursive function](https://javascript.info/recursion) is a function which calls itself within the definition, while a helper function is a function which abstracts away some code to make it both re-usable and more readable.

```js
function getElementsByClassName2(classNameStr) {

   function checkChildren(child) {

      // check if the child has a matching class. If so, push the the elements array
      if (child.classList.contains(className)) {
         elements.push(child)
      }

      // check if that child has children of its own. If so, call checkChildren one each child
      if (child.children) {
         const children = child.children
         children.forEach(checkChildren)
     }
   }

}
```

### Step 3: Put it all together

Now we want to call the `checkChildren` method on each of the `firstChildren`. After this function runs, our elements array should contain all of the matching elements!

```js
function getElementsByClassName2(classNameStr) {

   const elements = []
   const firstChildren = this.children

   function checkChildren(child) {

      if (child.classList.contains(className)) {
         elements.push(child)
      }

      if (child.children) {
         const children = child.children
         children.forEach(child => checkChildren(child))
     }
   }

   // call the checkChildren method on the firstChildren
   firstChildren.forEach(child => {
      checkChildren(child)
   })

    return elements
}
```

### Step 4: Add to the HTML Element prototype

Finally, in order for us to be able to call this function on any HTML Element, we need to add it to the HTML element [prototype](https://medium.com/better-programming/prototypes-in-javascript-5bba2990e04b).

```js
HTMLElement.prototype.getElementsByClassname2 = getElementsByClassName2
```

And just like that, we are done! Our new method `getElementsByClassName2` now has the same functionality as the original `getElementsByClassName`. I hope you found this process as interesting and informative as I did!

If you enjoyed the article, feel free to follow me on medium [@sptlonergan](https://medium.com/@sptlonergan) and twitter [@shane__lonergan](https://twitter.com/shane__lonergan)

## References

- [MDN Docs: Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [JavaScript.info: Recursion and Stack](https://javascript.info/recursion)
- [MDN Docs: ParentNode.children()](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)
- [MDN Docs: HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)
- [Medium: Prototypes in Javascript - Rupesh Mishra](https://medium.com/better-programming/prototypes-in-javascript-5bba2990e04b)
