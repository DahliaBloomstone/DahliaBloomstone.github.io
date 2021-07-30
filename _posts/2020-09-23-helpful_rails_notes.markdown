---
layout: post
title:      "rails stuff "
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

Resources: Any object that you want users to be able to access via URI and perform CRUD (or some subset thereof) operations on can be thought of as a resource. In the Rails sense, it is generally a database table which is represented by a model, and acted on through a controller.
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
			 
	**Think of foreign keys**:
	Columns that refer to the primary key of another table. Comprised of the name of the model you are referencing and id. Accessible through instance methods like ArtPlan.find(@art_plan.art_plan_id) would mean you could find an art plans with that active record query. by their id. Foreign keys correspond to the belongs to, has many, has many through relationships 

Mass assignment: params, every key in the hash has to respond to a writer. 


#new instantiates a new ActiveRecord model without saving it to the database, whereas #create immediately attempts to save it, as if you had called #new and then #save.

I attended the weekly study groups to understand errors I couldn't figure out myself. They were the most helpful part of the project! It was so nice to work with other people being an online self paced student. 

Project Planning:

Models: User, art_schedule, art_plan, art_project 

User: has many art plans, has many art projects through art plans, and has many art schedules through art projects

art_schedule: belongs to art project, belongs to art plan 

art_plan: belongs to user, has many art schedules, has many art projects, through art schedules 

art project: has many art schedules, has many art plans through art schedules 


Working with byebugs:
**byebug**:
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


Specifications for the Rails Assessment
Specs:

** Using Ruby on Rails for the project
I have used Ruby on Rails for the project. 
 
** Include at least one has_many relationship (x has_many y; e.g. User has_many Recipes)

 Include at least one belongs_to relationship (x belongs_to y; e.g. Post belongs_to User)
 
 Include at least two has_many through relationships (x has_many y through z; e.g. Recipe 
has_many Items through Ingredients)
 
 Include at least one many-to-many relationship (x has_many y through z, y has_many x through z; e.g. Recipe has_many Items through Ingredients, Item has_many Recipes through Ingredients)
 The "through" part of the has_many through includes at least one user submittable attribute, that is to say, some attribute other than its foreign keys that can be submitted by the app's user (attribute_name e.g. ingredients.quantity)

Include reasonable validations for simple model objects (list of model objects with validations e.g. User, Recipe, Ingredient, Item)

Include a class level ActiveRecord scope method (model object & class method name and URL to see the working feature e.g. User.most_recipes URL: /users/most_recipes)

Include signup
 Include login
 Include logout
 Include third party signup/login (how e.g. Devise/OmniAuth)
 Include nested resource show or index (URL e.g. users/2/recipes)
 Include nested resource "new" form (URL e.g. recipes/1/ingredients/new)
 Include form display of validation errors (form URL e.g. /recipes/new)
Confirm:

 The application is pretty DRY
 Limited logic in controllers
 Views use helper methods if appropriate
 Views use partials if appropriate
 
 
When Rails renders a view as a response, it does so by combining the view with the current layout, using the rules for finding the current layout that were covered earlier in this guide. Within a layout, you have access to three tools for combining different bits of output to form the overall response:

Asset tags
yield and content_for
Partials: With a partial, you can move the code for rendering a particular piece of a response to its own file.

Ex: <%= render "shared/page_title", title: "Your Art Project Planning Resource! Write your goals and project descriptions:" %>

You can also pass local variables into partials, making them even more powerful and flexible. For example, you can use this technique to reduce duplication between new and edit pages, while still keeping a bit of distinct content:

new.html.erb

<h1>New zone</h1>
<%= render partial: "form", locals: {zone: @zone} %>

<div class="well col-md-8 col-md-offset-2">


-Ruby on Rails: A server side web application framework written in ruby. It has an MVC framework. 

-Search function in Ruby on Rails
 
-scope method querying by the date rails

-model/class methods Ruby on Rails: https://api.rubyonrails.org/v3.2/classes/ActiveRecord/Associations/ClassMethods.html
 
-active record queries: Active record allows you to perform queries on the database. Finder methods that return a collection, such as where and group, return an instance of ActiveRecord relation. Methods that find a single entity, such as find and first, return a single instance of the model. You can play with this in the rails console. Example: ArtProject.first or artproject = ArtProject.find(5) 

