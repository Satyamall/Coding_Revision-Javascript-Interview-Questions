# Javascript Interview Questions

# What is hoisting?
=> JavaScript Hoisting refers to the process whereby the interpreter appears to move the declaration of functions, variables or classes to the top of their scope, prior to execution of the code.

Hoisting allows functions to be safely used in code before they are declared.

Variable and class declarations are also hoisted, so they too can be referenced before they are declared. Note that doing so can lead to unexpected errors, and is not generally recommended.

**Function hoisting:**
One of the advantages of hoisting is that it lets you use a function before you declare it in your code.
```js
catName("Tiger");

function catName(name) {
  console.log("My cat's name is " + name);
}
/*
The result of the code above is: "My cat's name is Tiger"
*/
```
Without hoisting you would have to write the same code like this:
```js
function catName(name) {
  console.log("My cat's name is " + name);
}

catName("Tiger");
/*
The result of the code above is the same: "My cat's name is Tiger"
*/
```
**Variable hoisting:**
Hoisting works with variables too, so you can use a variable in code before it is declared and/or initialized.

However JavaScript only hoists declarations, not initializations! This means that initialization doesn't happen until the associated line of code is executed, even if the variable was originally initialized then declared, or declared and initialized in the same line.

Until that point in the execution is reached the variable has its default initialization (undefined for a variable declared using var, otherwise uninitialized).

**var hoisting:**
Here we declare then initialize the value of a var after using it. The default initialization of the var is undefined.
```js
console.log(num); // Returns 'undefined' from hoisted var declaration (not 6)
var num; // Declaration
num = 6; // Initialization
console.log(num); // Returns 6 after the line with initialization is executed.
```
The same thing happens if we declare and initialize the variable in the same line.
```js
console.log(num); // Returns 'undefined' from hoisted var declaration (not 6)
var num = 6; // Initialization and declaration.
console.log(num); // Returns 6 after the line with initialization is executed.
```
If we forget the declaration altogether (and only initialize the value) the variable isn't hoisted. Trying to read the variable before it is initialized results in ReferenceError exception.
```js
console.log(num); // Throws ReferenceError exception - the interpreter doesn't know about `num`.
num = 6; // Initialization
```
Note however that initialization also causes declaration (if not already declared). The code snippet below will work, because even though it isn't hoisted, the variable is initialized and effectively declared before it is used.
```js
a = 'Cran'; // Initialize a
b = 'berry'; // Initialize b

console.log(a + "" + b); // 'Cranberry'
```

**let and const hoisting:**
Variables declared with let and const are also hoisted but, unlike var, are not initialized with a default value. An exception will be thrown if a variable declared with let or const is read before it is initialized.
```js
console.log(num); // Throws ReferenceError exception as the variable value is uninitialized
let num = 6; // Initialization
```
Note that it is the order in which code is executed that matters, not the order in which it is written in the source file. The code will succeed provided the line that initializes the variable is executed before any line that reads it.

**class hoisting:**
Classes defined using a class declaration are hoisted, which means that JavaScript has a reference to the class. However the class is not initialized by default, so any code that uses it before the line in which it is initialized is executed will throw a ReferenceError.

# What is scoping?
=> Scope in JavaScript refers to the current context of code, which determines the accessibility of variables to JavaScript. The two types of scope are local and global: Global variables are those declared outside of a block. Local variables are those declared inside of a block.

The current context of execution. The context in which values and expressions are "visible" or can be referenced. If a variable or other expression is not "in the current scope," then it is unavailable for use. Scopes can also be layered in a hierarchy, so that child scopes have access to parent scopes, but not vice versa.

A function serves as a closure in JavaScript, and thus creates a scope, so that (for example) a variable defined exclusively within the function cannot be accessed from outside the function or within other functions. For instance, the following is invalid:
```js
function exampleFunction() {
    var x = "declared inside function";  // x can only be used in exampleFunction
    console.log("Inside function");
    console.log(x);
}

console.log(x);  // Causes error
```
However, the following code is valid due to the variable being declared outside the function, making it global:
```js
var x = "declared outside function";

exampleFunction();

function exampleFunction() {
    console.log("Inside function");
    console.log(x);
}

console.log("Outside function");
console.log(x);
```

