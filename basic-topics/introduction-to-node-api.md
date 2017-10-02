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



### path and url

The `path` module provides a simple interface to manipulate OS paths \(e.g `/home` or `C:/`\) so you don't need to directly manipulate strings for paths. The interface to generate paths is the same regardless of the underlying operating system, so by using this module instead of strings your application will work almost the same way in Windows, Linux and OSX without making any modifications.

> TODO: list methods and examples here
>
> When

The `url` module provides a similar interface, this time to handle url directions such as `192.1.1.0` or `localhost:3131`. It is particularly useful for server applications.

> TODO: list methods and examples here

### utils





## process variable



