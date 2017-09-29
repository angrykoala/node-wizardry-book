# Promises in JavaScript

> I promise you, this is not that hard

Promises are a way of handling asynchronous code without falling into the dreaded "_callback hell_", they were introduced natively in ES6. Before trying to learn promises I recommend having a deep understanding on _callbacks_, as promises make use of them.

### The Problem

Callbacks are a neat way of handling asynchronous workflow, just by adding an anonymous function. However, in a complex environment, with complex workflows, this can easily turn into a mess:

```js
myfunction1((err,cb) => {
    if(err) // handle err
    myfunction2((err,cb) => {
        if(err) // handle another err
        myfunction3(cb);
    });
});
```

_Callback Hell_

As you can see, each function we call represents a new nesting level, and with each level we need to send the `err` parameter and check that is _undefined_. While we can reduce nesting by using named functions and a clean organisation, errors must be checked on each level. As an error thrown in a callback **won't** be caught by a `try...catch` on top level, so a variable must be carried over every callback.

### The solution

> Or at least **one** solution

Promises were created to improve legibility on complex asynchronous workflows, properly handling errors and avoid overly-nested callbacks.

A **promise** is a data structure that represents an asynchronous process that may or may not have finished yet. A promise may be returned from an asynchronous process, the same way a synchronous function would return a variable:

```js
const myPromise=asyncFunction(); 
// myPromise contains the state of the process and the resulting value
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

> **Pro tip: **promise.catch\(...\) can also be used standalone, but in this case it won't be executed if an error is thrown inside the _then_ block, to provide a consistent error handling,  I recommend using then...catch as described before.

### Advanced usage

While one of the most interesting features is the error handling, promises can also increase your code legibility, consider the following example, where we want to perform several asynchronous operations using promises:

```js
function readFileWithPromise(path){
    // Same as before
}

function processFileData(fileData){
    // Async process of data, returns a promise
}

function sendProcessedData(user, processedData){
    // sends data to given user, returns a promise
}

function readProcessAndSendData(user, path){
    return readFileWithPromise(path).then(processFileData).then((processedData)=>{
        return sendProcessedData(user,processedData);    
    });
}

readProcessAndSendData(myUser, myPath).then(()=>{
     console.log("Congrats");
 }).catch((err)=>{
     console.error("Error",err);
 });
```

As you can see, returning a Promise inside a Promise will automatically be handled, and is no need to use `then` for `sendProcessedData`, finally we don't have to care about errors, as all the thrown errors and rejected promises will be caught in the last catch block.

Compare the previous example with the same code using a callback-based interface:

```js
function readFileWithPromise(path, cb){
    // reads file with callback interface
}

function processFileData(fileData, cb){
    // Async process of data, calls cb at the end
}

function sendProcessedData(user, processedData, cb){
    // sends data to given user, calls cb at the end
}

function readProcessAndSendData(user, path, cb){
    readFileWithPromise(path,(err,fileData)=>{
        if(err) return cb(err);
        processFileData(fileData,(err, processedData)=>{
            if(err) return cb(err);
            sendProcessedData(user,processedData,(err)=>{
                return cb(err);
            });
        });
    });
}

readProcessAndSendData(myUser, myPath,(err)=>{
     if(err) console.error("Error",err);
     else console.log("Congrats");
 });
```

As you can see, not only you end up with a much more messy code, with nested callbacks, but you need to be extra-careful with the workflow, as you need to call `cb` several times to handle all errors, which must be handled mannually on each level

> **Pro Tip:** Inside a then block, you can either return a Promise or a variable, if the returning value is a Promise, it will automatically be resolved, and the result will be returned.
>
> **Pro Tip 2: **If a Promise is resolved before the `then` block is declared, don\`t worry, the "resolved" state is stored, and the then block will be executed immediately when is declared.
>
> **Pro Tip 3:** A Promise can have multiple `then` and `catch` blocks, and they could be executed multiple times, but it is not recommended, as doing so will contribute to confusion, anarchy, and kittens sacrifices. We don't want to sacrifice kittens, you monster.

**Promise.all**

Sometimes, we want to perform a arbitrary number of asynchronous operations at the same time, and execute a callback when all of them have finished. Using plain callbacks this could prove challenging, to the point that libraries such as async where used to solve this problem.

With Promises, however, this problem is trivial, as we can store promises in arrays and do whatever we want with them, and the Promises interface itself gives us the `Promise.all` method. The resulting code is usually quite readable and with a functional-programming style:

```js
// Sends an email to each user of given list, return promise
function sendEmailsTo(users){
    promises=users.map((user)=>{
        return sendEmail(user); //This function send an email asynchronously, returns a promise
    });
    return Promise.all(promises)
}

sendEmailsTo(["user1@mail.com","user2@mail.com"]).then(()=>{
    console.log("All emails were sent");
});
```

This examples uses `map` to generate an array of all the promises resulting after executing `sendEmail` with each user, `Promise.all` expects an array of promises, so this pattern is quite handy. It will return a promise that will be resolved when all the promises in the array are resolved.

As you can imagine, `Promise.all` will result in a rejected promise if _any_ of the promises fail. This can be changed if we add a catch block to each promise inside `sendEmail` \(or using then...catch instead of returning sendEmail directly\)

**Promise.resolve** and **Promise.reject**

There are some moments in life when you may want to immediately return a Promise, either resolved or rejected, instead of creating a new Promise with its callback.

`Promise.resolve()` and `Promise.reject()` do just that, if arguments are passed, those will be the result or error returned by the promise. This is useful to maintain a Promised-based interface, even if you don't need to perform an asynchronous task \(e.g. cached data, error handling...\)

### Final considerations about promises

Keep in mind that promises are intended to solve the problems of nesting callbacks and complex error handling, but for simple operations \(e.g. just one callback\) Promises are too verbose, as we saw in the first examples. Because of this, plain callbacks are still useful, as a more direct and simple way of handling asynchronous code. Don't  waste time trying to use promises everywhere, and instead use them where you can see an actual improvement.

Also remember that is easier \(and cleaner\) to wrap a Promise around a callback than the other way around. So usually external interfaces \(e.g. the API of a library\) are still callbacks-based instead of promises, even if promises are being used internally.

> **Pro Tip:** Some interfaces return a Promise if no callback is passed, allowing to use both patters seamlessly



