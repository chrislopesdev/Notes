# FUNCTIONS

## How to declare a function

**_Functions_** allow us to package up lines of code that we can use, and often reuse, in our programs.

Sometimes functions can take in parameters.

```
function reheatPizza(numSlices) {
  // code that completes reheat settings
}
```

Multiple parameters can be used and are separated by a comma.

```
function addNumbers(a, b) {
  console.log(a + b);
}
```

Other functions do not require any parameters.

```
function sayHello() {
  console.log('Hello!);
}
```

</br>
</br>

## Function Expressions

Functions can be stored inside variables, these are known as **_function expressions_**.

```
var catSays = function(maxNumber) {
  var catMessage = "";
  for (let i = 0; i < maxNumber; i++) {
    catMessage += "meow ";
  }
  return catMessage;
}
```

The function keyword no longer has a name and is considered an **_anonymous function_**.

### Patterns with Function Expressions

Being able to store functions in variables makes it easy to pass the function into another function. A function passed into another function is called a **_callback_**.

```
var catSays = function(maxNumber) {
  var catMessage = "";
  for (let i = 0; i < maxNumber; i++) {
    catMessage += "meow ";
  }
  return catMessage;
}

//function declaration helloCat accepting a callback
function helloCat(callback) {
  return "Hello " + callback(3);
}

// pass in catSays as a callback function
helloCat(catSays);
```

### Inline Function Expressions

You can pass a function as an argument to another function.

```
// Function expression that assigns the function displayFavorite
// to the variable favoriteMovie
var favoriteMovie = function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
};

// Function declaration that has two parameters: a function for displaying
// a message, along with a name of a movie
function movies(messageFunction, name) {
  messageFunction(name);
}

// Call the movies function, pass in the favoriteMovie function and name of movie
movies(favoriteMovie, "Finding Nemo");
```

> **_Returns:_** My favorite movie is Finding Nemo

You can bypass the first assignment of the function by passing the function to movies() function inline:

```
// Function declaration that takes in two arguments: a function for displaying
// a message, along with a name of a movie
function movies(messageFunction, name) {
  messageFunction(name);
}

// Call the movies function, pass in the function and name of movie
movies(function displayFavorite(movieName) {
  console.log("My favorite movie is " + movieName);
}, "Finding Nemo");
```

> **_Returns:_** My favorite movie is Finding Nemo

This type of syntax, writing function expressions that pass a function into another function inline, is really common in JavaScript.

**_Why use anonymous inline function expressions?_**

Using an anonymous inline function expression might seem like a very not-useful thing at first. Why define a function that can only be used once and you can't even call it by name?

Anonymous inline function expressions are often used with function callbacks that are probably not going to be reused elsewhere. Yes, you could store the function in a variable, give it a name, and pass it in like you saw in the examples above. However, when you know the function is not going to be reused, it could save you many lines of code to just define it inline.

</br>
</br>

## Return Statements

The `return` statements allows us to return a value from our function instead of just printing to the console. A function will always return a value. If a `return` value is not specified, the function will return `undefined`. The `return` keyword **_will exit the function_** and return a value.

```
function addNumbers(a, b) {
  return a + b;
}
```

### Using Return Values

You can store a return value in a variable:

```
function add(a, b) {
  return a + b;
}

let sum = add(5, 10);
```

</br>
</br>

## Running a Function

To get the function to work, you must **_call_** or **_invoke_** the function using its name followed by parenthesis and any **_arguments_** that need to be passed into it. A function is like a machine, you can build it, but it wont do anything unless you turn it on.

```
// declares the sayHello function
function sayHello() {
  var message = "Hello!"
  return message; // returns value instead of printing it
}

// function returns "Hello!" and console.log prints the return value
console.log(sayHello());
```

> **_Prints:_** "Hello"

</br>
</br>

## Parameters vs. Arguments

A **_parameter_** is a placeholder used in declaring your functions. The **_arguments_** are passed into the function when calling it.

```
function sayMyName(parameter) {
  console.log("Hello " + parameter)
}

sayMyName(argument);
```

</br>
</br>

## Scope

Two kinds of scope: **_global_** and **_function/block_**.

### Global Scope

Identifiers that can be accessed anywhere within your program. This may seem easiest to use as they can be used anywhere in your code, but as your programs get larger you can run into conflicts. It is best practice to minimize use of global variables.

### Function / Block Scope

Identifiers that can be accessed anywhere inside your function or block it was defined, but not outside of it. If an identifier is unavailable in function scope it will continue up the scope chain until it gets to the global scope.

```
let name = "chris"; // global scope

function myAge() {
  let age = 40; // function scope
}

console.log(name); // prints "chris"
console.log(age): // prints error
```

</br>

### Shadowing (Overriding)

This can be an issue when reusing variable names in global and function scope:

```
var bookTitle = "Le Petit Prince";
console.log(bookTitle);

funciton displayBookEnglish() {
  bookTitle = "The Little Prince";
  console.log(bookTitle);
}

displayBookEnglish();
console.log(bookTitle);
```

> **_Prints:_** </br>
> Le Petit Prince </br>
> The Little Prince </br>
> The Little Prince

bookTitle got reassigned in the global scope. To avoid this issue we should delcare the variable in the function scope.

```
var bookTitle = "Le Petit Prince";
console.log(bookTitle);

funciton displayBookEnglish() {
  var bookTitle = "The Little Prince";
  console.log(bookTitle);
}

displayBookEnglish();
console.log(bookTitle);
```

> **_Prints:_** </br>
> Le Petit Prince </br>
> The Little Prince </br>
> Le Petit Prince

</br>
</br>

## Hoisting

Sometimes Javascript can produce errors that seem counterintuitive. These issues can sometimes be caused by **_hoisting_**.

JavaScript hoists function declarations and variable declarations to the top of the current scope. Variable assignments are **_not_** hoisted. It is best practice to write code in the order it should be read by Javascript.

> **_Note:_** Function expressions are **_NOT_** hoisted.

```
sayGretting();

function sayGreeting() {
  console.log(greeting);
}
```

This will be interpreted as:

```
function sayGreeting() {
  console.log(greeting);
}

sayGretting();
```

Variable Hoisting:

```
function sayGreeting() {
  console.log(greeting);
  var greeting = "hello";
}

sayGretting();
```

This will be interpreted as:

```
function sayGreeting() {
  var greeting;
  console.log(greeting);
  greeting = "hello";
}

sayGretting();
```

This will cause an error in the code.
