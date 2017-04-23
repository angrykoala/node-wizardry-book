# What is Node

> **Baby don't hurt me**

So, you've heard about it, Node.js, the new cool \(ish\) kid in school, but what exactly is Node?

> Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8/). Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.
>
> **nodejs.org**

So, in a nutshell, Node.js is a fancy JavaScript interpreter with C++/OS bindings through the [Node API](https://nodejs.org/api/) and a kick-ass package manager glued together. 

This environment allows you to execute your "lovely" JS code in your computer \(just like if you were using Python or Ruby\) without a Browser \(or a DOM tree\). The API allows you to access to the usual OS features, such as reading-writiting files with JavaScript. 

Before embarking in the beauties of Node, it is highly recommended to know a bit of JavaScript.

## Two for the price of one

When installing Node.js, you usually get a 2x1 offer, as you get two separate programs which, along with your favourite text editor and a terminal, will compose your development environtment, no nasty IDE or weird libraries.

### Node

The main program you'll install is \(unsurprisingly\) node, the JavaScript _interpreter_, once installed, is pretty straighforward to use, in the same fashion as Python, just open a terminal \(sorry, anonymous Windows user, you'll have to open one this time\) and type:

```
$ node
```

This will open the Node REPL \(Read-Eval-Print-Loop\) that allows you to execute JavaScript commands in your terminal. Keep in mind that any DOM/Browser functionality \(like `alert` or `window`\) are not available.

Because this is a completely original book, and all our ideas are new and original, lets type the following code in our REPL:

```
> console.log("Hello, World!");
```

And in return, our friendly REPL will say:

```
Hello, World!
undefined
```

The last line shows the result of our command \(which is undefined for a console.log call, as it returns nothing\), the lines above are the stdoutput of our command. You can keep writing commands, to exit the REPL, just press Ctrl+C twice.

While the REPL is a lot of fun, you'll likely want to create your own programs in a separate file \(e.g. `my_program.js`\). So we will write our Hello, World example in that file, and execute it with:

```
$ node my_program.js
```

This will output:

```
Hello, World!
```

Notice how `undefined` is not shown anymore.

### NPM

The success of Node.js is, in great part, thanks to the _Node Package Manager_. Acting as a combination of a package manager, task runner, and project metadata, all in one.

While there are other fancy tools that will be discussed in following chapters, for most small/medium sized projects, **npm** \(along with node, a terminal and a text editor\) is all you'll need to manage your project.

The main usage of npm, is as a package manager, it allows you to install packages from the npm repository \([https://www.npmjs.com](https://www.npmjs.com%29\), you can install packages with:

```
npm install <my-package>
```

By default, it will install packages _locally_ to your folder, as a dependency, inside the folder `node-modules`, this allows you to use those packages within your project without affecting the rest of projects you may have. You can also install packages _globally_, allowing you to use them across all projects and execute \(when possible\) from the terminal as any other program:

```
npm install -g <my-package>
```

More details will be discussed in the chapter [Creating your first project](/creating-your-first-project.md) and [Managing your project](/advanced-topics/managing-your-project.md)

## About Node \(and JS\) versions

Node.js has been under constant development since its initial release in 2006, with several new versions being published every year since then.

JavaScript, as a language, received some updates lately too, the ECMAScript 5th and 6th version. It is important to note that not every JavaScript interpreters is up to date, and only some Node.js versions implement ES6.

Node.js \(and JS\) is, with some exception, retrocompatible, which means that usually a program made for a certain version, will keep working with newer implementations, but not the other way.

While node receives updates regularly, the important versions are \(usually\) the **LTS** versions. It is recommended to use one of these unless you want the latests features.

While using that latests LTS \(Node 6 at the moment\) should be a good option for most development projects, you should be aware of the following node versions:

* **0.12**: While no longer under maintenance \(and still a beta version\) node 0.12 is still heavily used, and a lot of packages are developed used this version. ES6 is not fully supported in this version
* **4.x**: This is the first official release of node and implements most of the ES6 functionality. Most app written with node 7 will work down to this version.
  * The _"jump"_ between node 0.12 and 4.x is due to a merge between the projects node.js and io.js, to avoid confusion and versioning problem between those, node was released with 4.x directly
* **6.x**: This version \(the latest LTS at the moment of writing this\) implements more ES6 features and provides improvements in performance.

> At the moment of writing this guide, **Node 7.9.0** is the latest version, for this guide we will assume **Node 6** is used

You can check the official LTS Schedule here: [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)

