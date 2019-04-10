---
title: "Searching Giphy"
slug: search-gifs
---

So now we have done some templating, so we are ready to build the actual feature of the app we want: a Giphy Search.

We've setup the template, so now we want to use the Giphy API to get some data.

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

# Updating the Template

It is a **Best Practice** to work from the "outside-in" so from what the user experiences in the views back to the controller logic and database structure. So we can start by making an HTML template (enhanced by Handlebars) ready to display images from the giphy API.

We'll use the Handlebars.js `{{#each}}` iterator to loop over the array of gifs that Giphy API will return.

```html
<!-- home.handlebars -->
...

{{#each gifs}}
  <img src="{{this.images.fixed_height.url}}">
{{/each}}
```

We access each gif's images and we use the `fixed_height` version so all the gifs are the same height.

If you reload `home` you won't see anything yet, because `gifs` is undefined. Let's define it using the Giphy API.

# Connecting to Giphy API with `giphy-api`

There are two options for using an API. Either you can use the native Node `http` module to call `http.get()` to make a request to these APIs, or someone might have made a **wrapper** to make communicating with an API easier.

In this example we'll first add the **wrapper** library and use that. Then as a stretch challenge you can try to implement the native node.js `http` module.

Let's use the giphy API wrapper called `giphy-api` that makes interacting with the giphy API much simpler. Here are the [giphy-api docs](https://github.com/austinkelleher/giphy-api) if you want to see what other options you have.

# Adding the Wrapper Library

> [action]
> First add `giphy-api` to your project's `package.json` file and `node_modules` folder using this bash command:

  ```bash
  $ npm install giphy-api --save
  ```

> Next change your `app.js` file and root route to look like this:

  ```js
  // app.js
  // Require Libraries
  ...
  const giphy = require('giphy-api')();

  ...

  // Routes
  app.get('/', (req, res) => {
    giphy.search(req.query.term, (err, response) => {
      const gifs = response.data;
      res.render('home', { gifs })
    });
  });
  ```

Now navigate to `/` and see your gifs.

When you refresh your root route with nothing in the form, why do you still see GIFs?

> [solution]
> The answer is because the Giphy API is smart enough to respond with trending GIFs if no search query term is supplied. Nice huh!?

Try adding a query term to your url to see an actual search: e.g. `?term=kittens`

# Connecting to the Giphy API with `http` (optional stretch)

Now that we've setup receiving the `giphy-api` package. As a strech challenge you can implement the query to the API without a library using Node's native `http` module and dealt with the stream of data coming from that http endpoint, now we can use another implementation that uses an open source wrapper called `giphy-api` that makes interacting with the giphy API much simpler.

Update your `app.js` root route to use the `http` to query the Giphy API and use the following code snippet for reference. There is a lot going on so read the comments for each line.

```js
// app.js
...
// REQUIRE HTTP MODULE
const http = require('http');

app.get('/', (req, res) => {
  console.log(req.query.term)
  const queryString = "funny cat";
  // ENCODE THE QUERY STRING TO REMOVE WHITE SPACES AND RESTRICTED CHARACTERS
  const term = encodeURIComponent(queryString);
  // PUT THE SEARCH TERM INTO THE GIPHY API SEARCH URL
  const url = 'http://api.giphy.com/v1/gifs/search?q=' + term + '&api_key=dc6zaTOxFJmzC'

  http.get(url, (response) => {
    // SET ENCODING OF RESPONSE TO UTF8
    response.setEncoding('utf8');

    var body = '';

    response.on('data', (d) => {
      // CONTINUOUSLY UPDATE STREAM WITH DATA FROM GIPHY
      body += d;
    });

    response.on('end', () => {
      // WHEN DATA IS FULLY RECEIVED PARSE INTO JSON
      const gifs = JSON.parse(body).data
      // RENDER THE HOME TEMPLATE AND PASS THE GIF DATA IN TO THE TEMPLATE
      res.render('home', { gifs });
    });
  });
})
```

> [info]
> Node's `http` module uses a data type called a **stream** to receive data as it "streams" into your server. That is why we have to add all the data into the `body` variable and wait until it is done streaming with the `response.on('end')` function. Weird right!? Node does this to take advantage of its unblocking I/O nature. What does that mean?

Still work?

This called **refactoring** code. Developers refactor code to make code more **elegant** meaning more economical, more efficient, and more easy to read.
