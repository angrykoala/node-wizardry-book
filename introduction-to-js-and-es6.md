# Introduction to JavaScript \(and ES6\)

> Remember: Java is to JavaScript what Car is to Carpet

JavaScript is a \(relatively\) easy-to-learn language, with a syntax that result familiar to most programmers, as is "\_similar" \_to C++, Java, or python. Originally intended for browser-side scripting, there are a big amount of tutorials and documentation to start programming in this messy and lovely language.

In this small introduction, however, I will quickly introduce the basics, skipping the references to browser-side programming as are not needed for node.js. I will also introduce the latest features in JavaScript \(ES6\) that are usually left out in old guides or browser-side programming \(aaah, lovely browser-compatibility\). With node.js we can use all the latests js features without fear, as long as our node.js is up to date.

You can tests all the snippets here by writing them on the node REPL

## Variables

JS is dynamically typed which means you don't have to specify what are you going to store in a variable. Not only that, but you can also change the type of a variable any moment.

Traditionally, `var` is used as keyword to define variables:

```js
var a=4; //a is a number
var b="Hello"; // b is a string
var c; //c is undefined

b=5; //we can assign b to a number
```

It is possible to directly assign a variable without `var`

```js
e=5; //This works, but it will create a global variable
```

It is **not** recommended to use variables without declaring them first with `var` to avoid unknown global variables

### Variable types

Even if is dynamically typed, JavaScript uses the following types for its variables:

* **Number**: used for integer and float numbers \(`5`, `0`, `-3`, `4.3`\)
* **String**: used for text and characters \(`"Hello"`, `"a"`, `""`\)
  * Strings can be delimited with `" "`,`' '` and, in ES6, with ``` ```, which allows _multiline_ strings
* **Boolean**: either `true` or `false` 

* **Undefined**: used for a non-defined variable \(e.g. `var a;`\)

  * It is possible to set a variable to _undefined_ by writing: `var a=undefined` 

* **Null**: Represents an invalid or non-defined object. While similar to _undefined_, null values must be explicitly set

  * To set a variable to null, `var a=null`

* **Object**: \(and arrays\)

* **Symbol**: Only in ES6, 



## Conditionals and loops

## Data Structures

### Basic data structures

### ES6 new data structures

## Functions

### Scopes

### The Magic of Callbacks

## The Treachery of Classes

## Some ES6 functions and methods

## Introduction to Node.js API



