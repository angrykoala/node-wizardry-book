# Introduction to JavaScript and ES6

> Remember: Java is to JavaScript what Car is to Carpet

JavaScript is a relatively easy-to-learn language, with a syntax familiar to most programmers, as it's "similar" to C++, Java, or Python. Originally intended for browser-side scripting, there are plenty of tutorials and documentation to start programming in this messy and lovely language.

In this introduction I will quickly introduce the basics, skipping the references to browser-side programming as are not needed for Node.js. I will also introduce the latest features in JavaScript \(ES6\) that are commonly left out in most guides. With Node.js we can use all the latests js features without fear, as long as our Node.js installation is up to date.

For a full guide on js programming, use a full js programming tutorial/books, as a lot of thing are not included in this introduction.

You can tests all the snippets here by writing them on the node REPL.

## Variables

Js is dynamically typed which means you don't have to specify what are you going to store in a variable. You also can also change the type of a variable at any moment.

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

It is **not** recommended to use variables without declaring them first with `var` to avoid unknown global variables.

### Variable types

Even if it is dynamically typed, JavaScript uses the following types for its variables:

* **Number**: used for integer and float numbers \(`5`, `0`, `-3`, `4.3`\).

* **String**: used for text and characters \(`"Hello"`, `"a"`, `""`\).

  * Strings can be delimited with `" "`,`' '` and, in ES6, with \`\`\`\`\`\`\`\`, which allows _multiline_ strings.

* **Boolean**: either `true` or `false`.

* **Undefined**: used for a non-defined variable \(e.g. `var a;`\).

  * It is possible to set a variable to _undefined_ by writing: `var a=undefined`. 

* **Null**: Represents an invalid or non-defined object. While similar to _undefined_, _null_ values must be set explicitly.

  * To set a variable to null, `var a=null`.

* **Object**: Any non-primitive type is defined as an _object_ \(including classes instances and arrays\), it is usually defined as a pair key-value inside brackets: `{key: value}`

  * `var a={}` will define an empty object.

* **Symbol**: Introduced in ES6, symbols can be used as keys of an object.

### Let and const

In ES6,  `let` and `const` keywords were added to be used in place of `var`

* **let** provides the same functionality as `var` however the scope of the variable is the code block in which it is defined, instead of the whole function. This avoids some pitfalls that may happen using `var` as _let_ rules are more intuitive.
* **const** declares a variable that can not be reassigned, this means that for primitive values \(string, number, boolean, null, undefined\) it cannot be modified. _Objects_, however, can be modified, even if they are constant, but the variable will always reference the same object.

```js
const a="Hello";
a="Bye"; //Error

const obj={
    foo: "bar"
};
obj.foo="Hello"; // Valid

