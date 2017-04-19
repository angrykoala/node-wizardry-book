# Introduction to JavaScript \(and ES6\)

> Remember: Java is to JavaScript what Car is to Carpet

JavaScript is a \(relatively\) easy-to-learn language, with a syntax that result familiar to most programmers, as is "similar" to C++, Java, or python. Originally intended for browser-side scripting, there are a big amount of tutorials and documentation to start programming in this messy and lovely language.

In this small introduction, however, I will quickly introduce the basics, skipping the references to browser-side programming as are not needed for node.js. I will also introduce the latest features in JavaScript \(ES6\) that are usually left out in old guides or browser-side programming \(aaah, lovely browser-compatibility\). With node.js we can use all the latests js features without fear, as long as our node.js is up to date.

For a full guide on JS programming, use explicit JS programming tutorials/books, as a lot of thing are not included in this introduction.

You can tests all the snippets here by writing them on the node REPL.

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

JavaScript is a particularly simple language when it comes to data structures, prior to ES6 you only had 2 options when it comes to store your data \(and, one is, in fact, implemented in the other\). Despite the few options, those structures are incredibly versatile, allowing to manipulate data in an extremely easy way.

### Basic data structures

The two "primitive" data structures of JavaScript are:

* **Objects: **
* **Arrays**:

_**Objects**_

"Hi, I'm an object. You may remember me from such chapters as _variable types_._ \_An object is a set of pairs key-values, it is used mainly to represent \_classes instances, map structures \_or just to glue several things together. It is describe between \_brackets _`{ }`, each pair is represented as `key: value`and each pair is separated by a _comma_. For example:

```js
let robot= {
    name: "Marvin",
    age: 124,
    race: "Paranoid Robot"
}
```

The **key** must be an _string_ \(or _Symbol_\), the **value** can be anything, including _functions_ or other objects \(including itself\).

