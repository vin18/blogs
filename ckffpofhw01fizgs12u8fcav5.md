## async vs defer attributes in Javascript

## Introduction
A `script` tag is used to load javascript inside a web browser. `async` and `defer` are the boolean attributes used along with the `script` tag to load the external scripts efficiently into the web page. In this article, we will cover the following scenarios of how a javascript file can be loaded using:

1. `script` tag.
2. `script` tag with `async` attribute.
3. `script` tag with `defer` attribute.

## What happens when you load a web page?
When you load a web page, there are 2 things that are happening inside the browser:
1. HTML parsing.
2. Loading of the scripts.

Loading of the script contains two parts:
1. Fetching the script from the network.
2. Actually executing the script line by line - know as **thread of execution**. 

## Using `script` tag
When your browser is parsing the HTML line by line building the DOM (Document Object Model) and if it encounters a `script` tag, It pauses the parsing of HTML, fetches the script from the network, and executes the script inside the browser. The rest of the DOM is built after the script is loaded and executed. 

```
<html>
  <head>
    <title>My Webpage</title>
    <script src="./main/javascript/helloWorld.js"></script>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```
Here, 
1. HTML parsing starts from line 1 and the browser starts building the DOM.
2. At line 4, when the browser encounters the `script` tag, it pauses the parsing. It fetches the file from the network and executes it line by line. After the execution of the script is completed, it resumes the parsing and moves onto the `body` tag to build the rest of the DOM.

This lead to two important issues: 
1. They can't add event handlers, etc as the DOM is not fully built.
2. It **blocks** the page. Users can't see the rest of the page content until it downloads and runs the script.

Both of these issues can be solved by specifying the `script` tag at the end of the `body` tag but that's not very efficient. We have `async` and `defer` attributes for this use case.

## Using `async` attribute
With the `async` attribute, whenever the HTML parsing is going on, the scripts are fetched from the network **asynchronously**. After the scripts are loaded and available inside the browser, the scripts are executed then and there. After the scripts are executed, the rest of the HTML parsing is done. Here, the loading of the scripts is done parallelly with HTML parsing unlike in the normal `script` tag.
Let's consider an example where there are two files -  **long.js** and **short.js**. Consider **long.js** script is heavier than **short.js** script:
```
<html>
  <head>
    <title>My Webpage</title>
    <script async src="./main/javascript/long.js"></script>
    <script async src="./main/javascript/short.js"></script>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

1. At line 1, HTML parsing is started.
2. At line 4, the browser encounters the `script` tag with the `async` attribute.
3. The **long.js** script is being fetched **asynchronously** in parallel and control moves to the next line. 
4. The **short.js** script is then fetched **asynchronously** in parallel and controls move to the next line. 
5. Whichever files are loaded first is executed. Therefore, even though **long.js** is encountered first, **short.js** is loaded first and executed.
6. The rest of the DOM is built.

## Using `defer` attribute
It is similar to the `async` attribute where the scripts are loaded in parallel. The difference being the scripts are only executed when the HTML parsing is fully complete and the DOM is built.

```
<html>
  <head>
    <title>My Webpage</title>
    <script defer src="./main/javascript/long.js"></script>
    <script defer src="./main/javascript/short.js"></script>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

1. At line 1, HTML parsing is started.
2. At line 4, the browser encounters the `script` tag with the `defer` attribute.
3. The **long.js** script is being fetched in parallel and control moves to the next line. 
4. The **short.js** script is then fetched in parallel and controls move to the next line. 
5. The HTML parsing is done and DOM is built. 
6. Execution of scripts.

> Note: Even though **short.js** is fetched first, the execution order is maintained. In this case, **long.js** will execute before **short.js**.

## When to use what
* Using `async` attribute doesn't guarantee the order of execution of scripts. Async scripts are mostly used to load the third-party scripts that are not dependent on each other like google analytics, etc. 
* Use `defer` attribute when scripts are dependent on each other. These scripts are mostly used as they give the best of both worlds - execution in order and parallel fetching of scripts while HTML parsing.

## Summary
* In normal `script` tags, whenever the scripts are encountered, the script is loaded and executed then and there, and the rest of HTML parsing is done.
* With the `async` attribute, scripts are fetched parallelly along with HTML parsing, and as soon as scripts are loaded they are executed.
* With the `defer` attribute,  scripts are fetched parallelly along with HTML parsing, and as soon as HTML parsing is done, they are executed.

That's pretty much the different efficient ways to load javascript files into the web browser. If you have any feedback or suggestions, feel free to reach out to me on [Twitter](https://twitter.com/vinitraut18) or [LinkedIn](https://www.linkedin.com/in/vinit-raut-404651148/). 

 