# How are var, let const different?
=> - var declarations are globally scoped or function scoped while let and const are block scoped. 
- var variables can be updated and re-declared within its scope; let variables can be updated but not re-declared; const variables can neither be updated nor re-declared. - - They are all hoisted to the top of their scope. But while var variables are initialized with undefined, let and const variables are not initialized.
- While var and let can be declared without being initialized, const must be initialized during declaration.

# What are the two main differences in arrow functions?
=> Arrow function — also called fat arrow function — is a new feature introduced in ES6 that is a more concise syntax for a writing function expression.

Following are the main differences:
- Syntax
- Arguments binding
- Use of this keyword
- Using a new keyword
- No duplicate named parameters

1. **Syntax:**
```js
// Regular Function Syntax ES5:
var add = function(x, y) {
  return x + y;
};
// Arrow function ES6
let add = (x, y) => { return x + y };
```
A developer can get the same result as regular functions by writing a few lines of code using arrow functions.

Curly brackets are not required if only one expression is present.
```js
let add = (x, y) => x + y;
```
If there’s only one argument, then the parentheses are not required either:
```js
let squareNum = x => x * x;
```

2. **Arguments binding:**
Arrow functions do not have arguments binding.

Regular Function
```js
// Object with Regular function.
let getData = {
// Regular function
    showArg:function(){
      console.log(arguments);
    }  
}
getData.showArg(1,2,3); // output {0:1,1:2,2:3}
```
Output:


Arrow Function:
```js
// Object with Arrow function.
let getData = {
// Arrow function
    showArg:()=>console.log(arguments)
}
getData.showArg(1,2,3); // Uncaught ReferenceError: arguments is not defined
```
Output:

3. **Use of this keyword:**
unlike Regular functions, arrow function does not have their own "this" keyword.

The value of this inside an arrow function remains the same throughout the lifecycle of the function and is always bound to the value of this in the closest non-arrow parent function.
```js
let name ={
  fullName:'Satya Prakash Mall',
  printInRegular: function(){
    console.log(`My Name is ${this.fullName}`);
  },
  printInArrow:()=>console.log(`My Name is ${this.fullName}`)
}

name.printInRegular();
name.printInArrow();
```
Output:

name.printInRegular();
name.printInArrow();

My name is Satya Prakash Mall
My name is undefined

4. **Using a new keyword:**
Regular functions created using function declarations or expressions are constructible and callable. Regular functions are constructible; they can be called using the new keyword.

However, the arrow functions are only callable and not constructible, i.e., arrow functions can never be used as constructor functions.

Regular function:
```js
let add = function(x,y){
    console.log(x+y);
}

new add(2,3)

output: 
5
```
Arrow function:
```js
let add = (x, y) => console.log(x + y);
new add(2,3);
```

5. **No duplicate named parameters:**
Arrow functions can never have duplicate named parameters, whether in strict or non-strict mode.

However, We can use duplicate named parameters for regular function in non-strict mode.

# Does Call apply bind work for arrow functions?
=> An arrow function expression is a compact alternative to a traditional function expression, but is limited and can't be used in all situations.

There are differences between arrow functions and traditional functions, as well as some limitations:

- Arrow functions don't have their own bindings to this or super, and should not be used as methods.
- Arrow functions don't have access to the new.target keyword.
- Arrow functions aren't suitable for call, apply and bind methods, which generally rely on establishing a scope.
- Arrow functions cannot be used as constructors.
- Arrow functions cannot use yield, within its body.

# What does call apply bind do?
=> The call, bind and apply methods can be used to set the this keyword independent of how a function is called. The bind method creates a copy of the function and sets the this keyword, while the call and apply methods sets the this keyword and calls the function immediately.

