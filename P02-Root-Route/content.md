---
title: "Adding a Home Page"
slug: root-route
---

So we have NodeJS and ExpressJS working and we've added a templating engine middleware to render HTML templates. So now we need to create a true homepage for our Giphy Search app.

# Adding a Root Route to your Gif Search

We're going to build a **root route** (a url endpoint that goes to the root path: `/`). But wait, isn't that what we've been using to display our adorable puppy gif?

It is! And now instead of just using it to test gif viewing, we're going to use it for its true purpose of allowing us to search gifs. To do this, we'll need to render a new template called `home.handlebars`.

> [action]
> Edit the root route in `app.js` so that it renders the `home` template.
>
```js
  // ROUTES
  app.get('/', (req, res) => {
    res.render('home')
  })
```
>
> Now create a new template `/views/home.handlebars` to act as our homepage:
>
```html
<h1>Search for GIFS</h1>
```

Right now you if you navigate to `localhost:3000`, but you'll only see the header. Pretty lame for a gif website to not show gifs. Let's fix that!

# Adding a Search Form

Let's add a search form to our home page!

> [action]
>
> Replace our current `/views/home.handlebars` with the following:
>
```html
<!-- home.handlebars -->
<h1>Search for GIFS</h1>
<form action="/">
  <input type="text" name="term">
  <button type="submit">Search</button>
</form>
```

Navigate to `localhost:3000` and take a look at your form. Pretty plain but it will work!

Enter something into the input field and hit enter or click on `Submit`. What do you expect will happen?

> [solution]
> Your form should navigate you to `/?term=YOUR+SEARCH+TERM` (check the URL in the browser to see). This means that their will be a **url query string** available called `term` inside of your root route.

# Log the Search Term

Let's update our root route to use that url query string called `term` that we are passing in through the `?term=` part of the url.

Let's use the JavaScript `console.log()` function to print the url query string and check that the url query string is available in the server. Since you are calling `console.log()` on the server, the log will print out on the terminal

> [action]
>
> Add a `console.log()` in the root route in `app.js`
>
```js
// example URL "http://localhost:3000/?term=hey"
app.get('/', (req, res) => {
[bold]  console.log(req.query) // => "{ term: hey" }[/bold]
  res.render('home')
})
```

What should you expect to see in your terminal window?

> [solution]
> You should see this in your terminal window that is running your server
>
```
[nodemon] starting `node app.js`
Example app listening on port 3000!
{ term: 'YOUR TEST TERM' }
```

Alright, we know how to capture our term, let's build out our search form now to actually return some gifs. Onward!

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'added search form'
$ git push
```
