---
layout: post
title:      "SINATRA PROJECT"
date:       2020-07-26 02:35:14 +0000
permalink:  sinatra_project
---

For this blog entry, I will go through the steps I did for building my app: Sinatra Good Person Tracker App! It's a silly little app that ended up helping me understand so much. 

STEP 1: For this project, I began by watching all of the videos available to Flatiron students. So, the pre-work for this project took over 15 hours! Watching all of those videos was so worth it because I learned so much and it solidified so many concepts in my head. For reference, I watched all of the Sinatra Mixshare App videos, Sinatra Journal App videos, and Sinatra Video Review Building A Site Generator videos. They were all so incredibly helpful! I wrote down endless notes and coded alongside the projects to make sure I knew what was happening. 

STEP 2: I wrote down my App Overview. I wrote down that I was going to build an app where a user can track their good deeds. The users will be able to log in, sign up, and log out. Users will be able to create a new good deed entry, see all good deeds entered by themselves and other users, edit their good deeds, and delete their good deeds. 

STEP 3: Wireframing! This next step would be to set up my models, their attributes, and their associations. My user model would have a name, password, and email. My user would have a has_many relationship to good_deeds. My good deeds model would have content, a user id, and a date. Good deeds would have a belongs_to relationship to the user. 

STEP 4: I thought about the minimum viable product. At a minimum, my app has to have certain functionalities. So the MVP's are a user can: sign up, log out, create a good deed entry, edit their own entries, and view their entries. My stretch goals were to make the app look cute with some kind of fun hidden images and also have a lot of flash messages so the user felt like the app had a lot of feedback and fun interaction. My stretch goals are stretch goals because they weren't as important for the core understanding of this section and I wasn't sure if I'd want to make time for them, but of course, they were fun and I made time for them! I'll probably go back and make the html/css features even better. For now, though, I focused on understanding CRUD actions and MVC. 

STEP 5: Open my desktop IDE, create a new respository on github, use CORNEAL gem - a generator for sinatra that creates basic folder scaffolding - SO HELPFUL!, and after these steps, it was coding time! I will put the steps here for a later date so I can remember: 
* gem install corneal 
*  // ♥ corneal new sinatra-good-person-tracker 
*  // ♥ cd sinatra-good-person-tracker-app
*  atom
*  create GitHub page 
*  Git command to initialize empty repository: git init 
*  Git add . 
*  Git status - green 
*  ♥ git commit -m "initial commit - scaffold project file structure with corneal” 
*  Git remote add origin
*  Git push -u origin master 


STEP 6: I built my models through migrations, model classes, associations, tested my models in the console, created some seed data, and adjusted my migrations as needed. As a reminder: the purpose of migrations is to build tables/database and is the structure of the database. It tells Active Record and sqlite columns and types. 

STEP 7: Reminder - Steps to create tables: 
* // ♥ rake db:create_migration NAME=create_users_table
* rake db:migrate ---> this will create your schema and development.sqlite files. 

STEP 8: COMMITS! 
* git add .
* git commit -m "modified this and that" 
* git push 

STEP 9: Played around with the seed data. (Open code to see seed data and play around if a reminder is needed) In terminal: rake db:seed, bundle exec tux, User, GoodDeed, User.count, User.all =>> Dahlia.good_deeds.count =>3

STEP 10: Building the users controller! This was a great experience because I played around a lot with the params and got a better understanding of them. Params is the vehicle or container that is holding the information and that is being passed in by the user. Basically, it is a hash that goes back and forth between the views and the controller. This is important to understand! So in the users controller, if you put a binding.pry in the post '/login' route, in the terminal, if you type "params" you get the information that entered by the user from the browser. Example, user types in email and password, the params will be => {"email"=>"D@gmail.com", "password"=>"password“} The Keys are email and password from login.erb, the values are what the user types in. To get out of pry: exit! Playing around with pry and tux was a very important part of my understanding for building this app and all of the lessons. 

STEP 11: For this step, I played around with return values. In the terminal, I ran bundle exec tux, and I'll just type what I was playing around with for anyone that wants to do the same. The "Type" Is what I typed into the terminal, "returns" is what tux returned as the value. Examples: 

* type: 
  User.find_by(email: “dahliabloomstone@gmail.com")
*   returns: 
 #<User id: 1, name: "Dahlia", email: "dahliabloomstone@gmail.com", password_digest: “$2a$12$4Xh1lWMFNl9e
* type:
 dahlia = _
* returns: 
=> #<User id: 1, name: "Dahlia", email: "dahliabloomstone@gmail.com", password_digest: “$2a$12$4Xh1lWMFNl9e
* type:
 dahlia
* returns:
=> #<User id: 1, name: "Dahlia", email: "dahliabloomstone@gmail.com", password_digest: “$2a$12$4Xh1lWMFNl9e
* type:
  dahlia.authenticate(“ploop”)
* returns: 
=> false
* type:
 dahlia.authenticate(“password")
* returns: 
=> #<User id: 1, name: "Dahlia", email: "dahliabloomstone@gmail.com", password_digest: “$2a$12$4Xh1lWMFNl9e

STEP 12: I created the signup page. Here is where I refreshed my memory on restful routing conventions. When we create a brand new user, we create a post request, the http verb, and our action is where we go. I also reminded myself of the difference between redirecting and rendering. Redirect = send a get request, separation of concerns - every route should have one job. So if we are in a post request, redirect to a get request so it does its one job and the get request does its one job. Render = happen from a get request. 

STEP 13: At this point, I am not sure which day I am on. This project takes a long time! But it is awesome! So far, as a user, I am able to sign up, sign in, create a good deed entry, get/post deed routes, and have good deed show and index routes. Time to make the "good deeds" controller! Reminder: ERB is a mix of HTML and RUBY! 

STEP 14: I might've skipped writing some steps. My hands are getting tired. Anyway, I added the ability to edit an entry, made sure nobody can edit someone elses entry by: 
* if @good_deed.user == current_user
* Redirect user to home page if user is not logged in or user is not current user. Use helper methods.
Then went over CRUD actions: create read destroy and edit actions. Reminder: current_user checks the session ID. 

STEP 15: FLASH MESSAGES! 
Flash messages: post, patch, delete controller actions. Because typically you make, edit, or delete with those requests. Inside of that controller action user makes a change. 

STEP 16: I HAD FUN WITH SOME OF THE HTML AND CSS! This is day 6. So, 6 days of notes and watching videos and coding! I'm tired! Whew! 

Github repo: https://github.com/DahliaBloomstone/sinatra-good-person-tracker-app-