obj={} // Error
```

If your application require full retro compatibility \(old browsers or node &lt;4\) `var` should be used instead. However, for modern js development `let` and `const` are recommended. For this guide we will use `let` and `const`.

## Operators
Most operators work in a similar way as they work in Java or other languages, with arithmetic operations (`+`,`-`,`*`,`/`,...), logical operators (`||`, `&&`, `!`) and bitwise operators (`&`,`|`,`~`,...) among others (`==`,`++`).

While most operators work as expected, there are a few interesting cases:

**Comparison operator**

The first difference is the **comparison** operator, in js there are 2 operators: `==` and `===`. The first one will return true if the values are equal, even if the type is different, the second one will also check the type:
```js
5=="5"; //true
5==="5"; //false
```
It is recommended to use the `===` operator whenever possible. Not equal operators work the same way (`!=`, `!==`).

**typeof operator**
The operator `typeof` will return the type of the variable as a string:
```js
typeof 5; // "number"
typeof {}; // "object"
```
This allows you to change the behavior of your code depending of the type of the variable or check that a certain variable is the correct type. Remember that any non-primitive type will return `object`.

> **Pro Tip:** The operator `instanceof` can be used to check the class of an object.


> A full list of operators can be found in https://developer.mozilla.org/en/docs/Web/JavaScript/Guide/Expressions_and_Operators

## Data Structures

JavaScript is a particularly simple language when it comes to data structures, prior to ES6 you only had 2 option to store your data \(and, one is, in fact, implemented in the other\). Despite the few options, those structures are incredibly versatile, allowing to manipulate data in an extremely simple way.

### Basic data structures

The two "primitive" data structures of JavaScript are:

* **Objects**
* **Arrays**

_**Objects**_

"Hi, I'm an object. You may remember me from such chapters as _variable types"_._ \_An object is a set of pairs_ key-values, _it is used mainly to represent class instances, map structures or just to glue several things together. It is describes inside brackets _`{ }`_, each pair is represented as _`key: value`_ and pairs are separated by a \_comma_. For example:

```js
let robot= {
    name: "Marvin",
    age: 124,
    race: "Paranoid Robot"
}
```

The **key** must be an unique _string_ \(or _Symbol_\), the **value** can be anything, including _functions_ or other objects \(even itself\).

Object elements can be accesses either with `.` \(`robot.name`\) or using the _square brackets_ \(`robot["name"]`\), trying to access to an non-defined member \(e.g `robot.love` will return `undefined)`.

> **Pro Tip**: Be aware that while accessing an undefined member will not be a problem, trying to access to a member of an `undefined` or `null` variable will throw an error \(e.g. `robot.love.me`\).

All non-primitive types are defined as objects \(including arrays and functions\), and any class you create will instantiate objects. An object can also be used as a _map_ data structure. However, ES6 also provides a specific data structure for this case, as we will see later.

_**Array**_

Arrays are represented using _square brackets _`[ ]`and each value is separated by a _comma. \_Arrays are commonly used as_ lists_ or \_vectors_. For example:

```js
let characters = ["Zaphod", "Ford", "Arthur", robot, 42];
```

As you can see, an array can store any type, and mix different types together \(this includes _objects_, _functions,_ and _itself_\)

To access/modify elements, you can use _square brackets_ with a number:

```js
characters[0]; // "Zaphod"
characters[1]; // "Ford"
characters[10]; // undefined
characters[-1]; // undefined
```

To add an element to the end of the array you can use the method `push`. The variable `length`  will returns the size of the array:

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

Arrays are usually represented as objects with numbers as keys \(or, particularly, stringified numbers\). However, most interpreters implement performance optimizations on arrays, making them usually faster than objects for adding/removing elements to the end and radom/iterative access.

Arrays also provide a lot of methods for manipulation like sorting or splitting, you can check them on [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array).

> **Pro Tip:** As arrays are also objects, you can use anything as index, but it is heavily **not** recommended, if you want an object, use an object.
>
> **Pro Tip 2:** You can set any index of the array at any moment \(e.g. `characters[40] = "Deep Thought"`\), making it's length equal the latest index used. This is **not** recommended either, due to decreased performance and _undefined_ elements.

### ES6 new data structures

ES6 introduced 2 more data structures as built-in objects: **map** and **set**, as well as the _weak_ key versions: **weakMap** and **weakSet**. While these structures are not as versatile as the primitive structures, its usage is recommended for the specific cases that are designed for, as they provide specific functionality, and usually come with improved performance, leading to a simpler and more efficient code.

_**Map**_

A map is a data structure that store elements assigning them to an unique key.

```js
let cast=new Map();
map.set("main","Arthur");
map.set("sidekick", "Ford");
map.get("main"); // Arthur
```

As you can see, maps are similar to native objects \(in fact, object have been traditionally used as maps structures\), but using `set` and `get` instead of _square brackets_. Maps, however, have some key differences with objects:

* The key can be anything, including **null**, **undefined **and **functions**.
* Maps contain a `size`variable and are iterable, like arrays.
* Maps don't contain default keys.

> **Pro Tip:** As maps are objects, using _square brackets_ in a map **won't** throw an error, in fact, the data will be stored as in any other object. It **won't** be stored as part of the map, but as a separate key. It is heavily recommended **not** to use square brackets at all with maps.

_**Set**_

Sets allows you to store unique values. It core difference with arrays is that if the same value is added twice, it will only store one instance.

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

These 2 structures behave almost exactly as the previous two, however they store the object references as _weak_ references, meaning that the references will be removed by the garbage collector if there are not other references to those. \(Garbage collection and performance will be further discussed in [js Performance and Garbage Collector](/advanced-topics/js-performance-and-garbage-collector.md)\).

Having weak references is particularly useful when you want to handle loose structures with a lot of living objects without handling memory allocation. However, you cannot reliably know the size of the structures when using weak references, as it may change at any moment.

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
for(let i=0;i<100;i++){
    // do stuff 100 times
}
```

