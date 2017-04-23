# You first app

Finally, the time has come, lets create something. For this first approach to Node.js development, we will cover some of the basics of writing a _web server _with node. As you may know, even if Node.js is as versatile (or more) than any other language, it is usually applied to back-end web development.

## Setting up

The best (and simplest) way to start a project with node JS is opening a terminal, going to the folder where you are going to put your code and write:

```bash
npm init
```

This command will start an interactive interface to create the _package.json_ file. It will also try to fill some items with reasonable values (e.g. using the current folder as project name). All the values can be changes later.

After executing `npm init` , you'll see the _package.json_ file. As mentioned before, this file contains all the metadata, dependencies and entry point of your project. If you open it, you'll see something like this:

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

This file, as you can see, contains mainly metadata on the project. Most of the fields are self-descriptive, however, some may need a bit of explanation:

- **main**: Defines the entry point of your package. When it is imported using `require`, that file will be the one imported. Depending on what are you building it may not be relevant.
- **scripts**: Scripts define a set of commands that can be run using `npm run <myScriptName>`. For example, `npm run test` will show the error. Scripts can have any name you want, and any command you want (beware, the command will be a bash/terminal command, and it may not work in different systems), however, some 'scripts' are special:

  - **start**: If there is a script named like that, it will be executed using `npm start`. It is a standard de-facto way of starting node.js applications (e.g. servers).
  - **test**: This command define the execution of tests (we will talk about testing in advanced topics), by default it only throws an error, as tests are not defined. It can be executed with `npm test`.
  - Some scripts are automatically executed on some steps, for example `postinstall` or `prepublish` after executing `npm install` and before `npm publish` is executed. The full list of _hooks_ can be found in the npm docs: <https://docs.npmjs.com/misc/scripts>

## Hello Server

We will start by creating a simple _http_ server, for that, we create the file `server.js`:

```javascript
const http=require('http');

//TODO: Create example
```

As you can see, we are using the library `http`, it is a node default library. You can check the full documentation of the node native packages in the official docs: https://nodejs.org/dist/latest-v6.x/docs/api

> Optionally, you can add a script in your package.json: `"start": "node server.js"` to start your server
