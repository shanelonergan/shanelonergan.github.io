---
layout: post
title:  "Loop the Loop"
date:   2020-1-19
description: 'Different ways to loop in JavaScript'
img: getElementsByClassName.png
tags: [programming, terminal, bash] # add tag
---
---

Loops. We all use them. Often one of the first things you learn in a programming language, loops can be used to solve for many purposes, from repeating something a specific number of times to enumerating through an array. In this article we will walk through the many different ways you can loop in JavaScript.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [`for` loops](#for-loops)
  - [Example](#example)
  - [`for...of`](#forof)
  - [`for..in`](#forin)
- [While loops](#while-loops)
  - [`do..while`](#dowhile)
  - [`while`](#while)
- [References](#references)

## `for` loops

A `for` loop continues until a given condition is false. The standard format of a `for` loop looks like this:

```js
for (inititalExpression; condition; incrementExpression) {
    statement
}
```

The initial expression evaluates before the first loop, and is usually used to set the value of a counter(a variable that will increment with each loop). The condition will be checked before each loop: if it evaluates as true, the loop will continue; if false, it will end. The increment expression is evaluated at the end of each loop, and is usually used to increment the counter. It is important to note the semicolons in the expression: they are not optional, and it is easy to mistakenly use commas instead, so beware.

### Example

```js
for (let i = 1; i <= 100; i++) {
    console.log(i)
}
```

`for` loops can also be used for array manipulation. We just have to set the initial counter to 0(since array indexes start at 0), and set the condition to check the length of the array.

```js
arr = [1, 2, 3, 4, 5, 6]

for (let i = 0; i <= arr.length; i++) {
    const current = arr[i]

    if (current % 2 === 0) {
        console.log(current)
    }

}
```

This loop will iterate though the array and print out only the even numbers. However, ES6 provides a more intuitive syntax for working with arrays, know as the `for..of` loop:

### `for...of`

```js
arr = [1, 2, 3, 4, 5, 6]

for (let number in arr) {

    if (number % 2 === 0) {
        console.log(current)
    }

}
```

This provides us with cleaner and more readable code compared to the traditional for loop. `for..of` works with both strings and arrays, but is not with key/value Objects. For those, we can utilize the `for..in` loop. This works similarly to the previous:

### `for..in`

```js
obj = {eggs: 2, milk: 1, apples: 6}

for (const key in obj) {

    console.log(`I need to get ${obj[key]} ${key}`)

}
```

This will print out the strings 'I need to get 2 eggs', 'I need to get 1 milk', etc. It is important to note that `for..in` runs in an arbitrary order, so if you need a defined sequence you should not use it. `for..in` can also be used with arrays, and the keys will be the index of each item.

## While loops

`while` loops are blocks of code that execute while a condition is true. These can take two forms, the `do..while` and `while` loops, but share the same basic structure. Each consists of a statement and a condition. The statement is executed for as long as the condition is true.

### `do..while`


```js
do
  statement
while (condition);
```

```js
let i = 1
do {
    console.log(i)
    i++
} while (i <= 5)
```

### `while`

```js
while (condition)
    statement
```

```js
let i = 1
while (i <= 5) {
    console.log(i)
    i++
}
```

If you enjoyed the article, feel free to follow me on medium [@sptlonergan](https://medium.com/@sptlonergan) and twitter [@shane__lonergan](https://twitter.com/shane__lonergan)

## References

- [MDN Docs: Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
- [JavaScript.info: Recursion and Stack](https://javascript.info/recursion)
- [MDN Docs: ParentNode.children()](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/children)
- [MDN Docs: HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)
- [Medium: Prototypes in Javascript - Rupesh Mishra](https://medium.com/better-programming/prototypes-in-javascript-5bba2990e04b)