2.6.1 :001 > artproject = ArtProject.find(3)
   (1.0ms)  SELECT sqlite_version(*)
  ArtProject Load (0.1ms)  SELECT "art_projects".* FROM "art_projects" WHERE "art_projects"."id" = ? LIMIT ?  [["id", 3], ["LIMIT", 1]]
 => #<ArtProject id: 3, medium: "drawing", day: "2020-10-01 00:00:00", idea: "Beauty", artist_reference: "Oursler", content: "Politics", price: 500, created_at: "2020-10-01 20:08:35", updated_at: "2020-10-01 20:08:35"> 

We can see the sql equivalent being generated. 

query: a request for data or information from a database table or tables. The data is generated by SQL.

-raw sql rails: We use SQL to manipulate the data. We can use the SQL language to query (select, delete, insert, update) data. 

-Scope:  Allow for cleaner code. Guarantee an active record relation. Scopes are custom queries that you define inside your Rails models with the scope method.
Every scope takes two arguments, a name and a lambda which implements the query. 
You will get an active record object when calling scope. https://www.rubyguides.com/2019/10/scopes-in-ruby-on-rails/


Search Feature in Ruby on Rails: 

So first, we’ll need to do it with a form. So we will go to the views page and go to the user show page. This shows the art projects so we can search through them on this page. So the steps here would be to create the tags in the view, WE WILL THEN HAVE TO CALL A SCOPE METHOD IN OUR CONTROLLER, but define the scope method in our model. It is good to put a pry in the method and play around with it in the console. Because basically, with a search, to implement a search, we are gonna be querying the database. We wanna query it in the MODEL, not the controller or view. Where would we call my search method? In an index action in the art projects controller.

Step 1: Create the form in the view 
Form tag or form for? 
Form tag is the better option because we will not be changing/creating/updating/editing an object/ any data in the database, we are just retrieving data. 

Form for is for creating or updating an object or a model. 

<%= form_tag(“/posts”) do  %>   

sending it to the page we want the search function on (posts page example)

From rails documentation: https://guides.rubyonrails.org/v5.2/form_helpers.html#a-generic-search-form

<%= form_tag("/search", method: "get") do %>
  <%= label_tag(:q, "Search for:") %>
  <%= text_field_tag(:q) %>
  <%= submit_tag("Search") %>
<% end %>

<%= form_tag("/art_projects", method: "get") do %>
    <%= label_tag(:q, "Search for:") %>
    <%= text_field_tag(:q) %>
    <%= submit_tag("Search") %>
  <% end %>

Can also use submit_tag(“Filter”) can make our results easier to see 

This will generate the following HTML:
<form accept-charset="UTF-8" action="/search" method="get">
  <input name="utf8" type="hidden" value="&#x2713;" />
  <label for="q">Search for:</label>
  <input id="q" name="q" type="text" />
  <input name="commit" type="submit" value="Search" />
</form>


Why a get request?  Get sends the parameters in the url. (Literally in the url) 
What is the label tag and the qs?  It’s just what they call the parameter. The query. The name of our key when we send parameters.  

Then we are seeing: The label tag just creates “Search for” in plain text, then the empty text field where the user can type, then the search button. 

Where is it going in my controller? Where would I implement the search? It would go to the index controller action. 

WE WILL THEN HAVE TO CALL A SCOPE METHOD IN OUR CONTROLLER. Because basically, with a search, to implement a search, we are gonna be querying the database. 
We wanna query it in the MODEL, not the controller or view. 
Where do we wanna invoke the search? 


2. SCOPE METHOD IN THE MODEL: 


Something like: 
class ArtProjectsController < ApplicationController 
   #filters: methods that are run before, after, or around a controller action
   #filters are inherited 
   #art project method to show edit or update
    before_action :set_art_project, only: [:show, :edit, :update]

def self.search(params) 
binding.pry
end

next… Think about how we want to write the query? We want the search to be an exact match to the term. 

In the pry: where(medium: “video”)


There is a sql lowercase function! LOWER!

In the binding pry terminal you use straight raw sql. So you can type:

where(“LOWER(medium) = ?”, ‘video’) 

https://www.w3schools.com/sql/sql_like.asp
The like operator can be used inside of a where clause that allows for flexibility. 
Looks for anything that has certain params.  “%video%”

the LOWER function converts all letters in the specified string to lowercase.