However, js offers alternative versions of for loops to iterate through an object or array:

**for...in loop**

The for in loop allows to iterate through the properties of an object:

```js
for (let key in obj) {
  if (obj.hasOwnProperty(key)) {
    // This if is required to ensure that we only iterate in the object properties, and not the parent

    // obj[key] is the value
  } 
}
```

**for...of loop**

Introduced in ES6, the for...of loop iterated through iterables such as arrays:

```js
let arr=[]
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

Functions are one of the most interesting features of js \(yes, functions, I know it doesn't sound very fancy\).

To declare a function in JavaScript we use the following syntax:

```js
function getUltimateAnswer(){
    return 42;
}

getUltimateAnswer(); // 42
```

As you can see, it is pretty straightforward. Now you may be thinking. What's so great about this?.

Simplifying a bit, the most interesting fact about js functions is that they are _objects_ \(throws confetti\), which means that they can be used just as any other variable:

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
}

ford.name; // "Ford"
ford.panic(); // "don't"
```

Hey, but that looks a lot like a class!. As we will discuss later, js provides a very specific way of dealing with OOP, which is, partialy solved with implementations similar to the one above.

> **Pro Tip 1:** As functions are objects, you can actually add other members to it `getUltimateAnswer.lifeUniverseEverything=42` However, it may lead to confussion.
>
> **Pro Tip 2:** Most of these "pro tips" are actually things you shouldn't do.

### Function parameters overloading

js doesn't support function overloading \(multiple functions with the same name but different parameters\). However, because of the loose behaviour of variables, we can easily imitate function overloading:

```js
function salute(name, surname){
    if(surname!==undefined) console.log("Hello "+name+" "+surname);
    else console.log("Hello "+name);
}

salute("Ford","Prefect"); // "Hello Ford Prefect"
salute("Marvin"); // "Hello Marvin"
```

When a parameters is not passed, instead of failing or throwing an error, that parameter is simply an _undefined_ function. because of this, we can simply compare with _undefined_ and modify the function behaviour.

Another common way of dealing with with parameters overloading is using _default_ values. The traditional way is using the operator `|| `:

```js
function salute(name,surname){
    surname=surname || "";
    console.log("Hello "+name+" "+surname);
}

salute("Marvin"); // "Hello Marvin "
```

The operator `|| ` will assign the first operand if is _truthy, _if not it will assign the second operand \(""\). This works for strings, as any string is interpreted as truthy_ _\(event empty string\), while _undefined_ or _null_ is interpreted as falsy. This will not work for numbers, as a 0 is falsy while any other number is truthy.

In ES6 there is a more intuitive way to define default variables:

```js
function salute(name,surname=""){
    console.log("Hello "+name+" "+surname);
}

salute("Marvin"); // "Hello Marvin "

```

**Rest parameters**    
ES6 implements _rest parameters_, which allows you to have n parameters in a function, which will be passed as an array:

```js
function setAliases(name, ...aliases){
        console.log("Name:"+name);
        console.log("A.K.A. "+aliases);
}

setAliases("The Doctor","John Smith", "Doctor Who?", "The Oncoming Storm");
// "Name: The Doctor"
// "A.K.A. ["John Smith", "Doctor Who?", "The Oncoming Storm"]"
```

Rest parameters can be used along with normal parameters, but they must be declared at the end (and only one array).

### The Magic of Callbacks

As mentioned before, functions can be handled as variables. This variables, like any other, can be passed to a function as a parameter, then, that function can call the function passed as a parameter. This is a _callback_ \(epic music\).

```js
function panic(){
    return "Panic!";
}

function dont(callback){
    console.log("Don't " + callback());
}

dont(panic); // "Don't Panic"
```

In this example you can see how callbacks can be used to modify the behavior of a function, here the result of the callback is used in the output generated by the `dont` function. Any function can be used as callback, including the same function, however, if the function doesn't behave as expected it usually ends like Sean Bean in \(any\) film.

Callbacks are commonly used to call a function when a certain task finish.

