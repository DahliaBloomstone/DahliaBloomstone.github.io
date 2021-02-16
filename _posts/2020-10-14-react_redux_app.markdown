---
layout: post
title:      "REACT REDUX APP - Character creator #"
date:       2020-10-14 19:25:03 -0400
permalink:  react_redux_app
---


![](https://media4.giphy.com/media/l0HlSJ8EcMwcxaomc/giphy.gif)


create github repository
npx create-react-app character-creator 
cd into the file 
npm start

API: generates.photos 
https://generated.photos/
create an account

https://generated.photos/account#apikey

API KEY:
https://api.generated.photos/api/v1/faces?api_key=YOUR_API_KEY

npm install axios 
add api key to app.js 

command shift c to go to console 
should see Object data to see api key data 

you can specify with indeces specific images 

Example: specifying female images 
&gender=female 
in the api key at the end write: 
    axios.get('https://api.generated.photos/api/v1/faces?api_key=-oSJ9MnkYiiimwgLEOefKQ&gener=female').then(res => {

then in the .then statement:
 .then(res => {
      console.log(res.data.faces[0].urls[4][512]);
--------------------------------------------------------------
			
**Redux notes **
State management library for javascript applications 
Storing application state in a central repository called a store
Store: It’s like a database for the frontend, Synchronizing the data across the UI. **

Redux: centralizes application and makes data flow predictable. 

Our entire application state is available on the client side inside a single javascript object. 

Functional programming introduces complexity. 

TO BEGIN IN VSCODE:
Npm i 
Npm start 

Things to learn in redux: 
Store, middleware, calling APIs, testing, integration with React 

Essential functional programming concepts:
Writing a bunch of small and reusable functions. 
There is functional, object oriented, procedural, and event driven.
It is about input and output. 

Javascript functions refresher: 
Can assign to a variable, pass as an argument, and return as other functions. 
Functions can be treated like any other variable! 

Example: 
Function sayHello() {
Return function() { <— anonymous function because it does not have a name 
	return “Hello World”;
	} 
}
let fn = sayHello(); 
let message = fn();

Higher order function: takes a function as an argument. 

Example: 
setTimeout(() => console.log(“Hello”), 1000); 


lodash.com —> popular utility library for javascript. 
 npm i lodash
import { compose, pipe } from 'lodash/fp'; 

Pure functions: 
No random values, no current data/time, no global state, no mutation of parameters  
The result does not change.
Immutability: Once we create an object, we cannot change it. 
Benefits: application predictability, faster change detection, and concurrency
Cons: memory overhead 

UPDATING OBJECTS:
Example: Object.assign 

const person = { name: “John” }; 
const updated = Object.assign ({ }, person, { name: “Bob”, age: 30 })    
console.log(updated)      

will copy all properties of person object into the empty object, and return new object 

Example: SPREAD OPERATOR
const person = { name: “John” }; 
const updated = { …person, name: “Bob” }; 
console.log(updated); 

More concise syntax! Both methods do a shallow copy. Nested objects can become verbose. 

Javascript is not a pure programming language. In javascript we can mutate objects. But we can still apply functional programming principles when writing javascript code. 

Again, const prevents reassignment. With const, you are not creating an immutable object. 

UPDATING ARRAYS:
Practice immutability when working with arrays. 

Example: ADDING TO AN ARRAY
Can also use: .indexOf, .slice 
const numbers = [1, 2, 3]; 
const added = […numbers, 4]; 
returns: [1,2,3,4]

Complex example: 

Const numbers = [1, 2, 3]; 
Const index = numbers.indexOf(2);
Const added = [
			…numbers.slice(0, index), 
			4, 
			…numbers.slice(index) 
		]; 
console.log(added); 
returns: [1, 4, 2, 3] 

//removing 
.filter method removes 

//updating
.map 
Const updated = numbers.map(n => n === 2 ? 20 : n) 
console.log(updated); 
saying: If n equals 2, we will return 20, if not, we will return n 
returns: [1, 20, 3]


CORE CONCEPTS IN REDUX: 


Store: single source of truth in our application, immutable, single javascript object that includes our application state. 
 
Functional programming, we don’t mutate state. Our store is an immutable object. 
So, because our store in an immutable object, so to update it, we take a function that takes the store as an argument, and returns the updated store. 

Example: 
function reducer(store, action) {
 	const updated = { …store }; 
} 
 
Spread operator and reducer! 

Reducer: The reducer is like the event handler. Takes store, returns updated store. Based on action, the reducer will know what properties of the state to update. 

Action: plain javascript object to explain what happens. (Like events) We Dispatch actions. 

Redux is great: we can log every action (redux dev tools), can easily implement undo and redo mechanisms, and there is essentially one entrance. 


Redux steps:
-design the store: maintain list of characters 
-define the actions: actions the user can perform, javascript objects 
-create a reducer: reducers take an action and return the updated state
-set up the store based on your reducer 

actions:
type: property that redux expects in your action objects. 

Reducer: state and action 

Rails: http://localhost:3000/api/characters

React components: two set properties, props and states. These components are like javascript classes. Components are mounted to the DOM. 

ASYNC REACT: remote data using fetch requests to remote APIs. 

The app mounts, fetch called to the api, DATA RETURNED, data stored in the state. 

Redux: stores all necessary data in our application in a javAscript object. 

Action —> reducer —> new State 

More on actions/reducers/state/props 

“Props” is a special keyword in React, which stands for properties and is being used for passing data from one component to another. Furthermore, props data is read-only, which means that data coming from the parent should not be changed by child components


Redux for beginners: react redux tutorial notes: 
Redux: state management package 
React redux: ability to connect react and redux together 
Store: the state, a globalized state, holds all the data, or state, for our application
Action: Ex: Button. Just describes what you want to do.
Reducer: describes how the actions transform the state into the next state. Checks which action you did, based on the action, will modify the store.
Dispatch: Dispatch this action to the reducer, checks what to do, then the store gets updated. 

MOST SIMPLE EXAMPLE:
First step: Create store which holds all of our state. 

import {createStore} from ‘redux’; //import globalized state 

let store = createStore(reducer) 

What does an action look like? A function that returns an object. With a type.
Ex: 
const increment = () => { 
	return {
			type: ‘INCREMENT’
		} 
	}

What does a reducer look like? Another function. Returns an object.
Switch action depending on its name 
We have one piece of store which is the counter. 
Based on name of the action, it will do something for us 
Then it will update our store.

	const counter = (state = 0; action ) => { 
		switch(action.type){
	case “INCREMENT”: 
	return state + 1;
}
}

Then add it to the store. 
Let store = createStore(counter); 

//DISPLAY IT IN THE CONSOLE: 
store.subscribe(() => console.log(store.getState());

DISPATCH:
To finally execute the action, we need to add dispatch: 
Call the action that you want.
Which action was dispatched? Look at the name, which is increment. Based on name, will return a piece of state. 
0 + 1. 
store.dispatch(increment()));

This is a way of seeing it all together in one place. It is best practice to separate it out in files, reducers, actions, and store. React displays the presentational components. 

Container is an informal term for a React component that is connect -ed to a redux store. Containers receive Redux state updates and dispatch actions, and they usually don't render DOM elements; they delegate rendering to presentational child components.


An error occurred inside a promise. Uncaught (in promise) TyperError
This is a common error. 
Look at some promise inside the app. 



After all, you get this error when calling the then() method on a Promise.
The function should be refactored to include a return statement so that a Promise can be returned to the caller. I have a return statement. 

Access a piece of state 
Import our actions 

import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import './index.css';
import App from './containers/App';
import registerServiceWorker from './registerServiceWorker';
import store from './store.js';


As the first argument passed in to connect, mapStateToProps is used for selecting the part of the data from the store that the connected component needs
	•	It is called every time the store state changes.
	•	It receives the entire store state, and should return an object of data this component needs.

These methods are called in the following order when an instance of a component is being created and inserted into the DOM:
	•	componentdidMount()


Localhost:3003/characters 
http://localhost:3000/api/characters

LIVE CODING IS JUST REACT BY ITSELF. 


issues: 	.	Content-Type: text/html; charset=UTF-8
	.	Content-Type: application/json; charset=utf-8
So the api request is being weird. Going to rails.
Turn off CSRF? 










	