def self.search(params)
where(“LOWER(medium) LIKE ?”, “%#{params%”)     <— makes the search more specific 
   binding.pry 
     end

def self.search(params)
where(“LOWER(medium) = ?”, params) <— without like keyword 
   binding.pry 
     end

Select any art projects with a title that is an exact match to the search term. How do we do that with queries? In the pry: where(medium: “video”) 
To make lowercase or uppercase not matter: .downcase

STEP 3: NEXT, IN THE CONTROLLER ACTION: 

 def index 
    if params[:art_plan_id] && artplan = ArtPlan.find_by_id(params[:art_plan_id])
    @art_projects = artplan.art_projects.paginate(page: params[:page], per_page: 2)
    else
     @art_projects = current_user.art_projects.paginate(page: params[:page], per_page: 2)
  if params[:q]     //if the user submitted a search 
  @art_projects = @art_projects.search(params[:q]).downcase)   //search through collection we already have  
@art_projects = @art_projects.filter(params[:art_project][:art_project_id]) if params.try(:art_project).try(:art_project_id)
     end
end 


How to use Scopes in Ruby on Rails: 
Scopes are related to models. 

Example:  in controller 
  Def index 
@books = Book.long_titles
 end 

This is an active record query, the name of our scope is  in the models 
How do we define a scope? In our models. 
Scope: All scope methods return an active record relation object. 

EXAMPLE: THESE ARE THE SAME THING. CLASS VS SCOPE METHOD.
class Article < ApplicationRecord  (in model folder)
  scope :published, -> { where(published: true) } 
end

class Article < ApplicationRecord (in controller)
  def self.published 
  where(published: true) 
end
end

Example: 

  class Book < ApplicationRecord 
  validates :title, :author, presence: true 

  scope :long_titles, ~> {  where(“LENGTH(title) > 30”)  }  We want an active record query. 
  scope :filter, -> (params){where(“category_id = ?” params))    

FILTER METHOD:   documentation
https://www.justinweiss.com/articles/search-and-filter-rails-models-without-bloating-your-controller/
 
Allows you to give a specific query a name. The scope definition will be in the model. 
The main benefit of scope is that now you can clearly see what it is doing. (By naming it) 
It is also now a reusable method. 

ERB VIEWS FILES: 
<%= only use the equal sign when we are outputting some type of variable. 
<% 

example: 
<h1>Blog Posts</h1>
<% @posts.each do |post| %> 
<% end %> 

FANCY GEMS: Next time: mysql2 gem and faker gem to randomly generate data and content. 
https://github.com/faker-ruby/faker


Scope method querying by the date: 
https://guides.rubyonrails.org/active_record_querying.html
Example on how to write that: 

scope :can_be_shown_now,  -> { poster_for_summary.where(["`posters`.start_time <= ? AND `posters`.end_time >= ?", t = DateTime.now, t]) }

18.1 find_or_create_by
The find_or_create_by method checks whether a record with the specified attributes exists. If it doesn't, then create is called. Let's see an example.
Suppose you want to find a client named 'Andy', and if there's none, create one. You can do so by running:
Client.find_or_create_by(first_name: 'Andy')
# => #<Client id: 1, first_name: "Andy", orders_count: 0, locked: true, created_at: "2011-08-30 06:09:27", updated_at: "2011-08-30 06:09:27">
The SQL generated by this method looks like this:
SELECT * FROM clients WHERE (clients.first_name = 'Andy') LIMIT 1
BEGIN
INSERT INTO clients (created_at, first_name, locked, orders_count, updated_at) VALUES ('2011-08-30 05:22:57', 'Andy', 1, NULL, '2011-08-30 05:22:57')
COMMIT

Or something like: 

QUERYING BY THE DATE: 

ArtProject.where("DATE(created_at) = ?", Date.today).count

selected_date = Date.parse(params[:selected_date])
# This will look for records on the given date between 00:00:00 and 23:59:59
sh = SupportHistory.where(
       :created_at => selected_date.beginning_of_day..selected_date.end_of_day)

https://stackoverflow.com/questions/13211916/rails-activerecord-find-search-by-date

Or you can create this method in your model: 
def created_date
   self.created_at.to_date
 end

And then queried like this: 
selected_date = Date.parse(params[:date])

 Ticket.all.map{|t| t if t.created_date == selected_date}.compact








