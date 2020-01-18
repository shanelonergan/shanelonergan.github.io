---
layout: post
title:  "Build document.getElementsByClassName From Scratch"
date:   2019-10-17
description: tbdß # Add post description (optional)
img: streak.jpg
tags: [programming, terminal, bash] # add tag
---
---

I am currently diving into my first job search as a software engineer, and so I recently had a mock technical interview. The interview was done in Javascript, and consisted of two questions. The first was a fairly standard algorithm question, but the second was quite interesting. I was asked to build the `Document.getElementByClassName` method from scratch, as if it didn't exist. I found it enlightening to build out a method that I had used so many times before, and improved my understanding of both DOM manipulation and Javascript as a whole. In this article I will walk you through the solution I came up with.

## Table of Contents

- [Table of Contents](#table-of-contents)
  - [Goal](#goal)
- [Example](#example)
  - [GitHub Gist](#github-gist)
  - [References](#references)

### Goal

The goal is to create a functionally equivalent version of [`Document.getElementByClassName`cc](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName). In order to do this, our new method needs to have to following functions:

1. Can be called on and HTML element
2. Takes an argument, a string, containing any number of class names.
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
// => <div class='parent'></div>

const helloWorlds = document.getElementsByClassName('hello')
// => [  <p class='hello'>hello world 1</p>,
//       <p class='hello'>hello world 2</p>,
//       <p class='hello'>hello world 3</p>,
//       <p class='hello'>hello world 4</p>  ]
```

###

### GitHub Gist

<script src="https://gist.github.com/shanelonergan/b86a6704ca1e7d7c9a4a610c8f363ee6.js"></script>

### References

- [MDN Docs: Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [Active Record Basics](https://guides.rubyonrails.org/active_record_basics.html)
- [What is an ORM and Why You Should Use it](https://blog.bitsrc.io/what-is-an-orm-and-why-you-should-use-it-b2b6f75f5e2a)
- [What is a Ruby Reducer?](https://mixandgo.com/learn/what-is-a-ruby-reducer)
- [Scopes for belongs_to](https://edgeguides.rubyonrails.org/association_basics.html#scopes-for-Belongs-to)
