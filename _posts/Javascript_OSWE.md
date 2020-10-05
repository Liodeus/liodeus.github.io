---
layout: post
title: Javascript personal course - OSWE
tags: [OSWE, Cheatsheet, Javascript]
description: "Javascript personal course - OSWE"
---

# Table of contents

- [JavaScript](#javascript)
  - [Course used](#course-used)
  - [Variables](#variables)
  - [Constants](#constants)
  - [Comments](#comments)
  - [Print variables](#print-variables)
  - [Determined variable type](#determined-variable-type)
  - [Object](#object)
  - [Class](#class)
  - [Tables](#tables)
  - [Set](#set)
  - [Map](#map)
  - [Conditions](#conditions)
  - [Loops](#loops)
  - [Functions](#functions)
  - [Method in a class](#method-in-a-class)

------

## JavaScript

### Course used

```
https://openclassrooms.com/fr/courses/6175841-apprenez-a-programmer-avec-javascript
```

------

### Variables

```
let test = 1;
```

------

### Constants

```
const hoursPerDAy = 24;
```

------

### Comments

```
# Single ligne
// This is a comment

# Multi lignes
/*
** This is a comment
** This is a comment
*/
```

------

### Print variables

```
alert(<VARIABLE>);

or 

console.log(<VARIABLE>);
```

------

### Determined variable type

```
let test = 42;
alert(typeof test); -> Output number
```

------

### Object

Object in JavaScript are written in JSON.

```
# Create
let Person = {
	Name: "Thibault",
	Pseudo: "Liodeus",
	Age: 24
}

# Access object data
let PersonName = Person.Name;
let PersonPseudo = Person.Pseudo;
let PersonAge = Person.Age;
```

------

### Class

```
# Create
class Book {
    constructor(title, author, pages) {
        this.title = title;
        this.author = author;
        this.pages = pages;
    }
}

# Instantiate a class
let myBook = new Book("Liodeus road to OSWE", "Liodeus", 250);
```

------

### Tables

```
# Create
let table = [
	"test",
	1,
	true
];

# Access data
let tableData2 = table[1];

# Add data at the end of a table
table.push("Liodeus");

# Add data at the start of a table
table.unshift("Liodeus");

# Size
table.length;

# Remove last element of a table
table.pop();
```

------

### Set

A set in JavaScript is the same as a set in Python.

```
# Create
let MySet = new Set();

# Add data
MySet.add(1);

# Has data
MySet.has(1);

# Size
MySet.size;

# Delete
MySet.delete(1)
```

------

### Map

A map in JavaScript is the same as a dict in Python.

```
# Create
let MyMap = new Map();

# Add data
MyMap.set(key, "Value");

# Get data
MyMap.get(key);

# Size
MyMap.size;

# Delete
MyMap.delete(key)
```

------

### Conditions

```
# if / else if / else
if () {
	console.log("Test");
} else if () {
	console.log("Test2");
} else {
	console.log("Default");
}

or 

# Switch
switch () {
	case 1:
		console.log("Test");
		break;
	case 2:
		console.log("Test2")
		break;
	default:
		console.log("Default")
}
```

------

### Loops

```
# For
for (let i = 0; i < 10; i++) {
    console.log(i);
}

# For in
const passengers = ["Will Alexander", "Sarah Kate", "Audrey Simon", "Tao Perkington"];
for (let i in passengers) {
    console.log("Embarquement du passager " + passengers[i]);
}

# For of
const passengers = ["Will Alexander", "Sarah Kate", "Audrey Simon", "Tao Perkington"];
for (let passenger of passengers) {
    console.log("Embarquement du passager " + passenger);
}

# While
let i = 10;
while (i != 0) {
	console.log(i);
	i--;
}
```

------

### Functions

```
function add(number1, number2) {
	return number1 + number2;
}

or

const add = (number1, number2) => {
	return number1 + number2;
}
```

------

### Method in a class

#### Instance method

```
class Person {
	constructor(name, pseudo, age) {
		this.name = name;
		this.pseudo = pseudo;
		this.age = age;
	}

	printAge() {
		console.log(this.name + " is " + this.age + " years old.")
	}

	birthday() {
		console.log("Happy birthday " + this.name + " !");
		this.age++;
	}
}

let test = new Person("Thibault", "Liodeus", 24);
test.printAge(); // Thibault is 24 years old.
test.birthday(); // Happy birthay Thibault !
test.printAge(); // Thibault is 25 years old.
```

#### Static method

The static keyword defines a static method for a class. Static methods aren't  called on instances of the class. Instead, they're called on the class  itself.

```
class Point {
	constructor(x, y) {
		this.x = x;
		this.y = y;
  	}

	static distance(a, b) {
		const dx = a.x - b.x;
		const dy = a.y - b.y;
		return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
p1.distance; // undefined
p2.distance; // undefined

console.log(Point.distance(p1, p2)); // 7.0710678118654755
```

