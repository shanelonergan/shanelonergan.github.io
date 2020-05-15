---
layout: post
title: 'TypeScript Cheat Sheet'
date: 2020-5-15
description: 'A crash course in the basics of the hottest development language'
img: git.png
tags: [programming, terminal, bash] # add tag
---

---

I am in the midst of searching for my first job as a developer. Recently, I had the the opportunity to interview for a company I thought I would be a great fit for. It was a junior position with a stack that I was mostly familiar with, and in a sector that I had prior work experience in. However, the job description said that most of the code is written in TypeScript. Now, I have heard a lot about TypeScript from other developers, but I hadn't had the chance to start learning it yet. I figured this was the perfect chance to take the plunge! I had an open weekend before the interview, so I decided to see how much I could learn! In this post I will walk you through the basics of TypeScript, as well as the benefits it offers over JavaScript. The goal is to learn enough to be conversational, as well as to give a strong jumping off point if you were to start learning it on the job.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [What is TypeScript](#what-is-typescript)
- [Why TypeScript](#why-typescript)
- [Getting Started](#getting-started)
- [Core Types](#core-types)
- [References](#references)

## What is TypeScript

TypeScript is a superset of JavaScript that horizontally compiles back to JavaScript. It provides the ability, among other things, to strongly type your JS code, but it can't actually be run in the browser or Node. So, why is this useful?

## Why TypeScript

TypeScript helps you avoid unwanted runtime errors by type-checking during development. TypeScript files are compiled into JavaScript files which can then be run in the browser or node, and the compiler catches bugs in advance, saving time and frustration during debugging down the line. TypeScript improved code clarity by explicitly defining the types of variables, function parameters, and function outputs. This allows you to tell at a glance exactly what the your code should be taking and returning, and the compiler will catch it if you accidentally pass something to a function that you shouldn't be. The TypeScript compiler also allows you to customize what version of JavaScript your TS files compile to. This allows the developers to utilize many newer features of JavaScript without worrying about browser compatibility. This also allows TypeScript to offer features such as generics,enums, and interfaces which are not available in JS. Additionally, TypeScript offers fantastic tooling in modern IDE's such as VS Code which can catch errors while the code as being written, saving even more time debugging.

## Getting Started

Lets go ahead and dive right in by analyzing our first piece of TypeScript code:

```TypeScript
const name = 'Shane'
let age = 24

function printNameAndAge(person: string, age: number): void {
    console.log(`${person} is ${age} years old.`)
}

printNameAndAge(shane)
```

Now, you might be thinking to yourself, "That looks a lot like JavaScript...". Well, thats because it is! Vanilla JavaScript is totally valid in TS. All of the features are optional to use, and exactly how they are utilized is up the the developer. Of course, you aren't getting any of the benefits of TS by doing this, so lets add a little bit to it:

```TypeScript
const name: string = 'Shane'
let age: number = 24

function printNameAndAge(person: string, age: number): void {
    console.log(`${person} is ${age} years old.`)
}

printNameAndAge(shane)
```

 As you can see, you can add type annotations after variable declarations or within function parameters using a colon `:` followed by the type. The `void` following the function parameters is the type annotation for the return value of the function. In this case, the function doesn't return anything, so the type will be `void`. If it returned a string, then we would set it to `string` instead. This allows us to ensure our function is always returning exactly what we want it to.

 Now that we know how to annotate a type, lets dive into the core types offered by TypeScript.


 ## Core Types

## References

- [Git](https://git-scm.com/)
- [What is Git and Github? - Core DNA](https://www.coredna.com/blogs/what-is-git-and-github-part-two)
- [Git Core Repo](https://git.kernel.org/pub/scm/git/git.git/about/)