---
layout: post
title:      "Let's write about rails! "
date:       2020-09-23 13:16:33 -0400
permalink:  helpful_rails_notes
---

# This will be a helpful guide in the future when I want to create a new rails app. 

**What is rails?** A web and MVC framework and a ruby gem! 

**To start:** gem install rails, rails new app-name, cd app-name, rake db:create, and rails s to start the server. To use the console: rails c. 

A review of **MVC architecture:** Model, View, Controller. 
*Model *files contain validations, database relationships, callbacks, and custom logic. It is a Ruby class that inherits from ActiveRecord::Base. 
*Views* directory contains the corresponding view for each page that the user will access. 
The *Controllers* have methods to manage data flow, using CRUD features (index, new, create, show, edit, update, and destroy). They connect the models, views, and routes. 

**HTTP routing** reminder: URL entered into the browser which is the HTTP request, request sent to server, router interprets the request, sends the message to the controller mapped to the route, controller communicates with the view, server returns HTTP response with the view page in the browser. 

The routes in my app: in config/routes.rb. RESTFUL CONVENTIONS:
Includes: the HTTP verb (ex: get)
*The path*: the path in the URL bar the route will be mapped to (ex: /signup')
The controller action: tells the Rails routing system that this route should be passed through the static controllers action. (ex: 'users#new')

root 'sessions#home'
get '/signup' => 'users#new' (render: new in controller)
get '/login' => 'sessions#new'
post '/login' => 'sessions#create'
delete '/logout' => 'sessions#destroy'
get '/auth/facebook/callback' => 'sessions#fbcreate'
 resources :users
 resources :art_plans
 resources :art_projects, only: [:edit, :index, :show ]
 resources :art_schedules
 resources :art_plans do
 resources :art_schedules, only: [:new, :index, :create]
 end
 resources :art_projects do
 resources :art_schedules, only: [:new, :index, :create]
end
end

Next, Rails will look to render the view explicitly or implicitly. Explicitly would render the new view page in users. 

**Models:** a user has many art plans, has many art projects through art plans, and has many art schedules through art projects. art schedules belong to art projects and art plans. art projects have many art schedules and have many art plans through art schedules. art plans belong to user, have many art schedules, and have many art projects. 

I set these up after my migrations. Running rails db:migrate and rails db:seed.
Remember and stress the importance of seed data for testing! Like this: 
#art plan:
ap = ArtPlan.create(goal: "paint once a day", description: "nice", user_id: 1)
ap1 = ArtPlan.create(goal: "make a video", description: "cool", user_id: 2)
You test in the rails console by: ArtPlan.all or ArtPlan.first, and should return data.

Example of URL route helper:   redirect_to user_path(@user) 
HTML friendly paths! 

Next reminder: **Rails form_tag, form_for element**.  Ex: <%= form_for (@art_plan)  do |f| %>
It knows we want to submit a form via a POST method, automatically renders the HTML. It allows us to submit form data that the controller can use to create or update the record in the database. Can pass in the route to which the params for the form will be sent, the http method, and the attributes for each field. form_for accepts the instance model as an argument (@art_plan). It also knows the route. Used when it is directly connected to a model!

Create Action: 
     def create
        @art_schedule = ArtSchedule.new(art_schedule_params)
      if @art_schedule.save
        flash[:success] = "Your art project schedule has been created! Start Working!"
        redirect_to art_schedule_path(@art_schedule)
      else
        render :new
      end
    end 
		
*What is happening here? *It creates a new art schedule and saves it. It redirects you to create the schedule, renders the new page. The save method generates a SQL script that inserts a new record into the database. Each of the ArtSchedule object's attributes are passed into the SQL statement, and the method returns true upon succeessful saving. In the console, you will see the art schedule data like the time you work on it and the type of art work it is. It creates a new ArtSchedule instance, passes in the params from the form, and saves the record. We can access the params hash at any time in the console by doing something like ArtSchedule.last. 

The resources call in the route file - 
 def set_art_plan
      @art_plan = ArtPlan.find(params[:id])
      #byebug
      if @art_plan.nil?
        flash[:danger] = "ART PROJECT Plan not Found!"
        redirect_to art_plans_path
      end
    end
	
	What's happening here? We have our art plan action store the ArtPlan record in an instance variable art_plan. Now we have access to the ArtPlan object stored in @art_plan. 
	
	def update
      if @art_plan.update(art_plan_params)
        flash[:success] = "Your changes were saved!"
        redirect_to art_plan_path(@art_plan)
      else
        render :edit
      end
    end
		
		What's happening here? Taking advantage of Active Record's update method! So we don't have to manually assign each attribute. 


**Strong Params: **security vulnerabilities. Abstracted the strong parameter into its own method: We use permit method so the params hash may have whatever keys are in it. 

private
    def user_params
      params.require(:user).permit(:name, :email, :password, :password_confirmation)
    end
  end
	
	**GENERATORS**: 
	Best practice: 
	mkdir artapp
	cd artapp
	artapp % rails new artapp-api --api --database=postgresql
	cd artapp-api
	code . 
	rails g controller whatever 
	rails g model whatever
	rails db:create
	rails db:migrate
	
	
	What should you think about when you see this in the schema? 
	    t.integer "art_project_id"
			 t.index ["art_plan_id"], name: "index_art_schedules_on_art_plan_id"
			 
	**Think of foreign keys**! Columns that refer to the primary key of another table. Comprised of the name of the model you are referencing and id. Accessible through instance methods like ArtPlan.find(@art_plan.art_plan_id) would mean you could find an art plans with that active record query. by their id. Foreign keys correspond to the belongs to, has many, has many through relationships 





#new instantiates a new ActiveRecord model without saving it to the database, whereas #create immediately attempts to save it, as if you had called #new and then #save.

I attended the weekly study groups to understand errors I couldn't figure out myself. They were the most helpful part of the project! It was so nice to work with other people being an online self paced student. 

Project Planning:

Models: User, art_schedule, art_plan, art_project 

User: has many art plans, has many art projects through art plans, and has many art schedules through art projects

art_schedule: belongs to art project, belongs to art plan 

art_plan: belongs to user, has many art schedules, has many art projects, through art schedules 

art project: has many art schedules, has many art plans through art schedules 


Working with byebugs:
byebug 
(byebug) artplan
#<ArtPlan id: 2, goal: "Write Gallery Description", description: "Medium", user_id: 1, created_at: "2020-09-13 19:57:23", updated_at: "2020-09-13 19:57:23">
(byebug) artplan.art_projects
  ArtProject Load (0.4ms)  SELECT "art_projects".* FROM "art_projects" INNER JOIN "art_schedules" ON "art_projects"."id" = "art_schedules"."art_project_id" WHERE "art_schedules"."art_plan_id" = ? ORDER BY "art_projects"."updated_at" DESC, "art_schedules"."updated_at" DESC LIMIT ?  [["art_plan_id", 2], ["LIMIT", 11]]
  ↳ app/views/art_plans/_artplan.html.erb:14
#<ArtProject::ActiveRecord_Associations_CollectionProxy:0x00007ffa83dfc3b8>
(byebug) artplan.art_projects.count
   (0.3ms)  SELECT COUNT(*) FROM "art_projects" INNER JOIN "art_schedules" ON "art_projects"."id" = "art_schedules"."art_project_id" WHERE "art_schedules"."art_plan_id" = ?  [["art_plan_id", 2]]
  ↳ (byebug):1
*** ActiveRecord::StatementInvalid Exception: SQLite3::SQLException: no such column: art_schedules.art_project_id

nil
(byebug) Artplan.all
*** NameError Exception: uninitialized constant #<Class:0x00007ffa83c253c8>::Artplan

nil
(byebug) User.all
  User Load (0.2ms)  SELECT "users".* FROM "users" LIMIT ?  [["LIMIT", 11]]
  ↳ app/views/art_plans/_artplan.html.erb:14
#<ActiveRecord::Relation [#<User id: 1, name: "dahlia", email: "dahliabloomstone@gmail.com", password_digest: [FILTERED], uid: nil, password_confirmation: nil, created_at: "2020-09-11 19:04:53", updated_at: "2020-09-11 19:04:53">]>
(byebug) ap = Artplan.create(goal: "paint once a day", description: "nice", user_id: 1)
*** NameError Exception: uninitialized constant #<Class:0x00007ffa83c253c8>::Artplan

nil
(byebug) ArtPlan.all
  ArtPlan Load (0.2ms)  SELECT "art_plans".* FROM "art_plans" ORDER BY "art_plans"."updated_at" DESC LIMIT ?  [["LIMIT", 11]]
  ↳ app/views/art_plans/_artplan.html.erb:14
#<ActiveRecord::Relation [#<ArtPlan id: 2, goal: "Write Gallery Description", description: "Medium", user_id: 1, created_at: "2020-09-13 19:57:23", updated_at: "2020-09-13 19:57:23">, #<ArtPlan id: 1, goal: "Write Gallery Description", description: "Medium", user_id: 1, created_at: "2020-09-13 19:55:26", updated_at: "2020-09-13 19:55:26">]>
(byebug) ap = ArtPlan.create(goal: "paint once a day", description: "nice", user_id: 1)
  CACHE User Load (0.0ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
  ↳ (byebug):1
   (0.1ms)  begin transaction
  ↳ (byebug):1
  ArtPlan Create (1.2ms)  INSERT INTO "art_plans" ("goal", "description", "user_id", "created_at", "updated_at") VALUES (?, ?, ?, ?, ?)  [["goal", "paint once a day"], ["description", "nice"], ["user_id", 1], ["created_at", "2020-09-15 16:32:27.120352"], ["updated_at", "2020-09-15 16:32:27.120352"]]
  ↳ (byebug):1
   (0.7ms)  commit transaction
  ↳ (byebug):1
#<ArtPlan id: 3, goal: "paint once a day", description: "nice", user_id: 1, created_at: "2020-09-15 16:32:27", updated_at: "2020-09-15 16:32:27">
(byebug) first = ArtPlan.first
  ArtPlan Load (0.2ms)  SELECT "art_plans".* FROM "art_plans" ORDER BY "art_plans"."updated_at" DESC LIMIT ?  [["LIMIT", 1]]
  ↳ (byebug):1
#<ArtPlan id: 3, goal: "paint once a day", description: "nice", user_id: 1, created_at: "2020-09-15 16:32:27", updated_at: "2020-09-15 16:32:27">
(byebug) first.art_projects
  ArtProject Load (0.4ms)  SELECT "art_projects".* FROM "art_projects" INNER JOIN "art_schedules" ON "art_projects"."id" = "art_schedules"."art_project_id" WHERE "art_schedules"."art_plan_id" = ? ORDER BY "art_projects"."updated_at" DESC, "art_schedules"."updated_at" DESC LIMIT ?  [["art_plan_id", 3], ["LIMIT", 11]]
  ↳ app/views/art_plans/_artplan.html.erb:14
#<ArtProject::ActiveRecord_Associations_CollectionProxy:0x00007ffab3b832f0>
(byebug) ArtProject.all
  ArtProject Load (1.0ms)  SELECT "art_projects".* FROM "art_projects" ORDER BY "art_projects"."updated_at" DESC LIMIT ?  [["LIMIT", 11]]
  ↳ app/views/art_plans/_artplan.html.erb:14
#<ActiveRecord::Relation []>
(byebug) 


TO FIX IN THE FUTURE:
How it looks!
https://github.com/turbolinks/turbolinks turbolinks might be the issue, I had a problem submitting forms where it wouldn't fully submit until I refreshed the page. 

