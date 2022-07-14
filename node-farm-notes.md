<!-- # Markdown Cheatsheet

# H1

## H2

### H3 etc.

**bold text**

_Italicised_

> blockquote

1. Ordered list

- Unordered list

`code`

--- horizontal rule

[title](https://www.example.com) link

![alt text](image.jpg) image -->

# WELCOME TO NODE.JS!

## What is Node.js?

**Node.js** is a runtime that allows us to run javascript outside of the browser. Node still runs on Google's V8 engine, just like in the Chrome browser, but Node has access to additional functionality via modules, such as **fs**, which can us to do things like access and modify files on the machine running the code.

We can run Node in **REPL** mode to execute javascript in the terminal by simply typing `node` into the terminal. Then we can create and use variables, perform operations, and even reference the last result with `_`.

This is just like running javascript code in the browser's console but obviously this is very limited. What we really want to do is to write scripts/files that will execute more complex operations for us.

To exit **REPL** mode either type `.exit` or hit _ctrl+c_ twice.

When not inside of **REPL** you can run a javascript file, assuming your terminal is in the correct directory, by typing one of the following

```
node filename.js
```

```
node filename
```

And if the file happens to be named `index.js` then we can even more simply type

```
node .
```

## Where is it running?

Usually we write javascript code to be executed in a browser and so we make and use html elements and operate inside the global **window** object.

Instead of **window** the global object for Node is an object actually called **global**.

To make this clearer, look at how you assign a global variable in javascript for browser vs Node (javascript for machine/server)

```
window["myvar"] = value
global["myvar"] = value
```

The only difference is the global object for each runtime

## Accessing files

### Read file

Node javascript is executed _on your machine_ or _on a server_. Because of this we can actually access files on the machine the code is being run on.

To do this we need to make use of **Node Modules**

We can see a list of the Modules available in Node by going into **REPL** mode (by typing `node` into the terminal) and tapping tab twice.

One of these modules is **fs** which means _file system_.

To use this module we need to _require_ it in our code before we use it (doesn't have to be at the top of the file like import, just before use).

```
const fs = require('fs')
```

Now we have access to a range of methods to access the files on the machine, both _synchronously_ and _asynchronously_.

First, let's look at accessing a text file in our project _synchrnoucly/blocking_. We need to use `.readFileSync()` from **fs** and pass in the relative file path from our script and the _character encoding_ we want to use (usually 'utf-8'). This will return the content of the file which we can save to a variable like so.

```
const textIn = fs.readFileSync('./txt/input.txt', 'utf-8')
```

We could then log this text to the console with `console.log(textIn)` just like we would for the browser console, only with Node it will not appear in our browser console but our machine's terminal (like powershell if working in that or in our IDE if using something like VScode).

### Write file

We're not limited to just accessing and reading files, we can also use **fs** to write files to the machine.

We can do this by using `fs.writeFileSync()` and passing in the pathway we want to write the new file to (including the extension) as the first argument and the actual content we want to put in this new file as the second argument (this could also be a variable).

```
fs.writeFileSync('./txt/output.txt', 'Example text to put in the new file')
```

Once we save our script nothing will happen and we won't see the new file, just like we do not see a `console.log()` in the terminal until we execute or Node code.

Executing the script would then create this new file with text in the second argument as its content.

If the file already exists then it will simply be overwritten/replaced as if it didn't before.

## Synchronous vs Asynchronous

Javascript is a _single-threaded_ language, meaning that it only has one _train of thought_ and can only do one thing as a time. Think of it like someone who cannot multitask and will do anything you tell them but only one at a time and they won't move on to the next task until their current task is complete.

This behaviour means that any line of our code that takes a long time to execute, or has to wait for something else to respond, can hold up all of the code below/after it until it has finished.

To get around this code that _blocks_ the execution of our program we can use **asynchrnous** code to execute certain tasks in a _non-blocking_ way.

Without getting into too much detail, asynchrnous code gets _put off to one side_ and will be executed _when it is ready_ and _when the remaining synchrnous/blocking code is finished first_.

Going back to our human worker analogy, think of the code as a todo list. If one of the todo items is listed as asynchronous/non-blocking they tear it out, put it to one side, then continue working down the list. Once all of the regular todo items are done _then_ the will turn their attention to executing the asynchronous task they put to one side before.

Asynchrnous tasks _get out of the way_ but they do not _get forgotten_.

Why does this matter? Because many thinks we want to do with the web and on servers will require responses from other machines around the world. If our code is blocking and we make a request for some data then nothing else will happen until we get the reponse, our program will essentially freeze.

Non-blocking code allows us to make time intensive operations and requests without locking/freezing our programs.

## Reading/writing files asynchronously

Before we used `fs.readFileSync()` and `fs.writeFileSync()` to read and write files in a blocking/synchronous way. Now we will use `fs.readFile()` and `fs.writeFile()` to do the same but **asynchronously** by use of a callback function as a third argument

```
const textIn = fs.readFile('./txt/input.txt', 'utf-8', (err, data) => {console.log(data)})
```

The callback function has access _err_ and _data_ and will execute the code inside the braces when either an error or the data is received.
