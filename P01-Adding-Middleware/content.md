---
title: "Adding a Template Engine to your Express App"
slug: adding-middleware
---

Now that our NodeJS environment is up and running and we have a basic hello world running in Express, let's extend that with some basic **middleware** like a templating engine.

# Add your First Middleware - a Template Engine

ExpressJS is a light weight or **unopinionated** web framework, meaning it does not make decisions for you, it lets the developer decide on what plugins to use. These plugins or libraries we use to extend a web framework are called **middleware**. The first piece of middleware we are going to add is a template engine so we can render HTML templates.

We're going to use [Handlebars.js](http://handlebarsjs.com/) - a minimalistic, logicless templating library for server-side templating. Handlebars.js is a stand-alone library, but to use it in the context of ExpressJS we can use the [express-handlebars](https://github.com/ericf/express-handlebars) library.

> [action]
> Install `express-handlebars`
>
>```bash
  $ npm install express-handlebars --save
>```

We're going to now put this code in the `// Middleware` section of our `app.js` file.

```js
// app.js

...

// Middleware
const exphbs  = require('express-handlebars');

app.engine('handlebars', exphbs({defaultLayout: 'main'}));
app.set('view engine', 'handlebars');
```

This "middleware" library will be used to allow Express (our web framework) to render HTML templates and send them back to the client using a new function: `res.render('template-name', { variables })`

# Views & Layout Folder Structure

> [action]
> Create a folder called `views` and in that folder create a folder called `layouts`. Inside your `layouts` folder create a file called `main.handlebars`.

So your file structure should look like this:

```
.
├── app.js
└── views
    ├── hello-gif.handlebars
    └── layouts
        └── main.handlebars
```

Your `main.handlebars` file should look like this. The triple brackets `{{{}}}` renders html of the sub template we will pass into this layout template.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Example App</title>
</head>
<body>

    {{{body}}}

</body>
</html>
```

# Update Your Hello World Route

Let's update the hello world route to be a hello gif route.

```js
// app.js

app.get('/hello-gif', (req, res) => {
  const gifUrl = 'http://media2.giphy.com/media/gYBVM1igrlzH2/giphy.gif'
  res.render('hello-gif', { gifUrl })
})
```

And define a new template in the `views` folder called `hello-gif.handlebars` that will display the gif image.

```html
<!-- hello-gif.handlebars -->
<img src="{{gifUrl}}">
```

# URL Parameters in Another Route

Let's add another route. This time let's use a variable in the route in order to say "greetings" to whoever is in the path.

> [action]
> Add a GET route so when you go to '/greetings/Bethany' your page should say "Greetings Bethany!"
>
```js
// index.js
app.get('/greetings/:name', (req, res) => {
  const name = req.params.name;
  res.render('greetings', { name });
})
```
```html
<!-- greetings.handlebars -->
<h1>Greetings {{name}}!</h1>
```
