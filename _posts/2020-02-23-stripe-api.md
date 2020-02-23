---
layout: post
title:  "Lighting-Fast Payment Processing"
date:   2020-2-16
description: 'Adding the Stripe API to your React-Rails application'
img: stripe.png
tags: [programming, terminal, bash] # add tag
---
---

If you have ever created, or wanted to create, and e-commerce site, deciding on how to handle payments was likely one of your major decision points. Handling payments online comes with large security risks, and has to be done according to strict specifications (source). Luckily for use, there are companies whose sole purpose to to handle of of these details for us. Stripe is one such company, and they offer a fantastic API. In this article I will walk through integrating the Stripe API into a web application build with React and Ruby on Rails. If you are working with a different stack, the concepts detailed here should still be applicable, and Stripe offers great language-specific documentation(link).

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Frameworks](#frameworks)
  - [Oh My Zsh](#oh-my-zsh)
  - [Others](#others)
  - [Summary](#summary)
- [Themes and Plugins](#themes-and-plugins)
  - [Spaceship Prompt](#spaceship-prompt)
  - [Powerlevel 9K](#powerlevel-9k)
  - [Typewritten](#typewritten)
