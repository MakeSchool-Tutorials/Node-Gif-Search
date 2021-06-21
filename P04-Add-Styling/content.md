---
title: "Now Add Styling"
slug: add-styling
---

Let's look back at what we did in order:

1. First we got the environment up and running with a simple hello world.
2. Then we setup the templating with Handlebars.js and updated our hello world to use a template.
3. Then we started from what the user sees - the template - and added a search form
4. Next we made sure that search term was making it to our server.
4. Then we proved we could get GIFs from Tenor.
5. Then we put our search term together with our proof we could get GIFs.

Throughout this initial development we made sure things looked OK, but we didn't spend a lot of time making things beautiful. Once basic functionality is working, then we can invest more time making this look pretty.

# Adding Static Assets: Scripts, Stylesheets, and Images

To add styles to our templates we need to use Cascading Style Sheets or **CSS** files which are one type of **static assets**. Other static assets are JavaScript scripts, images, and even fonts. The browser can then ask for these assets from the server and then they run on the browser.

But remember how Express is lightweight? It is SO lightweight that it doesn't even serve up anything to the browser unless we tell it to do so. So let's do that now:

> [action]
>
> 1) Create a folder called `public`
>
> 2) In `app.js`, tell your Express app that your static files will live in the `public` folder.
>
```js
// app.js
>
...
>
// Somewhere near the top
app.use(express.static('public'));
```
>
> 3) Now add a file called `styles.css` in your newly created `public` folder.
>
> 4) Now link that file in the `<head>` of `views/layouts/main.handlebars`.
>
```html
<link rel="stylesheet" href="styles.css">
```
> 5) Now let's add some nicer fonts. Put the following in your newly created `public/styles.css` file:
>
```css
/* ROOT FONT STYLES */
>
* {
  font-family: 'Lato', Helvetica, sans-serif;
  color: #333447;
  line-height: 1.5;
}
```

Refresh your browser and what changed? Can you inspect the elements that have changed by right clicking on them and clicking on "inspect element"?

# Adding More Styles

Now let's add some more styles!

> [action]
>
> 1) First let's add a container to `views/layouts/main.handlebars`:
>
```html
<!-- main.handlebars -->
>
...
>
  <body>
    <div class="container">
      {{{body}}}
    </div>
  </body>
```
>
> 2) Now let's center the text in the h1 tag by adding the following rule in our `public/styles.css` file:
>
```css
  h1 {
    text-align: center;
  }
```
>
> 3) Now let's add some style to the form and input and button fields in `public/styles.css` as well!
>
```css
  input {
    padding: .5em .6em;
    display: inline-block;
    border: 1px solid #ccc;
    box-shadow: inset 0 1px 3px #ddd;
    border-radius: 4px;
    vertical-align: middle;
    box-sizing: border-box;
    width:300px;
  }
>
  form {
    margin-bottom:10px;
  }
>
  button {
    height: 31px;
    width: 110px;
    text-align: center;
    color: #fff;
    font-size: 1rem;
    font-weight: 200;
    background: transparent;
    border: 1px solid #fff;
    border-radius: 4px;
    margin: 20px 0;
    cursor: pointer;
    transition: all 0.3s ease;
    outline: none;
    border: 1px solid #FE7880;
    color: #FE7880;
  }
```

Ok now we have things looking a little prettier! Great job on **styling the elements in your project!**

> [challenge]
>
> You've learned a lot in this tutorial! Try these extra challenges out if you're looking for something more:
>
> 1. The search box and gifs are all left-aligned. Get them all to be centered like the `h1` element
> 1. Add a button that displays the trending gifs from Tenor. This should not require a search term. Give the button a different style than the search one to flex your new styling muscles some more!

# Feedback and Review - 2 minutes

**We promise this won't take longer than 2 minutes!**

Please take a moment to rate your understanding of learning outcomes from this tutorial, and how we can improve it via our [tutorial feedback form](https://forms.gle/cdBt2dwPKiUYU5jp6)

This allows us to get feedback on how well the students are grasping the learning outcomes, and tells us where we can improve the tutorial experience.

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'styled page'
$ git push
```

**Congrats on building your gif search!** What can you do next? What features could you add?

> [action]
>
> Reflect on this lesson, and in your own words, describe what you've learned. See how you can relate the concepts learned in this tutorial to the rest of the class.

<!-- Feel free to reference [this repo](https://github.com/ajbraus/giphy-search) for a solution. -->
