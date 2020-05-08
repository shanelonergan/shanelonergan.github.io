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

Each new `Node` will be initialized with `data` and a `next_node`. We want to be sure to give the class an attribute accessor for both values, so we can both read and write them. Note that when we create a new Node, next will be automatically initialized as nill if we don't pass a value.

## Part 2: The Linked List

```ruby
class LinkedList
    def initialize(data)
        @head = Node.new(data, nil)
    end

    def first
        @head
    end

    def last
        current = @head

        while current.next_node != nil
            current = current.next_node
        end

        current
    end

    def add(data)
        current = @head

        while current.next_node != nil
            current = current.next_node
        end

        current.next_node = Node.new(data, nil)
    end

    def remove
        return if @head == nil

        if @head.next_node == nil
            @head = nil
        end

        previous = @head
        current = @head.next_node

        while current.next_node != nil
            previous = current
            current = current.next_node
        end

        previous.next_node = null
    end

    def add_first(data)
        @head = Node.new(data, @head)
    end

    def remove_first
        return if @head == nil
        @head = @head.next_node
    end

    def length
        counter = 0
        current = @head

        while current != nil
            counter += 1
            current = current.next_node
        end

        counter
    end

    def clear
        @head = nil
    end

    def print
        current = @head

        while current != nil
            puts current.data
            current = current.next_node
        end
    end
end
```

Here I have included a few of the standard methods you will see in linked lists. Lets walk through them one by one!

### first

This one just returns the head of the list!

### last

This one is a bit more complex, but it will lay the foundation for many of the methods to come. In order to reach the last node, we need to loop through the list. To do that, we set a variable `current` to the head of the list. Then, as long as `current` has a next node, we set the value of `current` to that next node. Once we reach a node that doesn't have a `next_node`, we must have reached the end of our list! Then we can simply return the value of `current`, which is our last node.

### add

`add` will accept an argument of `data` and add a new node with that data the to the end of the list. To do this, we need to loop through the list in the same way we did in out `last` method, but instead of returning the last node, we set its `next_node` value to a new `Node`, passing in `data`.

### remove

`remove` will remove the last node from the list. In this method we will use some guard clauses to avoid running the entire method if we don't need to. If the list has no head, then there is nothing to remove, and we should return out of the function. If the head had no next value, then we will remove the head. Besides those two cases this method also works similarly to the `last` method. However, this time, we want to set `current` to `@head.next_node` and `previous` to the head. This is because in order to remove the last node, we need to set the *second_to_last* node's `next_node` value to nil. SO then we can loop through out list again, and once we have reached the end, set the value of `previous.next_node` to nil.

### add_first

For this method, we want to add a ned head to our list, and set its `next_node` value to the original head.

### remove_first

Here we are using another guard clause to return out of our method early if there is no head, just like in `remove`. Otherwise, we can set the value of head to the current head's next node.

### length

We want this method to return the number of nodes in our list. Once again, we are going to loop through our list, but we will also increment a counter with each loop. Once we have reached the end of the list, we return that counter, giving us the total length.

### clear

This one is nice and short. We can just set the value of the head to nil. With no head, there is no list!

### print

This method will print out the data of each node in our list. One more time, we will loop through the list. In each loop, before setting the value of `current` to the next node, we want to `puts` the data of `current`.

## Congrats!

You have now implemented a linked list in Ruby! Thank you so much for reading, and good luck with your job search if thats what brought you here!
