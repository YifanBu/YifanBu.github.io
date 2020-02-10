---
title: "How JavaScript Works Under the Hood"
date: 2020-01-12
tags: [JavaScript]
header:
image:
excerpt: "Web Development, JavaScript"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# Foreword
No programming language is perfect. The weird parts of JS are it’s most powerful and beautiful parts. Big words just vocabularies, which are not as complicated as sound.

# Execution Contexts and Lexical Environments
*syntax parser*: a program that reads the code and determines what it does and if its grammar is valid.

*execution context*: a wrapper that helps manage the code which is running.

*global execution context*: the base execution context.

*lexical environment*: where something sits physically in the code you write.

*name-value pair*: a name which maps to a unique value.

*object*: a collection of name-value pairs.

JS engine creates two things in the global execution context: 

1. a global object: *window*, which is available to all the code running inside;
2. a special variable called *‘this’*, which refers to the window object.

*global*: not inside a function

When the variables and functions lexically not sitting inside a function, they are just sitting right there on the global object.

*Hoisting*: before your code being executed line by line, the JS engine has already set aside memory space for the **variables** and **functions** that you have created in your code. So those functions and those variables exist in memory. All variables in JS are initially set to a special value called *‘undefined’*, while functions are sitting in memory in their entirety.

*undefined* is a placeholder(don’t know the value yet).It is a special value that JS has within internally that means the variable hasn’t been set.

*scope*: where I can access a variable in my code.

*chain*: those links of outer environment references.

*let*: allows the JS engine to use what’s called block scoping, you are not allowed to use the variable until the line of code runs during the execution phase that actually declare the variable.

*Event Queue*: full of events, notifications of events that might be happening.	The event queue won't be processed until the execution stack is empty. When the execution stack is empty, the JS periodically looks at the event queue and deals with the events one by one. 

# Types and Operators
*Dynamic Typing*: JS engine figures out the type of data a variable holds while your code is still running.

*Primitive Type*: a type of data that represents a single value.

## 6 Primitive Types:  
*undefined , null*: both represents lack of existence, leave ‘undefined’ for the engine and you can use ‘null’ when you want to set a variable to nothing. 

*boolean*: true, false

*number*: Unlike other languages, JS only has one floating point number (there’s a;ways some decimals) type.

*string*: a sequence of characters.
symbol (used in ES6)

*operator*: a special function that is syntactically written differently. Generally, operators take two parameters and return one result. infix notation: a + b;

*precedence*: which operator function gets called first. Functions are called in order of precedence from **high** to **low**.

*associativity*: what order operator functions get called in: *left-to-right* or *right-to-left*.

For example: assignment ‘=’ is right associative.

*coercion*: converting a value from one type to another. This happens quite often in JS because JS is dynamically typed.

# Objects and Functions
*Object*: name-value pairs sitting in memory. They can contain other name-value pairs, which are other objects.

2 ways to access properties and methods of an object:
1. Member Access … . … left-to-right
2. Computed Member Access … […] left-to-right
(The preferred approach to find properties and methods is using the dot operator, which is clear and clean.)

*Object Literal*:

```javascript
var person = {};
```

When the JS engine sees "{}", it knows you are creating an object.

initialize the object by setting up the properties and methods all within the curly braces.
(the properties and methods are essentially treated as one line of code.)

## JSON:
JSON (JavaScript Object Notation): makes it easier to push data from the client to the server.

JSON is inspired by the JS literal syntax but they are different. JSON is technically a subset of the object literal syntax. In JSON, properties have to be wrapped in quotes.

```javascript
JSON.stringify();		// convert string to JSON
JSON.parse();		// convert JSON to string
```

## Functions are Objects:

*First Class Functions*: Everything you can do with other types (objects, strings, numbers, booleans), you can do with functions. You can assign a function to variables, pass it around as parameters to other functions, create it on the fly.

In JS, **function is a special type of object** because it has all the features of a normal object and has some other special properties like *NAME*(optional, can be anonymous) and *CODE*(Invocable) properties. You can attach properties and methods to a function.

```javascript
function greet() {
  console.log('hi');
}

greet.language = 'english';
```

The *NAME* property is 'greet'. The *CODE* property is 'console.log('hi');'.

## Function Statements & Function Expressions

*Expression*: A unit of code that results in a value. It does not have to save to a variable.

*Anonymous Function*: A function that doesn’t have a name in its *NAME* property. You can reference it with variable names that are pointing to the address where that object lives.

