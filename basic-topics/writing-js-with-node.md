# Writing with Node.js

In the previous chapter we were introducing the basic features of JavaScript. These should work for any JS modern environment, including most browsers. However, Node also implements some extra features, in a similar way as browsers implements others \(like `alert`\). In this Chapter, we will discuss the specifics of writing with Node.js.

## Modules
When writing JavScript in a browser you usually need to import each script you want to use, resulting in a poor encapsulation of code. Node.js, however provides a simple way to structure code: _modules_.

Modules works in the same fashion as _imports_ or _includes_ in other languages. You can import modules into your script (and each module imports other modules as well).

### Require
The usual way to import a module is by using `require`, this is, for example, the way to import dependencies:
```js
const fs=require('fs');
```
In this example, we are importing the built-in `fs` (_FileSystem_) module, which is available in Node.js by default, and we assign its content to a variable with the same name. Note that we use `const` as it is not recommended to reassign a variable of an imported module.

When we use require 2 things happen:
1. The script is loaded and executed.
2. The module _"exports"_ and object and is returned.
    * As described below, a module can export an object, usually it will be a plain object, a function or a class.

Apart from built-in modules or dependencies, you can require any js file in your project, for this, you need to set the path, starting with `.`.

```js
const mySecondFile=require('./app/my_second_file');
```
This way, you can split your code in several files. Note that we haven't added the extendion (`.js`). Extension must be added only if the imported file is not `.js`.

While `require` can be used at any moment, it is important to note that it will trigger a reading, parsing and execution of a js script (which, may have other imports). All of this is done synchronously, so the execution will be blocked until all the dependencies are resolved. Because of this, it is heavily recommended to have **all** the `require` statements at the beginning of each file, so everything is loaded before starting the actual execution of the code and avoid blocking the execution.

When the same module is required in different files, the code will only be executed **once** and references to the same object will be returned. This mean that any change to the object will affect the rest of the dependents files.


> **Pro tip:** Using require with `.json` files will automatically parse the json and store in an object. While it is extremely handy, the load is done synchronously and it is only recommended for static files that won't be changed.

### Export
In order to return an object when using `require` you must `export` it:

```js
module.exports={
    my_awesome_name: "Marvin"
}
```
_a.js_

```js
const a=require('./a');

console.log(a.my_awesome_name); // "Marvin"
```
_b.js_

Only the exported object can be accessed from other modules, this greatly improves encapsulation comparing to classic JavaScript in browsers:

```js
let age=18;

module.exports={
    my_awesome_name: "Marvin"
}
```
_a.js_


```js
const a=require('./a');

console.log(a.my_awesome_name); // "Marvin"
console.log(a.age); // undefined
```
_b.js_

> **Pro Tip:** As mentioned in the previous chapter, js doesn't provide _private_ variables, however, using module encapsulation is it possible to emulate _private_ variables and methods (with some limitations)


## Dependencies

Node.js have a lot of built-in modules that you can import in the same way as `fs`, these modules are listed and documented in https://nodejs.org/api. 

However, you may want to use third-party modules. These modules are, in general, published in https://www.npmjs.com and are called _packages_, because instead of simple files, they are full projects.

You can import these packages the same way, but you must install them before with `npm`:

1. `npm install express --save` will install the package `express` from npm in the folder `node_modules`. The `--save` option will store that module as a dependency in your `package.json`.
    * `npm install -g express` will install the package _globally_ in your system
    * `npm install express --save-dev` will add the package as a _development dependency_
    * You don't need to save the package as a dependency, but doing it allows you to install all the dependencies by writing just `npm install`.

2. After being installed, you can import it just using the name `const express=require('express')`.
    * While you could also import it accessing directly to the file in `node_modules` it is **heavily** not recommended, as it break _packages_ encapsulation and you cannot guarantee the package will be installed there.

> **Pro Tip:** The folder `node_modules` must be used only for packages installed with npm, never for your code or manually downloaded packages

### Packages vs. Modules
You may sometimes see that the words _"module"_ and _"package"_ are interchangeable. However, there are some small differences:
* A module is anything that can be required, like js files.
* A package is a directory described by a _package.json_. In general, every node application is a package, and a package can be a module (e.g. the dependencies you may install).

So, in a proper Node.js environment, you are creating a _package_, the package is composed of several _modules_ (files) and uses other _packages_ (that are also _modules_, as you can import them).