**bind():**
The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
```js
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// expected output: undefined

const boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42
```
**apply():**
The apply() method calls a function with a given this value, and arguments provided as an array (or an array-like object).
```js
const numbers = [5, 6, 2, 3, 7];

const max = Math.max.apply(null, numbers);

console.log(max);
// expected output: 7

const min = Math.min.apply(null, numbers);

console.log(min);
// expected output: 2

const array = ['a', 'b'];
const elements = [0, 1, 2];
array.push.apply(array, elements);
console.info(array); // ["a", "b", 0, 1, 2]
```
**call():**
The call() method calls a function with a given this value and arguments provided individually.
```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

console.log(new Food('cheese', 5).name);
// expected output: "cheese"
```

# What are closures?
=> A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

Lexical Scoping
```js
function init() {
  var name = 'Mozilla'; // name is a local variable created by init
  function displayName() { // displayName() is the inner function, a closure
    alert(name); // use variable declared in the parent function
  }
  displayName();
}
init();
```
Run the code using this JSFiddle link and notice that the alert() statement within the displayName() function successfully displays the value of the name variable, which is declared in its parent function. This is an example of lexical scoping, which describes how a parser resolves variable names when functions are nested. The word lexical refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. Nested functions have access to variables declared in their outer scope.

Closure
```js
function makeFunc() {
  var name = 'Mozilla';
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```
Running this code has exactly the same effect as the previous example of the init() function above. What's different (and interesting) is that the displayName() inner function is returned from the outer function before being executed.

```js
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```
In this example, we have defined a function makeAdder(x), that takes a single argument x, and returns a new function. The function it returns takes a single argument y, and returns the sum of x and y.

In essence, makeAdder is a function factory. It creates functions that can add a specific value to their argument. In the above example, the function factory creates two new functions—one that adds five to its argument, and one that adds 10.

add5 and add10 are both closures. They share the same function body definition, but store different lexical environments. In add5's lexical environment, x is 5, while in the lexical environment for add10, x is 10.

# Write a program to debounce a search bar?
=>  In JavaScript, a debounce function makes sure that your code is only triggered once per user input. Search box suggestions, text-field auto-saves, and eliminating double-button clicks are all use cases for debounce.

**OR**

Debouncing in JavaScript is a practice used to improve browser performance. There might be some functionality in a web page which requires time-consuming computations. If such a method is invoked frequently, it might greatly affect the performance of the browser, as JavaScript is a single threaded language. Debouncing is a programming practice used to ensure that time-consuming tasks do not fire so often, that it stalls the performance of the web page. In other words, it limits the rate at which a function gets invoked.

```js
<html>
<body>
<button id="debounce">
	Debounce
</button>
<script>
var button = document.getElementById("debounce");
const debounce = (func, delay) => {
	let debounceTimer
	return function() {
		const context = this
		const args = arguments
			clearTimeout(debounceTimer)
				debounceTimer
			= setTimeout(() => func.apply(context, args), delay)
	}
}
button.addEventListener('click', debounce(function() {
		alert("Hello\nNo matter how many times you" +
			"click the debounce button, I get " +
			"executed once every 3 seconds!!")
						}, 3000));
</script>
</body>
</html>
```

# Write a program to throttle a search bar?
=> Throttling or sometimes is also called throttle function is a practice used in websites. Throttling is used to call a function after every millisecond or a particular interval of time only the first click is executed immediately.

Let’s see, what will happen if throttle function is not Present in the web page. Then the number of times a button is clicked the function will be called the same number of times. Consider the example.

```js
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
		content="width=device-width, initial-scale=1.0">
<title>
	JavaScript | With Throttling
</title>
</head>
<body>
<button id="throttle">Click Me</button>
<script>
	const btn=document.querySelector("#throttle");
	
	// Throttling Function
	const throttleFunction=(func, delay)=>{

	// Previously called time of the function
	let prev = 0;
	return (...args) => {
		// Current called time of the function
		let now = new Date().getTime();

		// Logging the difference between previously
		// called and current called timings
		console.log(now-prev, delay);
		
		// If difference is greater than delay call
		// the function again.
		if(now - prev> delay){
		prev = now;

		// "..." is the spread operator here
		// returning the function with the
		// array of arguments
		return func(...args);
		}
	}
	}
	btn.addEventListener("click", throttleFunction(()=>{
	console.log("button is clicked")
	}, 1500));
</script>
</body>
</html>
```