```javascript
greet();

//function statement
function greet() {
  console.log('hi');
}

//function expression
var anonymousGreet = function() {
  console.log('hi');
}

anonymousGreet();
```

## By Value & By Reference

*By Value*: setting one value to another **primitive** by copying the value into **two separate spots in memory**.

*By Reference*: all **objects** interact by reference, pointing to the **same spot in memory**.

## 'this'

When a function is invoked, a new execution context is created and put on the execution stack. 

Each execution context has a variable environment, where the variables created inside that function live.

Each execution context has a reference to its outer lexical environment, where it sits physically in the code, which tells it how to look down the scope chain for the variable or the function.  

Every time that an execution context is created, JS engine gives us a variable called *"this"* without having to create or declare it.

**"this" will be pointing at a different object, depending where the function is or how the function is invoked.**

```javascript
console.log(this); // "this" points to the global object: Window

function a() {
  console.log(this); 
  this.newvariable = 'hello';
}

var b = function() {
  console.log(this);
}

a(); // "this" still points to the global object: Window

console.log(newvariable); // a variable on the global object

b(); // "this" still points to the global object: Window
```

In the case where a function is actually a method attached to an object, *"this"* keyword becomes the object that method is sitting inside of, c.

```javascript
var c = {
  name: 'The c object',
  log: function() {
    console.log(this);
  }
}

c.log(); // Object {name: "The c object", log: function}
```

Using *"this"* to access other properties and methods on the same object:

```javascript
var c = {
  name: 'The c object',
  log: function() {
    this.name = 'Updated c object';
    console.log(this);
  }
}

c.log(); // Object {name: "Updated c object", log: function}
```

The 'bug':

```javascript
var c = {
  name: 'The c object',
  log: function() {
    this.name = 'Updated c object';
    console.log(this);

    var setname = function(newname) {
      this.name = newname;
    } // When the internal function's execution context is created, 'this' points to the global object
    setname('Updated again! The c object');
    console.log(this);
  }
}

c.log(); 
// Object {name: "Updated c object", log: function} 
// Object {name: "Updated c object", log: function}
```

A common fix pattern:

```javascript
var c = {
  name: 'The c object',
  log: function() {
    var self = this;

    self.name = 'Updated c object';
    console.log(self);

    var setname = function(newname) {
      self.name = newname;
    } // When the internal function's execution context is created, 'this' points to the global object
    setname('Updated again! The c object');
    console.log(self);
  }
}

c.log(); 
// Object {name: "Updated c object", log: function} 
// Object {name: "Updated again! The c object", log: function}
```

## Array: Collection of Anything

```javascript
var arr = [];

for (var i = 0; i < 3; i++) {
  
}
```

## Immediately Invoked Function Expressions

```javascript
var greeting = function(name) {
  console.log('Hello ' + name);
}('John');

var firstname = 'John';

(function(name) {

  var greeting = 'Inside IIFE: Hello';
  console.log(greeting + '' + name);

}(firstname)); // IIFE
```

'Hola' is stored in Global Execution Context while 'Hello' is in the Execution Context for the anonymous function:

```javascript
var greeting = 'Hola';

(function(name) {

  var greeting = 'Hello';
  console.log(greeting + '' + name);

}('John')); // IIFE
```

## Closures

Invoke a function that returns a function:

```javascript
function greet(whattosay) {
  
  return function(name) {
    console.log(whattosay + ' ' + name);
  }

}

greet('Hi')('Tony'); // Hi Tony

// it is possible because of the closures
var sayHi = greet('Hi');
sayHi('Tony'); // Hi Tony

```

What's happening: When the code starts, we have our Global Execution Context. When I hit this line sayHi = greet, it invokes the greet function. The new Execution Context for greet() is created, and the variable that is passed to it, whattosay, is sitting in its variable environment. greet() returns a new function object. So after that return, the greet execution context is popped off the stack. Every Execution Context has a space in memory, where the variables and functions created inside of it live. What happens to that memory space when the Execution Context goes away? **The memory space for that Execution Context is still there.** We are in the Global Execution Context again. And then we invoke the anonymous function that sayHi is pointing at. A new Execution Context is created with the name variable Tony in it. When I hit console.log(whattosay + ' ' + name), and the JS engine sees the whattosay variable, the engine goes up the scope chain. In other words, it goes to the next point outside where the function was created to look for that variable, since it could not find the variable inside of the function itself.

