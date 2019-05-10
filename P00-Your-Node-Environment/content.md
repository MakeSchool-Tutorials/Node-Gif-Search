---
title: "Setting up your NodeJS environment"
slug: your-node-environment
---

NodeJS or node.js or just node, is a web server built with JavaScript. But... JavaScript is for the client!? What's going on!?

JavaScript only ran in the browser until Google invented the V8 Engine and Ryan Dahl used the V8 Engine to create a JavaScript based server in 2009.

Now Node is a fast growing and popular web server. And now you get to learn how to use it to build a simple gif search engine using the Tenor API.

If you haven't been to [Tenor](https://tenor.com) before, head over to their website now to see how it works.

# Learning Outcomes

By the end of this tutorial, you should be able to...

1. Set up a development environment for building a node.js-powered website
1. Use a templating engine to quickly create layouts for your website
1. Build basic route logic that uses parameters
1. Integrate a simple API into your project
1. Style elements in your project beyond the default

# Setting Up Your Node Environment with Package Managers

We're going to use NodeJS as our **web server** for this project. We could write just plain JavaScript to use NodeJS, but that would mean writing a lot of **boilerplate**. Instead, we will use the **web framework** ExpressJS, which uses NodeJS.

**Package managers** are pieces of software that manage the versions of various libraries so they can work together without errors on your computer. We'll use [Homebrew](https://brew.sh/) the MacOS **package manager** to install [NodeJS](https://nodejs.org/en/). When we install NodeJS, the **Node Package Manager (npm)** will be installed as well so we can then install node packages (like ExpressJS!).

If you don't already have Homebrew installed, install that first and then NodeJS & npm.

## Mac Instructions:

> [action]
>
> Open your terminal and run the following commands to install homebrew and then nodejs:
>
```bash
  $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  $ brew install node
```

<!-- -->

> [info]
> **IMPORTANT**—Whenever you see the `$` in a command, that means it should be called in your computer's terminal. Remember: Don't include the `$` in your command.`

## Linux Instructions

Choose the proper installer at the [Node.js download](https://nodejs.org/en/download/) page.

Now open your Terminal program and type `npm -v` to check if npm is installed. This should print out a version number, e.g. `4.10.0`.

# Starting a Node Project

> [info]
>
> If you do not already have a text editor, download and install either the [Atom Text Editor](https://atom.io/) or [Visual Studio Code](https://code.visualstudio.com/).

<!-- -->

> [action]
>
> Use npm to initialize a Node project from the terminal.
>
```bash
$ mkdir gif-search
$ cd gif-search
$ npm init
# (hit enter for each option it asks for to select the default choice)
$ atom . # to open your project in the Atom text editor
```

Now that you have initialized a node project with `npm init`, you will see that you have a `package.json` file in your folder.

> [action]
>
> Open up your `package.json` file and set your `main` file to `app.js`:
>
```json
{
  ...
  "main": "app.js",
  ...
}
```

In future steps we'll create the `app.js` file. That is a more conventional name for the root file of an ExpressJS project.

# Using Git/GitHub

As you go through this tutorial, you will be using a program called [Git](https://git-scm.com/) and a website called [GitHub](https://github.com/). Git is a form of **version control** and GitHub is a hosting service for version control. In short, version control is a way to save your work in milestones as you build out your project (i.e. saving different "versions" of the project through various stages of its lifecycle). These "milestones" are known as **commits**, which we'll be making at the end of each chapter (if not multiple times within it). This is a requirement, you must make a commit whenever the tutorial prompts you. This not only further enforces best practices for software engineering, but also will help you more easily figure out where a bug originated from if you break your progress up into discrete, trackable chunks.

> [action]
>
> Read [this article](https://www.atlassian.com/git/tutorials/why-git) on why you should be using Git, and the advantages it offers

When prompted to commit, you'll see a sample commit message. Feel free to use your own message, so long as it clearly and concisely covers the work done.

Lastly, the commit prompts in this tutorial should be the minimum amount of times you commit. If you want to do more commits, breaking your chunks into even smaller chunks, that is totally fine! We'll do an initial one, but there's some setup we need to do first

# Git Setup

> [action]
>
> 1. [Follow these instructions](https://git-scm.com/book/en/v1/Getting-Started-Installing-Git) to install Git on your computer for your operating system
> 1. Follow the [GitHub sign up instructions](https://github.com/) and make an account.
> 1. You will also need to [add your SSH key](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account) to your GitHub account in order to make commits.

You should now be all set up with Git and GitHub! In Git we use **repositories, or repos,** to hold our projects. Now let's make that first commit:

>[action]
> Make your first commit
>
```bash
# initialize git in our project
$ git init
# add everything that has been changed/added/deleted to git
$ git add .
# save all the items that were just added into a commit
$ git commit -m 'project init'
```

Now we need to make a repository for our project.

> [action]
>
> Go to GitHub and create a public repository called `tenor-search`. Don't worry about the `.gitignore` or `LICENSE` for now, we'll cover that another time.

Finally, you need to associate it as a remote for your local git project and then push to it.

>[action]
>
> Push your project up! Replace GITHUB-REPO-URL with your actual github repo url which you can obtain from the **Clone or download** button on the repo page
>
```bash
# associate our github repo with our local git
$ git remote add origin GITHUB-REPO-URL
# push all of our comitted changes up to our GitHub repo
$ git push origin master -u
```

Alright enough of that, back to the code!

# Add Express Package and Start Node

Now we need to add ExpressJS to this project. We will use npm to install ExpressJS and npm will add a line to our `package.json` file to track the libraries that our project uses. It will also add ExpressJS and its dependences to a `node_modules` folder inside our project. You won't ever need to touch any of the files inside the `node_modules` folder during this tutorial, it's just used to hold libraries and dependencies we add to the project.

> [action]
> Install ExpressJS to your project
>
```bash
$ npm install express --save
```

# Adding `app.js`

Add an `app.js` file to your project.

You can either use your terminal to create your root file `app.js` or you can use your text editor.

> [action]
>
> Watch this brief video to review how to do this on MacOS for terminal or Finder/Atom:
>
> ![ms-video-youtube](https://www.youtube.com/watch?v=DI77fe5aEOM)

Using either method you learned in the video, let's add some files to our project:

> [action]
>
> Create an `app.js` file in your project directory

Now we'll add some code to `app.js` that will add express, and then uses it to start a web server.

This code also has some **Comments** that separate out the various parts of the `app.js` file. Throughout this tutorial, we'll be updating this file, so keep your eyes peeled for these comments as clues for where code goes.

> [action]
>
> Add the following to `app.js`:
>
```js
// Require Libraries
const express = require('express');
>
// App Setup
const app = express();
>
// Middleware
>
// Routes
>
// Start Server
>
app.listen(3000, () => {
  console.log('Gif Search listening on port localhost:3000!');
});
```

Notice that last line which tells the app to log a message on port 3000. Once we start the server, we should see that message in the terminal!

> [action]
> Run your server from your terminal with this command:
>
```bash
$ node app.js
```

You should see "Gif Search listening on port 3000!" output in your terminal. And if you enter `localhost:3000` into your browser's address bar, you should see `Cannot GET /`. This is because we haven't defined a **root route**, a route for the path: `/`.


Using the `$ node` method to start your server is kinda annoying because you'll have to stop and restart your server every time you make a change. Instead let's start our node server with a program called `nodemon`.

> [action]
>
> Install `nodemon` through the terminal:
>
```bash
 $ npm install nodemon -g
 ```

 Now start your server by typing `$ nodemon`. Now your server will restart anytime you make any changes to your code!

# Your First Route in an Express Project

Now that we have Node and npm installed we're going to start an Express project and make it say "hello world".

Web servers are built to receive requests to various predefined **URL endpoints** or **routes**. These routes or endpoints are defined as unique **URL paths**. Let's look at some examples of a path. To get to your public facebook profile, you must go to facebook.com + your facebook user name:

`https://www.facebook.com/YOUR_USER_NAME`

