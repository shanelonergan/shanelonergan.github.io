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

First, we need to define exactly what the bot should be listening for. There are a variety of events a Slackbot can listen for, and SlackBots.js provides a few simple ones for us to use. We want our bot to respond to messages sent by users, so we will be using the `message` event. For other events, feel free to consult the [docs](https://www.npmjs.com/package/slackbots). To do this, we will create a function just like our start function, but instead of `start`, pass in `message`. It will also accept a callback function, which is automatically called with the `data` parameter whenever a message is sent to the channel the bot lives in, `data` contains all of the data about the message that was sent. I would recommend `console.log`-ing it first to get a feel for what information you have access to.

```js
bot.on('message', (data) => {
    console.log(data)
})
```

For our purposes, we will want to pull out the text of the message to analyze, as well as the user who sent it. Then, we will send this information to a helper function, which will analyze it for us. Before we call the helper function, we will want to wrap it in a conditional that checks for two things: First, that a message has been posted (the `bot.on('message)` handler is also called when a user begins typing), and that is was not sent by another bot.

```js
bot.on('message', (data) => {
    const msg = data.text
    const user = data.user

    if(data.type === 'message' && data.subtype !== 'bot_message') {
        handleMessage(msg, user);
    }
})
```

## handleMessage Function

## fetchToxicAPI

## analyzeMessage
