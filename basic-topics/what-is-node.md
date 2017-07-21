# What is Node

> **Baby don't hurt me**

You've heard about it, Node.js, the new cool-ish kid in school. You want to learn it, but, What is Node?

> Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8). Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, [npm](https://www.npmjs.com), is the largest ecosystem of open source libraries in the world.
>
> **nodejs.org**

In a nutshell, Node.js is a fancy JavaScript interpreter with C++/OS bindings and a kick-ass package manager glued together.

This environment allows you to execute your happy little code in your computer just like other programming languages such as Python or Ruby, without a Browser. The API allows you to access to the usual OS features, such as reading-writing files with JavaScript.

## Two for the price of one

When installing Node.js, you get a 2x1 offer, as you get two separate programs, _node_ and _npm_ which, along with your favorite text editor and a terminal, will compose your development environment. No nasty IDEs or plugins.

You can download Node in the official web page: [https://nodejs.org/en/download](https://nodejs.org/en/download)

Node works pretty much the same way in Linux, Windows and Mac. However, the way to install it may change.

### Node

The main program you'll need to install is \(unsurprisingly\) node, the JavaScript _interpreter_, once installed, it's pretty straightforward to use, in the same way you would use Python for example, just open a terminal \(sorry, anonymous Windows user, you'll have to do it this time\) and type:

```
$ node
```

This will open the Node REPL \(Read-Eval-Print-Loop\) that allows you to execute JavaScript commands in your terminal. Keep in mind that DOM/Browser functionalities \(like `alert` or `window`\) are not available.

> In some systems, you may find out that the command is `nodejs`

So, lets type some code in our REPL:

```js
> console.log("Hello, World!");
```

In return, our friendly REPL will say:

```
Hello, World!
undefined
```

The last line shows the result of our command \(which is `undefined` because `console.log` doesn't return anything\), the lines above are the output of our command \(`Hello, World!`\). You can write more commands if you want. To exit the REPL, press Ctrl+C twice.

While the REPL is a lot of fun, you'll probably want to create your own programs in a separate file \(e.g. `my_program.js`\). So we will write our Hello World example in that file, and execute it with:

```
$ node my_program.js
```

This will output:

```
Hello, World!
```

Notice how `undefined` is not shown anymore.

### NPM

The success of Node.js is, partially, due to the _Node Package Manager_. Acting as a combination of a package manager, task runner, and project meta-data, all in one. It allows to easily manage your project.

While there are other fancy tools that we will discuss in other chapters, for most small/medium sized projects, **npm**  is all you'll need to manage your project.

The main usage of npm is as a package manager, it allows you to install packages from the npm repository\([https://www.npmjs.com](https://www.npmjs.com)\), you can install packages with:

```
$ npm install <my-package>
```

By default, it will install packages _locally_ to your folder, inside the folder `node-modules`, this allows you to use those packages within your project as dependencies without affecting the rest of projects you may have. You can also install packages _globally_, allowing you to use them across all projects and execute \(when possible\) from the terminal as any other program:

```
$ npm install -g <my-package>
```

More details will be discussed in the chapter [Creating your first project](/projects/creating-your-first-project.md) and [Managing your project](/advanced-topics/managing-your-project.md)

## About Node versions

Node.js has been under constant development since its initial release in 2006, with new versions published frequently since then.

JavaScript, as a language, received some updates lately too, \(ECMAScript 5th and 6th\). Not every JavaScript interpreter is up to date, and some old Node.js versions don't fully implement ES6.

Node.js and JS are, with some exceptions, backwards compatible, which means that a program made for a certain version will keep working with newer node implementations, but not the other way.

While node receives updates regularly, the important versions are the **LTS** versions. It's better to use one of these unless you need the latests features.

While using the latest LTS \(Node 6 at the moment\) should be a good option for most development projects, you should be aware of the following node versions:

* **0.12**: While no longer under maintenance, node 0.12 is still used, and a lot of packages were developed using this version. ES6 is not fully supported in this version.
* **4.x**: This is the first official release of node and implements most of the ES6 functionality. Most apps written with node 7 will work down to this version.
  * The _"jump"_ between node 0.12 and 4.x is due to a merge between the projects node.js and its fork [io.js](https://iojs.org), to avoid confusion and versioning problems between those, node was released with 4.x directly.
* **6.x**: This version is the latest LTS at the moment of writing this implements even more ES6 features and general performance improvements among other changes.

To see what version is installed in your system, type:

```bash
$ node -v
```

> At the moment of writing this guide, **Node 8.2.1 **is the latest version, for this guide we will use **Node 6**.

You can check the official LTS Schedule in [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)

