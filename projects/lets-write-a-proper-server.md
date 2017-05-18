# Let's Write a proper server
In the first project we wrote a simple server. As you know, server-side code is the main use of Node.js, now we are going to write a full featured server.

## Description
Writing a web application is usually done in 3 parts:
* Server-side or _back-end_: This is the code in the server, it handles stores, provides and compute the required data. Its logic can be written in almost any language, but scripting languages such as Python, Php or in this case, JavaScript (Node) are commonly used.
    * Server-side code will usually be running along with an standalone server such as Apache or Nginx
* Client-side of _front-end_: This is the code executed in the client machine, if we are writing a web we will use JavaScript, Css and Html, as those are the languages accepted by most browsers, however, we may want to write a different client, like a mobile or desktop application.
* Database: The database is actually part of the server, but is usually treated as a separate part. Usually you will use a relational (SQL) or non-relational (like Mongo) database.

For this server, we will focus in the server-side using Node.js, the Express framework and mongo. We are going to write a database and webpage of _tv shows_, for this we are going to build:
1. Simple webpage based on templates using EJS
2. Mongo database
3. RESTful API to request the data from the server
    * Writing a REST API is one of the ways of decoupling our webpage and our server, allowing the same _"service"_ to be used in any other application, like a mobile app, by implementing the API client.
    
    
TODO: explain API REST better

> The **MEAN** Stack (Mongo, Express, Angular, Node) is one of the possible stacks to use with Node, for now we will not use Angular, a front-end framework.

## Setup
To begin our project:
1. `npm init`
2. `npm install --save express mongodb` to install the express library and mongodb drivers
    * **express@4.15.2** is a lightweight http framework for node, which will simplify the process of creating a webserver.
    * **mongo**

This project, as most web-based projects, require two separate _"programs"_, the _back-end_, which will be our Node.js server, and the _front-end_, which will be a webpage written with Html and JavaScript.

We will begin with a simple http server to provide our webpage.


## Possible improvements
* Implement an Nginx server to handle the requests and the static resources
