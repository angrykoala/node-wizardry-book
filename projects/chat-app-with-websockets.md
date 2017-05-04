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

## HTTP Server

```js
const express = require("express");
const app = express();
const http = require('http').Server(app);

app.use(express.static('public'));

//server starts listening to port 9090
http.listen(9090, () => {
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

## Client Webpage
To create the _"client"_, we need to implement the webpage code with plain Html and JavaScript. This code will be served by our server and will be executed by the browser, not by node.js.

To do this, we are going to put our webpage in a a new folder `public/`. In that folder we will create the file `index.html`, which is, by default, the first file a browser will request when accessing a webpage:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <title>My Chat</title>
    </head>
    <body>
        <h1>Don't Panic!</h1>
    </body>
</html>
```
_index.html_

This is a simple example of an html webpage. If we start our server now and go to `localhost:9090` we should see _"Don't Panic!"_ in big letters.

> We also can access the same page by going to `localhost:9090/index.html`.

## Socket.io
The Socket.io library implements a server-side, which is going to be executed by our node.js back-end, and a client, which can be executed in our browser.

Socket.io is based on _events_ to manage our messages. There are two important methods:
* `on`: Will listen to an event, and execute a callback when that event is received.
    * `socket.on('my_message',callback)`
* `emit`: Will send a message (event), and optionally some content as text.
    * `socket.emit('my_message','content')`
    * With `socket.send('content')` we can send a message with a default event `message`
    
These two methods can be implemented in the back-end or front-end, when an `emit` is fired in one side, it will execute the `on` in the other side. If there is no listener the event will be ignored.

> Socket.io is a complex library that allows peer-to-peer communication, broadcasting and channels, the full documentation can be found at <https://socket.io/docs>

With Socket.io we can send any event we want, but there are a few events sent by default, the most important are:   
* **message**: Default event for our messages using `socket.send`
* **connection/connect**: Automatically fired when a socket connects
    * In the client the event is always `connect`
* **disconnect**: Fired when a socket disconnects

> The events connect and disconnect allows us to know when a client or server disconnected or connected. There are other events such as `reconnect` or `error`.

### Socket.io - Server
We already installed socket.io in the _setup_ section, we need to import it into our _server.js_, we can do it under the previous `require` we did for express and http:

```js
// requires
const io = require('socket.io')(http);
// ...
```
_server.js_

As you can see, we are binding our http server to the socket.io library the same way we did with `express`. In this case we execute the socket.io method directly without storing it in a separate variable.

Our server must listen to any message, and the broadcast it to all the users:
```js
io.on('connection', (socket) => {
     console.log("User connected");

    socket.on('msg', (content) => {
        console.log("Received:"+content);
      });

    socket.on('disconnect', () => {
        console.log('User disconnected');
    });
});

// http.listen...
```

The first event `io.on` will fire for every websocket that connect, you may think of an user _"login"_. The callback passes an argument which is the actual socket.

The other 2 events are attached to that given socket, the first one will fire for every `msg` event received, we will use that event to send the message. For now we will only log the content received.

Finally, a `disconnect` event that will be fired when the socket is disconnected.

> In this case, we don't need to perform any actions in connect/disconnect, but usually you'll store some users data while they are connected.


### Socket.io - Client
We have a simple http server with websocket support, now we need to implement our client. The first step is to get the socket.io library, usually we will want to download it as a resource or from a _CDN_. However, the server-side socket.io library automatically serves the client _js_ file, so we only need to add the following code to our `index.html` file:
```html
    <!-- Body Code -->
    <script src="/socket.io/socket.io.js"></script>
</body>
```

We also need to implement a bit of logic in our client, in order to keep everythin nice and tidy, we will create in our `public` folder a new folder `js`, inside the folder we create the file `chat.js` with our chat implementation:

```js
const socket = io.connect();

socket.on('connect', () => {
    alert("Connected");
});
```
_/public/js/chat.js_

The implementation here is much simpler, as we only need to handle one socket. The client-side library automatically exposes the `io` object, so to create our socket we only need to execute `io.connect()` which creates and connects the websocket, we can set any URL we want, but by default will connect to the same origin server.

Then, when the connection is successful, the callback will be executed. For now we will show and _alert_ notifying we are connected, remember that `alert` is a browser specific command.

Now we are ready to perform our first test if you fire the server and go to `localhost:9090` you should see the same page as before, but shortly after you should see an alert saying _"connect"_. If you go to your terminal, you should also see a _"User Connected"_ log in the server.

> You can now try some of the basics socket.io features commented before, if you close your browser you should see a "User disconnected" message in the server. You could also try opening several browsers and you should see how the server understands how multiple "users" (or different sockets) are connected. Not only that, but if you close the server with the page opened and start again the server, you will see the alert again. This is thanks to the automatic reconnection feature of Socket.io

## Let's spice it a bit
