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

## Foreword
No programming language is perfect.
JS weird parts are often it’s most powerful and beautiful parts.
Big words just vocabularies, which are not as complicated as sound.

## Execution Contexts and Lexical Environments
*syntax parser*: a program that reads your code and determines what it does and if its grammar is valid.
*execution context*: a wrapper to help manage the code that is running.
*lexical environment*: where something sits physically in the code you write.

*name/value pair*: a name which maps to a unique value.
*object*: a collection of name/value pairs.

*global execution context*: the base execution context

the JS engine creates two things in the global execution context: 
1. a global object: window, which is available to all the code running inside the window
2. a special variable called ‘this’, which refers to the window object

*global*: not inside a function

the variables and functions when lexically not sitting inside a function, they are just sitting right there on the global object.

‘undefined’ is a placeholder: don’t know the value yet.

*Hoisting*: before your code being executed line by line, the JS engine has already set aside memory space for the variables and functions that you have created in your code.
So those functions and those variables exist in memory.
All variables in JS are initially set to a special value called ‘undefined’, while functions are sitting in memory in their entirety.

*‘undefined’*: a special value that JS has within internally that means the variable hasn’t been set.

*scope*: where I can access a variable in my code.
*chain*: those links of outer environment references.

*let*: allows the JS engine to use what’s called block scoping, you are not allowed to use the variable until the line of code runs during the execution phase that actually declare the variable.

*Event Queue*: full of events, notifications of events that might be happening.	
when the execution stack is empty, then JS periodically looks at the event queue and deals with the events one by one.
the event queue wont be processed until the execution stack is empty.

## Types and Operators
JS is Dynamic Typing: you don’t tell the engine what type of data a variable holds, it figures it out while your code is still running.

*Primitive Type*: a type of data that represents a single value.

### 6 Primitive Types in JS:  
undefined , null: both represents lack of existence, leave ‘undefined’ for the engine and you can use ‘null’ when you want to set a variable to nothing. 
boolean: true, false
number: Unlike other languages, JS only has one floating point number (there’s a;ways some decimals) type.
string: a sequence of characters.
symbol (used in ES6)

*operator*: a special function that is syntactically written differently.
Generally, operators take two parameters and return one result.
infix notation: a + b;
*precedence*: which operator function gets called first (functions are called in order of precedence from high to low).
*associativity*: what order operator functions get called in: left-to-right or right-to-left.

assignment ‘=’ is right associative.

*coercion*: converting a value from one type to another.
This happens quite often in JS because it is dynamically typed.

## Objects and Functions
Objects: name-value pairs sitting in memory. They can contain other name-value pairs, which are other objects.

2 ways to access properties and methods of an object:
1. Member Access … . … left-to-right
2. Computed Member Access … […] left-to-right
the preferred approach to find properties and methods is using the dot operator, which is clear and clean.

*Object Literal*:
var person = {};
When the JS engine sees the curly braces, it knows you are creating an object.
initialize the object by setting up the properties and mothods all within the curly braces.
the properties and mothods are essentially treated as one line of code.

### JSON:
JSON (JavaScript Object Notation): makes it easier to push data from the client to the server.
JSON is inspired by the JS literal syntax but they are different.
JSON is technically a subset of the object literal syntax.
In JSON, properties have to be wrapped in quotes.
JSON.stringify();		// convert string to JSON
JSON.parse();		// convert JSON to string

*First Class Functions*:
Everything you can do with other types (strings, numbers, booleans), you can do with functions.
You can assign them to variables, pass them around, create them on the fly.

In JS, function is a special type of object because it has all the features of a normal object and has some other special properties like NAME and CODE properties.

*anonymous function*: 
a function that doesn’t have a name in its name property.
you can reference it with variable names that are pointing to the address where that object lives.

## Object-Oriented JS and Prototypal Inheritance

## Building Objects

## Odds and Ends

## jQuery
