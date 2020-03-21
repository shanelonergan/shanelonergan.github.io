---
layout: post
title:  "Big O Cheatsheet?"
date:   2020-3-15
description: 'A quick guide to identifying runtime complexity'
img: rest.jpg
tags: [programming, terminal, bash] # add tag
---
---

Welcome to the Big O cheatsheet! This is meant to be a reference point fo quickly identifying some of the most common runtime complexities. It is generalized, so it is not meant to perfectly classify all complex algorithms, but hopefully it can provide a starting point to jump off from. Without further ado, lets dive in!

## Constant Time: O(n) = 1

In order for an algorithm to be constant time, it must take the same amount of time to run no matter what variables are passed in. Whether the algo is passed an array with 1 item or 100 items, it will take the same time to execute.

## Logarithmic Time: O(n) = log(n)

If doubling the number of elements you pass your algo doesn't double the amount of work it has to do, it is likely logarithmic time. Searching operations can usually be assumed to be Logarithmic if the data collection is *sorted*.

## Linear Time: O(n) = n

Linear time is one of the most common runtimes. If you are iterating through every element in a data collection, it is probably going to be linear runtime. This is because for each *n* number of elements we add to the data collection, be have to do exactly *n* more work.

## Quasilinear Time: O(n) = n*log(n)

This is usually the case if each element you add adds an extra unit of work *plus a little bit extra*. For example, doubling the number of elements would take a little bit more than double the work. A handy rule of thumb is that Sorting algorithms are usually quasilinear.

## Quadratic Time

Quadratic time is an option if adding an element greatly increases the amount of work you have to do.

## Exponential Time

If you add a single element to your data collection, the amount of work doubles.
