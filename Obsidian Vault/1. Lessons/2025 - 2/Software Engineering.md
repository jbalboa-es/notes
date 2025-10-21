#university
#software
#programming_languages 
# Content table
>[[#HTML]]

> [[#CSS]]
 > 	- [[#CSS Flex-box]]
 > 	- [[#CSS GRID]]
 
> [[#JavaScript]]
 > 	- [[#First hour]]
  > 		- Start
  > 		- Variables
  > 		- Arithmetic operators
   > 		- Accept user input
  > 		- Type conversion
  > 		- Constants
 > 	- [[#Second hour]]
  > 		- Math Object
  > 		- Random Number Generator
  > 		- If statements
  > 		- Checked property
  > 		- Ternary operator
  > 		- Switches
  > 		- String methods
 > 	- [[#Third hour]]
  > 		- String slicing
  > 		- Method chaining
  > 		- Logical operators
  > 		- Strict equality
  > 		- While loops
  > 		- For loops
  > 		- Number guessing game
  > 		- Functions
 > 	- [[#Fourth hour]]
  > 		- Variable scope
  > 		- Temperature conversion program
  > 		- Arrays
  > 		- Spread operator
  > 		- Rest parameters
  > 		-  Dice Roller program
  > 		- Random password generator
 > 	- [[#Fifth hour]]
  > 		- Callbacks
  > 		- forEach()
  > 		- map()
  > 		- filter()
  > 		- reduce()
  > 		- Function expressions
  > 		- Arrow functions
 > 	- [[#Sixth hour]]
  > 		-  JavaScript Objects
  > 		- What is THIS
  > 		- Constructors
  > 		- Classes
  > 		- STATIC keyword
  > 		- Inheritance
  > 		- SUPER keyword
  > 		- Getters & Setters
 > 	- [[#Seventh hour]]
  > 		- Destructuring
  > 		- Nested objects
  > 		- Arrays of objects
  > 		- Sorting
  > 		- Shuffle an array
  > 		- Dates
  > 		- Clousures
  > 		- setTimeOut()
 > 	- [[#Eighth hour]]
  > 		- Digital Clock program
  > 		- Stopwatch program
  > 		- ES6 Modules
  > 		- Asynchronous code
  > 		- Error handling
  > 		- Calculator program
 > 	- [[#Ninth hour]]
  > 		- What is the DOM?
  > 		- Element selectors
  > 		- DOM navigation
  > 		- Add & change HTML
 > 	- [[#Tenth hour]]
  > 		- Mouse events
  > 		- Key events
  > 		- Hide/Show HTML
  > 		- NodeLists
  > 		- classList
  > 		- Rock Paper Scissors
 > 	- [[#Eleventh hour]]
  > 		- Image Slider
  > 		- Callback Hell?
  > 		- Promises
  > 		- Async/Await
  > 		- JSON files
 > 	- [[#Twelfth hour]]
  > 		-  Fetch data from an API
  > 		- Weather APP project

> [[#Django]]

 >[[#Git & GitHub]]
# HTML
```
<br>
	break line
<hr>
	horizontal rule
<a>
	target : _bank / _self
	href : "mailto:corre"
	// its possible to concatenate with other tag like img
<audio> / <video> : self-closed (also img)
	controls
	autoplay
	muted
	loop
text
	<b> : bold
	<i> : italic
	<big>
	<small>
	<sub>
	<sup>
	<ins>
	<del>
	<mark>
<dl>
	<dt>term</dt>
	<dd>definition</dd>
</dl>
// you can concatenate lists with lists
<tr> : table row
	<th> / <td> : head / data
</tr>

<span> : to mark a portion of text or document
<meta> : to tell the web browser what our page is about
	charset="UTF-8"
	name= description / keywords / author / 
	viewport content="width=device_width, initial-scale=1.0"
	http-equiv="refresh" content="30" // reload webpage after 30 seconds
<iframe> : embed content to another source
<button>
	onclick="jsFunction()"
// you can concatenate button with <a>
<input>
	type: reset / submit / tel / mail / radio
<form>
	action=""
	mehtod="POST" / "GET"

<select>
	<option>
	
```
# CSS
```
// in <head>
<link rel="stylesheet" href="style.css"

.class
#id
tag

font-
	family
	style
	size
	wight
text-
	decoration: color type (wavy / dotted) decoration (underline)
	shadow: x-axis y-axis spread color
		// x-axis: position, positive > to the rigth
		// y-axis: position, positive > to below
		// spread: extension of shadow, positive > expand
		// you can put other shadows, separated by comma
	align
border-
	style
	width
	color
	radius
background: linear-gradient(to position( left / top), color_1, color_2)
	-repeat
	-attachment
	-image: url(link)
	-position: center
	-size
float // positions an element to the left or rigth of a container
clear // to control the position of an element in relation to precedeing floated elements.
position:
	relative // to some point, e.g. box relative to its top-left corner
	absolute // it's ignoring, like it was etheral. it will search for any parents that are positioned non-statically, if it does not have a parent it will use the viewport.
	fixed //follows your scroll
	sticky // like fixed but only in the place that you specified, if you scroll and pass throught the limit position, its follows your scroll in the limit position. 

// to make a tag child of another, generate the tag into the other tag.

$ pseudo-clases
	a:
		link
		visited
	tag:
		hover // mouse is over to
		active // click
	li:
		nth-child(x)
			x: number / even / odd / equation (3n)
box-
	shadow: x-axis y-axis spread color
	
<html>
i: for icons
	// fontawesome.com > icons
	class:

$css
transform:
	translateX(positive>right)
	translateY(positive>down)
	translate(X, Y)
	rotateX(e.g 180deg)
	scaleX()
	scale(X, Y)
	swekX(45deg) // like italian text
	swek(X, Y)
	matrix(scaleX, skewy, swekX, scaleY, translateX, translate Y)

@keyframes animationName {
	from{start-properties} // e.g margin-left: 0%
	to{end-properties} //e.g. margin-left: 100%
}
	100%{property} // % of the animation's total duration: you can play with that



animation: animationName
	-play-state: running / paused
	-iteration-count: number / infinite
	-delay
	-timing-function:
		ease-in //accelerates
		ease-out // accelerates but then slowly decelerate
		linear
	-duration
animation: duration timing-function delay iteration-count play-state animationName
```
## CSS Flex-box
block take up the entire width of the screen, elements being forced to the next line.

- display: flex;
- justify-content: along the main axis
	- flex-start
	- flex-end
	- center
	- space-between: espacio entre a ambos lados, sin los de los bordes 
	- space-around: con los de los bordes
	- space-evenly: mismo espacio entre todos
- min-heigth:
- align-items: to control the alignment along the cross axis of every flexbox line
	- flex-start
	- flex_end
	- center
- flex-direction: to control the direction of the main axis
	- row: left to right *default*
	- row-reverse
	- column: from top to bot
- gap: space **between**n (column and row)
- flex-wrap: to don't modify the items when their are enough on the width screen per line, instead, move this items to the next line. Create a different flex layout
	- wrap
	- nowrap
- align-content: to align along the one cross axis of the div
	- space-around *default*
- column-gap (space between each column)
- row-gap
- flex-shrink (become or make smaller in size or amount)
	- 0 to don't resize and produce overflow
	- 1 *default*
- flex-grow: (enables the elements to grow along the main axis)
	- 0 *default* (don't grow)
	- 1 to fill out the empty space
	- 5 (grow five times faster than 1)
- max-width
- min-width
- max-heigth
- min-heigth 
@media(max-width: 575px){
	body{
	flex-wrap: wrap;
	}
}
- align-self (align items but you use it on the flex item) 
- *don't exist justify-self*

## CSS GRID

```CSS
body{
	display:grid;
	grid-template-columns
	grid-template-areas:
	"navbar navbar"
	"sidebar main"
	"sidebar footer";
}
nav{
	grid-area: navbar;
}
aside {
	gride-area: sidebar;
}
main{
...
}

@media(max-width: 800px){
	body{
		grid-template-columns: 1fr;
	}
	aside{
		position: fixed;
		width:300px;
		display:none;
	}
	.show{
		display: block;
	}
}

/* En JS
function toggleSidebar(){
	sidebar.classList.toggle('show')
}
*/
```

# JavaScript

## First hour

- Start
```JS
//we must close the sentence with ;
'option_1';
"option_2";
`option_3`; //we prefer that

console.log(`some_output`);
window.alert(`some_alert`);
document.getElementById("some_id").textContent = `some_content`;
//comment in a line
/*
	comment
	in
	multiple
	lines
*/
```
-  Variables
```JS
let var; //declaration
var = content; //assignament
let var = content; //also possible

//type of data (basic)
typeof(10)==number;
typeof("Hello")==string;
typeof(true || false)== boolean;

//to concatenate a var with some text:
`Some text concatenate with ${var}`; //we can use this in console.log or any other thing
//also it is possible to concatenate string with '+' operator
```
- Arithmetic operators
```JS
//-- OPERATORS --
/*
	+
	-
	*
	/
	**
	%: remainder
*/

//-- SOME UTILITIES -- 
/*
	we can do:
		var+=1; //works for any other operator
	or:
		var++;
*/

//-- ORDER TO SOLVE--
/*
	PAPOMUDAS, with % operator in the same level of multiplication and division
*/
```
- Accept user input
```JS
//--EASY WAY--
window.prompt("some_text_to_ask"); //store a string data

//--PROFESSIONAL WAY--
let username;

document.getElemenById("mySubmit").onclick =  function(){
	username=document.getElementById("MyText").value;
	document.getElementById("MyH1").textContent = `Hello ${username}`;
}
```
- Type Conversion
```JS
//--TO STRINGS--
/*
	works normally with the exception of no assignament variables,
	in that case, return undefined
*/

//--TO NUMBERS--
/*
	Return NaN (Not a Number) when you try to convert something that is
	not a number.
	When you put an empty string, convert that to a Zero.
	With not assignament variables, return NaN
*/

//--TO BOOLEAN--
/*
	
*/
```
- Constants
```JS
// variables that can't be changed
const NUMBER = 1;
const BOOL = true;
const string = "some_text";
```
- Excercise: Counter Program
## Second hour

- Math Object
```JS
// Provides a collection of properties and methods
Math.round()
	.floor 
	.ceil //techo
	.trunc
	.pow
	.sqrt
	.log
	.sin
	.cos
	.tan
	.abs
	.sign //1 if is a positive number, -1 if is negative and 0 if the number is 0
	.max//numbers as parameters separates with commas
	.min
```
-  Random number generator
```JS
let randomNum = Math.floor(Math.random() * max) + min;
//Math.random: Between 0 and 1
// * max : Between 0 and max
// + min : Between min and max
```
- If statements
```JS
if(conditionOne){
	//body1
}
else if(conditionTwo){
	//body2
}
else{
	//body3
}
```
- Checked property
```JS
/*
	Property that determines the checked state of an HTML checkbox or radio button element
*/

const myCheckBox = document.getElementById("myCheckBox");
if(myCheckBox.checked){
	//body
}
```
- Ternary operator
```JS
/*
	condition ? codeIfTrue : codeIfFalse;
*/

let message = age >= 18 ? "You're an adult" : "You're a minor";
```
- Switches
```JS
let day = 1;

swtich(day){
	case 1:
		console.log("It is Monday");
		break;
	case 2:
		...
	default:
		console.log(`${day} is not a day`); //`` : when you have to insert a variable
}

switch(true){
	case conditionOne:
		//body
		break;
	case conditionTwo:
		//body
		break;
	default:
		//body
		break;
}
```
- String methods
```JS
/*
	.charAt(index)
	.indexOf(char); first
	.lastIndexOf(char)
	.length
	.trim() //to short the whitespace before or after
	.toUpperCase()
	.toLowerCase()
	.repeat(n)
	.startsWith(char or string); returna boolean4
	.endsWith()
	.includes(char or string); if include the char or string
	.replaceAll(string to change, for change)
	.padStart(n, string); to pad until n positions with string
	.padEnd(n, string)
*/
```
## Third hour

- String slicing
```JS
string.slice(start, end); // end - 1
string.slice(start);      // from start until the end of the string
string.slice(-2);         // last two chars
```
-  Method chaining
```JS
username = username.trim(); // to remove any white space before or after

// METHOD CHAINING
username = username.trim().charAt(0).toUpperCase() + username.trim().slice(1).toLowerCase();
```
- Logical operators
```JS
// AND: &&
// OR:  ||
// NOT: !
```
-  Strict equality
```JS
// = assignament operator
// == comparision operator
// === strict equality operator(compare values & datatype are equal)
// != inequality operator
// !== strict inequality operator
```
-  While loops
```JS
//while
while(c){
	body
}
//do-while
do{
	body
}while(c);
```
- For loops
```JS
for(let i = 0; i<n; i++){
	body
	continue; // to skip the current iteration
	break;    // to break out of the loop entirely
}
```
- Number guessing game
```JS
//utils
isNaN(v); // to check if a variable v is not a Number
```
- Functions
```JS
function id(var){
	body
	return result; // also tou can ommite that if is necessary
}
```
## Fourth hour

- Variable scope
 If you have two variables with the same name, but they're in different scopes, JavaScript will use the local version first.
- Temperature conversion program
cursor: pointer;  in CSS
- Arrays
```JS
let array = [element0, element1, element2];
array[i];                                   // elementi or undefined
array.push(element4)
array.pop();
array.unshift(elment0);                     // to add at the beggining
array.shift();                              // to pop at the beggining
array.length;
array.indexOf(element);

for(let element of array){
	element.function;
}

array.sort();                              // alphabetical order
array.sort().reverse();
```
- Spread operator
```JS
let string = "word";
let array = [elements];

let elements = [...elements];
let letters = [...string];                 // to unpacks elements
let letters = [...string].join("-");       // to put - between letters, the output is a string
```
- Rest parameters
Using spread operator as a parameter in a function definition
- Dice Roller program
- Random password generator
## Fifth hour

- Callbacks
```JS
// callback : a function that is passed as an argument to another function.
function f1(callback){
	body
	callback();
}

function f2(){
	body
}

f1(f2);                            // will do body of f1 then f2()

function f3(callback, p1, p2){
	body
	result = some(p1,p2)
	callback(result);
}

function f4(p0) {
	body
	return some;
}

f3(f4, p1, p2);                    // will do body of f3 then f4
```
- forEach()
to iterate over an array and apply a specified callback to each element
```JS
// string is like an array of Char

// -- FIRST WAY --
let array = [elemts];

array.forEach(f1);

function f1(element){
	// do something with element
}

// -- SECOND WAY --

array.forEach(f2);

function f2(element, index, array){
	array[index] = element*2; //example
}

```
- map()
accepts a callback and applies that function to each element of an array, then return a new array
```JS
const array;
array.map(callback);
```
- filter()
creates a new array by filtering out elements
```JS
let numbers;
let evenNums = numbers.filter(isEven) // an array with elements of numbers that return True on isEven function

function isEven(element){
	return element % 2 === 0;
}
```
- reduce()
reduce the elements of an array to a single value
```JS
const numbers;
const total = numbers.reduce(sum);

function sum(accumulator,element){
	return accumulator + element
}

// accumulator for i-th element going to be the return of sum for i-1th element 

// .toFixed(2) to return a double with 2 decimals
```
- Function expressions
a way to define functions as values or variables.
```JS
// replace callbacks by the all definition function

const hello = function(){
	console.log("Hello");
}

f1(function f2(){
	fo2.body;
}, p2);
```
- Arrow functions
a concise way to write function expressions. Good for simple function that you use **only once**.
```JS
// syntax: (parameters) => some code

const hello = () => console.log("Hello");
hello();

const hello = (name, age) => {console.log(`Hello ${name}`)
							  console.log(`You are ${age} years old`)};
hello("name", age);

const squares = numbers.map((element) => Math.pow(element, 2))
console.log(squares);
```
## Sixth hour

- JavaScript Objects
a collection of related properties and/or methods
```JS
object = {
	key1: value,
	key2: function, // also arrow function
}
object.key;
object.key2();
```
- What is THIS
reference to the object where THIS is used. The object depends on the immediate context
```JS
object = {
	key: value,
	key_function: function(){console.log(`Hi ${this.name}`)} // can't use arrow function I guess
}
```
- Constructors
```JS
function Constructor(p1, p2, p3){
	this.p1 = p1,
	this.p2 = p2,
	this.p3 = p3
}

const object = new Constructor(v1, v2, v3);
```
- Classes
```JS
class Object{
	constructor(p1, p2){
		this.p1 = p1;
		this.p2 = p2;
	}
	
	function(){
		// doSomething;
	}
}

const object = new Object(v1, v2);
```
- STATIC keyword
keyword that defines properties or methods that belong to a class itself rather than the objects created.
- Inheritance
```JS
class Parent{
	variable = value;
	
	method(){
		doSomething;
	}
}

class Child extends Parent{
	another_variable = value;
	
	another_method(){
		doSomething;
	}
}

const child = new Child();
child.variable;
child.method;
child.anothcer_method;      // its possible, due to inheritance
```
- SUPER keyword
`this` : this object
`super` : the parent

```JS
class Parent{

	constructor(){
	}
}

class Child extends Parent{
	constructor(p1, p2){
		super(); //necessary
		this.p1 = p1;
		this.p2 = p2;
	}
}


class Parent{

	constructor(p1){
		this.p1 = p1;
	}
	
	method(p){
		doSomethingWithP;
	}
}

class Child extends Parent{
	constructor(p1, p2){
		super(p1); //necessary
		this.p2 = p2;
	}
	
	child_method(){
		doSomethingUnique;
		super.method(this.p2);
	}
}
```
- Getters & Setters
```JS
class Class{
	constructor(p1, p2){
		this.p1 = p1;
		this.p2 = p2;
	}
	
	set p1(newP1){
		if(true){
			this._p1 = newP1;
		}
		else {
			console.error("error");
		}
	}
	
	get p1(){
		return this._p1;
	}
}
```
## Seventh hour

- Destructuring
```JS
// SWAP THE VALUE OF TWO VARIABLES
[a, b] = [b, a]; // also possible with array elements

// ASSIGN ARRAY ELEMENTS TO VARIABLES
array = [e1, e2];
const [var1, var2] = array; // var1 = e1 ; var2 = e2 

// EXTRACT VALUE FROM OBJECTS (SAME AS ASSIGN ARRAY ELEMENTS TO VARIABLES)
const {v1, v2} = object;

	// APPLY IT TO FUNCTION PARAMETERS
	function display({p1, p2}){
		//doSomething
	}
	display(object);
```
- Nested objects
Objects inside of other Objects
```JS
// some considerations:
class Class {
	constructor(object){
		this.object = new Object(...object)
	}
}
```
- Arrays of objects
```JS
array = [{key: val},
		 {}];
array[0].key;

// forEach
array.forEach(obj => someAction(obj.key))
// also worth for map(), filter(), reduce()
```
- sort()
sort in lexicographic order.
lexicographic = (alphabet + numbers + symbols) as strings.
```JS
// for numbers:
let arrayOfNumbers = [];

arrayOfNumbers.sort((a,b) => a - b); // in ascending way
// b - a to order in a reverse way
```
- Shuffle an array
```JS
function shuffle(array){
	for(let i =  array.length - 1; i > 0; i--){
		const random= Math.floor(Math.random()* (i+1));
		[array[i], array[random]] = [array[random], array[i]];
	}
}
```
- Date objects
```JS

// Date(year, month, day, hour, minute, second, ms)
const date = new Date(); // my current time
const date = new Date(y, m, d, h, m, s, ms);
const date = new Date("2024-01-02T12:00:00Z"); // T for time and Z for UTC
const date =  new Date("yy-mm-dd")
// can compare with logical operators
new Date(0); // near to 31th december
new Date(170000000); // 17... ms

// getters 
.getFullYear(); // year
.getMonth();    // number of month, January: 0
.getDate();     // day of the month
.getHours();    // hour
.getMinutes();  // minutes
.getSeconds();  // seconds
.getDay();      // number of the day on the week, Sunday: 0

// also exists the setters

.setFullYear(n); // set the year in n



```
- Clousure
a function defined inside of another function
- setTimeout()
allows you to schedule the execution of a function afeter an amount of time (miliseconds)
```JS
// syntax: setTimeout(callback, delay);
const timeoutId = setTimeout(callback, delay);

clearTimeout(timeoutId); // to cancel the execution
```

## Eighth hour

- Digital Clock program
shows the current time
utilities:
	getHours().toString().padStart(2,0);
	padStart(targetLength, padString) :
		targetLength: the total length that you want the final string to have
		padString: The string used to pad, default is " "
- Stopwatch program
```JS
elapsedTime = currentTime -  startTime
let hours = Math.floor(elapsedTime / (1000 * 60 * 60));
// minutes = / (1000 * 60) % 60
// seconds = / 1000 % 60
// milliseconds = elapsedTime % 1000 / 10
```
- ES6 Modules
```JS
// HOW TO IMPORT
import {id_1, id_2} from 'relative/path';
```
- Asynchronous
synchronous :  executes line by line consecutively in a sequential manner
asynchronous : allows multiple operations to be performed concurrently without waiting

Utilities: I/O operations, network requests. fetching data
- Error handling
```JS
// try { } : ecloses de code that migth potentially cause an error
// catch { } : catch and handle any thrown Errors from try { }
// finally { } : (optional) always executes. Used mostly for clean up

try{
	// NETWORK ERRORS
	// PROMISE REJECTION
	// SECURITY ERRORS
	console.log(x);
}
catch(error){
	console.error(error); // highligth errors
}
finally {
	// CLOSE FILES
	// CLOSE CONNECTIONS
	// RELEASE RESOURCES
}


if(condition){
	throw new Error("someTextError");
}
```
- Calculator program

## Ninth hour

- What is the DOM?
Document Object Model: represents the page you see in the webbrowser and provides you with an API to interact with it.
```JS
console.log(document); // the html
console.dir(document); // all properties

document.title = "title";
document.body.style.backgroundColor = "black"; 
```
- Element selectors
```JS
.getElementById()        // element or NULL
.getElementsClassName()  // HTML collection
.getElementsByTagName()  // HTML collection
.querySelector()         // first element or NULL
.querySelectorAll()      // NodeList

const variable =  document.getElementsClassName("class");
variable[0].style.backgroundColor = "color";

Array.from(variable).forEach(element =>{
	someAction
});

Array.from(variable); // to convert to an Array the HTML collection

querySelector("tag");
querySelector(".class");
querySelector("#id");
```
- DOM navigation
process of navigating through the structure of an HTML document
```
.firstElementChild
.lastElementChild
.nextElementSibling        // next 
.previousElementSibling
.parentElement
.children                  // HTML collection
```
- Add & change HTML
```JS
// STEP 1. CREATE THE ELEMENT
const newElement = document.createElement("tag");
// or .class or #id  (i think so)

// STEP 2. ADD ATTRIBUTES/PROPERTIES
newElement.textContent = "text";
.id
.style.someAttributeOfStyle

// STEP 3. APPEND ELEMENT TO DOM

document.parent.append(newElement); // add as a last child of parent (parent examples: body, elementById, etc.)
document.parent.prepend(newElement); // add as a first child
document.grandparent.insertBefore(newElement, nextSibling);

// REMOVE HTML ELEMENT

document.parend.removeChild(newElement);
```

## Tenth hour

-  Mouse events
```JS
// eventListener : Listesn for specific events to create interactive web pages
// events : click, mouseover, mouseout
.addEventListener(event, callback);

function callback(event){
	event.target.style... // target : is what we clicked on
}

element.addEventListener("click", event => {
	event.target...
})
```
-  Key events
```JS
// events : keydown, keyup
event.key; // to access to the char
```
- Hide/Show HTML
```JS
// display don't reserve space
element.style.display = "none"; // to hide
element.style.display = "block"; // to show

// visibility reserve space
element.style.visibility = "hidden";
element.style.visibility = "visible";
```
- NodeLists
static collection of HTML element by (id, class, element). Can be created by usin querySelectorAll(). NodeList won't update to automatically reflect changes
```JS
// 1. can be created by using querySelectorAll()
// 2. don't has map, filter, reduce
// 3. won´t update to automatically reflect changes

// ADD HTML/CSS PROPERTIES

elements.forEach(element => {
	element.style...
})

// .addEventListener
// REMOVE AN ELEMENT


// 3.

let elements = document.querySelectorAll(".class");
// add an element
// then, you have to reassign the NodeList to update it (necessary NodeList has to be let and no const)
elements = document.querySelectorAll(".class");


```
- classList
Element property used to interact with an element's list of classes (CSS classes)
```JS
add("identifier_class") // add the class to the element
remove()
toggle()   // remove if present, add if not
replace(oldClass, newClass)
contains() // return true if contains else false
```
- Rock Paper Scissors
## Eleventh hour

- Image Slider
- Callback Hell?
```JS
// Old pattern to handle asynchronous functions
// Use Promises + async/await to avoid Callback Hell

function task1(callback){
	setTimeout(()=> {
		console.log("task1 completed");
		callback;
	}, 2000)
}

function task2(callback){
	setTimeout(()=> {
		console.log("task2 completed");
		callback;
	}, 1000)
}

function task3(callback){
	setTimeout(()=> {
		console.log("task3 completed");
		callback;
	}, 3000)
}

function task4(callback){
	setTimeout(()=> {
		console.log("task4 completed");
		callback;
	}, 1500)
}


task1(() => {
	task2(() => {
		task3(() => {
			task4(()=> console.log("All task completed")); 
		});
	});
})

// task1, then task2 then...
```
- Promises
an object that manages asynchronous operations
```JS
// "I promise to return a value"
// PENDING -> RESOLVED or REJECTED
// new Promise((resolve, reject) => {asynchronous code})


// change the callbackHell method to:
function task1(){

	return new Promise((resolve, rejected) => {
		setTimeout(()=>{
			const boolean = true;
			
			if(boolean){
				resolve(value);
			}
			else{
				rejected(value_error);
			}
		}, ms);
	});
}

// do the same with other tasks

task1().then(value => {console.log(value); return task2()})
	   .then(value => { // some code with value of task2() ; return task3() })
	   .catch(error => console.error(value));
	   
```
- Async/Await
```JS
// async : makes a function return promise
// await : makes an async function wait for a promise

// task1(), task2()... of Promises section

async function doTasks(){
	try{
		const task1Result = await task1();
		console.log(task1Result); // like value of resolve
		// ...
		
			console.log("task completed");
	}
	catch{
		console.error(error); // like value of rejected
	}
}
```
- JSON files
```JS
// JavaScript Object Notation
// used for exchanging data between a server and a web application
// JSON files {key:value} OR [value1, value2, value3]

// JSON.stringify() : converts a JS object to a JSON string
// JSON.parse() : JSON string to a JS object


const array = [value1, value2]

const jsonString = JSON.stringify(array);

console.log(jsonString);

// will print "[value, value2]"
// same with an Object

// JSON.stringify() converts the array or object to an a long string

// JSON.parse() do the reverse, but the strings must have the 

fetch("archivo.json")
	.then(responde => response.json()) //response.json return a promise
	.then(values => values.forEach(value => console.log(value.attribute)))
	.catch(error => console.error(error));
```
## Twelfth hour

- Fetch data from an API
fetch :  
	- function used for making HTTP requests to fetch resources.
	- (JSON style data, images, files)
	- used for interacting with APIs to retrieve and send data asynchronously over the web
```JS
// fetch( url, {options})
// options may be {method: "GET"}, {method: "POST"}, {method: "PUT"}, {method: "DELETE
// GET to get data
// POST to send
// PUT to replace
// DELETE to delete


fetch("url")
	.then(response => console.log(response)) // to see what it is 
	// then replace for response.json(), don't make a new line, replace the above one
	.then(response => response.json())
	.then(data => console.log(data)) // parse json part of url to an json object
	.catch(error => console.error(error));



fetch("url")
	.then(response => {
		if(!response.ok){
			throw new Error("Could not fetch resource"); // catched by catch
		}
			return response.json();
	})
	.catch(error => console.error(error));
	

// other way

async function fetchData(){

	try{
		const response =  await fetch("url");
		
		if(!response.ok){
			// ..
		}
			// ..
	}
	catch(error){
		// ..
	}
}

variable = document.getElementById("id").value.toLowerCase();
`part/of/url/${variable}`;
```
- Weather APP project
```JS

// also an event for addEventListener: "type_button"
// react to click on the button

```
# Django

## Installation & Setup
- Install Python
- Create an environment
- Activate environment
- pip install django
- django-admin to see all the commands
```python
"""
- Install Python
- Create an environment
- Activate environment
- pip install django
- django-admin : to see all the commands
- django-admin startproject **name_of_project**
- in the project:
	  python manage.py runserver
wsgi: stands for web server Gateway interface
urls: all the URL routing
settings: core project configuration
views: what happens when someone goes to a specific URL
models: to configurate the databases

"""
```

# Git & GitHub
