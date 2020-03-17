---
title: "Day 7: React Components & Firebase"
weight: 3
---

<date>Wednesday, June 13, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 7, Part 1](https://www.youtube.com/watch?v=KCk5Hiq-jrs&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp&index=81)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 7, Part 1](https://www.youtube.com/watch?v=AGDQRToOTbA&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA&index=86)

## Topics

### React

* Methods as props
* [Conditional Rendering] (https://reactjs.org/docs/conditional-rendering.html#___gatsby)
* The Component Lifecycle
* [If-Else in JSX](https://react-cn.github.io/react/tips/if-else-in-JSX.html)

### JavaScript

* [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
* [Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
* [Ternary operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

### Firebase

* [Firebase](https://firebase.google.com/)

## Examples

### [React](https://facebook.github.io/react/)

#### Methods as props

Sometimes one component needs to update another component's state. It can't do that directly, but it can call a method from that other component if it's available via a prop.

{{< code lang="jsx" line="5,23" class="line-numbers" >}}
import React from 'react'
import ReactDOM from 'react-dom'

const PartyButton = ({ celebrate, celebrations }) =&gt; {
  return &lt;button onClick={celebrate}&gt;Party! {celebrations}&lt;/button&gt;
}

class App extends React.Component {
  constructor() {
    super()
    this.state = {
      celebrations: 0,
    }
    this.celebrate = this.celebrate.bind(this)
  }

  celebrate() {
    const celebrations = this.state.celebrations + 1
    this.setState({ celebrations })
  }

  render() {
    return &lt;PartyButton celebrate={this.celebrate} celebrations={this.state.celebrations} /&gt;
  }
}

ReactDOM.render(&lt;App /&gt;, document.querySelector('main'))
{{< /code >}}

#### The Component Lifecycle

* [React.Component](https://reactjs.org/docs/react-component.html#the-component-lifecycle)
* [State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)

### JavaScript (ES6+)

#### Destructuring assignment

[Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

{{< code js >}}
const myObj = {
  a: true,
  b: 'Destructuring!'
}

let { a, b } = myObj

console.log(a) // => true
console.log(b) // => 'Destructuring!'
{{< /code >}}

## Projects

* Chatarang: [Morning](https://github.com/xtbc18s2/chatarang) | [Afternoon](https://github.com/xtbc18s2/chatarang/tree/afternoon)

## Homework

* Add support for multiple rooms/channels! _Hint_: The first argument (`endpoint`) to `base.syncState` should be different for each room/channel.

* Don't forget to make the sidebar links work!

### Super Mega Bonus Credit

* Add direct messages too!

### Super Mega Bonus Credit Hyper Fighting

* Use Firebase authentication when signing in users. _Hint_: Google authentication is the easiest method.
