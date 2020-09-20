## Variable Scopes in Javascript

## Introduction
Welcome to the first part of the series, [Javascript - The Tricky Parts](). This series is all about learning some tricky, albeit the important parts of Javascript. In this article, we will explore an important concept in Javascript called `Scope`. 

## Scopes in Javascript
> Scope is the context in which values and expressions are "visible" or can be referenced - MDN

By scopes, we mean the lifetime of a variable where the variable is visible and available for you to use in your code. 

In Javascript, we have different types of scopes:

1. Global Scope
2. Function Scope
3. Block Scope

### 1. Global scope

Any variable declared outside of a block or a function, we refer to them as **global** scope variables.
```
var myAge = 21;
```
Here, we have declared `myAge` variable that can be used in any part of the program including deeply nested loops or functions.

We can also declare a global variable with the help of the `window` object.
```
window.myName = "Vinit";
```
Here, we have declared another global variable `myName`. We can also access the `myAge` variable using `window.myAge`, the reason we can use global variables with the `window` object is that all the global variables are the properties of the `window` object.

> Note: `window` object is only available inside the browser environment. We have a `global` object inside the node environment that behaves the same way.

### 2. Function scope (Local scope)
As the name implies, the variables that are declared inside of a function are **function scoped**.  This means the variables are **only** accessible within that particular function.

```
function printName() {
  var myName = "Vinit";
}
printName();
console.log(myName); // ReferenceError: myName is not defined

```
Here, we get an error because `var` are function scoped. We can only access the `myName` inside the `printName` function.  

```
function printName() {
  var myName = "Vinit";
  console.log(myName); // "Vinit"
}
printName();
```
Now, the engine won't throw an error because we have access to the `myName` variable inside the `printName` function.


Let's talk about a tricky case:
```
for (var i = 0; i < 5; i++) {
  var j = 5;
}

console.log(i); // 5

```
Is `i` accessible outside of a `for` loop? If you're coming from another programming background, you may think this block of code will throw an error, but it prints 5. In other programming languages like C++ or Java, if we declare a variable using a loop such as `for` loop, they are block-scoped but this is different in Javascript. `var` in javascript are **function** scoped. If `var` is declared inside a function, it's available inside that particular function.

> Note: `j` here will be declared as a global variable since it's not declared within a function.

### 3. Block scope
In ES6, another scope was introduced which is a block-level scope with keywords like `const` and `let`. The difference between `const` and `let` is that we can't reassign variables that are declared with `const`. The idea here is the visibility of variables inside a block scope is limited to that particular block only. Let's see an example:
```
{
  var myName = 'Vinit';
}
console.log(myName); // Vinit 

```
Even though we have defined a block, variables declared with `var` are always **function** scoped. What happens if we declare the same with a `let` or `const` keywords?

```
{
  let firstName = 'Vinit';
  const lastName = 'Raut';
}
console.log(firstName);  // ReferenceError: firstName is not defined. 
console.log(lastName);   // ReferenceError: lastName is not defined. 
```

We are getting errors because variables declared with `let` and `const` are **block-scoped**. We can only access `firstName` and `lastName` inside that particular block.

```
{
  let firstName = 'Vinit';
  const lastName = 'Raut';

  console.log(firstName);  // Vinit
  console.log(lastName);  // Raut
}

```

> Tip: Always use `const` while declaring a variable unless you want to modify it, use `let` for this use case. Avoid using `var` while declaring variables to write more robust code.

### Quiz time
Can you guess the output of the code?

1. Quiz A
```
for (let i = 0; i < 5; i++) {
  console.log(i);
}
console.log(i); // ?
```

2. Quiz B
```
function person() {
  const name = "Vinit";
    function printName() {
      console.log(name); // ?
    }
    printName();
}
person()
```

Solution A: It will print `0, 1, 2, 3, 4` and then throw reference error because `i` is only accessible (block scoped) inside the `for` loop.

Solution B: It will print `Vinit` since variables can be accessible by the inner functions and nested loops but it's not vice versa.

## Summary

- In Javascript, we have three different types of scope - Global scope, Function scope, and Block-level scope.
- Variables declared with `var` keyword inside a function are **function scoped** and are accessible inside that particular function only. 
- Variables declared outside of a function or a block are **global scoped** that can be accessed in any part of the program. 
- Variables declared with `let` and `const` (recommended) inside a block are **block-scoped** that is accessible inside that particular block only.

If you found this useful, feel free to like and share this article. If you have any feedback or suggestions you can reach out to me on  [Twitter](https://twitter.com/vinitraut18) or [LinkedIn](https://www.linkedin.com/in/vinit-raut-404651148/). In the next article, we will explore **Hoisting** in Javascript.
