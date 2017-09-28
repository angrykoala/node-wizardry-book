# Promises in JavaScript

> I promise you, this is not that hard

Promises are a way of handling callbacks without falling into the dreaded "_callback hell_" introduced in ES6. Before trying to learn promises I recommend having a deep understanding on _callbacks_, as promises make use of them.



### The Problem

Callbacks are a neat way of handling asynchronous workflow, just by adding a anonymous function. However, in a complex environment, with complex workflows, this can easily turn into a mess

```js
myfunction1((err,cb)=>{
    if(err) #handle err
    myfunction2((err,cb)=>{
        if(err) #handle another err
        myfunction3(cb);
    });
});
```

_Callback Hell_

As you can see, each function we call represents a new nesting level, and with each level we need to send the `err` parameter and check is _undefined_. While we can reduce nesting by using named functions and a clean organisation, errors must be checked on each level. As an error thrown in a callback **won't** be caught by a `try...catch` on top level, so a variable must be carried over every callback.



### The solution

> Or at least **one** solution

Promises were created to improve legibility on complex asynchronous workflows, properly handle errors and avoid overly-nested callback.

A **promise** is a data structure that represents an asynchronous process that may or may not have finished yet. A promise may be returned  from an asynchronous process, the same way a synchronous function would return a variable:

```js
const myPromise=asyncFunction(); 
//myPromise contains the state of the process and the resulting value
```

To access a promise result, we use `then`, along with a callback:

```js
const myPromise=asyncFunction();
myPromise.then((result)=>{
    //Do stuff with the result
});
```

Using  `then` is asynchronous as well.

You may now think that we haven't actually improved anything, we need a callback in then anyway. However, the nice thing about this particular callback is that a `then` also returns a promise, allowing you to easily concatenate and "untangle" nested calls as we will see in a moment.

### Creating Promises



