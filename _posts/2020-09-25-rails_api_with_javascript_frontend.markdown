---
layout: post
title:      "RAILS API WITH JAVASCRIPT FRONTEND!"
date:       2020-09-26 02:40:13 +0000
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
		
		then do rails s, and the browser shows the json representation of our app 
IN NEW VS FOLDER: 
mkdir js-frontend
cd js-frontend
Mkdir bin src styles 
Touch index.html creates index.html
		
		use frontend to talk to rails api to get data.  going like ! Creates: 
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
		
		see notes on oo-js in the adapter  
		open index.html and the console: 
		if you put in index.js console.log(welcome!). you will see that when you inspect/console 


	⁃	next, you want to take the array of objects in the console, and get them appended to the DOM and present them to the actual user. 
	⁃	build out additional methods in gooddeeds class  
	⁃	
	⁃	 git push -f origin master 


