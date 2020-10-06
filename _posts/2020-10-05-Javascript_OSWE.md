---
layout: post
title: Javascript personal course - OSWE
tags: [OSWE, Cheatsheet, Javascript]
description: "Javascript personal course - OSWE"
---

# Table of contents

- [Table of contents](#table-of-contents)
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
      - [Instance method](#instance-method)
      - [Static method](#static-method)
  - [DOM](#dom)
    - [Course used](#course-used)
    - [Get elements](#get-elements)
    - [Modify elements](#modify-elements)
      - [Modify the content of an element](#modify-the-content-of-an-element)
      - [Modify classes](#modify-classes)
      - [Change the style of an element](#change-the-style-of-an-element)
      - [Modify attributes](#modify-attributes)
      - [Modify elements](#modify-elements)
        - [Create new elements](#create-new-elements)
        - [Add child](#add-child)
        - [Remove and replace elements](#remove-and-replace-elements)
    - [Events](#events)
      - [onclick](#onclick)
      - [preventDefault](#preventdefault)
      - [mouseMove](#mousemove)
      - [input](#input)

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

------

## DOM

### Course used

```
https://openclassrooms.com/fr/courses/5543061-ecrivez-du-javascript-pour-le-web
```

------

### Get elements

getElementById()

```
<p id="test">Test</p>
const test = document.getElementById('test');
```

getElementsByClassName()

```
<div>
    <div class="content">Contenu 1</div>
    <div class="content">Contenu 2</div>
</div>
const contents = document.getElementsByClassName('content');
```

getElementsByTagName()

```
<div>
    <article>Contenu 1</article>
    <article>Contenu 2</article>
    <article>Contenu 3</article>
</div>
const articles = document.getElementsByTagName('article');
const thirdArticle = articles[2];
```

Parent / child

```
<div id="parent">
    <div id="previous">Précédent</div>
    <div id="main">
        <p>Paragraphe 1</p>
        <p>Paragraphe 2</p>
    </div>
    <div id="next">Suivant</div>
</div>

const elt = document.getElementById('main');

const child = elt.children; // Return paragraphe 1/2 
const parent = elt.parentElement; // Return div (id=parent)
const sibling = elt.nextElementSibling; // Return div (id=next)
const previous_sibling = elt.previousElementSibling; // Return div (id=previous)
```

------

### Modify elements

#### Modify the content of an element

```
<p>Paragraphe 1</p>
<p>Paragraphe 2</p>

const test = document.getElementsByTagName("p")[0];
const test2 = document.getElementsByTagName("p")[1];

test.innerHTML = "<p>Exemple <i>Test</i></p>"; // Test will be in italic
test2.textContent = "<p>Exemple <i>Test</i></p>"; // Test will not be in italic
```

#### Modify classes

```
<div id="main"></div>

let elt = document.getElementById('main');

elt.classList.add("nouvelleClasse"); // Adds the newClass to the element
elt.classList.remove("nouvelleClasse"); // Deletes the new classClass that was just added
elt.classList.contains("nouvelleClasse"); // Will return false because it has just been deleted
elt.classList.replace("oldClass", "newClass"); // Will replace oldClass by newClass if oldClass was present on the element
```

#### Change the style of an element

```
elt.style.color = "#fff"; // Change the color of the text of the element to white
elt.style.backgroundColor = "#000"; // Change the background color of the element to black
elt.style.fontWeight = "bold"; // Bold the text of the element
```

#### Modify attributes

```
<div id="main"></div>

let elt = document.getElementById('main');

elt.setAttribute("type", "password"); // Change the input type to a password type
elt.setAttribute("name", "my-password"); // Change the name of the input to my-password
elt.getAttribute("name"); // Returns my-password
elt.removeAttribute("name") // Remove the name attribute of the input
```

#### Modify elements

##### Create new elements

```
const newElt = document.createElement("div");
```

##### Add child

```
<div id="main"></div>

const newElt = document.createElement("div");
let elt = document.getElementById("main");

elt.appendChild(newElt);
```

##### Remove and replace elements

```
<div id="main"></div>

const newElt = document.createElement("div");
let elt = document.getElementById("main");
elt.appendChild(newElt);

elt.removeChild(newElt); // Removes the newElt element from the elt element
elt.replaceChild(document.createElement("article"), newElt); // Replaces the newElt element by a new element of type article
```

------

### Events

```
addEventListener(<event>, <callback>);
```

#### onclick

```
const elt = document.getElementById('link');

elt.addEventListener('click', function() {
    elt.innerHTML = "Clicked !";
});
```

#### preventDefault

```
const elt = document.getElementById('link');

elt.addEventListener('click', function(event) {
    event.preventDefault(); // We use the preventDefault function of our event object to prevent the default behavior of this element when the mouse is clicked.
});
```

#### mouseMove

```
elt.addEventListener('mousemove', function(event) {
    const x = event.offsetX;
    const y = event.offsetY;
});
```

#### input 

Works for :

- \<input\>\</input\>
- \<select\>\</select\>
- \<textarea\>\</textarea\>

```
input.addEventListener('input', function(event) {
    output.innerHTML = event.target.value; 
});
```

------