# create a custom method for an array called myMap, use prototype chain to achieve this
```js
const arr = [1,2,3]
arr.myMap(a=>a*5)
// [ 5, 10, 15 ]
it should work in this manner
```
=> Answer:  
```js
Array.prototype.myMap = function(callback) {
  let newArray = [];
  let x = this.length;
  for (let i = 0; i < x; i++) {
    let counter = callback(this[i]);
    newArray.push(counter);
  }
  return newArray;
};

const arr = [1,2,3]
arr.myMap(a=>a*5)
console.log(arr);
// [ 5, 10, 15 ]
```

# What is event bubbling?
=> Event bubbling is a method of event propagation in the HTML DOM API when an event is in an element inside another element, and both elements have registered a handle to that event. It is a process that starts with the element that triggered the event and then bubbles up to the containing elements in the hierarchy. In event bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements.

Syntax:
```js
addEventListener(type, listener, useCapture)
```
type: Use to refer to the type of event.
listener: Function we want to call when the event of the specified type occurs.
userCapture: Boolean value. Boolean value indicates event phase. By Default useCapture is false. It means it is in the bubbling phase.

```js
<!DOCTYPE html>
<html>

<head>
	<title>
		Bubbling Event in Javascript
	</title>
</head>

<body>

	<h2>Bubbling Event in Javascript</h2>

	<div id="parent">
	  <button>
		  <h2>Parent</h2>
	  </button>
	  <button id="child">
          <p>Child</p>
	  </button>
	</div>
    <br>
	<script>
		document.getElementById(
"child").addEventListener("click", function () {
			alert("You clicked the Child element!");
		}, false);

		document.getElementById(
"parent").addEventListener("click", function () {
			alert("You clicked the parent element!");
		}, false);
	</script>

</body>

</html>
```
From above example we understand that in bubbling the innermost element’s event is handled first and then the outer: the <p> element’s click event is handled first, then the <div> element’s click event.

# What is event loop?
=> JavaScript has a runtime model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks. This model is quite different from models in other languages like C and Java.

The event loop got its name because of how it's usually implemented, which usually resembles:
```js
while (queue.waitForMessage()) {
  queue.processNextMessage()
}
```
queue.waitForMessage() waits synchronously for a message to arrive (if one is not already available and waiting to be handled).

# Explain promises to a 5 year old, with simple examples
=> The Promise object supports two properties: state and result. While a Promise object is "pending" (working), the result is undefined. When a Promise object is "fulfilled", the result is a value. When a Promise object is "rejected", the result is an error object.
```js
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript Promise</h2>

<p id="demo"></p>

<script>
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some;
}

let myPromise = new Promise(function(myResolve, myReject) {
  let x = 0;

// some code (try to change x to 5)

  if (x == 0) {
    myResolve("OK");
  } else {
    myReject("Error");
  }
});

myPromise.then(
  function(value) {myDisplayer(value);},
  function(error) {myDisplayer(error);}
);
</script>

</body>
</html>
```

# Write a function called sleep that will return a promise, if you do not provide a number to the function, then it will return an error and goto the catch block
```js
sleep(500).then(res=> {
 console.log('slept for ${res} milli seconds})
})
.then(errr=>{
  console.log(err)
})
```
=>  Code:
```js
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// or
// const sleep = ms => new Promise(r => setTimeout(r, ms));

sleep(500).then(res=> {
 console.log('slept for ${res} milli seconds})
})
.then(errr=>{
  console.log(err)
})
```

# what does async await mean?
=> An async function is a function declared with the async keyword, and the await keyword is permitted within it. The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains.

Async functions may also be defined as expressions.
```js
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
  // expected output: "resolved"
}

asyncCall();
```
Async/Await is the extension of promises which we get as a support in the language. You can refer Promises in Javascript to know more about it. Async: It simply allows us to write promises based code as if it was synchronous and it checks that we are not breaking the execution thread.

