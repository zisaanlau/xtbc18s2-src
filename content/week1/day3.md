---
title: "Day 3: The DOM Cont'd / Arrays and Objects"
weight: 3
---

<date>Wednesday, June 6, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 3, part 1](https://www.youtube.com/watch?v=ISXr_1-5FzE&index=22&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 3, part 1](https://www.youtube.com/watch?v=ABbWcqaRbrg&index=25&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA)
 
## Topics

### DOM

If we start with the following markup:
{{< code html >}}
&lt;div id=&quot;my-div&quot;&gt;&lt;/div&gt;
{{< /code >}}
We can add additional markup to it programmatically using JavaScript.  One way is to create new HTML elements using `document.createElement`, and adding them by using `appendChild`.  Styling of the element can even be changed by manipulating the element's `style` property.

{{< code js >}}
// create an h1 and modify text content and color
const heading = document.createElement('h1')
heading.textContent = "This is the best heading I've ever seen"
heading.style.color = "red"

// get a reference to the existing div and add the heading as a child element
const div = document.querySelector('#my-div')
div.appendChild(heading)
{{< /code >}}

This will produce the following markup:
{{< code html >}}
&lt;div id=&quot;my-div&quot;&gt;
  &lt;h1 style=&quot;color: red;&quot;&gt;This is the best heading I've ever seen&lt;/h1&gt;
&lt;/div&gt;
{{< /code >}}

* ["Utilizing" the Developer Tools: Selecting and Inspecting DOM Elements](https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference)

### Arrays

* [CodPen Example](https://codepen.io/dstrus/professor/WyxWQE/)
* `Array.map` - [Docs on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map?v=control)
* [Understanding JavaScript's `map()`](https://www.discovermeteor.com/blog/understanding-javascript-map/) blog post

### Objects
* Object literals
* Property Naming
* Retrieving property values
* Setting property values

### Styling

#### Flexbox

* [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [Flexbox.io](https://flexbox.io/)
* [Flex-grow](https://css-tricks.com/almanac/properties/f/flex-grow/)

#### Tips and Tricks on CSS

* [CSS Tricks](https://css-tricks.com/)
* [Overflow Property in CSS](https://css-tricks.com/almanac/properties/o/overflow/)

### This

* _default_ binding through function invocation
* _implicit_ binding through method calls
* _explicit_ binding with `.bind`

## Examples

### Arrays
Arrays are extremely useful data structures in JavaScript, as they can be easily iterated and transformed through methods like `map`, `filter`, and `reduce`.  Sometimes, you may have an 'array-like' collection (like a `NodeList` or function arguments) that you would need to convert to an actual Array before you could use these methods.  This can be done using `Array.from`

{{< code js >}}
let paragraphs = document.querySelectorAll('p')
paragraphs.map((p) => {
  p.textContent = "This won't work because paragraphs is a NodeList, not Array!"
})
// => Uncaught TypeError: paragraphs.map is not a function

let actualArrayOfParagraphs = Array.from(paragraphs)
actualArrayOfParagraphs.map((p) => {
  p.textContent = "This totally does work because we created an Array from our NodeList!"
})
{{< /code >}}

{{% aside info "Requirements for 'Array.from'" %}}
What objects can you convert to an Array using 'Array.from'?  

* Any array-like object with a 'length' property and indexed elements
* Iterable objects (like Map or Set)

For more info, check out [this article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from?v=control) on MDN.
{{% /aside %}}

### Objects
Almost everything in JavaScript is an Object.  The easiest way to create new Objects is with the [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer), more commonly known as 'object literal' syntax.  Basically, use curly braces to make an object `{}` and fill in the properties that you want.

Objects contain `key`/`value` pairs that allow you to set and retrieve values from them.

{{< code js >}}
// create a new object and assign some properties
const myObject = {
  prop1: 'Hello there',
  prop2: 42
}

// access the values in several ways, usually 'dot' or 'square bracket' notation
myObject.prop1 // => 'Hello there'
myObject['prop1'] //=> 'Hello there'

// new key/value pairs can also be assigned with these notations
myObject.prop3 = 'New Value!'
myObject['prop4'] = 'Newest Value!'

console.log(myObject)
// { 
//   prop1: 'Hello there',
//   prop2: 42,
//   prop3: 'New Value!',
//   prop4: 'Newest Value!'
// }
{{< /code >}}

We know that we can iterate through an Array using `map` or `forEach`.  Can we do something similar with objects?  There are a few ways to do it, but one of the newest and easiest is the `Object.keys` method.  It iterates through the enumerable properties of an object, returning an array of the property keys. Once we have an array of keys, we can `map` over _that_ and access each of the object properties individually.

{{< code js >}}
const myObj = {
  a: 'hi',
  b: 42,
  c: [1, 2, 3]
}

const myObjKeys = Object.keys(myObj)    // ['a', 'b', 'c']

myObjKeys.map(key => myObj[key])        // ['hi', 42, [1, 2, 3]]
{{< /code >}}

### This

The same function can have different values for `this` depending on how the function is called/invoked.

{{< code js >}}
const app = {
  sayYeah() {
    console.log(`Yeah, ${this}`)
  },
  
  toString() {
    return 'app object'
  }
}

// When invoked as a method
app.sayYeah() // "Yeah, app object"

// When invoked as an event handler
document
  .querySelector('button')
  .addEventListener('click', app.sayYeah)
  // "Yeah, [object HTMLButtonElement]"

// When manually set with bind
app.sayYeah.bind('w00t')() // "Yeah, w00t"
{{< /code >}}

* [MDN Docs on ES6 Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## Presentations

* <a target="_blank" href="/03-events-functions-arrays-objects.pdf">Day 3 Review</a>

## Projects

### Spellbook

[Morning](https://github.com/xtbc18s2/spellbook) | [Afternoon](https://github.com/xtbc18s2/spellbook/tree/afternoon)

## Homework

* In addition to building a list item and adding it to the DOM (as we are now), also store each spell in an array.

### Bonus Credit

* Add a _delete_ button to each list item that removes it from the list.

### Super Mega Bonus Credit

* Remove the item from the array as well.
