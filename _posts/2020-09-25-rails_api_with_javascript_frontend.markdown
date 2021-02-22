---
layout: post
title:      "JAVASCRIPT FRONTEND WITH RAILS API BACKEND"
date:       2020-09-25 22:40:14 -0400
permalink:  rails_api_with_javascript_frontend
---


![](https://images6.fanpop.com/image/photos/41400000/Playful-Kitry-kittens-41499027-361-640.jpg))


More writing to come...
Good deeds javascript rails app!

1) In terminal:
dahliabloomstone@MacBook-Pro ~ % mkdir gooddeeds
dahliabloomstone@MacBook-Pro ~ % cd gooddeeds
dahliabloomstone@MacBook-Pro gooddeeds % rails new gooddeeds-api --api --database=postgresql

Using Postgresql because heroku doesn’t work with sqlite3 

dahliabloomstone@MacBook-Pro gooddeeds % cd gooddeeds-api
dahliabloomstone@MacBook-Pro gooddeeds-api % 

Code . 
Opens vs code 

2) in VS code: open integrated terminal 
Uncomment rack cors gem 
Run bundle 
Go to config, initializers, cors.rb and uncomment out all of that 
Allow all origins ‘*’

Start with controllers: 
Rails g controller gooddeeds 

Define routes in config.rb routes.rb
Resources :gooddeeds 
Rails routes in terminal 

models:
Rails g model Gooddeed
 invoke  active_record
      create    db/migrate/20200922194617_create_gooddeeds.rb
      create    app/models/gooddeed.rb
      invoke    test_unit
      create      test/models/gooddeed_test.rb
      create      test/fixtures/gooddeeds.yml
Creates migration file 

Rails db:create  bc we are using Postgres 
Then rails db:migrate

Seed data, rails db:seed
gd1 = Gooddeed.create(body: "I donated", day: Date.today)
gd2 = Gooddeed.create(body: "I recycled", day: Date.today)
gd3 = Gooddeed.create(body: "I was nice", day: Date.today)



u1 = User.create(name: "Bobby", email: "bobby@gmail.com", password_confirmation: "password")
u2 = User.create(name: "Bobbi", email: "bobbi@gmail.com", password_confirmation: "password")
u3 = User.create(name: "Dahlia", email: "Dahlia@gmail.com", password_confirmation: "password")


If local host is not working:
		even easier: there is a folder called tmp, go inside pids/server.pid and delete the number inside the file
		lsof -i :3000
		kill -9 40781
		
		then do rails s, and the browser shows the json representation of our app&#x2028;
IN NEW VS FOLDER: 
mkdir js-frontend
cd js-frontend
Mkdir bin src styles 
Touch index.html creates index.html
		
		use frontend to talk to rails api to get data.&#x2028;&#x2028;going like ! Creates: 
		<!DOCTYPE html>
		<html lang="en">
		<head>
		    <meta charset="UTF-8">
		    <meta name="viewport" content="width=device-width, initial-scale=1.0">
		    <title>Document</title>
		</head>
		<body>
		    
		</body>
		</html>

		
		After you are done building our your index.html and seeing it in the browser by doing (open index.html) you will start working on your JAVASCRIPT! 
		
		Js is going to be used to make requests to the backend to get the current good deeds populated inside of the good deeds container. 
		
		cd into src directory 
		touch index.js
		it will be the main application file 
		mkdir adapters components 
		
		see notes on oo-js in the adapter &#x2028;
		open index.html and the console: 
		if you put in index.js console.log(welcome!). you will see that when you inspect/console 


	⁃	next, you want to take the array of objects in the console, and get them appended to the DOM and present them to the actual user. 
	⁃	build out additional methods in gooddeeds class &#x2028;
	⁃	
	⁃	 git push -f origin master&#x2028;


**Javascript basics:**
Data types: (primitives) 
Number, string, null, boolean, undefined, object, symbol

**Functions**are first class objects: functions can be: stored in variables, passed around as arguments, returned from functions, stored as values within structures. 

**Javascript Hoisting**: When JS starts, there are 2 phases: compilation and execution. Compilation: variable and function declarations are read into memory, and execution, when assignments and executions happen. 

Has function and variable declarations get raised to the top of the current scope. 

What is **Scope**? 
The context where something is available. Global, function, or block scope. Global scope = variable available everywhere. 

**this** 
contextual reference
current object where we are running code
shows a list in the console of properties 
MDN: A property of an execution context (global, function or eval) that, in non–strict mode, is always a reference to an object and in strict mode can be any value

Inside a function, this is the object that represents the functions execution context. The execution context is associated with the javascript object, can be accesed by keyword this. 

**Target event property**
The target event property returns the element that triggered the event.
The target property of the Event interface is a reference to the object onto which the event was dispatched. 

