---
title: "Adding a Home Page"
slug: root-route
---

So we have NodeJS and ExpressJS working and we've added a templating engine middleware to render HTML templates. So now we need to create a homepage for our Giphy Search app.

# Adding a Root Route to your Gif Search

Let's add a **root route** (a url endpoint that goes to the root path: `/`). And let's render a template called `home.handlebars`.

```js
app.get('/', (req, res) => {
  res.render('home')
})
```

```html
<h1>Search for GIFS</h1>
```

# Adding a Search Form

Let's add a search form to your html.

```html
<!-- home.handlebars -->
<h1>Search for GIFS</h1>
<form action="/">
  <input type="text" name="term">
  <button type="submit">Search</button>
</form>
```

Navigate to `localhost:3000` and let's look at your form. Pretty plain but it will work!

Enter something into the input field and hit enter or click on `Submit`.

> [solution]
> Your form should navigate you to `/?term=YOUR+SEARCH+TERM`. This means that their will be a **url query string** available called `term` inside of your root route.

# Log the Search Term

Let's update our root route to use that url query string called `term` that we are passing in through the `?term=` part of the url.

Let's use the JavaScript `console.log()` function to print the url query string and check that the url query string is available in the server. Since you are calling `console.log()` on the server, the log will print out on the terminal

```js
// example URL "http://localhost:3000/?term=hey"
app.get('/', (req, res) => {
  console.log(req.query) // => "{ term: hey" }
  res.render('home')
})
```

> [solution]
> You should see this in your terminal window that is running your server
```
[nodemon] starting `node app.js`
Example app listening on port 3000!
{ term: 'YOUR TEST TERM' }
```