Now you may be thinking. Couldn't I just execute `panic` and pass the result as a parameter to `dont`? The answer is _yes_. Your next question may be. If I can do that. Why, by the beard of Thorin would I use callbacks?

The answer, of course, is the asyncronous magic of JavaScript. Remember the "Node.js uses an event-driven, non-blocking I/O model"? But, What does non-blocking I/O means?.

For those that already worked with JavaScript (e.g. JQuery), callbacks may be a weird quirk of the language that sometimes must be used. However, in Node they are heavily used in almost every API.

I will not bore you anymore with "_Node.js is cool because it does weird async stuff_" anymore, just keep in mind that studying is important, but callbacks are _importanter_.

To understand callbacks a bit better, lets write an example with the plain old javascript, without Node.js API. In the following example we can see a real use of callbacks:

```js
function onFinish(){
    console.log("So Long, and Thanks for All the Fish");
}

setTimeout(onFinish,1000);
console.log("The dolphin said");
```

`setTimeout` is a js built-in function that executes the callback after the given time \(in ms\) pass. In this case, it will execute onFinish after one second.

Intuitively, you may think that setTimeout will wait 1 second,  _"So Long, and Thanks for All the Fish"_ will be logged, and afterwards, _"The dolphin said"_. However, if you execute the example you'll see that _"The dolphin said"_ is logged right away, and after 1 second, the other message is shown.

This is due to the async nature of JavaScript \(Now your mouth should be open as you find yourself in a new state of consciousness above the rest of the mortals\). Well, maybe it is not such a surprise, but is a cool thing, as you can keep doing other stuff while we wait for the message.

Now, maybe, you could imagine setTimeout not only as a "Wait" function, but as an actual I/O function that doesn't depends on your code, something like _readFile\(\)_ or _download\(\)_.Being able to asynchronously perform tasks like those in the same fashion as setTimeout, allows you to avoid working with nasty threads and optimize resources when you want to perform several I/O operations at the same time \(which, surprise!, is the usual case for a webserver\).

So, using a pseudocode with an invented library, we could write something like this:

```js
onFinish(){
    console.log("File loaded");
}

readFile("File1",onFinish);
readFile("File2",onFinish);
```

In that example, we will start reading both files roughly at the same time, and when any of those is finished, _onFinish_ will be called. This means that _onFinish_ will be called twice.

In a classic, sequential fashion, first, File1 will be loaded, and after, File2 will start loading. With the asynchronous approach, if File1 is extremely large, while File2 is small, File2 will finish before and we will be able to start processing it _asap_. This is particularly convenient, not only for reading files, but for example, handling users requests. We don't want a simple request to be blocked until another, potentially larger and slower, request is finished.

To solve this problem, in most other languages, multithreading is used. With a different thread per request. This not only causes overhead, but it also over-complicates the code in some cases. With js by using a few callbacks, I/O can be handled efficiently in a single thread.

So, in a nutshell: "_Node.js is cool because it does weird async stuff"._

### Scopes

Scopes is one of the main "_gotcha_" of JavaScript. While they may posses strange and mystical behaviors, usually are part of the things that make js so dynamic and fast to write. It doesn't seem useful to dive in how scopes work in this quick guide, but it is important to look to a few examples on how scopes work while using callbacks.

Lets take the following example:

```js
function awesomeTask(){
    let greetings="Hello World";
    setTimeout(function(){
        console.log(greetings); // Hello World
    },1000);
}
```

In this snippet we are using `setTimeout` as in the examples before. You can see that instead of declaring a function, and passing it as a callback, we are declaring an _anonymous_ function directly in the parameters. This callback will be executed after a second due to setTimeout. But it's doing a weird thing, it is trying to access a variable `greetings` that is outside the function. This is possible due to js scopes. A function can access any variable of its scope, in this case, the function is created as part of the _awesomeTask_ scope.

If we try to extract that function, and declare it out of _awesomeTask_:

```js
function myCallback(){
    console.log(greetings);
}

function awesomeTask(){
    let greetings="Hello World";
    setTimeout(myCallback,1000); // ReferenceError
}
```

In this case, greetings is not defined. As greetings is not in the scope of _myCallback_. As you can see, scopes depends on where the variables and code blocks are defined. Scopes are important when it comes to working with callbacks. This is not everything when it comes to scopes, and we will see more of them in the future.

