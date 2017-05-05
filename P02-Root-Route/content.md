---
title: "Adding a Template Engine to your Express App"
slug: adding-templating-engine
---

# Adding a Root Route to your Gif Search

Let's add a _root route_ (a url endpoint that goes to the root path: `/`). And let's render a template called `home.handlebars`.

```js
app.get('/', function (req, res) {
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
> Your form should navigate you to `/?term=YOUR+SEARCH+TERM`. This means that their will be a _url query string_ available called `term` inside of your root route.

# Adding a Search to the Root Route

Let's update our root route to use that url query string called `term` that we are passing in through the `?term=` part of the url.

## console.log

Let's use the JavaScript `console.log()` function to print the url query string and check that the url query string is available in the server. Since you are calling `console.log()` on the server, the log will print out on the terminal

```js
app.get('/', function (req, res) {
  console.log(req.query)
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
