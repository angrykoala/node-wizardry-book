# Introduction to Node API

Node.js provides a set of modules that can be used at any moment by importing them just like any module:

```js
const http=require('http'); // Imports http module
```

These modules are already installed by default with Node, so they don't have to be downloaded or installed. The API may be different depending on the version of Node you are using, remember to check the official documentation \([https://nodejs.org/api](https://nodejs.org/api)\) to see the current specification.

> Remember that this guide is written using **Node 6 LTS**

Most Node modules are just bindings to the OS, providing an efficient implementation of most needed features that are not in JavaScript by default such as file I/O or Networking.

## Modules

Lets see some of the most common modules:

### fs

The `filesystem` \(fs\) module handles the interaction with the OS file system, such as reading and writing files, folder creation and navigation. This library abstracts most of the OS differences, allowing to reuse most of the code in different OS \(Windows, Mac and Linux\).

**Create and deleting directories**

The methods `mkdir` and `rmdir` allows you to create and remove directories:

```js
const fs=require('fs');

// Create directory "my_directory" in current execution path
fs.mkdir("my_directory",(err)=>{
    // Creates folder "other" inside "my_directory"
    fs.mkdir("my_directory/other", (err)=>{
        // Removes "other" folder
        fs.rmdir("my_directory/other",(err)=>{

        });
    });
});
```

As you can see in this example, folder manipulation is an asynchronous task, which mean we have to work with callbacks to know when an operation has finished.

Most I/O apis are async, because these operations depend on the Operative System and we don't want to block our code execution waiting for them to finish.

In the previous example, the variable `err` is passed as the first parameter of the callback, most APIs work this way, if there is any problem in the folder creation \(e.g. the folder already exists\), the variable `err` will return the error information. If there was no problem, the variable will be `null` or `undefined`.

So, if we wanted to rewrote the previous code, but taking in account possible errors:

```js
const fs=require('fs');

fs.mkdir("my_directory",(err)=>{
    if(err) return console.error(err);
    fs.mkdir("my_directory/other", (err)=>{
        if(err) return console.error(err);
        fs.rmdir("my_directory/other",(err)=>{
            if(err) return console.error(err);
        });
    });
});
```

This way, on each step we check if there was an error, log it, and finish the callback execution calling `return`.

> Most Async apis behave these way regarding errors, because the common `try...catch` pattern doesn't work with asynchronous code. to improve error handling, we can use `Promises` which we will learn about in a different chapter.

Node I/O also provides a synchronous version of most methods, these will block execution, and are usually not recommended, but for cases where you need to wait for a OS operation to finish before continuing they may come handy:

```js
const fs=require('fs');

try{
    fs.mkdirSync("my_directory");
    fs.mkdirSync("my_directory/other");
    fs.rmdirSync("my_directory/other");
} catch(e){
    console.error(e);
}
```

This version is something more similar to what you may find in another programming languages such as Python or Java.

> When dealing with paths, you can use relative paths to your code execution, full paths \(`./`\) or paths relative to current file using the variable `__dirname` \(`__dirname+"/my_folder"`\)

**Create and remove files**  
The fs module provides methods to handle write and read streams, mainly needed when dealing with large chunks of data or when performance is important. However, the method `writeFile` is the simplest way to create files, it will create or truncate the file:

```js
fs.writeFile("my_file.txt","file content",(err)=>{

});
```

This will create \(or overwrite\) the file `my_file.txt`, adding the content in the second parameter. The callback works the same way as in `mkdir`.

The method `unlink` allows to remove a file:

```js
fs.unlink("my_file.txt",(err)=>{

});
```

Both, `writeFile` and `unlink` have the sync versions `writeFileSync` and `unlinkSync`

**File system navigation**

The fs module also provide methods to read the contents of a folder and get data of each element:

The method `readdir` retrieves an array with all the files \(and folders\) inside the given directory, excluding `.` and `..`

```js
fs.readdir("my/path", (err, files)=>{
    // files == ["my_file1.txt", my_file2.png", "my_folder"]
});
```

With `stat` you can get information about a certain file or folder:

