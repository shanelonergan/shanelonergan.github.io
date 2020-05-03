---
layout: post
title:  "Building a Slackbot with IBM Watson, Part 2"
date:   2020-5-1
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

For our purposes, we will want to pull out the text of the message to analyze, as well as the user who sent it. Then, we will send this information to a helper function, which will analyze it for us (we will define this function later). Before we call the helper function, we will want to wrap it in a conditional that checks for two things: First, that a message has been posted (the `bot.on('message)` handler is also called when a user begins typing), and that is was not sent by another bot.

```js
bot.on('message', (data) => {
    const msg = data.text
    const user = data.user

    if(data.type === 'message' && data.subtype !== 'bot_message') {
        handleMessage(msg, user);
    }
})
```

Next, we should set up an error handler that logs any errors our bot encounters. We can do this the same way we logged the message data, but instead call it on errors.

```js
bot.on('error', (err) => {
    console.log(err);
})
```

## fetchToxicAPI

Before we define `handleMessage`, lets create a separate function, `fetchToxicAPI`, to fetch from the IBW Watson API. We will utilize this function with `handleMessage`, so I think it makes more sense to define it first. We are going to be utilizing an async axios request here, so lets make sure to define it as an async function.

```js
const fetchToxicAPI = async (msg, username) => {

    await axios.post('http://max-toxic-comment-classifier.max.us-south.containers.appdomain.cloud/model/predict', {
        text: [msg]
    })
    .then((res) => {
        console.log(res)
    })
    .catch((error) => {
        console.error(error.config)
    })
}
```

Feel free to test this function out by sending a few messages through the api and looking through the results! The result object we get back from IBM is huge, and contains a lot of information we don't need. To narrow it down to just the results of the language processing, traverse the data like so: `res.data.results[0].predictions`. Once we have the results, we want to send them to be processed by our final helper function, `analyzeMessage`. The final code for our function should look something like this:

```js
const fetchToxicAPI = async (message, username) => {
    let responseMessage

    await axios.post('http://max-toxic-comment-classifier.max.us-south.containers.appdomain.cloud/model/predict', {
        text: [message]
    })
    .then((res) => {
        const results = res.data.results[0].predictions
        response = analyzeMessage(results, username)
    })
    .catch((error) => {
        console.error(error.config)
    })

    return responseMessage
}
```

Lets move on and build out that `analyzeMessage` function before looping back and finishing up with `handleMessage`.

## analyzeMessage

In this function, we are going to be breaking down the results of IBM's classification of the user's message, and building an output string letting them know if their message was indeed toxic. The API returns an object, which we are calling `results`, which contains 6 metrics on which the message was graded: toxic, severely toxic, obscene, threatening, insulting, and identity hate. Each category receives a score between 0 and 1, 0 being unlikely to contain that category of speech, and 1 being extremely likely. For our purposes, we will check to see if any of the categories received over a 0.75. If not, then we will assume the message does not contain any toxic speech, and our function will return null. However, if it is found that any of them are above 0.75, then we will check each individually, and create a string notifying our user of each flag they hit.

Lets break this down into steps

### Determine if any of the results are above 0.75

First, lets pull out all the values from the results object we received from the API using `Object.values`. Then we can use JavaScript's handy `Array.some()` method to check if those values contain any that are greater than or equal to 0.75. If so, then we will build our message to send back. If, not, we return null!

```js
const analyzeMessage = (results, username) => {

    const resultValues = Object.values(results)
    const checkValues = (value) => value >= 0.75

    if (resultValues.some(checkValues)) {
        // do stuff here
    } else {
        return null
    }
}
```

### Build the message

If the message is indeed toxic, then we want to let the user which flags they hit. To do this, we will build two strings which make up the skeleton of every message, and then insert the flags into the middle. To do this, we can create an array of strings based on which flags were hit, and then concatenate them together to build the final message. How exactly you format this string is totally up to you, but you can see I I did it below.

```js
if (resultValues.some(checkValues)) {
        let responsePart1 = `it looks like your message contains toxic speech. It has been flagged as: \n\n     🛑 `
        let responsePart2 = '\n\n Please refrain from using this kind of speech. Our slack community is one of love and inclusion, and we would like to keep it that way.'

        let flagsArr = []

        if (predictions.toxic > 0.75) {
            flags.push('toxic')
        } if (predictions.severe_toxic > 0.75) {
            flags.push('severely toxic')
        } if (predictions.obscene > 0.75) {
            flags.push('obscene')
        } if (predictions.threat > 0.75) {
            flags.push('threatening')
        } if (predictions.insult > 0.75) {
            flags.push('insulting')
        } if (predictions.identity_hate > 0.75) {
            flags.push('identity hate')
        }

        const flagsStr = flagsArr.join('\n     🛑 ')

        return responsePart1 + flagsStr + responsePart2
    }
```

Okay! Now that we have determined whether or not the message is toxic and generated an response, we can finally loop back and build our `handleMessage` function!

## handleMessage Function

This is the function that is called in response to every message. It, in turn, calls our `fetchToxicAPI` function, which then calls the `analyzeMessage` function. The return value of `analyzeMessage ` is then passed back all the way to handleMessage. I know this is a little confusing, so a diagram of the data flow can be seen below:

![Diagram]()

Now, if the return value of `fetchToxicAPI` is a response string, then we will send that string to the channel as a message! Now,, I haven't figured out exactly how to tag another user in the message, so for the time being I am just appending their username to the message. If anyone knows how I could improve this, please let me know! Since the original message data only contains the user ID and not the username, I have to currently get all the users and filter them by user ID for the right user. Then I can pull out their username, and append it the the message.

```js
const handleMessage = async (msg, user) => {
    const response = await fetchToxicAPI(msg)
    const users = await bot.getUsers()

    if (users && response) {
        const userData = users['members'].filter(member => member.id === user)
        const username = userData[0].profile.display_name, 89

        const output = `${username}, ${response}`

        bot.postMessageToChannel('bot-testing', output, params)
    }
}
```
---

## Congrats!

You have now built a Slackbot which can identify and respond to toxic speech! Thanks you very much for reading, and I hope you found this guide helpful.

