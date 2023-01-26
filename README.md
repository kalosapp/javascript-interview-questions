# Jvascript Interview Questions

| Sl.No|  Questions       |
|------|------------------|
| 01. |[What is closure in JavaScript?](#q-what-is-closure-in-javascript)|
| 02. |[What is hoisting in JavaScript?](#q-what-is-hoisting-in-javascript)|
| 03. |[What is the difference between a promise and a callback?](#q-what-is-the-difference-between-a-promise-and-a-callback)|
| 04. |[What are the differences between let and var?](#q-what-are-the-differences-between-let-and-var)|
| 05. |[List ES6 features.](#q-list-es6-features)|
| 06. |[Explain Spread and Rest Operators](#q-explain-spread-and-rest-operators)|
| 07. |[What is Destructuring?](#q-what-is-destructuring)|
| 08. |[Different between promise and async await?](#q-different-between-promise-and-async-await)|
| 09. |[Explain "this" in JavaScript?](#q-explain-this-in-javascript)|
| 10. |[Explain `call`, `apply` and `bind` in JavaScript!](#q-explain-call-apply-and-bind-in-javascript)|
| 11. |[Type of error in JavaScript?](#q-type-of-error-in-javascript)|

<br/>

## Q. ***What is closure in JavaScript?***

In JavaScript, a closure is a function that has access to variables in its parent scope, even after the parent function has returned. Closures are created when an inner function references variables from an outer (enclosing) function. The inner function has access to the variables in the outer function's scope, even after the outer function has returned.

Here is an example of a closure:

```js
function outerFunction(x) {
    var y = 10;
    return function innerFunction() {
        return x + y;
    }
}

var closure = outerFunction(5);
console.log(closure()); // Output: 15
```
In this example, the outerFunction takes a parameter x and creates a variable y. It then returns the innerFunction, which has access to both x and y. When we call outerFunction(5), it returns the innerFunction and assigns it to the variable closure. When we call closure(), it returns the sum of x and y (5 + 10 = 15).

Closures are useful in many ways, for example:

* They can be used to create private variables by returning an inner function that has access to the private variables.
* They can be used to create a module pattern, where an object with a private state is returned.
* They can be used to keep track of state across multiple function calls.
It's important to note that closures can cause memory leaks if not handled properly. Since closures have access to the variables in their parent scope, they keep those variables in memory even after the parent function has returned. This can cause a problem if the closure

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***What is hoisting in JavaScript?***

In JavaScript, hoisting is the behavior of moving function and variable declarations to the top of the scope they are defined in, at the time of the code execution.

JavaScript engine internally moves the variable and function declarations to the top of their scope during the compilation phase, before the code execution.

In JavaScript, variable declarations are hoisted, but not the assignment. This means that if you declare a variable and then initialize it later, the declaration will be moved to the top of the scope, but the assignment will stay in its original position.

Here's an example of hoisting:

```js
console.log(x); // Output: undefined
var x = 5;
In this example, the var x declaration is hoisted to the top of the scope, but the assignment x = 5 is not. So when we access the variable before the assignment, it has the value of undefined.

In the case of function declarations, the entire function is hoisted, including the function body.

Copy code
hoistedFunction(); // Output: "I am a hoisted function"

function hoistedFunction() {
    console.log("I am a hoisted function");
}
```
In this example, we are able to call the function before its declaration.

On the other hand, function expressions are not hoisted.

```js
notHoistedFunction(); // Output: ReferenceError: notHoistedFunction is not defined

let notHoistedFunction = function(){
    console.log("I am a not hoisted function");
}
```
In this case, if you try to call the function before its declaration, you will get a reference error, because the variable notHoistedFunction is hoisted but not the function itself.
    
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***What is the difference between a promise and a callback?***

A callback is a function that is passed as an argument to another function, which is then invoked inside the function, while a Promise is an object that represents a value that may not be available yet but will be at some point in the future.

Callbacks are commonly used in JavaScript to handle asynchronous operations, such as an HTTP request or a timeout. For example:

```js
function getData(callback) {
    setTimeout(() => {
        callback({ data: "Hello World!" });
    }, 2000);
}

getData(function(response) {
    console.log(response.data); // Output: "Hello World!"
});
```
In this example, the getData function takes a callback as an argument and invokes it after 2 seconds with some data.

Promises, on the other hand, are a more modern and elegant way of handling asynchronous operations. A promise is an object that wraps an asynchronous operation and provides a way to register callbacks for when the operation completes (or fails). For example:

```js
let promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve({ data: "Hello World!" });
    }, 2000);
});

promise.then(response => {
    console.log(response.data); // Output: "Hello World!"
});
```

In this example, the Promise constructor takes a function as an argument, which is called immediately. The function takes two arguments resolve and reject. We use the resolve function to return the response data after 2 seconds. We can use the then method on the promise object to register a callback for when the promise is fulfilled.

Promises have several advantages over callbacks:

* They make the code more readable, by chaining asynchronous operations with then and catch methods
* They can be composed and reused more easily.
* They are supported natively in modern JavaScript and can be used with async/await syntax.
It's important to note that, both Callbacks and Promises are used to handle Asynchronous operations in JavaScript, but Promises are more modern and provides more features and flexibility.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***What are the differences between let and var?***

In JavaScript, var and let are both used to declare variables, but they have some key differences:

* Scope: Variables declared with var have function scope, which means that they are only accessible within the function where they are defined. On the other hand, variables declared with let have block scope, which means that they are only accessible within the block where they are defined, and any nested blocks.
```js
function varScope() {
    if (true) {
        var x = 5;
    }
    console.log(x); // Output: 5
}

function letScope() {
    if (true) {
        let y = 5;
    }
    console.log(y); // Output: ReferenceError: y is not defined
}
```

* Hoisting: Variables declared with var are hoisted to the top of their scope, which means that you can access them before they are declared. On the other hand, variables declared with let are not hoisted, so you cannot access them before they are declared.
```js
console.log(x); // Output: undefined
var x = 5;

console.log(y); // Output: ReferenceError: y is not defined
let y = 5;
```
* Redeclaration: Variables declared with var can be redeclared within the same scope, whereas variables declared with let cannot be redeclared within the same scope.

```js
var x = 5;
var x = 10; // This is valid

let y = 5;
let y = 10; // This will throw an error
```
In general, it is recommended to use let instead of var when declaring variables in JavaScript. let provides more intuitive and predictable behavior with regards to scope and hoisting.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***List ES6 features***

Some of the most popular ES6 features are:

* let and const: These are new ways of declaring variables, which provide block-scoping and prevent variables from being redeclared or reassigned.

* Arrow Functions: Arrow functions are a shorthand for defining anonymous functions, and they automatically bind to the context of their parent scope.

* Template Literals: These are a new way of defining strings that allows for embedding expressions and creating multi-line strings.

* Destructuring: This feature allows you to extract values from arrays and objects and assign them to new variables.

* Spread and Rest Operators: The spread operator allows you to spread an array or an object into multiple variables, and the rest operator allows you to gather multiple variables into an array or an object.

* Classes: ES6 introduces a new syntax for defining classes, which makes it easier to create objects and organize your code.

* Modules: ES6 introduces a new way of organizing and importing code with the use of modules.

* Promises: Promises are a new way of handling asynchronous operations, they provide a way to register callbacks for when an operation completes or fails.

* Generators: These are a new type of function that allows you to pause and resume code execution.

* Iterators: Iterators allow you to define a specific way of iterating over an object's properties.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>


## Q. ***Explain Spread and Rest Operators***
The spread operator (...) and the rest operator (...) are used to manipulate arrays and objects.

Spread Operator: The spread operator allows you to spread the elements of an array or an object into multiple variables. For example:
```js
let numbers = [1, 2, 3];
let [a, b, c] = [...numbers];
console.log(a); // Output: 1
console.log(b); // Output: 2
console.log(c); // Output: 3
```
In this example, we are spreading the elements of the numbers array into separate variables a, b, and c.

It also can be used to merge arrays together:

Copy code
let array1 = [1, 2, 3];
let array2 = [4, 5, 6];
let array3 = [...array1, ...array2];
console.log(array3); // Output: [1, 2, 3, 4, 5, 6]
Rest Operator: The rest operator allows you to gather multiple variables into an array or an object. It is represented by three dots ... preceding the parameter name. For example:
```js
function add(...numbers) {
    let sum = 0;
    for (let number of numbers) {
        sum += number;
    }
    return sum;
}
console.log(add(1, 2, 3)); // Output: 6
console.log(add(5, 10, 20)); // Output: 35
```
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***What is Destructuring?***

destructuring is a feature that allows you to extract values from arrays and objects and assign them to new variables. It is a concise way of extracting and reassigning data in a single line of code.

There are two types of destructuring:

Array destructuring: This allows you to extract values from arrays and assign them to new variables. For example:
```js
let numbers = [1, 2, 3];
let [a, b, c] = numbers;
console.log(a); // Output: 1
console.log(b); // Output: 2
console.log(c); // Output: 3
```
In this example, we are destructuring the numbers array and assigning its elements to the variables a, b, and c.

Object destructuring: This allows you to extract values from objects and assign them to new variables. For example:
```js
let person = { name: "John", age: 30 };
let { name, age } = person;
console.log(name); // Output: "John"
console.log(age); // Output: 30
```
In this example, we are destructuring the person object and assigning its properties name and age to the variables name and age respectively.

You can also use destructuring to assign default values to variables, in case the value being destructured is undefined.

```js
let { name = 'Unknown', age = 0 } = {};
console.log(name); // Output: Unknown
console.log(age);  // Output: 0
```
Destructuring can also be used in function parameters to easily extract the properties of an object.

```js
function printPerson({name, age}){
  console.log(name, age);
}
printPerson({name: 'John', age: 30});
```
In this example, we are using destructuring to extract the properties of the passed object to function printPerson directly, instead of having to access them via the object.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***Different between promise and async await?***

A promise is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises provide a way to register callbacks for when an asynchronous operation completes or fails, and can simplify the management of asynchronous code.

Example:

```js
let promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Hello, World!');
  }, 1000);
});

promise.then((value) => {
  console.log(value);
});
```
Async/await is a more recent way of writing asynchronous code that builds on top of promises. It allows you to write asynchronous code that looks similar to synchronous code by using the async keyword and the await keyword.

Example:

```js
async function getData() {
  let response = await fetch('https://example.com/data');
  let data = await response.json();
  console.log(data);
}
```
The main difference between Promises and async/await is that Promises are a pattern for handling asynchronous code, while async/await is a language feature built on top of Promises that makes it easier to write asynchronous code in a more "synchronous-like" way.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***Explain "this" in JavaScript?***

The keyword "this" in JavaScript refers to the object that the current function is a method of. The value of "this" can change depending on the context in which the function is called.

Here are a few examples of how "this" can be used:

In a method of an object, "this" refers to the object that the method belongs to:
```js
let person = {
    name: 'John',
    sayName: function() {
        console.log(this.name);
    }
};

person.sayName(); // prints 'John'
```
In a function defined in the global scope, "this" refers to the global object (e.g. window in the browser):
```js
function printThis() {
    console.log(this);
}

printThis(); // prints the global object
```
In an event handler, "this" refers to the element that the event occurred on:
```js
<button id="myButton">Click me</button>

let button = document.getElementById("myButton");
button.addEventListener("click", function() {
    console.log(this);
});
```
It is important to remember that the value of "this" can be different depending on the context in which a function is called, and it can be changed using methods like call, apply, and bind.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***Explain `call`, `apply` and `bind` in JavaScript!***

call, apply, and bind are methods in JavaScript that allow you to change the value of the this keyword within a function.

* call method:
```js
let person1 = { name: "John" };
let person2 = { name: "Mary" };

function sayName() {
    console.log(this.name);
}

sayName.call(person1); // prints "John"
sayName.call(person2); // prints "Mary"
```
The call method allows you to invoke a function and set the this keyword to the first argument passed to the method. The remaining arguments will be passed to the function as arguments.

* apply method:
```js
let numbers = [1, 2, 3];

function sum() {
    return Array.prototype.reduce.call(arguments, (a, b) => a + b);
}

console.log(sum.apply(null, numbers)); // prints 6
```
The apply method is similar to call, but instead of passing the function arguments as separate values, you pass them as an array.

* bind method:
```js
let person = {
    name: "John",
    sayName: function() {
        console.log(this.name);
    }
};

let sayName = person.sayName.bind(person);

sayName(); // prints "John"
```
The bind method creates a new function with the this keyword set to the first argument passed to the method. The new function can be invoked later, and the value of this will remain the same even if the context changes.


<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>

## Q. ***Type of error in JavaScript?***

There are several types of errors that can occur in JavaScript, some of the most common include:

* SyntaxError: occur when the JavaScript code is not written in the correct syntax, for example, if you forget a semicolon or a closing bracket.

* ReferenceError: occur when a variable or function is used before it has been declared, or when an object property is accessed that does not exist.

* TypeError: occur when a value is used in a way that is not consistent with its type, for example, when a string is used where a number is expected.

* RangeError: occur when a number is used that is outside the range of valid values, for example, when a negative value is passed to the Math.sqrt() function.

* URIError: occur when a global method is used in an incorrect way, such as when a malformed URI is passed to the encodeURI() function.

* EvalError: occur when the eval() function is used in an incorrect way.

* Custom Error: JavaScript also allows developers to create their own custom error types by creating a new object that inherits from the Error object.

* Asynchronous errors: Some of the errors like network error, XHR error, or other errors which are occurred during asynchronous operation.

<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>
