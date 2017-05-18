# Introduction to Node API

Node.js provides a set of modules that can be used at any moment by importing them just like any module:
```js
const http=require('http'); // Imports http module
```

These modules don't have to be imported, as are by default in Node, however, the API may be different depending on the version of node you are using, remember to check (TODO: insert web here) to see the current specification.

These modules are usually bindings to the OS, which provide a fast implementation of most needed features of Node.js such as file I/O or Networking among others. 

## modules
In this chapter we will discuss some of these modules.

### fs
The `filesystem` (fs) module handles all the interaction with the OS file system, such as reading and writing files, folder creation and navigation.


### http

### path and url
The `path` module provides a simple interface to manipulate OS paths (e.g `/home` or `C:/`) so you don't need to directly manipulate strings for `paths`. The interface to generate paths is the same regardless of the underlying operating system, so by using this module instead of strings your application will work almost the same way in Windows, Linux and OSX without making any modifications.


>TODO: list methods and examples here

The `url` module provides a similar interface, this time to handle url directions such as `192.1.1.0` or `localhost:3131`. It is particularly useful for server applications. 

>TODO: list methods and examples here

### utils

## process variable
