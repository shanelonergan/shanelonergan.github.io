---
layout: post
title: 'React's useContext in 3 minutes'
date: 2020-5-22
description: 'Access your state anywhere with a convenient hook'
img: hook.jpg
tags: [programming, terminal, bash] # add tag
---

---

Hooks are my personal favorite way to manage state in a React application. I prefer functional components over class components most of the time, and Hooks feel like a simple and effective extension of react itself. Now, if you are anything like me, you have probably found yourself endlessly passing state down as props until you feel like you are descending into madness. Luckily, there is a solution! `useContext` is a Hook which allows you to pass data throughout the competent tree without having to manually pass down props on each individual level.

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
- [Congrats!](#congrats)
- [References](#references)

## What is TypeScript?

TypeScript is a superset of JavaScript that horizontally compiles back to JavaScript. It provides the ability, among other things, to strongly type your JavaScript code. However, TypeScript files can't actually be run in the browser or Node. So, why is this useful?
