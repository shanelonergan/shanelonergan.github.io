---
layout: post
title:  "Building a Slackbot with IBM Watson, Part 2"
date:   2020-2-30
description: 'Eliminate toxic language in your slack channel with Toxic Comment Bot'
img: slackbot.jpeg
tags: [programming, terminal, bash] # add tag
---
---

Welcome back to Building a Slackbot with IBM Watson! If you haven't read part 1 of this series, feel free to check it out [here](https://shanelonergan.github.io/chatbot/). In part 2 we will be adding the IBM Watson Toxic Comment Classifier to our slackbot and having it respond to messages containing toxic speech. Les dive right in!

## Review

When we left off, our `index.js` file looked like this:

```js
require('dotenv').config()
const SlackBot = require('slackbots');
const axios = require('axios')

const bot = new SlackBot({
    token: process.env.API_TOKEN,
    name: 'Toxic Comment Bot'
});

const params = {
    icon_emoji: ':rotating_light:'
};

bot.on('start', function() {
    bot.postMessageToChannel('general', 'I am listening...', params);
});
```

We currently have a bot that just hangs out in the `#general` channel, listening. Now it is time to tell it exactly what it should be listening for!

## Message and Error Handlers

## handleMessage Function

## fetchToxicAPI

## analyzeMessage
