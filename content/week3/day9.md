---
title: "Day 9: Routing and Fetching"
weight: 1
---

<date>Monday, June 18, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 9, Part 1](https://www.youtube.com/watch?v=U3mrPNcW5FY&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp&index=109)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 9, Part 1](https://www.youtube.com/watch?v=gsWh6N557yU&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA&index=115)

## Topics

### Routing

* React Router
  * `<Router />`
  * Links and NavLinks
  * Routes
  * `history`

### Fetching Data

* The Fetch API
* Promises
* Parsing the response

### Deployment
* [Firebase](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#firebase)

## Examples

### Routing

[React Router](https://github.com/ReactTraining/react-router) provides a routing solution that allows us to change what UI we render based on the current URL.  The router is a _Higher Order Component_ that wraps a React app and allows us to navigate without additional requests and responses to and from the server.

#### Router Setup

Setting up React Router is easy. For web projects, install `react-router-dom`

{{< term >}}
yarn add react-router-dom  # install react router with yarn
{{< /term >}}

or

{{< term >}}
npm install --save react-router-dom  # install react router with npm
{{< /term >}}

Then, in your `ReactDOM.render` call, attach the Router as your base element, wrapping the root-level `<App />` component.  The whole app is now contained within the Router component, so we can take advantage of it anywhere.

**index.js**

{{< code jsx >}}
import React from 'react'
import ReactDOM from 'react-dom'
import { BrowserRouter as Router } from 'react-router-dom'
import App from './App'

ReactDOM.render(
  &lt;Router&gt;
    &lt;App /&gt;
  &lt;/Router&gt;,
  document.getElementById('root')
)
{{< /code >}}

#### Routes

The core of React Router is the `<Route />` component.  It allows you to specify what UI to render when a particular URL is matched.  For instance, if we wanted to render a `<Users />` component when we matched a `/users` URL, we could make the following Route:

{{< code jsx >}}
&lt;Route path='/users' component={Users} /&gt;
{{< /code >}}

If you don't want to render a whole component, a Route can alternatively accept a `render` prop, which accepts a function that returns JSX:

{{< code jsx >}}
&lt;Route path='/users' render={() => &lt;h1&gt;Users Path!&lt;/h1&gt;} /&gt;
{{< /code >}}

One important thing to keep in mind is that if we define a Route's path as `/users`, that will match both `/users` _and_ `/users/123`, because both begin with `/users`.  If we want the Route to match only when the path is _exactly_ `/users`, we can add the prop `exact` to our Route component.

{{< code jsx >}}
&lt;Route exact path='/users' component={Users} /&gt;
{{< /code >}}

#### Links

React Router also provides `<Link />` and `<NavLink />` components to make it easy to generate links to Routes. If we want to generate a Link that goes to `/about`, we can do the following:

{{< code jsx >}}
&lt;Link to='/about'&gt;About&lt;/Link&gt;
{{< /code >}}

NavLinks are similar, but provide some additional functionality.  The main difference is that they will add an `activeClassName` to the rendered link if the current URL matches the `to` property of the NavLink.  This allows active links to be styled differently than inactive links.

{{< code jsx >}}
&lt;NavLink to='/'&gt;Home&lt;/NavLink&gt;    // rendered link tag will have '.active' class when URL is '/'
{{< /code >}}

#### History

The `history` object is maintained and updated by the Router to keep track of where the user has navigated within the app.  It is passed to every component contained within the Router as part of the component's `props`.  It has a variety of helpful properties and methods that provide information and navigation. Here are just a few:

{{< code js >}}
history.length             // number of history entries
history.location           // provides the current location
history.push(path)         // navigates to a new path
history.go(n)              // navigates n steps through history stack
history.goBack()           // go back one step (history.go(-1))
history.goForward()        // go forward one step (history.go(1))
history.block(prompt)      // block navigation
{{< /code >}}

### Fetch

> The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.  It also provides a global `fetch()` method that provides an easy, logical way to fetch resources asynchronously across the network.

[_MDN - Using Fetch_](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

If we need to get data from a remote server (or send some to one), there are several ways to do it.  In vanilla JS, there is `XMLHttpRequest`, jQuery provides `$.ajax`, and there are a variety of other packages and libraries that provide their own version.  Luckily, there is a new kid in vanilla JS town - the _Fetch API_.

`fetch()` is a globally available, easy to use way to asynchronously send and receive data.  The simplest usage of fetch is to simply provide it with the URL of the request, and it will perform a `GET` request by default.  The `fetch()` function returns a promise that resolves when the data is received.  Once it is received, we can process and use the data with functions provided to the promise's `.then()` callbacks.

{{< code js >}}
fetch('https://api.mywebsite.com/users')    // fetch users data from 'mywebsite' api
  .then(response => response.json())        // parse the response json into JavaScript object(s)
  .then(users => console.log(users))        // log the parsed users to the console
  .catch(error => console.warn(error))      // if any errors occur, log them to the console
{{< /code >}}

{{% aside info "Fetch does more than just fetch" %}}
If no second argument is provided to `fetch()`, it defaults to a standard `GET` request.  However, the second argument can be a configuration object, allowing it to use different HTTP methods, set Headers, include Credentials, etc.  To find out more, check out [the docs](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
{{% /aside %}}

### Deploying

Now that Chatarang has routing, deployment gets a bit more complicated.  Our app is a single-page application, so the server that our app is deployed to needs to always return `index.html` (the one page in our single-page app).  However, if we type `https://{yourdomainhere}/notes` in the address bar, the server will try to find a file called `notes.html` to send back (which it won't find, of course).  So how do we get it to always respond with `index.html` and let our client-side router handle the routing?

#### Firebase

Firebase _does_ allow for the server to be configured to always return `index.html`, so that is the option we chose during class.  To do so, we first need to install Firebase's CLI tools.

{{< term >}}
npm install -g firebase-tools
{{< /term >}}

Once the Firebase tools are installed, we can use them to login, initialize a firebase project, and deploy.  (Note, make sure you have made a production build with `npm run build` before deploying).

{{< term >}}
firebase login
firebase init
firebase deploy
{{< /term >}}

{{% aside info "Firebase Init" %}}
`firebase init` will prompt you to answer a bunch of questions about how you want to configure the app you are deploying.  For more information about how to answer those questions, check out the `create-react-app` README [here](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#firebase).
{{% /aside %}}

## Projects

* API Party [Morning](https://github.com/xtbc18s2/api-party) | [Afternoon](https://github.com/xtbc18s2/api-party/tree/afternoon)
* Chatarang: [Morning](https://github.com/xtbc18s2/chatarang) | [Afternoon](https://github.com/xtbc18s2/chatarang/tree/afternoon)

## Homework

#### Chatarang

* Move the list of rooms in state to `Main`, and be sure that the description updates appropriately when changing rooms.

#### API Party

Your assignment, should you choose to accept it (and you should), is to add some more routes to the API Party and fetch data from your favorite APIs. The API you choose is up to you, but be sure to get some data and try to display it in a visually-pleasing way.

In case you don't have a favorite API, here are some suggestions:

* [Google Maps](https://developers.google.com/maps)
* [The Pokéapi](https://pokeapi.co)
* [OpenWeatherMap](https://openweathermap.org/api)
* [Spotify](https://developer.spotify.com/web-api/)