Object elements can be accesses either with `.` \(`robot.name`\) or using the _square brackets_ \(`robot["name"]`\), trying to access to an non-defined member \(e.g `robot.love` will return `undefined)`

> **Pro Tip**: Be aware that while accessing an undefined member will not be a problem, trying to access to a member of an `undefined` or `null` variable will throw an error \(e.g. `robot.love.me`\)

All non-primitive types are defined as objects \(including arrays and functions\), and any class you create will instance objects \(classes will be reviewed later\). An object can also be used as a _map_ data structure. However, ES6 also provides a specific data structure for this case, we will see it later.

_**Array**_

Arrays are represented using _square brackets _`[ ]`and each value is separated by a _comma. Arrays are commonly used as lists_ or _vectors_. For example:

```js
let characters = ["Zaphod", "Ford", "Arthur", robot, 42];
```

As you can see, an array can store any type, and mix types \(this includes _objects_, _functions_ and, _itself_\)

To access/modify elements, you can use \_square brackets \_with a number:

```js
characters[0]; // "Zaphod"
characters[1]; // "Ford"
characters[10]; // undefined
characters[-1]; // undefined
```

To add an element to the end of the array you can use the method `push`to add an element to the end of the array. The variable `length` returns the size of the array:

```js
let races=["Humans"];
races.length; // 1
races.push("Vogons");
races.length; // 2
```

The method `pop` will remove and return the last element of the array:

```js
races.pop(); // "Vogons"
races.length; // 1
```

Arrays are usually represented as objects with numbers as key \(or, particularly, stringified numbers\). However, most interpreters make a lot of performance optimizations on arrays, making them usually faster than objects for adding/removing elements to the end and radom/iterative access.

Arrays also provide a lot of methods to manipulate the array, you can check them on [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

> **Pro Tip:** As arrays are also objects, you can use anything as index, but it is heavily **not** recommended, if you want and object, use an object.
>
> **Pro Tip 2:** You can set any index of the array at any moment \(e.g. `characters[40] = "Deep Thought"` , it will fill the array with `undefined` values up to that point, making it's length equal the latest index used. This is **not** recommended either unless an array full of undefined is you desired result.

### ES6 new data structures

ES6 introduced 2 more data structures as built-in objects: **map** and **set**, as well as the _weak_ key versions: **weakMap** and **weakSet**. While these structures are not as versatile as the primitive structures, its use is recommended for the specific cases that are designed for, as provide specific functionality for those cases, and usually an improved performance, leading to a simpler and more efficient code.

_**Map**_

A map is a data structure that stored elements assigning them to an unique key.

```js
let cast=new Map();
map.set("main","Arthur");
map.set("sidekick", "Ford");
map.get("main"); // Arthur
```

As you can see, maps are similar to a native objects \(in fact, object have been traditionally used as Maps structures\) but using `set` and `get` instead of \_square brackets. \_However, maps have some key differences with objects:

* The key can be anything, including **null**, **undefined **and **functions**.
* Maps provides a `size`variable and are iterable, like arrays.
* Map doesn't contain default keys.

> **Pro Tip:** As maps are objects, using _square brackets_ in a map **won't** throw an error, in fact, the data will be stored as in any other object, but it **won't** be stored as part of the map, but as a separate key. It is heavily recommended **not** to use square brackets at all with maps.

_**Set**_

Sets allows you to store unique values. It is different of an array as if the same value is added twice, it will only store one instance.

```js
let spaceships=new Set();
spaceships.add("Heart of Gold");
spaceships.add("Vogon Constructor");
spaceships.size(); // 2

spaceships.has("Heart of Gold"); // true
spaceships.has("Tardis"); // false
spaceships.add("Heart of Gold");
spaceships.size(); // 2

spaceships.delete("Hearth of Gold"); // true
spaceships.size(); // 1
spaceships.delete("Tardis"); // false
```

As you can see, sets are useful to count or remove repeated elements.

> **Pro Tip:** When adding objects, equity is defined by the object reference, so a Set may store different objects that have the same members, but not multiple references to the same object.

**WeakMap** and **WeakSet**

These 2 structures behave almost exactly as the previous two, however they store the object references as _weak_ references, which mean that the references will be removed by the garbage collector if there are not more references to those \(Garbage collection and performance will be further discussed in [JS Performance and Garbage Collector](/advanced-topics/js-performance-and-garbage-collector.md).

Having weak references is particularly useful when you want to handle loose structures with a lot of living objects without handling memory allocation. However, you cannot reliably know the size of the structures when using weak references.

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
  if (obj.hasOwnProperty(key)) {
    // This if is required to ensure that we only iterate in the object properties, and not the parent

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

> No, here we are not going to talk about functional programming

Functions is one of the most interesting features of js \(yes, functions, I know it doesn't sound very fancy\).

To declare a function in JavaScript we use the following syntax:

```js
function getUltimateAnswer(){
    return 42;
}

getUltimateAnswer(); // 42
```

As you can see, it is pretty straightforward. Now you may be thinking. What's so great about this?.

In a nutshell, the most interesting fact about JS functions is that they are _object_ \(throws confetti\), which means that they can be used as any other variable:

```js
function funcA(){
    return "A";
}
let f1=funcA;
f1(); // "A"

let f2=function(){
    return "B";
}
f2(); // "B"
```

As you can see, it is possible to creare _anonymous_ functions with _function\(\)_ and assign one or more variables to them. This allows to some interesting behaviours that we will discuss in a moment.

Functions, as any other object, can be attached to an object as a value:

```js
let ford={
    name: "Ford",
    items: ["Towel", "Guide"],
    panic: function(){
        return "don't";
    }

ford.name; // "Ford"
ford.panic(); // "don't"
```

Hey, but that looks a lot like a class! Is that funny little voice in your head that. As we will discuss later, JS provides a very specific of dealing with OOP, which is, partialy solved with implementations similar to the one above.

> **Pro Tip:** As functions are objects, you can actually add other members to it `getUltimateAnswer.lifeUniverseEverything=42` However, it may lead to confussion.
>
> **Pro Tip 2:** Most of these pro tips are actually things you shouldn't do.

### The Magic of Callbacks

As mentioned before, functions can be handled as variables, and can be assigned. This variable, like any other variable, can be passed to a function as a parameter, then, that function can call the function passed as a parameter. This is a _callback_ \(epic music\).

```
function panic(){
    return "Panic!";
}

function dont(callback){
    console.log("Don't " + callback());
}

dont(panic); // "Don't Panic"
```

In this example you can see how callbacks can be used to modify the behaviour of a function, here the result of the callback is used in the output generated by the `dont` function. Any function can be used as callback, including the same function, however, if the function doesn't behave as expected it usually ends like Sean Bean in \(any\) film.

Callbacks are commonly used to call a function when a tasks finish \(hence the name callback\).

Now you may be thinking. Couldn't I just execute `panic` and pass the result as a parameter to `dont`? The answer is _yes_. Your next question may be. If I can do that. Why, by the beard of Thorin would I need callbacks?

The answer, of course, is the asyncronous behaviour of JavaScript. Remember the "Node.js uses an event-driven, non-blocking I/O model"? What does non-blocking I/O means?.

For those that already worked with JavaScript using JQuery, or the classic setTimeout, callbacks may be a weird quirk of the language that sometimes must be used. However, because of how Node.js API is made \(you hear a whisper in the darkness "non-blocking I/O"\) and how internally works, callbacks are constanly needed.

I will not bore you anymore with "_Node.js is cool because it does weird async stuff" _anymore, just keep in mind that studying is important, but callbacks are _importanter._

To understand callbacks a bit better, lets write an example with the plain old javascript, without Node.js API:

```js
function onFinish(){
    console.log("So Long, and Thanks for All the Fish");
}

setTimeout(onFinish,1000);
console.log("The dolphin said");
```

`setTimeout` is a JS built-in function that executes the callback after the given time \(in ms\) pass. In this case, it will execute onFinish after one second.

Intuitively, you may think that setTimeout will wait 1 second,  _"So Long, and Thanks for All the Fish" _will be logged, and afterwards, _"The dolphin said"_. However, if you execute the example you'll see that "_The dolphin said"_ is logged inmediatly, and after 1 second, the other message is shown.

This is due to the async nature of JavaScript \(Now your mouth should be open as you find yourself in a new state of consciousness above the rest of the mortals, among the gods that left the cavern before you\). Well, maybe it is not such a surprise, but is a cool thing.

Now, maybe, you could imagine setTimeout no only as a "Wait" function, but as an actual I/O function that doesn't depends on your code, something like _readFile\(\)_ or _download\(\)_.Being able to asyncronously perform tasks like those, in the same fashion as setTimeout allows you to avoid working with nasty threads and optimise resources when you want to perform several I/O operations at the same time \(which, suprise, is the usual case for a webserver\).

So, in a pseudocode with an invented library, we could write something like this:

```js
onFinish(){
    console.log("File loaded");
}

readFile("File1",onFinish);
readFile("File2",onFinish);
```

In that example, we will start reading both files roughly at the same time, and when any of those is finished, _onFinish_ will be called. This means that _onFinish_ will be called twice.

In a classic, on thread secuantial fashion, first File1 will be loaded, and after that File2 will start loading. With this approach, if File1 is extremely large, while File2 is small, File2 will finish before and we will be able to start processing _asap_. This is particularly convenient, not only for reading files, but for example, handling users requests. We don't want a simple request to be blocked until another, potentially larger and slower, request is finished.

To solve this problem, in most other languages, multithreading is used. With a different thread per request. This not only causes overhead, but it also overcomplicates the code in most cases. Whith JS non-blocking I/O, any multithread used is transparent, and with a few callbacks I/O can be handled in an efficient way.

So, in a nutshell: "_Node.js is cool because it does weird async stuff"._

### Scopes

### Arrow functions

## The Treachery of Classes

> Ceci n'est pas une classe

## Some ES6 functions and methods

## Introduction to Node.js API

## Error Handling

try..catch

## Common Pitfalls