> Remember the difference between **var** and **let**? It basically comes down to scopes.

> **Pro Tip:** To avoid the so called _callback hell_, you must structure the nested callbacks in separate functions and modules.

### Arrow functions

As we saw, we can declare functions in different ways. In ES6 exists a new way to declare _anonymous_ functions: The _arrow functions_.

```js
setTimeout(()=>{
    console.log("Timeout");
    },1000);
```

Arrow functions where added to provide two small, but useful, features against traditional anonymous functions:

* More compact syntax: While it may seem of little importance, when it comes to declare callbacks (and callbacks in callbacks)  compact syntax greatly improves readability.
* Binding the `this`scope to the callback: This is important when working with classes, as we will see in the following section.

Arrow functions also provide an alternative syntax for only returning variables:

```js
()=> "Hello"; //Equivalent to ()=>{return "hello"}
//With one parameter the following is also possible:
name=>"Hello "+name;
```

These, again, are _"sugar"_ syntax to reduce verbosity and make callbacks more compact. Arrow functions are not required, and are only compatible with ES6, but for this guide we will stick to them, as it results in a more readable code.

## The Treachery of Classes
> Ceci n'est pas une classe

Let's start this section by looking to a simple class in JavaScript:

```js
class Orc{
    constructor(name){
        this.name=name;
    }

    greet(){
        return "Urhgz";
    }

    getName(){
        return this.name;
    }   
}


let azog=new Orc("Azog");
azog.greet(); // "Urhgz"
azog.getName(); // "Arzog"
azog.name; // "Arzog"
```
_Orc class_

As you can see, classes are pretty straightforward... Except they aren't classes at all.

JavaScript is, in fact, an Object-Oriented language without classes: A prototype-based language. If you come from an older version of JavaScript you may know a different syntax that looks something like this:

```js
function Orc(name){
    this.name=name;
}

Orc.prototype.greet=function(){
    return "Urhgz";
}

Orc.prototype.getName=function(){
    return this.name;
}
```
_Orc prototype_

As you can see, this is a more verbose and complex syntax, and it gets worse with inheritance. Again, ES6 implemented a sugar-syntax (`class` keyword) which increases readability, but is still good to know that classes are, in fact, `functions` and that the `new` keyword creates an object using the function as some kind of constructor which defines the prototype methods and attributes which the instantiated object inherits. For this guide we will, again, use the modern ES6 syntax.

Note how the instance of a class is a simple js object with the attributes and methods defined in the class. This means that you may redefined any attribute and method afterwards, like in any other object. You may think of classes as "object generators" and objects as loose instances of a class. This allows for a much more dynamic programming, but at the cost of worse class encapsulation.

In the first example, you will notice that we define the attributes directly by accessing `this` in the constructor. As the class is so permissive, you can defined attributes anywhere, anytime, and is not required nor possible to strictly define the class attributes. Is not possible to create _private_ attributes either.

Due to the permissive nature of js classes, is better to avoid "hacks" or weird implementations to avoid confusion, and stick, when possible, to clear and well-defined implementations.

> **Pro Tip:** While private members and other features are not part of js, playing around with scopes and Node.js _import_ system makes possible to emulate private variables in some cases (We will comment this in the following chapter)

### Classes Inheritance

OOP is not OOP without some inheritance. Js classes (and prototypes) allow inheritance, for which, again, we have a pretty straightforward syntax:

```js
class UrukHai extends Orc{
    constructor(name){
        super("Uruk-"+name);
    }

    greet(){
        return "We are taking the hobbits to Isengard";
    }
}

let lurz=new UrukHai("Lurz");
lurt.getName(); // Uruk-Lurz
lurz.greet(); // We are taking the hobbits to Isengard
```

The `super` keyword allows you to access the parent methods, to override a method redeclare it in the child class.

Js doesn't implement `interfaces`, it doesn't make sense in a language as dynamic as js. Multiple inheritance is not allowed, so a class can only inherit from one single parent, though the parent may inherit from a third class.

There aren't abstract classes either. You can emulate them by throwing errors in the constructor, but is usually better to simply use normal classes instead:

