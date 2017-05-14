# Creating Your First Project
_Remember: With Great Power Comes Great Responsibility_

The time has come, lets create something cool. For this first approach to a Node.js project, we will cover some basics of writing a _web server_ with node. As you may know, even if Node.js makes js as versatile as any other language, is commonly applied to web back-end development.

## Description
Node.js, as a web server (or _back-end_) programming language, can be used to start an http server and listen to request to that server. While it is recommended to use along with an standalone http server such as Apache or Nginx, Node.js can work by itself.

One of the reasons of using Node.js as a server language is the asynchronous I/O of Node, this allows to use the same thread for several concurrent requests, instead of spawning a new thread (and node runtime) per requests, like PHP or Java.

This behavior makes a more efficient use of computing resources, at the cost of having to manually spawn several instances to make use of multiple cores.

This first project will show how to work with a simple http server in Node.js, no setup is needed to start the server and no dependencies are required. However, this approach is not recommended for its use in production.

## Setup

The best and simplest way to start a project with Node.js is by opening a terminal, going to the folder where you want to put your code and write:

```bash
npm init
```

This command will fire an interactive interface to create the _package.json_ file. It will also try to fill some items with reasonable values (e.g. using the current folder as project name). All the values can be changes later.

After executing `npm init` , you'll see a _package.json_ file. As mentioned before, this file contains all the meta-data, dependencies, and entry point of your project. If you open it, you'll see something like this:

```json
{
  "name": "my-impressive-app",
  "version": "0.0.1",
  "description": "My awesome description",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "the_doctor",
  "license": "GPL-3.0"
}
```
_package.json_

This file, as you can see, is pretty readable, as most fields are self-descriptive, but some may need some explanation:

* **main**: Defines the entry point of your package. When it is imported using `require`, that file will be the one imported. Depending on what are you building it may not be relevant.
* **scripts**: Scripts define a set of commands that can be executed using `npm run <myScriptName>`. For example, `npm run test` will show the error. Scripts can have any name and command you want (beware, the command will be a bash/terminal command, and it may not work in different systems). Some 'scripts' are special:
    * **start**: If there is a script named like that, it will be automatically executed using `npm start`. It is a standard de-facto way of starting node.js applications (e.g. servers).
    * **test**: This command define the execution of tests (we will talk about testing in advanced topics), by default it throws an error, as tests are not defined. You can execute them with `npm test`.
    * Some scripts are automatically executed on some steps, for example `postinstall` or `prepublish` after executing `npm install` and before `npm publish` is executed. The full list of "_hooks_" can be found in the npm docs: <https://docs.npmjs.com/misc/scripts>

## Hello Server

We will start by creating a simple _http_ server, for that, we create the file `server.js`:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    console.log("Request received");
    res.end("Hello World");
});

server.listen(3000, (err) => {
    if (err) {
        return console.error('Error in server', err);
    }

    console.log("Server is listening on port " + port);
});
```
_server.js_

To execute this example, write in your terminal:
```bash
$ node server.js
```

If everything goes fine, you should see the following message:
```bash
Server is listening on port 3000
```

If you open a browser and go to the URL `http://localhost:3000` you should see `Hello World` in the browser. You should also see the log `Request received` in the terminal.
To stop the server you can either close the terminal or press `Ctrl+C`

> Optionally, you can add a script in your package.json: `"start": "node server.js"` to start your server using `npm start`

Lets break down this example a bit:

```js
const http = require('http');
```

First, we import the dependencies we are going to use. In this case we use the built-in library `http`, because is a node library we do not need to explicitly add it as a dependency or install it with _npm_.   

> You can check the full documentation of the http built-in package in the official node docs https://nodejs.org/api/http.html
    
```js
const server = http.createServer((req, res) => {
    console.log("Request received");
    res.end("Hello World");
});
```

Next, we create an http server with the method `createServer`. We pass a callback, which will be called for every request sent to the server. The parameters of the callback are _request_ and _response_ respectively.
* The Request contains all the request data (Url, method, ...). 
* The response object allows to manipulate and send the response (e.g. status code). 

For now, we will just log the request using `console.log` and send the classic Hello World message.

> _Fun tip_: If we add html tags to the response such as `<h1>Hello World</h1>`, we will see the page formatted in the browser (yay, our first 90s styled webpage).

Even if we have already configured the server, is still idle. We need to start listening to a port (in this case, port `3000`).

```js
server.listen(3000, (err) => {
    if (err) {
        return console.error('Error in server', err);
    }

    console.log("Server is listening on port " + port);
});
```

After executing `server.listen`, the application will stay active, even after reaching the end of the file, as the server is still running indefinitely. 

The optional callback passed to the method will execute _after_ the server is mounted. The parameter `err` will contain the error data if there was a problem setting up the server or `null` if everything was correct.

In another languages, such as python, setting up a server will either completely block the execution for anything else (acting like an infinite loop) or span a new _thread_. In JavaScript we can keep executing other commands without worrying for blocking them, as a server act as an I/O asynchronous process. Because of this, we could, for example, set up a second server right afterwards binding it to a separate port.
    
This is all you need to set up a simple server with Node.js, there are several built-in packages that can be used just as easily, all documented here: https://nodejs.org/api

While it is possible to build a full-featured server using only the built-in packages, most projects will use third-party packages such as [Express](http://expressjs.com) to speed up development. We will install and use some of those packages in future projects.
