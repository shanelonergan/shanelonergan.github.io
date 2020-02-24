---
layout: post
title:  "Lighting-Fast Payment Processing"
date:   2020-2-23
description: 'Adding the Stripe API to your React-Rails application'
img: stripe.png
tags: [programming, terminal, bash] # add tag
---
---

If you have ever created, or wanted to create, and e-commerce site, deciding on how to handle payments was likely one of your major decision points. Handling payments online comes with large security risks, and has to be done according to strict specifications (source). Luckily for use, there are companies whose sole purpose to to handle of of these details for us. Stripe is one such company, and they offer a fantastic API. In this article I will walk through integrating the Stripe API into a web application build with React and Ruby on Rails. If you are working with a different stack, the concepts detailed here should still be applicable, and Stripe offers great language-specific documentation(link).

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Set Up](#set-up)
- [Front-End](#front-end)
- [Back End](#back-end)

## Set Up

First things first: we need to create a Stripe account to manage our API calls. Once you do, you can retrieve your Text API keys, which will be found on the home page under the 'Get your test APY keys' header. They can also be found on the Developer page. Once you have access to your keys, we can get started on integrating them.

## Front-End

I have found that the quickest way to get Stripe up and running on the front end is by using a great package called `react-stripe-checkout`. This is a React implementation of Stripe's [Checkout](https://stripe.com/docs/payments/checkout) feature. A Checkout creates a secure, Stripe-hosted payment page which collects all the essential information and handles it for you in one quick step. One downside of going this route is that you don't have full control of the checkout flow or style. If those are things that you value highly, you can use [Stripe Elements](https://stripe.com/docs/payments/accept-a-payment) to build a bespoke checkout experience. To get started, we need to install a few dependancies, react-stripe-checkout and dotenv:

```zsh
npm install react-stripe-checkout dotenv
```

Next we need to set up our environmental variables, if you haven't done so yet. I like to use dotenv, but you can use any method that suits you. To do this, create a `.env` file in the root of your directory. Be sure to add this file to your `.gitignore`, so that it isn't committed to your Github(link). Now you can add your Stripe api key to this env file.

Next, we want to add a Stripe Checkout component to our app. To do this, we first need to import the package like so:

```js
import StripeCheckout from 'react-stripe-checkout';
```

This gives us access to the `<StripeCheckout/>` component. This will render a styled button which, when clicked, will open up a checkout window. It can take a wide variety of props, but the only two are required: `token`, and `stripeKey`. The token prop is where we pass our callback function to handle the token we will receive, and  `stripeKey` is of course our stripe api key, which we will pull from the .env file. Once we add this component to our application, it should look something like this:

```js
export default function App() {
return (
    <StripeCheckout
        token={onToken}
        stripeKey={process.env.REACT_APP_STRIPE_KEY}
    />
)

```

- dotenv (React specific)
- react-stripe-checkout
- add different props
- make a token handler
- controlled form

## Back End

- dotenv
- cors
- charge controller
- route
- params
