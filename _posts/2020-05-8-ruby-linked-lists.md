---
layout: post
title:  "Building a Linked List in Ruby"
date:   2020-5-8
description: 'An introduction to a common data structure'
img: slackbot.jpeg
tags: [programming, terminal, bash] # add tag
---
---

Hello there! Welcome to building a Linked List in Ruby. Linked Lists are one of the most common data structures in programming, and if you are preparing for Software Engineering interviews, you will likely come across them frequently. Linked Lists are essentially a list of items where each item points to the next one, forming a chain. Each item contains some information, and a pointer to the next item. From now on, we will call these items *Nodes*. A visualization of a linked list can be seen below:

![]()

Linked Lists have benefits that cause them to be preferable over arrays in come cases, but also some drawbacks. It is faster to add and remove items from a linked list than an array, but is is slower to look up items.

Alright, lets dive right on in!

## Part 1: The Node

A linked list is typically implemented with two classes: a `Node` and a `LinkedList`. Lets start off by building our `Node` class, which we will use for each individual item within the list.

```ruby
class Node
    attr_accessor :data, :next_node

    def initialize(data, next_node)
        @data = data
        @next = next_node
    end
end
```

Each new `Node` will be initialized with `data` and a `next_node`. We want to be sure to give the class an attribute accessor for both values, so we can both read and write them.
