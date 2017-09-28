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

You may now think that we haven't actually improved anything, we need a callback in `then` anyway. However, the nice thing about this particular callback is that a `then` also returns a promise, allowing you to easily concatenate and "untangle" nested calls as we will see in a moment.

### Creating Promises

We already know the basics on how to handle the result of a promise, but how do we create one?

To create a new promise, we use the Promise built-in class:

```js
function readFileWithPromise(path){ // Interface to readFile using promises
    return new Promise((resolve,reject)=>{
        fs.readFile(path, (err, data) => {
          if (err) reject(err);
          else resolve(data);
        });     
    });
}
```

In this example, we want to read a file, but we want to use a Promises-based interface, so we "wrap" the built-in `readFile` method. As you can see, the Promise constructor takes a callback as an argument with 2 parameters:

* `resolve`: a callback to be executed in case the operation is successful, this callback takes the result, if any, as parameter.
* `reject`: a callback to execute in case the operation fails, the callback accepts an error as parameter.

When the callback returns an error, instead of sending it to the next callback, we simply "_reject_" the promise, we will see in a moment how to handle those rejections.

> It is heavily recommended to execute **only** one of those callbacks, and only once, to avoid ambiguous resolutions of a Promise

With our new interface, we can now read files like this:

```js
const myPromise=readFileWithPromise("my/path/my_file.txt");

myPromise.then((fileData)=>{
    // Work with the data
});
```

### Handling Errors

Following the previous example, we know what to do if a promise is resolved, but what happen if a promise is rejected?

To handle this, we simply need to concatenate a catch method:

```js
readFileWithPromise("my/path/my_file.txt").then((fileData)=>{
    //Work with data
}).catch((err)=>{
    console.error(err);
});
```

The `catch` block will be called if:

* The `reject` method is called
* An error is thrown in `readFileWithPromise`
* An error is thrown in the `then` block

Note how we are not storing the promise anymore, we can easily concatenate then and catch blocks, as those also return promises.

> **Pro-tip: **promise.catch\(...\) can also be used standalone, but in this case it won't be executed if an error is thrown inside the _then_ block, to provide a proper error handling, then...catch should be used as described before.

### Advanced usage

While one of the most interesting features is the error handling, promises can also increase your code legibility, consider the following example, where we want to perform several asynchronous operations using promises:

```js
readFileWithPromise(path){
    // Same as before
}

readAndProcessFileData(path){
    // Async process of data, returns a promise
}

sendProcessedData(user, processedData){
    // sends data to given user, returns a promise
}

readProcessAndSendData(user, path){
    readFileWithPromise(path).then((data)=>{
    
    
    });




}


```





**Promise.all**