```js
class BigMonster{
    constructor(){
        if (new.target === BigMonster) { 
            // true if "new" calls BigMonster constructor
            // throw error here
        }
    }
}

class Troll extends BigMonster{
    constructor(){
        super();
    }
}
```
_Example of and enforced abstract class_

These limitations, again, enforces a more dynamic and loose implementation of OOP instead of the rigid structure you'll find in languages such as Java.

Using prototypes, to _extend_ another class/prototype you would use:

```js
UrukHai.prototype = Object.create( Orc.prototype );
```

Which is as intuitive as writing assembly with unicode characters, including emoji.

> **Pro Tip 1:** Unlike other languages such as Java, in js you **always** need to use `this` when referring to the class methods or attributes.

> **Pro Tip 2:** JavaScript doesn't support multiple constructors or method overloading, it follows the same rules as normal functions.

### instanceof

Even if being instances of a class won't ensure the object structure to be similar, all objects created from a class will return `true` when applying the operator `instanceof` over the object class or a parent of that class:

```js
const orc=new Orc();
const uruk=new UrukHai();

orc instanceof Orc; // true
orc instanceof UrukHai; // false

uruk instanceof Orc; // true
uruk instanceof UrukHai; // true
```

Don't confuse with `typeof` operator, the latests will return `Object` in all the previous examples, as, any instance is, in fact, an object.

### Classes and Scopes

Classes introduced a whole new level of scoping problems. In a class you would use `this` to access other members, but `this` is not part of the scope inside a callback:

```js
class Hobbit{
    //....
    takeBreakfast(){
        this.eat();
        setTimeout(function(){
            this.takeSecondBreakfast(); // this is undefined
        },1000);
    }

    takeSecondBreakfast(){
        this.eat();
    }
}
```

Note that for this example we didn't use the _arrow function_ `=>`.

To solve this problem, there are 3 approaches:

We can save the function in a variable, before the callback, making it part of the scope:

```js
takeBreakfast(){
    this.eat();
    let secondBreakfast=this.takeSecondBreakfast;
    setTimeout(function(){
        secondBreakfast();
    },1000);
}
```

We can also use `.bind`, which allows you to bind variables to the scope of a function:

```js
takeBreakfast(){
    this.eat();
    setTimeout(function(){
        this.takeSecondBreakfast(); // this exists because of .bind(this)
    }.bind(this),1000);
}
```

These two options work fine, but both are a bit _"hacky"_, and while they are still used (mainly due to compatibility), the third option, the _arrow function_, solves the problem, as an arrow function automatically binds _this_:

```js
takeBreakfast(){
    this.eat();
    setTimeout(()=>{
        this.takeSecondBreakfast(); // "this" is defined as part of the arrow-function callback
    },1000);
}
```

As you can see, arrow functions are not only as a visual improvements for anonymous syntax, they slightly simplify scoping rules in the same way `let` improves over `var`.

### Static Methods
ES6 classes implements _static methods_, which you may call without creating an instance of the class:

```js
class Dragonborn{
    //...
    static shout(){
        return "Fus Ro Dah";
    }    
}

let nord=new Dragonborn();

nord.shout(); // Error: undefined
Dragonborn.shout(); // "Fus Ro Dah"
```

Remember that within a _static_ method you cannot access _this_. 

> You cannot create static variables.

### Setters and Getters
ES6 implements setters and getters functions for classes and objects, these allows to use functions as variables, acting as something similar as a _proxy_:

```js
class Wizard{
    constructor(name){
        this.firstName=name;
        this.type="grey";
    }
    set level(level){
        if(level>10){
            this.type="white";
        } else this.type="grey";
    }
    
    get name(){
        return this.firstName+" the "+this.type;
    }
    //...
}
 
const gandalf=new Wizard("Gandalf");
gandalf.name; // "Gandalf the grey"
gandalf.level=11;
gandalf.name; // "Gandalf the white"
```

In this case, we use them to achieve a more readable syntax compared to classic setters and getters (`setLevel`, `getName`). Keep in mind that overusing _setters_ and _getters_ may lead to confusion and performance issues, as there is no clear hints on what is a function and what a variable. It's better to use them in specific cases where we want to specifically hide the internal representation of a variable.

> **Pro Tip:** Setters and Getters are also useful to log changes to a variable for debugging purposes. To do it,, change the internal variable name, and create setters and getters with the original name.

