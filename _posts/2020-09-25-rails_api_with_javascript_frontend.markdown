---
layout: post
title:      "RAILS API WITH JAVASCRIPT FRONTEND!"
date:       2020-09-25 22:40:14 -0400
permalink:  rails_api_with_javascript_frontend
---

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

