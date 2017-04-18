# Introduction to JavaScript \(and ES6\)

> Remember: Java is to JavaScript what Car is to Carpet

JavaScript is a \(relatively\) easy-to-learn language, with a syntax that result familiar to most programmers, as is "similar" to C++, Java, or python. Originally intended for browser-side scripting, there are a big amount of tutorials and documentation to start programming in this messy and lovely language.

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

* **Number**: used for integer and float numbers \(`5`, `0`, `-3`, `4.3`\).
* **String**: used for text and characters \(`"Hello"`, `"a"`, `""`\).
  * Strings can be delimited with `" "`,`' '` and, in ES6, with ` `, which allows _multiline_ strings.
* **Boolean**: either `true` or `false`.

* **Undefined**: used for a non-defined variable \(e.g. `var a;`\).

  * It is possible to set a variable to _undefined_ by writing: `var a=undefined`. 

* **Null**: Represents an invalid or non-defined object. While similar to _undefined_, null values must be explicitly set.

  * To set a variable to null, `var a=null`

* **Object**: Any non-primitive type is defined as an object \(including classes instances and arrays\), it is usually defined as a pair key-value inside brackets: `{key: value}`

  * `var a={}` will define an empty object.

* **Symbol**: Introduced in ES6, symbols can be used as keys of an object.

### Let and const

In ES6,  `let` and `const` keywords were added to be used in place of `var`

* **let** provides the same functionality as `var` however the scope of the variable is the code block it is defined, instead of the whole function. This avoids some pitfalls that may happen using `var` as let rules are more intuitive.
* **const** declares a variable that can not be reassigned, this means that for primitive values \(string, number, boolean, null, undefined\) it cannot be modified. Objects, however, can be modified, even if they are constant, but the variable will always reference the same object.

```js
const a="Hello";
a="Bye"; //Error

const obj={
    foo: "bar"
};
obj.foo="Hello"; // Valid

obj={} // Error
```

If your application required wide compatibility \(old browsers-compatible or node &lt;4\) `var` should be used instead. However, for modern js development `let` and `const` are recommended. For this guide we will use `let` and `const`.

## Data Structures

### Basic data structures

### ES6 new data structures

## Conditionals and loops

JavaScript implements conditionals and loops in a similar fashion as C, Java or Python:

**If-else clause**

```js
if(condition){
    // do this
} else if(secondCondition){
    // do that
} else{
    // no conditions met
}
```

**Switch clause**

```js
switch(expression) {
    case "a":
        // do Stuff if a
        break;
    case "b":
        // do stuff if b
        break;
    default:
        // if no condition met
}
```

**for loop**

The basic implementation of for loops is similar to that found in C or Java:

```js
for(var i=0;i<100;i++){
    // do stuff 100 times
}
```

However, JS offers alternative versions of for loops to iterate through an object or array:

**for...in loop**

The for in loop allows to iterate through the properties of an object:

```js
for (var key in obj) {
  if (obj.hasOwnProperty(key)) { // Required to ensure that we only iterate in the object properties, and not the parent
    // obj[key] is the value
  } 
}
```

**for...of loop**

Introduced in ES6, the for...of loop iterated through iterables such as arrays:

```
var arr=[]
for (let value of iterable) {
  value += 1;
  console.log(value);
}
```

**while loop**

While loops \(and do-while\) work exactly as in other languages:

```js
while(condition){
    // do stuff
}

do{
    // do stuff (at least once)
} while(condition);
```

## Functions

### Scopes

### The Magic of Callbacks

## The Treachery of Classes

## Some ES6 functions and methods

## Introduction to Node.js API

## Error Handling

try..catch

## Common Pitfalls



