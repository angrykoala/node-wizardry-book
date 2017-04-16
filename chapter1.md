# What is Node

> **Baby don't hurt me**

So, you've heard about it, Node.js, the new cool \(ish\) kid in school, but what exactly is Node?

> Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8/). Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.
>
> **nodejs.org**

So, in a nutshell, Node.js is a fancy JavaScript interpreter with C++/OS bindings through the [Node API](https://nodejs.org/api/) and a kick-ass package manager glued together. This allows you to execute your lovely JS code in your computer \(just like if you were using Python or Ruby\) without a Browser \(or a DOM tree\). The API allows you to access to the usual OS features, such as read-write files with JavaScript. Before embarking in the beauties of Node, it is highly recommended to know a bit of JavaScript.

## Two for the price of one

When installing Node.js, you usually get a 2x1 offer, as you get two separate programs which, along with your favourite text editor and a terminal, will compose your development environtment, no nasty IDEs or weird libraries.

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

The main usage of npm, is a package manager, it allows you to install packages from the npm repository \(https://www.npmjs.com\)





More details will be discussed in the chapter [Managing your project](/advanced-topics/managing-your-project.md)

## About Node \(and JS\) versions



