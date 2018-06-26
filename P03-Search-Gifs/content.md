---
title: "Searching Giphy"
slug: search-gifs
---

So now we have done some templating, so we are ready to build the actual feature of the app we want: a Giphy Search.

# Adding a Search to the Root Route (Step 1 - Getting Search Term)

Let's update our root route to use that url query string called `term` that we are passing in through the `?term=` part of the url.

## console.log

Let's use the JavaScript `console.log()` function to print the url query string and check that the url query string is available in the server. Since you are calling `console.log()` on the server, the log will print out on the terminal

```js
app.get('/', (req, res) => {
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

# Adding a Search to the Root Route (Step 2 - Connecting to API)

Now we want to use the Giphy API to get some data.

An **API** stands for **Application Programming Interface**. If a **UI** is a **User Interface**, or how humans use a program, an API is the way another computer program uses a program. APIs are other web servers with their own url endpoints much like the ones you are creating now. Instead of returning HTML templates, however, API endpoints return structured data called JSON.

> [info]
> JSON is a series key/value pairs that can be nested into a hierarchical tree structure, for example:
>
> ```
{
  user: {
    name: "Samuel",
    age: 15,
    hometown: "Iowa City"
    friends: [
      { name: "David" },
      { name: "Sarah" },
      { name: "Kelly" }
    ]
  }
}
> ```

## Connecting to the Giphy API with `http`

There are two options for using an API. Either you can use the native Node `http` module to call `http.get()` to make a request to these APIs, or someone might have made a **wrapper** to make communicating with an API easier.

In this example we are going to avoid adding new modules to our project, so we'll use the `http` module to query the Giphy API search endpoint.

Update your `app.js` root route to use the `http` to query the Giphy API and use the following code snippet for reference. There is a lot going on so read the comments for each line.

```js
// app.js
...
// REQUIRE HTTP MODULE
const http = require('http');

app.get('/', (req, res) => {
  console.log(req.query.term)
  let queryString = "funny cat";
  // ENCODE THE QUERY STRING TO REMOVE WHITE SPACES AND RESTRICTED CHARACTERS
  let term = encodeURIComponent(queryString);
  // PUT THE SEARCH TERM INTO THE GIPHY API SEARCH URL
  let url = 'http://api.giphy.com/v1/gifs/search?q=' + term + '&api_key=dc6zaTOxFJmzC'

  http.get(url, (response) => {
    // SET ENCODING OF RESPONSE TO UTF8
    response.setEncoding('utf8');

    let body = '';

    response.on('data', (d) => {
      // CONTINUOUSLY UPDATE STREAM WITH DATA FROM GIPHY
      let += d;
    });

    response.on('end', () => {
      // WHEN DATA IS FULLY RECEIVED PARSE INTO JSON
      let parsed = JSON.parse(body);
      // RENDER THE HOME TEMPLATE AND PASS THE GIF DATA IN TO THE TEMPLATE
      res.render('home', {gifs: parsed.data})
    });
  });
})
```

> [info]
> Node's `http` module uses a data type called a **stream** to receive data as it "streams" into your server. That is why we have to add all the data into the `body` variable and wait until it is done streaming with the `response.on('end')` function. Weird right!? Node does this to take advantage of its unblocking I/O nature. What does that mean?

Now update your template and use the Handlebars.js `{{#each}}` iterator to loop over the array of gifs that Giphy has returned.

```html
<!-- home.handlebars -->
...

{{#each gifs}}
  <img src="{{this.images.fixed_height.url}}">
{{/each}}
```

We access each gif's images and we use the `fixed_height` version so all the gifs are the same height.

# Adding the Search Term

So now we have to update our code to use the actual term we are getting from our input field. All we have to do is put our `req.query.term` variable in for "funny cat", and now whatever we enter into the form will be queried.

```js
app.get('/', (req, res) => {
  let queryString = req.query.term;
...
});
```

Does it work if you put in "funny puppies" into your search form input and hit the "Search" button?

When you refresh your root route with nothing in the form, why do you still see GIFs?

> [solution]
> The answer is because the Giphy API is smart enough to respond with trending GIFs if no search query term is supplied. Nice huh!?

# Connecting to Giphy API with `giphy-api`

Now that we've setup receiving the giphy api gifs using Node's native `http` module and dealt with the stream of data coming from that http endpoint, now we can use another implementation that uses an open source wrapper called `giphy-api` that makes interacting with the giphy API much simpler.

Here are the [giphy-api docs](https://github.com/austinkelleher/giphy-api) if you want to see what other options you have.


First add `giphy-api` to your project's `package.json` file and `node_modules` folder using this bash command:

```bash
$ npm install giphy-api --save
```

Next change your `app.js` file and root route to look like this:

```js
// app.js

// INITIALIZE THE GIPHY-API LIBRARY
const giphy = require('giphy-api')();

...

app.get('/', (req, res) => {
  giphy.search(req.query.term, (err, response) => {
    res.render('home', {gifs: response.data})
  });
});
```

Still work?

This called **refactoring** code. Developers refactor code to make code more **elegant** meaning more economical, more efficient, and more easy to read.