## Error Handling

JavaScript errors sometimes are not easy to manage, being a dynamically typed language, and having objects with arbitrary content usually leads to a lot of code just for handling edge cases.

While sometimes we need to rely on classic js _"tricks"_ to handle errors such as comparing with `undefined` or manually checking and asserting on classes, in most cases we may rely on the js built-in error handler.

The js error handler works in a similar way as in _Java_ using `try...catch` blocks:

```js
try{
    // Operation that may throw an error
} catch (e) {
    // If the operation fails
    console.error(e.message); // Logs the error message
}
```
_try...catch example_

Common operations that may fail are file handling, type errors and connections. You can also throw errors yourself. The `catch` block returns the thrown variable, while you can throw anything, you will usually get an `Error` object. You can access the message of the error with `e.message`.

You can also use `finally` to execute code **after** the `try...catch`, regardless of the result.

### Throwing errors
You may want to throw your own errors when something goes wrong, so you can properly handle it with `try...catch` to avoid using conditionals or error codes to handle them:

```js
function setAge(age){
    if(age<0) throw new Error("Invalid Age");
    // ...
}

try{
    setAge(-1);
} catch (e){
    console.error(e.message); // "Invalid Age"
}
```

### Callback Error Handling
Callbacks are a problem when it comes to error handling because you cannot ensure a thrown error to be caught if the callback is called asynchronously after the `try...catch` block is over.

The first approach to solve this problem, used by most APIs and libraries, is to send the error as the first parameter of all callbacks:

```js
fs.readFile('secret_codes.txt', (err, data) => {
    if(err){
        // Handle error
    } else {
        // Everything correct
    }
});
```

Most libraries will send a `null` as first parameter if everything is correct. The error field is always the first parameter, as callbacks may use a different number of parameters, and is useful to alway handle the errors the same way.

When implementing a library or code using callbacks, it's better to keep this style to match the rest of the libraries.

> Promises are another style of handling asynchronous code. One of the main improvements is that you can catch Promises and handle errors with try...catch blocks, we will see more about promises in the chapter [Promises](advanced-topics/promises)

## ES6 fuctional-style methods
ES6 introduced several methods and utilities in standalone JavaScript. Most are quite straightforward and simple to use, however, the following array methods where added to provide a more functional programming style, and generally produces a cleaner, more encapsulated code avoiding obscure loops, but using callbacks:

**map**
Returns a new array with the same size as the original arra. It is useful to modify all the content of an array:
```js
const ages=[10,12,5];

const mySecondArr=myArr.map((element)=>{
    element+1;
});

// mySecondArr = [11,13,6];
```

The callback has one parameter, the array element, and the returned element will be the element in new array in the same position. In this example we are adding one to all the ages of the original array.

**filter**
It returns an array with **only** the elements that are accepted by the callback. This function is particularly useful to modify the array content without having to handle pointers or counters manually:

```js
const ages=[4,16,20,8,19];

const allowedAges=ages.filter((age)=>{
    return age>=18;
});

// allowedAges = [20,19]
```

**reduce**
Works in the same way as map, but in this case it returns a single variable:

```js
const ages=[6,12,10];

const totalAge=ages.reduce((total,current)=>{
    return total+current;
},0);

``` 
The function accepts two parameters, first the callback to be executed for each element and second the initial value of the returned variable.
With each execution of the callback, two parameters will be passed to it, the accumulated value of the previous executions (beginning with the initial value) and the value of the current element. The returned variable of the function will be sent to the next function.

In the previous example, all the ages of the array are added into a single number, the total age, which is then returned. As you can see, the initial value is 0.

_Reduce_ is useful to generate objects from arrays, as you can accumulate all the elements into the same object:

```js
const peopleArray=[["Bilbo",90],["Gandalf",560],["Frodo",30]];

const peopleObject=peopleArray.reduce((total,current)=>{
    total[current[0]]={
        age: current[1]
    }
},{});

/* peopleObject = {
    Bilbo: {
        age: 90
    },
    Gandalf: {
        age: 560
    },
    Frodo: {
        age: 30
    },  
}*/
```

**Concatenating array methods**
All these methods are useful to perform operations such as parsing or data manipulation avoiding loops, but the main advantage over simple loops is that the returned array can be used to perform another method, leaving patters such as _"map-reduce"_ to perform operations.

