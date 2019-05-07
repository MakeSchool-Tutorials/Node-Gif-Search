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

Throughout this initial development we made sure things looked OK, but we didn't spend a lot of time making things beautiful. Once basic functionality is working then we can invest more time making this look pretty.

# Adding **Static Assets**: Scripts, Stylesheets, and Images

To add styles to our templates we need to use Cascading Style Sheets or .css files which are one type of **static assets**. Other static assets are JavaScript scripts, images, and even fonts. The browser can then ask for these assets from the server and then they run on the browser.

But remember how Express is lightweight? It is SO lightweight that it doesn't even serve up anything to the browser unless we tell it to do so. So let's do that now:

1. Create a folder called `public`
1. Tell your Express app that your static files will live in the `public` folder.

    ```js
    // app.js

    app.use(express.static('public'));
    ```
1. Now add a file called `public/styles.css`.
1. Now link that file in the `<head>` of your `main.handlebars`.

    ```html
    <link rel="stylesheet" href="styles.css">
    ```
1. Now let's add some nicer fonts.

    ```css
    /* ROOT FONT STYLES */

    * {
      font-family: 'Lato', Helvetica, sans-serif;
      color: #333447;
      line-height: 1.5;
    }
    ```

Refresh your browser and what changed? Can you inspect the elements that have changed by right clicking on them and clicking on "inspect element"?

# Adding More Styles

Now let's add some more styles

1. Let's add a container

    ```html
    <!-- main.handlebars -->
    <body>
      <div class="container">
        {{{body}}}
      </div>
    </body>
    ```
1. Now let's center the text in the h1 tag

    ```css
    h1 {
      text-align: center;
    }
    ```
1. Now let's make the form and input and button field prettier.

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

    form {
      margin-bottom:10px;
    }

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

Ok no we have things a little prettier!

# Now Your Turn!

What can you do next? What features could you add?

<!-- Feel free to reference [this repo](https://github.com/ajbraus/giphy-search) for a solution. -->
