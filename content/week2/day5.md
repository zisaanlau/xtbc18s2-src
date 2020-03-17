---
title: "Day 5: Intro to React"
weight: 1
---

<date>Monday, June 11, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 5, Part 1](https://www.youtube.com/watch?v=n-lJN7LcgfM&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp&index=50)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 5, Part 1](https://www.youtube.com/watch?v=vgOsNnD09qM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA&index=62)

## Topics

### ES2015+ (ES6+)
* Modules (import/export) - [ES2015 modules on Babel](https://babeljs.io/learn-es2015/#ecmascript-2015-features-modules)

### [React](https://facebook.github.io/react/)
* [Imperative vs. Declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/)
* Components
  * JSX - [Docs: Introducing JSX](https://facebook.github.io/react/docs/introducing-jsx.html)
  * Props - [Docs: Components and Props](https://facebook.github.io/react/docs/components-and-props.html)
  * State - [Docs: State and Lifecycle](https://facebook.github.io/react/docs/state-and-lifecycle.html)

## Examples

### React

#### Basic App
A basic React application requires a minimum of four things:

1. An HTML file with at least one empty element
2. The React library
3. One or more React Component(s)
4. A JavaScript call to attach the React Component to the empty element in step one

A minimal example:

{{< code html >}}
&lt;-- index.html --&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;Basic React App&lt;/title&gt;
    &lt;script src=&quot;App.js&quot;&gt;&lt;/script&gt;
  &lt;/head&gt;
  &lt;body&gt;
    &lt;div id=&quot;app&quot;&gt;&lt;/div&gt;
  &lt;/body&gt;
&lt;/html&gt;
{{< /code >}}

{{< code jsx >}}
// App.js
class App extends React.Component {
  render() {
    return (
      &lt;h1&gt;Hello, world!&lt;/h1&gt;
    )
  }
}

ReactDOM.render(&lt;App /&gt;, document.querySelector('#app'))
{{< /code >}}

The body of the HTML above contains only an empty `div` with an id of 'app'.  This is where we will tell React to render our app. The `App.js` file defines the `App` component, and also makes the call to `ReactDOM.render`, which attaches `<App />` to the `div#app` element.

React will 'fill in' the div with the return result of the `App` component's `render` method, in this case, the markup `<h1>Hello, world!</h1>`.

#### Props

React components can be thought of as JavaScript functions.  They take in arguments, called `props`, and return markup that gets rendered to the page. Props can be just about anything, including strings, booleans, functions, objects, etc...

{{< code jsx >}}
class App extends React.Component {
  render() {
    return (
      &lt;h1&gt;Hello, {this.props.name}!&lt;/h1&gt;
    )
  }
}

&lt;App name=&quot;Bob&quot; /&gt;
{{< /code >}}

By passing in the string `"Bob"` to the `App` component, we can access that value from within the `App` class as a property on `this.props`.

Our rendered output would then be:

{{< code html >}}
&lt;h1&gt;Hello, Bob!&lt;/h1&gt;
{{< /code >}}

#### State

Components receive _props_ as arguments and cannot change their values. Data that needs to change belongs in _state_.

State should be initialized in the constructor and updated via `setState`.

{{% aside danger Do Not Modify State Directly %}}
Always use `setState` to modify a component's state. The only time you should set state directly is in the constructor.
{{% /aside %}}

{{< code jsx >}}
class App extends React.Component {
  constructor() {
    super()
    this.state = {
      count: 0
    }
  }

  increment(ev) {
    count = this.state.count + 1
    this.setState({ count })
  }

  render() {
    return (
      &lt;button type="button" onClick={this.increment.bind(this)}&gt;
        Click to Increment
      &lt;/button&gt;
      &lt;p&gt;
        Button has been clicked {this.state.count} times
      &lt;p&gt;
    )
  }
}

&lt;App /&gt;
{{< /code >}}

#### Modules

With [modules](https://babeljs.io/learn-es2015/#ecmascript-2015-features-modules), you can define each component in separate files, importing them as needed.

**Header.js**

{{< code jsx >}}
class Header extends React.Component {
  render() {
    return (
      &lt;h1&gt;Hello, {this.props.name}!&lt;/h1&gt;
    )
  }
}

export default Header
{{< /code >}}

**App.js**

{{< code jsx >}}
import Header from './Header'

class App extends React.Component {
  render() {
    return (
      &lt;Header name=&quot;Bob&quot; /&gt;
    )
  }
}

export default App
{{< /code >}}

## Presentations

* <a target="_blank" href="/intro-to-react.pdf">Intro to React</a>

## Projects

* Reactrobats on CodePen: [Morning](https://codepen.io/dstrus/professor/XYMVpg/) | [Afternoon](https://codepen.io/dstrus/professor/rKyqWr/)
* [Dwarf-Underground (Original)](https://github.com/xtbc18s2/dwarf-underground)
* Dwarf-Underground (Edited, with React Components): [Morning](https://github.com/xtbc18s2/dwarf-morning) | [Afternoon](https://github.com/xtbc18s2/dwarf-afternoon)

## Homework

### Basic Requirements

* Split the page into at least 6 total components

### Bonus Credit

* Split the page into at least 10 total components, including components *in* components

### Super Bonus Credit

* Render the four article links at the bottom of the screen using `map` and passing in the props they need

### Super Mega Bonus Credit

* Make a component that contains a text field for leaving a comment
* Have the text field appear only when the 'comments' link at the bottom of the article is clicked

### Super Mega Bonus Credit Hyper Fighting

* Actually display comments that are entered and submitted