# What does the this keyword mean?
=> In JavaScript, the this keyword refers to an object. Which object depends on how this is being invoked (used or called). 
The this keyword refers to different objects depending on how it is used: 
- In an object method, this refers to the object.
- Alone, this refers to the global object.
- In a function, this refers to the global object.
- In a function, in strict mode, this is undefined.
- In an event, this refers to the element that received the event.
- Methods like call(), apply(), and bind() can refer this to any object.

Example:
```js
const person = {
  firstName: "John",
  lastName : "Doe",
  id       : 5566,
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};
```

# What are classes? what are getters and setters?
=> Classes are in fact "special functions", and just as you can define function expressions and function declarations, the class syntax has two components: class expressions and class declarations.

Class declarations:
One way to define a class is using a class declaration. To declare a class, you use the class keyword with the name of the class ("Rectangle" here).
```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```
Class expressions:
A class expression is another way to define a class. Class expressions can be named or unnamed. The name given to a named class expression is local to the class's body. However, it can be accessed via the name property.
```js
// unnamed
let Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle"

// named
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle2"
```
Getters and setters are used to protect your data, particularly when creating classes. For each instance variable, a getter method returns its value while a setter method sets or updates its value. Given this, getters and setters are also known as accessors and mutators, respectively.

Getter Syntax:
```js
return_type get field_name{
    ...
}
```
Setter Syntax:
```js
set field_name{
    ...
}
```
Example:
```js
// Creating Class named Gfg
class Gfg {
// Creating a Field/Property
String geekName;

// Creating the getter method
// to get input from Field/Property
String get getName {
	return geekName;
}

// Creating the setter method
// to set the input in Field/Property
set setName(String name) {
	geekName = name;
}
}

void main() {
// Creating Instance of class
Gfg geek = Gfg();

// Calling the set_name method(setter method we created)
// To set the value in Property "geekName"
geek.setName = "GeeksForGeeks";

// Calling the get_name method(getter method we created)
// To get the value from Property "geekName"
print("Welcome to ${geek.getName}");
}
```

# How do you declare private and static variables in classes?
=>  Private class features:
Class fields are public by default, but private class members can be created by using a hash # prefix. The privacy encapsulation of these class features is enforced by JavaScript itself.

Syntax:
```js
class ClassWithPrivateField {
  #privateField;
}

class ClassWithPrivateMethod {
  #privateMethod() {
    return 'hello world';
  }
}

class ClassWithPrivateStaticField {
  static #PRIVATE_STATIC_FIELD;
}

class ClassWithPrivateStaticMethod {
  static #privateStaticMethod() {
    return 'hello world';
  }
}
```
Example:
```js
class ClassWithPrivateMethod {
  #privateMethod() {
    return 'hello world';
  }
  getPrivateMessage() {
    return this.#privateMethod();
  }
}
const instance = new ClassWithPrivateMethod();
console.log(instance.getPrivateMessage());
// hello world



class ClassWithPrivateAccessor {
  #message;
  get #decoratedMessage() {
    return `🎬${this.#message}🛑`;
  }
  set #decoratedMessage(msg) {
    this.#message = msg;
  }
  constructor() {
    this.#decoratedMessage = 'hello world';
    console.log(this.#decoratedMessage);
  }
}
new ClassWithPrivateAccessor();
// 🎬hello world🛑
```

**static:**
The static keyword defines a static method or property for a class, or a class static initialization block (see the link for more information about this usage). Neither static methods nor static properties can be called on instances of the class. Instead, they're called on the class itself.

Static methods are often utility functions, such as functions to create or clone objects, whereas static properties are useful for caches, fixed-configuration, or any other data you don't need to be replicated across instances.

Example:
```js
class ClassWithStaticMethod {
  static staticProperty = 'someValue';
  static staticMethod() {
    return 'static method has been called.';
  }
  static {
    console.log('Class static initialization block called');
  }
}