For example, we can easily parse, filter and format data in one go:

```js
const moneyInAccounts=[100,300,1600];

function payMonth(money){
    return money-400;
}

function isNegative(number){
    return number<0;
}

function accumulateDebt(debt1,debt2){
    return debt1-debt2;
}

const totalDebt=moneyInAccounts.map(payMonth).filter(isNegative).reduce(accumulateDebt,0);

// totalDebt=400
```

Here, to calculate how much money we owe the bank after reducing our expenses from all the acocunts, we perform 3 operations:
1. We reduce our expenses (400) per account, this results in `[-300,-100,1200]`
2. We only need the accounts with negative balance, so we filter, resulting in `[-300,-100]`
3. Finally, we accumulate our debt of all the accounts, 300 and 100 gets us a total debt of 400

Compare, the same logic, using a loop:
```js
const moneyInAccounts=[100,300,1600];

function payMonth(money){
    return money-400;
}

function isNegative(number){
    return number<0;
}

function accumulateDebt(debt1,debt2){
    return debt1-debt2;
}

let totalDebt=0;

for(let m in moneyInAccounts){
    let money=moneyInAccounts[m];
    money=payMonth(money);
    if(isNegative(money)){
        accumulateDebt(totalDebt,money);
    }    
}
```

In this case, instead of performing three encapsulated operations, we do all the calculations in one go, so we need a `loop` block and an `if` nested block, with an external variable that we are going to modify in each iteration, making all the logic more obscure and easy to produce hidden changes in our code. 
In the functional approach, however, each operation is completely independent of the others, without shared variables, you can note how we are only using one variable (`totalDebt`) and is a `const` variable, so we are not modifying it at any point. While in the second example we are using 2 temporal variables in the loop and the resulted variable must be a `let` variable.

Of course, not all loops and conditionals can be turned into functional-style with JavaScript


> **Pro Tip 1:** The original arrays are not modified when using map, reduce or filter

> **Pro Tip 2:** The callbacks used can be, like any other callback, separate functions, resulting in a cleaner, more understandable code

## Common Pitfalls
JavaScript **is** an ugly programming language, making it asynchronous doesn't improve its cleanliness. However, with little practice it is possible to craft clean code with js. To partially avoid falling into the spiral of madness of desperation which is ugly JavaScript _hacky_ code here are some common mistakes that should be avoided when writing in Node.js

### Callback Hell
By far, the most well-known anti-pattern with node, is the _callback hell_, this happens when nested callbacks start generating a pyramid-code, which, by the way, you could compare to the 9 levels of Dante's Inferno:

```js
Purgatory(()=>{
    FirstLevel(()=>{
        SecondLevel(()=>{
            ThirdLevel(()=>{
                FourthLevel(()=>{
                    FiftLevel(()=>{
                        
                    });
                });
            });
        });
    });
});
```
There are several solutions to this, such as _Promises_, but avoiding a `callback hell` is surprisingly easy, this problem is, in fact, the same as nested loops, which you can find in almost any other language:
```js
for(...){
    for(...){
        if(...){
            for(...){
                ...
            }
        }
    }
}
```
And how would you solve that? Easy, use a bit of functions and OOP. The arrow functions help to bring OOP to callbacks.

> **Pro Tip:** As we will see, most Callback-based APIs return a first parameter `err` followed by all the other parameters. This parameter is usually `null` or `undefined` unless there was a problem. This is needed because `try...catch` patterns doesn't work well with callbacks. Promises solve that problem


### Variable comparisons
JavaScript variables comparisons are weird, and node is no exception to it. The best way to avoid (some) pitfalls here is to follow a few simple rules and patterns:

* Use triple equal `===` instead of simple equal `==`. The first compares type as well (so 5 is not `===` to "5")
    * It may be useful, however, to use simple compare to compare with `null`, as it will return true for `undefined` and `null`
* You can compare existence of objects (`if(!myVar) console.error(...)`), but beware of `0` `false` and empty strings, as those return `false` even if exist
* Using `||` to provide default values is useful (`const myVar=otherVar || {}`) but you must be careful with `0` `false` and empty strings. For those cases you can simply use `equal` operators
* `typeof` return object for `arrays` and all objects
