---
layout: post
title:  "Finding the Perfect Terminal, Part 1"
date:   2020-2-8
description: 'Emulators and Shells'
img: hyper-term.png
tags: [programming, terminal, bash] # add tag
---
---

The terminal is usually one of the first things that a new programmer learns how to use. Also referred to as the command line, or Command Line Interface (CLI), it is our way of speaking directly to the computer. What is often referred to as the terminal is a terminal emulator. This is a program that opens a window and allows us to interact with the shell. The shell is a program that takes input from the user in the form of text and hands it to the operating system to perform.

If you are anything like me, it didn't take a long time before you started customizing your terminal. Luckily, there are tons of ways to tailor your terminal to perfectly match your workflow and aesthetic preferences. In this guide, I will walk through some of the different emulators and shells I have worked with, and take a look into which could be right for you.

**note** I use macOS, so this series will be written for macOS users. Most should work on any unix-based operating systems, but I will not have tested it.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Emulators](#emulators)
  - [Terminal.app](#terminalapp)
  - [iTerm 2](#iterm-2)
  - [Hyper](#hyper)
  - [Alacritty](#alacritty)
  - [kitty](#kitty)
  - [Summary](#summary)
- [Shell](#shell)
  - [Bash](#bash)
  - [Zsh](#zsh)
  - [Fish](#fish)

## Emulators

When it comes to deciding on an emulator, there are three major factors to consider: speed, features, and aesthetics. How you prioritize these will likely determine which is best for you. There are many options to choose from for emulators, so I will cover the five I have experience with.

### Terminal.app

The standard terminal that ships with MacOS it quite good. It can likely handle anything you would need to use it for, and it is easy to use. However, it is not as customizable or performant as some other options, which is why many people like to download a third-party emulator.

### iTerm 2

iTerm2 seems to be the most popular third-party emulator. It is extremely feature rich and easy to customize. Some of its major features include:

- split panes
  - divide the window into multiple panes, each with a different session. can be split vertically or horizontally
- hotkey window
  - assign a hotkey that bring iTerm2 to the foreground when using another application.
- robust search
- autocomplete
- paste history
- instant replay
  - Allows you to rewind and view your terminal history in real-time

One of the main drawbacks of iTerm2 used to be speed, but recently they added GPU rendering which provides a significant performance increase. If you are looking for the most well rounded emulator, iTerm2 is likely it.

### Hyper

Hyper is a popular terminal among those looking for the most beautiful emulator experience possible, and for good reason. Built using web technologies (html/css/javascript), Hyper is the most A E S T H E T I C emulator on this list. If you are familiar with web development, your customization of Hyper is limited only by your JS skills! However, this beauty does come at a cost. In my experience, Hyper is by far the slowest of all the emulators. While it does have a rich plugin ecosystem, I have encountered many bugs in even some of the most popular plugins. If you want the most beautiful terminal possible, and don't mind sacrificing some performance, then Hyper may be the right choice.

### Alacritty

Alacritty is the self-proclaimed fastest terminal emulator in existence,  utilizing GPU rendering and minimal features for performance optimization. While the exact performance benchmarks are subject to some controversy, Alacritty certainly feels fast. In my personal experience it feels the fastest of all on this list, both in startup and command execution times. On the other hand, Alacrity is quite minimalist when it comes to features. It doesn't support tabs or split planes, and doesn't have any menu items on MacOS. Additionally, I found Alacritty to be the least intuitive to install and customize. If speed is your #1 factor, Alacritty is likely your best bet.

### kitty

kitty is an emulator that I believe fills the gap between iTerm2 and Alacritty. It is also a GPU based emulator, but it provides a great set of features and is designed with keyboard centric use in mind. Some of kitty's best features are:

- supports tabs and windows, with multiple layouts
- has a good ecosystem of plugins called kittens
- multiple copy/paste buffers
- highly configurable
- key-binding centric

If you are looking for a blazing fast terminal but still want access to a good amount of features, kitty is a great option.

### Summary

Most feature-rich: iTerm2
Best looking: Hyper
Fastest: Alactrity
Fast + features: kitty

## Shell

Alright, you have decided on an emulator. Congrats! Now it is time for the next step: deciding which shell to use.

### Bash

Bash, which stands for Bourne Again Shell, is the shell that, until recently, came as the default on MacOS. It is one of the most common shells out there. It works well, and there is nothing wrong with it. However, if you are looking for more features from your shell, it may be time to consider alternatives.

### Zsh

Zsh, in my experience, seems to be the most common shell people switch to from bash. It feels pretty much the same to use, but provides some nice features:

- automatic CD (just type the name of the directory and hit enter)
- path expansion (type /u/lo/b and hit tab and it automatically expands to /usr/local/bin)
- plugins and frameworks

The last feature is often one of the largest draws of Zsh, as it gives you access to the community-driven framework Oh-My-Zsh.

### Fish
