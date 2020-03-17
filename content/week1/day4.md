---
title: "Day 4: Cloning and localStorage"
weight: 4
---

<date>Thursday, June 7, 2018</date>

## Lecture Videos

Morning:

* [Playlist](https://www.youtube.com/watch?v=AxtgfBl_yIw&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp) | [Day 4, part 1](https://www.youtube.com/watch?v=eEYJ1o8MJ6o&index=37&list=PLuT2TqJuwaY-wZ8GKN0bjgCwNVf1WpEGp)

Afternoon:

* [Playlist](https://www.youtube.com/watch?v=GOQvgEk9IBM&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA) | [Day 4, part 1](https://www.youtube.com/watch?v=ALB4iyvwGUM&t=0s&list=PLuT2TqJuwaY90mQ7meSdhHMX6FbfCaLNA&index=43)

## Topics

### `bind()`

* [`bind()` on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
* [JavaScript `bind` function](http://krasimirtsonev.com/blog/article/JavaScript-bind-function-setting-a-scope) blog post by Krasimir Tsonev

### DOM Manipulation

* [remove](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove) (experimental)/[removeChild](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
* [cloneNode](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode)
* [parentElement](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentElement)/[parentNode](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode)
* [insertBefore](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore)
* [closest](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest) (experimental)

### `localStorage` [↓](#localstorage)
* [Using `localStorage`](https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/)
* `JSON.stringify`
  * [Using `JSON.stringify`](http://www.dyn-web.com/tutorials/php-js/json/stringify.php)
  * [Live example](http://jsfiddle.net/queryj/hLkUz/)
  * [API reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), including optional arguments for whitelisting properties and transforming the data as it's stringified
* `JSON.parse`
  * [Using `JSON.parse`](http://www.dyn-web.com/tutorials/php-js/json/parse.php)
  * [API reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse), including optional argument for transforming the data as it's parsed

### Font Awesome [↓](#font-awesome)
* [Docs](https://fontawesome.com/)
* [Getting started](https://fontawesome.com/get-started/svg-with-js)
* [Icon list](https://fontawesome.com/icons?d=gallery&m=free)
* [How to use it](https://fontawesome.com/how-to-use/svg-with-js)

### JavaScript Classes [↓](#javascript-classes)
* Class declarations
* The `constructor` function
* Methods
* Instantiating objects from a class

## Examples

### `.cloneNode`
Sometimes it may be easier to clone an existing node rather than build an entirely new one, especially if the markup is complex.  In our 'Tatum Tots' project, we kept a hidden `li` in the DOM that we cloned every time we needed to render a new list item.

{{< code html >}}
&lt;li class="flick grid-x align-middle template"&gt;
  &lt;span class="flick-name cell auto"&gt;sdfkjhgds&lt;/span&gt;
  &lt;span class="actions button-group cell shrink"&gt;
    &lt;button class="fav button warning"&gt;fav&lt;/button&gt;
    &lt;button class="remove button alert"&gt;del&lt;/button&gt;
  &lt;/span&gt;
&lt;/li&gt;
{{< /code >}}

{{< code css >}}
/* hides any 'li' with a 'template' class */
li.template {
  display: none;
}
{{< /code >}}

{{< code js >}}
const list = document.querySelector('ul')
const templateItem = document.querySelector('li.template')

// Make a copy of the templateItem
// Pass 'true' as an argument to clone all children as well
const newItem = templateItem.cloneNode(true)

// remove 'template' class so it is no longer hidden
newItem.classList.remove('template')

list.appendChild(newItem)
{{< /code >}}

### localStorage

`localStorage` is storage in your web browser that conforms to Web Storage API.  It is scoped by domain, meaning other websites cannot access data stored by your website and vice versa.  The data in `localStorage` persists in the browser until removed, even if the browser is closed and re-opened.

To set an item, use `localStorage.setItem`, and retrieve data using `localStorage.getItem`.  It is important to remember that values stored will always be strings, so it may be use necessary to use the `JSON.stringify` and `JSON.parse` methods to set and retrieve non-string data.  JSON stands for **J**ava**S**cript **O**bject **N**otation.  To learn more about JSON, click [here](https://www.w3schools.com/js/js_json_intro.asp).

{{< code js >}}
const myObject = {
  thisIsCool: true
}

localStorage.setItem('myObject', myObject)
localStorage.getItem('myObject') // => "[object Object]"
// localStorage saves the result of the implicit myObject.toString() call

localStorage.setItem('myObject', JSON.stringify(myObject))
// calling JSON.stringify converts the object to a JSON string representation
// so it can be stored in localStorage without loss of data

const retrievedObject = localStorage.getItem('myObject') // => "{"thisIsCool":true}"
JSON.parse(retrievedObject) // => {thisIsCool: true}
// JSON.parse converts the retrieved JSON string back into a JavaScript object
{{< /code >}}

### Font Awesome

Font Awesome provides hundreds of vectorized, professional-looking icons for free.  Once you've linked to the CDN or have Font Awesome downloaded and included in your project, use `<i>` tags with appropriate classes to render the icons you want.

{{< code html >}}
&lt;-- Sample script tag to include Font Awesome in HTML --&gt;
&lt;script defer src=&quot;https://use.fontawesome.com/releases/v5.0.13/js/all.js&quot; integrity=&quot;sha384-xymdQtn1n3lH2wcu0qhcdaOpQwyoarkgLVxC/wZ5q7h9gHtxICrpcaSUfygqZGOe&quot; crossorigin=&quot;anonymous&quot;&gt;&lt;/script&gt;

&lt;-- Renders a sweet camera icon --&gt;
&lt;i class=&quot;fas fa-camera-retro&quot;&gt;&lt;/i&gt;
{{< /code >}}


### JavaScript Classes

JavaScript is not a class-based language like C++, Java, or Ruby.  It uses [prototypal inheritance](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) instead.  However, as of ES2015, the `class` keyword was added to the language to provide a more concise syntax and similarity to popular class-based languages.

A class is essentially a constructor of Objects.  Methods and properties in the class will be inherited by each object that is constructed by the class.  Object instances are created by using the `new` keyword.  Classes have a `constructor` method, which is called when instances are created and allows for configuration of the object.

{{< code js >}}
class Dog {
  constructor() {
    this.furColor = 'brown'
  }

  bark() {
    console.log('WOOF')
  }
}

const bowser = new Dog();
bowser.furColor // => 'brown'
bowser.bark()   // => 'WOOF'
{{< /code >}}

Classes can also inherit from another class.  Inheritance is specified using the `extends` keyword.  When a class inherits from another, it has access to the methods and properties of *both* classes, although if both classes implement the *same* property or method, the child class will take precedence.

{{< code js >}}
class Animal {
  constructor() {
    this.furColor = 'brown'
  }

  speak() {
    console.log('Some sort of noise')
  }
}

class Dog extends Animal {
  constructor() {
    this.furColor = 'black'
  }

  bark() {
    console.log('WOOF')
  }
}

const bowser = new Dog()
bowser.furColor // => 'black'
bowser.speak()  // => 'Some sort of noise'
bowser.bark()   // => 'WOOF'

const rodent = new Animal()
rodent.furColor // => 'brown'
rodent.speak()  // => 'Some sort of noise'
rodent.bark()   // => Uncaught TypeError: rodent.bark is not a function
{{< /code >}}


## Projects

### Spellbook

[Morning](https://github.com/xtbc18s2/spellbook) | [Afternoon](https://github.com/xtbc18s2/spellbook/tree/afternoon)

## Homework

* Do whatever practice is necessary to better understand the topics we've covered this week.

* Try the official [React Tutorial](https://reactjs.org/tutorial/tutorial.html)

### Bonus Credit

* Continue to enhance the Spellbook project. For example, make spells editable (look up `contentEditable`).

### Super Mega Bonus Credit

* Have a great weekend!
