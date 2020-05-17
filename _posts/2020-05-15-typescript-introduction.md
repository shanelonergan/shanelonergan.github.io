---
layout: post
title: 'TypeScript in a Weekend'
date: 2020-5-15
description: 'A crash course in the basics of the hottest development language'
img: TypeScriptImage.jpeg
tags: [programming, terminal, bash] # add tag
---

---

I am in the midst of searching for my first job as a developer, and I recently interviewed at a company for which I thought I would be a great fit. However, the job description said that most of the code is written in TypeScript. Now, I have heard a lot about TypeScript from other developers, but I hadn't had the chance to start learning it. I figured this was the perfect chance to take the plunge! I had an open weekend before the interview, so I decided to see how much I could learn. In this post I will walk through what I discovered: the basics of TypeScript, as well as some of the benefits it offers over JavaScript. The goal of this guide is to provide enough knowledge to be conversational, as well as to give a strong jumping off point if you were to start learning TypeScript on the job.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [What is TypeScript?](#what-is-typescript)
- [Why TypeScript?](#why-typescript)
- [Getting Started](#getting-started)
- [Core Types](#core-types)
  - [Number](#number)
  - [String](#string)
  - [Boolean](#boolean)
  - [Array](#array)
  - [Tuple](#tuple)
  - [Enum](#enum)
  - [Any](#any)
  - [Null and Undefined](#null-and-undefined)
  - [Never](#never)
  - [Object](#object)
- [Union Types and Aliases](#union-types-and-aliases)
- [Interfaces](#interfaces)
- [Congrats](#congrats)
- [References](#references)

## What is TypeScript?

TypeScript is a superset of JavaScript that horizontally compiles back to JavaScript. It provides the ability, among other things, to strongly type your JavaScript code. However, TypeScript files can't actually be run in the browser or Node. So, why is this useful?

## Why TypeScript?

TypeScript helps you avoid unwanted runtime errors by type-checking during development. TypeScript files are compiled into JavaScript files which can then be run in the browser or Node. The compiler catches bugs in advance, saving time and frustration during debugging down the line. TypeScript improves code clarity by explicitly defining the types of variables, function parameters, and function outputs. This allows you to tell at a glance exactly what your code should be taking and returning, and the compiler will throw an error if you accidentally pass something to a function that you shouldn't be. The TypeScript compiler also allows you to customize what version of JavaScript your TS files compile to. This allows the developers to utilize many newer features of JavaScript without worrying about browser compatibility. Because of this, TypeScript can also offer features such as generics, enums, and interfaces which are not available in JavaScript. Additionally, TypeScript offers fantastic tooling in modern IDE's such as VS Code that can catch errors while the code as being written, saving even more time debugging.

## Getting Started

Lets go ahead and dive right in by analyzing our first piece of TypeScript code:

```TypeScript
const name = 'Shane'
let age = 24

function printNameAndAge(person: string, ageInYears: number): void {
    console.log(`${person} is ${ageInYears} years old.`)
}

printNameAndAge(name, age)
```

Now, you might be thinking to yourself, "That looks a lot like JavaScript...". Well, thats because it is! Vanilla JavaScript is totally valid in TypeScript. All of the features are optional to use, and exactly how they are utilized is up the the developer. Of course, you aren't getting any of the benefits of TypeScript by doing this, so lets add a little bit to it:

```TypeScript
const name: string = 'Shane'
let age: number = 24

function printNameAndAge(person: string, ageInYears: number): void {
    console.log(`${person} is ${ageInYears} years old.`)
}

printNameAndAge(name, age)
```

As you can see, you can add type annotations after variable declarations or within function parameters using a colon (`:`) followed by the type. The `void` following the function parameters is the type annotation for the return value of the function. In this case, the function doesn't return anything, so the type will be `void`. If it returned a string, then we would set it to `string` instead. This allows us to ensure our function is always returning exactly what we want it to.

Now that we know how to annotate a type, lets dive into the core types offered by TypeScript.

## Core Types

### Number

Just like JavaScript, there isn't a difference between integers and floats (decimals), as all numbers are treated as floats.

```ts
let luckyNum: number = 13
```

### String

Strings, a series of characters, can be represented using `' '` or `" "`. You can also use template literals with `` ``.

```ts
let name: string = 'Shane'
```

### Boolean

A simple true or false value.

```ts
let isDone: boolean = false
```

### Array

When you create an array, you want to annotate the type as an array, as well as the type of the values inside the array. This can be done in two ways:

```ts
let listOfEvens: number[] = [2, 4, 6, 8]
let listOfOdds: Array<number> = [1, 3, 5, 6]
```

### Tuple

A tuple lets you create an fixed-length array of mixed types.

```ts
let nameAgeArr: [string, number]
nameAgeArr = ['Shane', 24] // ✅
nameAgeArr = [24, 'Shane'] // ❌
```

### Enum

An enum is a way of giving  more friendly names to sets of numeric values. For example, if you have an object property that can only be set to a set number of options, you can label them as numbers instead of strings. That saves confusion over spelling, capitalization, and other string semantics, while increasing code readability.

```ts
enum Genre {
    Rock,
    Jazz,
    Hip-Hop,
}

let giantSteps = {
    artist: "John Coltrane",
    genre: Genre.Jazz
}

let genreName: string = Genre[0] // will be "Rock"
```

Numeric values for enums automatically start at 0. However you can change the first value to be any number, and the remainder will increment from there. You can also set the values for each manually.

```ts
enum Genre {
    Rock = 3,
    Jazz, // => 4
    Hip-Hop, // => 5
}

enum Genre {
    Rock = 5,
    Jazz = 30,
    Hip-Hop = 13,
}
```

### Any

The type of any can be used for variables whose values we do not yet know, or if we want to opt out of type-checking. This allows TypeScript to be very flexible, but use sparingly, as it eliminates the value added by TypeScript.

### Null and Undefined

Just as in JavaScript, null and undefined are types in TS. By default, null and undefined are subtypes of all other types, meaning you can assign null or undefined to a variable with the number type.

```ts
let luckyNumber = 13
luckyNumber = undefined // ✅
```

### Never

Never type represent the type of values that never occur. For example, a function that always throws an error when called will never return, so we can set the return type to `never`. An infinite loop could also have the return type `never`.

```JavaScript
function throwError(msg: string): never {
    throw new Error(msg)
}
```

### Object

In Javascript, everything that isn't a primitive is an object. Thus, the object type represents any non-primitive, or anything that isn't a number, string, boolean, symbol, null, or undefined.

```ts
let shane: object
shane = { name: "Shane", age: 24 } // ✅

shane = () => console.log("Hi, my name is Shane") // ✅

shane = "Shane" // ❌
```

## Union Types and Aliases

If you variable or parameter needs to have more flexibility, you can specify multiple type options using union types.

```ts
let numberOrString: number | string
numberOrSting = 13 // ✅
numberOrSting = 'thirteen' // ✅
```

You can also define your own types, known as aliases, which can be used as type definitions later.

```ts
type FlexibleNumber = number | string
let luckyNumber: flexibleNumber = 13
luckyNumber = 'thirteen' // ✅
```

## Interfaces

Typescript allows us to define specific object shapes as a type, called an `interface`, which allows us to ensure the objects we are using always have the proper keys and value types.

```ts
interface Album {
    name: string;
    artist: string;
    sumSongs: number;
}

const sgtPepper: Album = {
    name: "Sgt. Pepper's Lonely Hearts Club Band",
    artist: "John Coltrane",
    numSongs: 13
    isGood: true // Allowed to have additional properties
}

const help: Album = {
    isGood: true // ❌, must contain all properties from interface
}
```

## Congrats

You now have an understanding of the fundamentals of TypeScript. Thank you so much for reading, and best of luck on your TS journey!

## References

- [TypeScript Docs](https://www.typescriptlang.org/docs/home)
- [Lear TypeScript from Scratch - Academind](https://www.youtube.com/watch?v=BwuLxPH8IDs&t=8649s)