console.log(ClassWithStaticMethod.staticProperty);
// output: "someValue"
console.log(ClassWithStaticMethod.staticMethod());
// output: "static method has been called."
```

# Create a Calculator class, it should be able to add, reduce multiply and divide. it should have a value getter, and that should return final output. keep the history of changes made as well, and keep that private, and a user should be able to see previous changes made to the value.
=> 
```js
class Calculator {
  constructor(previousOperandTextElement, currentOperandTextElement) {
    this.previousOperandTextElement = previousOperandTextElement
    this.currentOperandTextElement = currentOperandTextElement
    this.clear()
  }
  clear() {
      this.currentOperand = ''
    this.previousOperand = ''
    this.operation = undefined
}

delete() {
    this.currentOperand = this.currentOperand.toString().slice(0, -1)
}

appendNumber(number) {
    if (number === '.' && this.currentOperand.includes('.')) return
    this.currentOperand = this.currentOperand.toString() + number.toString()
}

chooseOperation(operation) {
    if (this.currentOperand === '') return
    if (this.previousOperand !== '') {
      this.compute()
    }
    this.operation = operation
    this.previousOperand = this.currentOperand
    this.currentOperand = ''
}

compute() {
    let computation
    const prev = parseFloat(this.previousOperand)
    const current = parseFloat(this.currentOperand)
    if (isNaN(prev) || isNaN(current)) return
    switch (this.operation) {
      case '+':
        computation = prev + current
        break
      case '-':
        computation = prev - current
        break
      case '*':
        computation = prev * current
        break
      case '÷':
        computation = prev / current
        break
      default:
        return
    }
    this.currentOperand = computation
    this.operation = undefined
    this.previousOperand = ''
}

updateDisplay() {
    this.currentOperandTextElement.innerText =
      this.getDisplayNumber(this.currentOperand)
    if (this.operation != null) {
      this.previousOperandTextElement.innerText =
        `${this.getDisplayNumber(this.previousOperand)} ${this.operation}`
    } else {
      this.previousOperandTextElement.innerText = ''
    }
}
getDisplayNumber(number) {
   const stringNumber = number.toString()
    const integerDigits = parseFloat(stringNumber.split('.')[0])
    const decimalDigits = stringNumber.split('.')[1]
    let integerDisplay
    if (isNaN(integerDigits)) {
      integerDisplay = ''
    } else {
      integerDisplay = integerDigits.toLocaleString('en', { maximumFractionDigits: 0 })
    }
    if (decimalDigits != null) {
      return `${integerDisplay}.${decimalDigits}`
    } else {
      return integerDisplay
    }
}
}

const calculator = new Calculator(previousOperandTextElement, currentOperandTextElement)

```

# What is currying?
=> Currying is an advanced technique of working with functions. It’s used not only in JavaScript, but in other languages as well.

Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c).

Currying doesn’t call a function. It just transforms it.

Example:
```js
function curry(f) { // curry(f) does the currying transform
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}

// usage
function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

alert( curriedSum(1)(2) ); // 3
```

# Write a program to flatten an array
```js
// input: [ 1, [ 2, 3 ], [ 3 ], [ [ [ 5]],  6]  ]
// output => [ 1, 2, 3, 3, 5, 6 ]
```
=> 
1. Simple methods to obtain a flattened array in JavaScript
```js
a. Using concat() and apply()
input=[ 1, [ 2, 3 ], [ 3 ], [ [ [ 5]],  6]  ]
let flatArray = [].concat.apply([], input);
// output => [ 1, 2, 3, 3, 5, 6 ]

b. Using the spread operator
let flatArray = [].concat(...input);

c. Using the reduce method
let flatArray = input.reduce((acc, curVal) => {
    return acc.concat(curVal)
}, []);

```
2. Obtaining a flattened array by specifying the depth
```js
a. Using the flat() method
// The flat() method is used to create a new array with all sub-array elements concatenated into it recursively up to the specified depth. The depth parameter is optional and when no depth is specified, a depth of 1 is considered by default

input=[ 1, [ 2, 3 ], [ 3 ], [ [ [ 5]],  6]  ]
console.log(input.flat());
console.log(input.flat(4));
console.log(input.flat(4));
```