**catch**
The catch statement lets you handle the error.


**const**
It defines a constant reference to a value.
You can change the properties of a constant object:
You can change the elements of a constant array:
Constants are block-scoped, much like variables defined using the let keyword. The value of a constant can't be changed through reassignment, and it can't be redeclared.

**Javascript event listening**
The first argument is the event name to listen for
The second argument is the callback function. It's work that will be executed when the node "hears" the event



JS will start locally, go up the scope chain. 


**Javascript Fundamentals:**

*variables:* We use variables to store data temporarily. We give them names to store them. From ES6, we use most often the let keyword to declare a variable. Variables cannot be reserved keywords like let. Variables should be meaningful. They cannot start with a number, either. We use camelcase. 

Example: let firstName = 'Dahlia';
console.log(firstName);

*Objects:* {} is an object literal. Objects are collections of key value pairs. We add key value pairs in the object, which we can call properties. We can access these properties via dot notation. Dom nodes are javascript objects that can be manipulated. 


*Arrays:* Store lists! Each element has an index. 

*data structures:* An array is a data structure used to represent a list of items. You can perform a number of operations on arrays, like push, pop, shift, spread (...), and join. 

*functions:* In Javascript, functions are objects. functions are first class data in Javascript. Think of abstraction that holds a series of steps under a new name. They determine values. The argument is the actual value supplied by the parameter. Concatenating strings! 

syntax: 

function greet(name) {
console.log('Hello' + name);
}

greet('Dahlia'); 
greet('Alice'); 


*hoisting:* Hoisting is how variable and function declarations get raised to the top of the current scope. You declare the variable within the function. 

*scope:* think of variables being accessible! parameters in functions are locally scoped variables. Scope is where something is available. There is global, function, and block scope. Like the name sounds, global scope variables are accessible everywhere. Lexical scoping allows for a variable to be accessible even when defined inside another function. 

*context:*  Execution context is how a JS function runs. It can be acceessed by keyword this.

*this:*  Special keyword! *this* is the object that represents the functions execution context and returns current execution context. It is used inside a function. It represents the object that is executing the current function. It always *returns a reference to the current object*. The value of this is determined by how the function is called. returns *window object* if it is a standalone object.

**Example 1:**

let contextExample = { 
name: "Dahlia"
warn: function() {
console.log(`${this.name} is great!`) }
}
contextExample.warn() ==> Dahlia is great!

warn gets contextExample as its context. 
this was set to contextExample. 
this.name = contextExample.name = "Dahlia"


**Example 2:**

const video = {
title: 'a', 
play() { 
console.log(this)
}
};
function Video(title) {
this.title = title;
console.log(this); 
}
const v = new Video('b');  // {}

==> Video {title: "b"} 
title: "b" 

**new** operator creates a new empty object and sets this in the constructor function to point to the empty object. by default it references the global object. but if you call this new operator, or constuctor functions, it will reference a new empty object. 


**Example 3:**
const video = {                 //video object 
title: 'a', 
tags: ['a', 'b', 'c'], 
 showTags() {               //method showTags 
   this.tags.forEach(function(tag) {     
	 
	 //for each method has two parameters including thisArg, will reference that object 
      
			console.log(this.title, tag);             //inside callback function 
     }, this); 
   }
}; 
video.showTags(); 
==> a a 
         a b 
				 a c
				 
				 //this references the current object this.title and this.tags 


*bind*  Bind is a method that returns a copy of the function but with the execution context set to the argument that is passed to bind. Bind a function to an object. It will return a new instance of the function it is binded to. **Set the value of THIS permanently.** Based on arg passed in bind method. 

**Example**: 

const person = {
     name: "Dahlia",
		 walk() {
		     console.log(this); 
		 }
}; 
person.walk();
const walk = person.walk.bind(person); 
walk(); 

//walk always attached to the person object. Person object on the console. 

==>  {name: "Dahlia", walk: f} 

*closures:* A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

*ES6 syntax:* camelcase. let, const. 

*let, const:* The value of a constant *const* cannot change. They are block scoped. You cannot reassign a constant. If you don't need to reassign, const should be your first choice. Otherwise, if you need to reassign a variable, use let. 
Variables declared with the*let* keyword are scoped to the block in which they are defined. 

*arrow functions:* =>
Arrow functions are cleaner syntax code. Like using return.
*Arrow functions and this:* they don't rebind the this keyword. It inherits this in the context in which the code is defined. 

**Example**
const square = function(number) {
   return number * number; 
	 }; 
	 
	* is the same as: *
	 
const square = number => number * number; 

console.log(square(5));  equals 25 in the console.

**Example: **

