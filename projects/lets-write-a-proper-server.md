# Let's Write a proper server
In the first project we wrote a simple server. As you know, server-side code is the main use of Node.js, now we are going to write a full featured server.

## Description
Writing a web application is usually done in 3 parts:
* Server-side or _back-end_: This is the code in the server, it handles stores, provides and compute the required data. Its logic can be written in almost any language, but scripting languages such as Python, Php or in this case, JavaScript (Node) are commonly used.
    * Server-side code will usually be running along with an standalone server such as Apache or Nginx
* Client-side of _front-end_: This is the code executed in the client machine, if we are writing a web we will use JavaScript, Css and Html, as those are the languages accepted by most browsers, however, we may want to write a different client, like a mobile or desktop application.
* Database: The database is actually part of the server, but is usually treated as a separate part. Usually you will use a relational (SQL) or non-relational (like Mongo) database.

For this server, we will focus in the server-side (Node.js) but we will also use a common stack of Node.js, Mongo, and web technologies.

> The **MEAN** Stack (Mongo, Express, Angular, Node) is one of the possible stacks to use with Node, for now we will not use Angular, a front-end framework.



## Possible improvements
* Implement an Nginx server to handle the requests
