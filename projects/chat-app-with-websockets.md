# Chat App

## Description
For this project we will be building one of the classics of Node.js, a IRC-style chat application. We will rely on [Socket.io](https://socket.io) library, which allows us to easily use _websockets_. Thanks to this, out chat will be up and running in no time.

### About websockets
Websockets is a relatively new technology standard in most moder browsers, and with implementation in most languages and platforms (e.g. Android). When creating a websocket we will have a permanent bi-directional connection between a client and our server, this way, with very little overhead, we can send data both ways without creating and destroying connections with each message.

This provides, not only a simpler implementation for some cases, but several performance improvements:
* No need of polling, because the server can notify the client directly.
* Very little message size. Each message is only a few bytes, as no handshake or connection data is required.
* Large number of concurrent connections. In most cases, a server can handle more concurrent active connections with websockets than the same number of plain HTTP request.

# ![](/assets/websocket.png)
_WebSocket diagram (www.pubnub.com)_

> Even if websockets are so great, they are not suitable for everything. Because of the overhead of having an active connection, websockets will provide an improvement over plain HTTP request when there are a lot of small messages or you actually need bi-directional messages. It may not behave prorperly with big messages like sending big JSONs or files.

For this problem, websockets provides an ideal solution, as we can send messages to the server, and the server can notify all the other clients in real-time.

## Setup
To begin our project:
1. `npm init`
2. `npm install --save socket.io express` to install the express and socket.io libraries
    * **socket.io@1.7.3** is the websockets library we will use.
    * **express@4.15.2** is a lightweight http framework for node, which will simplify the process of creating a webserver.

This project, as most web-based projects, require two separate _"programs"_, the _back-end_, which will be our Node.js server, and the _front-end_, which will be a webpage written with Html and JavaScript.

We will begin with a simple http server to provide our webpage.

### HTTP Server

```js
const express = require("express");
const app = express();
const http = require('http').Server(app);

app.use(express.static('public'));

//server starts listening to port 9090
http.listen(9090, function() {
    console.log("Magic happens in port 9090");
});
```
_server.js_


In the first block, as usual, you'll see the libraries we are importing. We are also creating and setting up our express server:
```js
const app=express();
```

This is one way to create a new express app. We can create other express instances the same way. While it is not needed in some cases, here we are going to explicitly create a native `http` server and bind our express app to it.

```js
const http = require('http').Server(app);
```

Express provide a simplified syntax to configure our server and create our APIs, like the plain http server discussed before, we are going to configure it before starting it.

```js
app.use(express.static('public'));
```

The `use` command allows us to set a `middleware` to our express server, several libraries work as middlewares that are executed with each request. In this case we create a built-in `static` middleware, which automatically serves a folder as static resources.

> While express.static provides a similar behavior as more heavy servers as `nginx` and `apache`, it is not as fast or reliable for production environments for serving static files.

Serving that folder means that writing in our browser `localhost:9090/my_file` when the server is running will retrieve the file `/public/my_file`.

Finally, we start our http server as seen before, in the port `9090`.

If we execute `node server.js` we will see the text:
```
Magic happens in port 9090
```

If we try to access with our browser to `localhost:9090` we will see a message `Cannot GET /`. This happens because there is no route or file pointing there (we are trying to serve a `public` folder that doesn't exists).

For this to work, we need to create our webpage

### Client Webpage
We begin by creating the folder `public/`