Even though the execution context of greet() was popped off the stack, the sayHi Execution Context still has a reference to the variables, to the memory space of its outer environment. In other words, even though the greet() function ended, any functions created inside of it, when they are called, will still have a reference to that greet() function's memory. **This phenomenon of closing in all the outer variables that it is supposed to have access to, is called a closure.** Closures are simply a feature of the JS, which is very important and powerful. It allows us to make some really interesting coding patterns.

A classic example of closure:

```javascript
function buildFunctions() {

  var arr = [];

  for (var i = 0; i < 3; i++) {
    arr.push(function() {
      console.log(i);
     });
  }

  return arr;

}

var fs = buildFunctions();

fs[0](); // 3
fs[1](); // 3
fs[2](); // 3
```

```javascript
function buildFunctions() {

  var arr = [];

  for (var i = 0; i < 3; i++) {
    arr.push(
      (function(j) {
        return function() {
          console.log(j);
        }
     }(i))
    )
  }

  return arr;

}

var fs = buildFunctions();

fs[0](); // 0
fs[1](); // 1
fs[2](); // 2
```

## Callbacks

```javascript
function sayHiLater() {
  var greeting = 'Hi!';

  setTimeout(function() {
    
    console.log(greeting);

  }, 3000);

}

sayHiLater();
```

*Callback Function*: A function that you give to another function, to be run when the other function is finished.

## call(), apply(), and bind()



# Object-Oriented JS and Prototypal Inheritance

## Classical vs Prototypal Inheritance

*Inheritance*: one object gets access to the properties and methods of another object.

Prototypal Inheritance is much simpler than the Classical one.

## Prototype

All objects including functions in JS have a *prototype property*, which is simply a reference to another object called *proto{}*.

The scope chain is about looking for where we have access to a variable. However, the **prototype chain** is about where we have access to a property or method amongst a sequence of objects that are connected via this prototype property. The JS engine will search the prototype chain for the properties and methods.

## Everything is an Object or a Primitive



## Reflection and Extend

*Reflection*: An object can look at itself, listening and changing its properties and methods.

# Building Objects

## Function Constructors and 'new'

```javascript
function Person() {

  console.log(this); // Person {}
  this.firstname = 'John';
  this.lastname = 'doe';
  console.log('This function is involed.');

}

var john = new Person();
console.log(john); // Person {firstname: "John", lastname: "Doe"}
```

*Function Constructor*: A normal function that is used to construct objects.

*'new'*: an empty object is created and the function is invoked. The 'this' variable is pointing to that empty object in memory. 'firstname' and 'lastname' was added to that object. That object is returned from the function automatically.

```javascript
function Person(firstname, lastname) {

  console.log(this); // Person {}
  this.firstname = firstname;
  this.lastname = lastname;
  console.log('This function is involed.');

}

var john = new Person('John', 'Doe');
console.log(john); // Person {firstname: "John", lastname: "Doe"}

var jane = new Person('Jane', 'Doe');
console.log(jane); // Person {firstname: "Jane", lastname: "Doe"}
```

## Function Constructors and '.prototype'

```javascript
function Person(firstname, lastname) {

  console.log(this); // Person {}
  this.firstname = firstname;
  this.lastname = lastname;
  console.log('This function is involed.');

}

Person.prototype.getFullName = function() {
  return this.firstname + ' ' + this.lastname;
}

var john = new Person('John', 'Doe');
console.log(john); // Person {firstname: "John", lastname: "Doe"}

var jane = new Person('Jane', 'Doe');
console.log(jane); // Person {firstname: "Jane", lastname: "Doe"}

Person.prototype.getFormalFullName = function() {
  return this.lastname + ',' + this.firstname;
}
```

**The prototype property on a function is not the prototype of the function.** It's **the prototype of any objects** created by the function constructor.

Good code: Properties are set up inside the function constructor because they are often different values. But methods are sitting on the prototype. Because functions are objects and they take up memory space if they are put in the function constructors. 

## 'new' and functions

## Built-in Function Constructors

## ES6 and Classes

In other languages, class is not an object. It is just a definition, like a template. In JavaScript, class is an object. We creates new objects from that object.

```javascript
class Person {

  constructor(firstname, lastname) {
    this.firstname = firstname;
    this.lastname = lastname;
  }

  greet() {
    return 'Hi ' + firstname;
  }

}

var john = new Person('John', 'Doe');
```

```javascript
class InformalPerson extends Person {

  constructor(firstname, lastname) {
    super(firstname, lastname);
  }

  greet() {
    return 'Yo ' + firstname;
  }

}

```

# Odds and Ends

# jQuery