fetchAndLoadGooddeeds() {
    this.adapter.getGooddeeds() 
    .then( gooddeedsJSON => gooddeedsJSON.forEach( gooddeed => this.gooddeeds.push( new Gooddeed(gooddeed) )))
      .then( this.render.bind(this))
      .catch(error => console.log(error))
  }
	
	removeDeletedGooddeed(deleteResponse) {
    this.gooddeeds = this.gooddeeds.filter( gooddeed => gooddeed.id !== deleteResponse.gooddeedId )
    this.render()
  }
	
*filter*: filter method that takes an object and returns a true or false. iterates over an array, takes the gooddeed object and determines if the object should be returned from the filter method. It's saying filter gooddeeds. 

*Explain how Rails routes a request to a controller and method based on the URL and HTTP verb: *

The router is the doorman of your application. When an HTTP request arrives from the user’s browser, it needs to know which controller action (method) should be run. Should we display the “new user” webpage? Should we edit an existing user with whatever data got sent along?

The Router is basically just a matching service. It looks at the HTTP verb (GET, POST, PUT, DELETE) and the URL that is being requested and matches it with the appropriate controller action to run. It’s a pretty simple function but an essential one. If it can’t find a route that matches the request, your application will throw an error.


*Use render json: to render serialized JSON: * 
With json, think of sending a web request and returning json that can be shared by javascript. 

*Select, Create, and Modify DOM nodes: *
DOM modification is the key to creating “live” pages.

To create an element: 
let div = document.createElement('div');

To remove a node: there’s a method node.remove().

**Summary of Dom modification methods**

Methods to create new nodes:

document.createElement(tag) – creates an element with the given tag,
document.createTextNode(value) – creates a text node (rarely used),
elem.cloneNode(deep) – clones the element, if deep==true then with all descendants.
Insertion and removal:

node.append(...nodes or strings) – insert into node, at the end,
node.prepend(...nodes or strings) – insert into node, at the beginning,
node.before(...nodes or strings) –- insert right before node,
node.after(...nodes or strings) –- insert right after node,
node.replaceWith(...nodes or strings) –- replace node.
node.remove() –- remove the node.
Text strings are inserted “as text”.

There are also “old school” methods:

parent.appendChild(node)
parent.insertBefore(node, nextSibling)
parent.removeChild(node)
parent.replaceChild(newElem, node)
All these methods return node.

Given some HTML in html, elem.insertAdjacentHTML(where, html) inserts it depending on the value of where:

"beforebegin" – insert html right before elem,
"afterbegin" – insert html into elem, at the beginning,
"beforeend" – insert html into elem, at the end,
"afterend" – insert html right after elem.
Also there are similar methods, elem.insertAdjacentText and elem.insertAdjacentElement, that insert text strings and elements, but they are rarely used.

To append HTML to the page before it has finished loading:

document.write(html)
After the page is loaded such a call erases the document. Mostly seen in old scripts.


*Attach listeners to DOM nodes to respond to user interaction:* 
addEventListener() listens for an event like clicking. 

*Use preventDefault to control form submit behavior:*
This is an event method. 
The preventDefault() method cancels the event if it is cancelable, meaning that the default action that belongs to the event will not occur.

For example, this can be useful when:

Clicking on a "Submit" button, prevent it from submitting a form
Clicking on a link, prevent the link from following the URL.


*Use fetch with 'GET', 'POST', 'PATCH' & 'DELETE' HTTP methods:* 
fetch() is a function that retreives data. When you think of fetch, think of promise, AJAX, asynchronous Javascript, JSON, event loops. fetch uses an http get request to retrieve content specified by a url. json-server dependency. 

*Create a JavaScript object with ES6 class syntax:* 
Arrays are objects. You access a javascript object via dot notation. An object can be created via a key, value pair. 
Ex: 
const meals = { 
lunch: 'salad' };
let hungry = 'lunch';
meals[hungry];
==> salad 

*Instantiate JavaScript objects and call methods on them* 
Calling a javascript object is like running it. You can call a javascript object by using something like document.querySelector(), which returns an html element. 


*OOJS*: prototypal inheritance. constructor functions. 

*array.map*: 

gooddeedsHTML() {
    return this.gooddeeds.map( gooddeed => gooddeed.render() ).join('')
  }

This function transforms each element in the array. Takes each element and returns the new item.  

*Inheritance and constructors* 
constructor functions create objects.
extends
new 

*Modularity or modules* each file is a module. 
Modularizing an application is moving each class into a seperate file. 
The objects we define in a module are private by default. 
**import and export**

**Javascript promises**
a promise represents a value that is unknown now, but may be known in the future. It manages a single async value that can be handled in the future. On the left we are making promises, on the right we are using them. It starts off in a pending state, and we have to define a callback function to resolve the promise. (executor)
consumer of the promise calls the then method. waiting for the aynch value to be fulfilled. 
fulfill the promise by calling resolve 
the catch method handles the error 
.then( ) 
.then( )
they can be chained together 














