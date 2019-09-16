---
layout: post
title:  "Make a simple personal website using Jekyll and Github Pages"
date:   2019-09-02
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: computer.jpg
tags: [Programming, Terminal] # add tag
---
___
# Before you begin:
This guide assumes some basic Ruby, HTML/CSS, and git experience. It will still be possible to follow without, but it may require a bit of extra research. I have added some articles that I found helpful in the further reading below.
---

**tl;dr:** Custom bash commands are keywords that you can explicitly define to either execute a new function or shorten an existing command. These commands are extremely versatile and customizable, allowing you to tailor them to increase your productivity. Once they are defined in your `.bash_profile` document, you will be able to call on them in any new terminal session.

---

Creating your personal website can often be a daunting task. There are a ton of options for a variety of skill levels, from using Wix or Wordpress templates to coding one from scratch. Building from scratch gives you the most control over the end product, while using a template can get you up and running quickly with the lowest learning curve. Sometimes, however, you are looking for something in the middle. If you have a little bit of programming experience, you can use Jekyll to create a simple, beautiful website quickly, and deploy it for free(yes, FREE!) on GitHub Pages. Jekyll is a ruby gem which is great for creating personal websites and blogs, and is what I used to make my own blogging site. It offers a variety of themes, is extremely customizable, and most importantly, it is fast! Creating and deploying your own personal website using Jekyll can be done in less than an hour.

### Set up your environment(optional)

1. Download a text editor if you don't already have one. I use atom, but a lot of people really love Visual Studio Code as well.
2. Create a github account
3.  install ruby and bundler

### Make a new Jekyll project

Jekyll is a Ruby gem, which is essentially a library of code created by a group of dedicated programmers and released, for free, to us. It is open source, which means that is it maintained by amazing programmers who volunteer their time to make great software free and accessible.

Getting started with Jekyll is super simple. Just enter the following commands in your terminal:

```
~ $ cd ..

~ $ mkdir jekyll-projects

~ $ cd jekyll-projects

~ $ gem install bundler jekyll

~ $ jekyll new my-awesome-site

~ $ cd my-awesome-site

~ $ bundle exec jekyll serve
```

Now, open up your web browser and go to http://localhost:4000. TaDa! You have a website up and running! Take a browse through this website to familiarize yourself with the basic Jekyll theme.

### Make a custom Jekyll project

Now that you have created your first Jekyll site, you will want to take a look at the themes and decide which one you want to use for your own. You can find all of the themes available at jekyllthemes.io. There is a wide variety of beautiful free and paid themes designed for blogs, portfolios, landing pages, and more. Once you have decided on your theme, it is time to dive in.

# Step 1: Open the theme on your local computer

1. Navigate the the GitHub page for the theme of your choice (there should be a link in the description).
IMAGE
2. Fork the repository
IMAGE
3. Clone the repo into your local folder
```
stuff
```
4. Navigate into the project folder
5. Open it in your editor
6. Run your server

Now you can browse your template on http://localhost:4000.

# Step 2: Customize the project with your own information

In your project directory, you should see a file called `_config.yml`. Click on that file to open it, and you will see a document with all of the stock information in it. You can replace this placeholder text with all of your personal information, and it will show up on your web page. If you want to add any images, drag and drop them into the `img` folder. Then just provide the file name in the config file, and you are good to go!

# Step 4: Add your content

If you are creating a personal blog, there should be a couple sample posts. 

---

# References

- [How to create your own custom terminal commands](https://medium.com/devnetwork/how-to-create-your-own-custom-terminal-commands-c5008782a78e)
- [What is a bash script?](https://ryanstutorials.net/bash-scripting-tutorial/bash-script.php)
- [What is the difference between .bash_profile and .bashrc?](https://ryanstutorials.net/bash-scripting-tutorial/bash-script.php)
- [ASCII Art Generator](http://patorjk.com/software/taag/#p=display&f=Graffiti&t=Type%20Something%20)

# Further Reading

[^1]:[Show hidden files and folders on mac](https://nektony.com/how-to/show-hidden-files-on-mac)
[^2]:[Non-login shell and Login Shell](https://www.unixmen.com/non-login-shell-login-shell/)
---