```js
fs.stat("path/to/foo.txt", (err, fileStats)=>{
    fileStats.size; // 527
    fileStats.isFile(); // true
    fileStats.isDirectory() // false
});
```

The returned object is an instance of the class `Stats`, you can check the full description of it in the official documentation.

**Watching directories**

Finally, another useful feature of the fs module, is "_watching_" directories and files, allowing you to trigger events the moment one of those is modified. Either by your own application or by and external program or user:

With `watch` you can hook events to changes in a directory:

```js
fs.watch("my/path", (eventType, filename)=>{
    // eventType is a string that defines what happened with the file
    // filename is the name of the file affected
});
```

The method `watchFile` does the same, but attached to a single file.

> You can check the full documentation of the fs module here: [https://nodejs.org/api/fs.html](https://nodejs.org/api/fs.html)

### http

There are several frameworks and libraries in Node.js to help you handle anything related to web servers and http requests. But in the end most of them use the _http_ built-in package. While it is recommended to use a framework for most use cases, the _http_ package is still very powerful and quite useful. Here we will only cover some basics.

**Creating an http server**


**Making requests**

> You can check the full documentation of the http module here: [https://nodejs.org/api/http.html](https://nodejs.org/api/http.html)

### path and url

The `path` module provides a simple interface to manipulate OS paths \(e.g `/home` or `C:/`\) so you don't need to directly manipulate strings for paths. The interface to generate paths is the same regardless of the underlying operating system, so by using this module instead of strings your application will work almost the same way in Windows, Linux and OSX without making any modifications.


**Formatting paths**   
The following methods ease the creation of paths, regardless of the platform:

* `path.join`: Given multiple strings, generates a path combining all of them, solving for relative paths

```js
const path=require('path');
path.join("my","folder"); // "my/folder" in Linux
path.join("/my/folder","inside",".."); // "/my/folder" in Linux
```

* `path.relative(from, to)`: Gives the relative path between 2 paths

```js
path.relative("folder","folder/inside.txt"); // "inside.txt"
path.relative("/", "."); // "home/angrykoala/folder/current_folder"
```

**Parse paths**
The path module also allows you to extract information from a path without manually handling strings
* `path.parse`: Given a path, `parse` returns an object with information about it.
```js
path.parse("path/to/file.txt");
/*{
 root: '',
 dir: 'path/to',
 base: 'file.txt',
 ext: '.txt',
 name: 'file'
}*/
```

Instead of doing the whole parse of the path, a few specific methods exists:
```js
const myPath="path/to/file.txt";
path.basename(myPath); // "file.txt"
path.dirname(myPath); // "path/to"
path.extname(myPath); // "-txt"
```

> Remember `__dirname` contains the path of the file being executed. Instead of concatenating (`__dirname+/local/path`), it is better to use `path.join(__dirname, "local/path")`

> You can check the full documentation of the path module here: [https://nodejs.org/api/path.html](https://nodejs.org/api/path.html)

The `url` module provides similar features, this time to handle url directions such as `192.1.1.0` or `localhost:3131`. It is particularly useful for web applications.

**URL object**
The URL class defines an URL and allows you to access to its metadata:
```js
const URL=require('url').URL;

const my_url=new URL("api", "http://foo.bar"); // Same as new URL( "http://foo.bar/api")

my_url.host; // "http://foo.bar"
my_url.hostname; // "foo.bar"
my_url.pathname; // "api"
```
Basically, it allows you to easily parse all the data from a URL (including queries, port,...) from the raw string.

* `url.format`: Given an URL object, returns the string with the url properly formatted.
```js
const url=require('url');
const URL=url.URL;

const my_url=new URL("api", "http://foo.bar");
url.format(my_url); // "http://foo.bar/api"
```


* `url.resolve`: Allows you to resolve a relative url from a given base url

```js
url.resolve("http://foo.bar/index.html", "api"); // http://foo.bar/api
```
Note how only the base (`http://foo.bar/`) was used, the index.html was stripped. In this example no URL objects are used.

> You can check the full documentation of the path module here: [https://nodejs.org/api/url.html](https://nodejs.org/api/url.html)

### utils

## process variable





> The latest documentation of these modules is in [https://nodejs.org/api](https://nodejs.org/api)
