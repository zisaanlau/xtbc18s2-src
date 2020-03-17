---
title: "Day 2: Functions and The DOM"
weight: 2
---

<date>Tuesday, June 5, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 2, part 1](https://www.youtube.com/watch?v=piSflVSmiOI&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp&index=6)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 2, part 1](https://www.youtube.com/watch?v=Olz7MncGYJA&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA&index=8)

## Topics

### Functions
* Function Expressions
* Function Declarations
* Function Hoisting ([MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting))

### DOM

* Basic DOM manipulation
  * `document.querySelector`/`document.querySelectorAll`
  * `.textContent`
  * `.innerHTML`
* Developer console
  * `console.log`
  * `debugger`
* Basic [event](https://www.w3schools.com/js/js_events.asp) handling
  * [Events in JavaScript](https://www.kirupa.com/html5/javascript_events.htm) - blog post with more detail than we discussed in class
  * `.addEventListener()` - [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
  * `.preventDefault()`
  * `.target`

### Git

* [Git Guide](http://rogerdudler.github.io/git-guide/)
* [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
* [Understanding Git (part 1): Explain It Like I'm Five] (https://hackernoon.com/understanding-git-fcffd87c15a3)

<div class="img github-flow"></div>

### Other Topics

* [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
* [Google Fonts](https://fonts.google.com/)
* Polyfills
  * [Definition from MDN](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill)
  * [What is a Polyfill?](https://remysharp.com/2010/10/08/what-is-a-polyfill)
* [Placeholder attribute](https://www.w3schools.com/tags/att_placeholder.asp)
* [Child and Sibling Selectors](https://css-tricks.com/child-and-sibling-selectors/) 

## Examples

### Functions
{{< code js >}}
  // Function Declaration (use 'function' keyword)
  function aMostExcellentFunction() {
    console.log('This function is excellent!')
  }

  aMostExcellentFunction() // => 'This function is excellent!'

  // Function Expression (defines a function as part of a larger expression syntax - usually assignment to a variable)
  const anotherExcellentFunction = () => {
    console.log('This function is also excellent!')
  }

  anotherExcellentFunction() // => 'This function is also excellent!'
{{< /code >}}

## Presentations

* <a target="_blank" href="/day02.pdf">Review: Functions</a>

## Projects

### Spellbook

[Morning](https://github.com/xtbc18s2/spellbook) | [Afternoon](https://github.com/xtbc18s2/spellbook/tree/afternoon)

## Homework

* Add a second field of your choice to the form.

### Bonus Credit

Look up `document.createElement` and `appendChild`, and try adding the list items that way, instead of with `innerHTML`.

### Super Mega Bonus Credit

Display each value in the list item (the name, whatever other field you add) in separate elements, and style them differently somehow.

For example:

```html
<li>
  <span class="spellName">Fireball</span>
  <span class="level">lvl 4</span>
</li>
```

### Super Mega Bonus Credit Hyper Fighting

* Build each new element (the `li`, each `span`, etc.) in separate functions.
