---
title: "Typescript Design Patterns"
date: 2019-12-02
tags: [TypeScript]
header:
image:
excerpt: "Web Development, TypeScript"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# Intro

## What is TypeScript

- Superset of JS developed by Microsoft
- Compile to plain JS
- Easily integrated into JS projects
- Designed for development of larger applications

## Benefits

TypeScript makes our code more strict.

- Static Type Checking
- Class Based Objects: Object Oriented & Encapsulation
- Modularity
- ES6 Features
- Syntax closer to Java and other high level languages

## Setup

index.js:

```html
<script src="filename.js"></script>
```

Watch mode:

`tsc filename.ts -w`


# Types

- String
- Number
- Boolean
- Array
- Any
- Tuple
- Enum
- Generics

```typescript
let myString: string;
let myNum: number;
let myBool: boolean;
let myVar: any;

let strArr: string[];
let numArr: number[];

// another way to define an array
let strArr: Array<string>;
let numArr: Array<number>;

let strNumTuple: [string, number]

myString = 'Hello World';
myNum = 22;
myBool = true;
myVar = ; // any type

strArr = ['Hello', 'World'];
numArr = [1, 2, 3];

strNumTuple = ['Hello', 4];
```

- Void
- Null

```typescript
let myVoid: void = null;
let myNull: null = undefined;
let myUndefined: undefined = null;
```

# Functions

TypeScript allows us to define the types of argument and output of a function.

```typescript
function getSum(num1: number, num2: number): number{
  return num1 + num2;
}

console.log(getSum(1, 4));
```

# Interfaces

```typescript
interface Todo{
  title: string;
  text: string;
}

function showTodo(todo: Todo){
  console.log(todo.title + ': ' + todo.text);
}

let myTodo = {title: 'Trash', text: 'Take out trash'}

showTodo(myTodo);
```

# Classes

```typescript
class User {
  name: string;
  email: string;
  age: number;

  constructor(name: string, email: string, age: number){
    this.name = name;
    this.email = email;
    this.age = age;

    console.log('User Created: ' + this.name);
  }
}

let john = new User('Ivan Bu', 'IvanBu@gmail.com', 26);
```



<!-- 
# Type System

# Annotations

## Type Annotations in Action

## Annotations With Functions and Objects

# Typed Arrays

# Tuples

# The All-Important Interface

# Functionality with Classes

# Design Patterns

## Building Design Patterns with Typescript

## More on Design Patterns

# Reusable Code
-->