In express this would be defined like this:

```js
// Routes
app.get('/:username', (req, res) => {
  // Here you would look up the user from the database
  // Then render the template to display the users's info
})
```

This is an example of an endpoint or route. It is called a **GET** route because we are "getting" information to read, not saving or changing information in the database. Hence, the function name we call is `app.get()`. Remember that `app()` is an instance of Express, and that means that the `get()` function is a native Express function (not middleware that we added).

For reference you can look at [ExpressJS's Getting Started](https://expressjs.com/en/starter/installing.html) docs

> [action]
>
> Add the following code directly below the `// Routes` comment in `app.js`, which will print 'Hello Squirrel' in the web browser.
>
```js
// Routes
app.get('/', (req, res) => {
  res.send('Hello Squirrel');
});
```

Go back to `localhost:3000` in your browser and make sure it says "Hello Squirrel". Congrats! You just built your first route! Let's make sure to save this point and commit:

# Now Commit

Whenever you see a green box like the one below, it marks a **stretch challenge**. Unlike action boxes (denoted by the stars), stretch challenges are are optional, and aren't needed to complete the tutorial. If you're looking for an extra challenge though, we encourage you to take them on!

> [challenge]
>
> If you push the above code, you'll also be pushing up `node_modules`. We only care about that in our local development environment, and don't need to track that in Git (it also takes up a lot of space)
>
> Before you add/commit/push below, add a [gitignore](https://git-scm.com/docs/gitignore) file and edit it so that `node_modules` doesn't get tracked in git. What else shouldn't be tracked?

Make sure you do the below steps, regardless of if you did the above challenge or not:

>[action]
>
> Add/commit/push your code!
>
```bash
$ git add .
$ git commit -m 'first route built'
$ git push
```

Excellent work! By this point you've established a **fully set up development environment for building a node.js-powered website!** Now let's build this into an actual search engine for gifs!
