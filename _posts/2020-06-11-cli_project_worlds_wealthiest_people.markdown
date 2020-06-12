---
layout: post
title:      "CLI Project! Worlds Wealthiest People"
date:       2020-06-11 20:13:53 -0400
permalink:  cli_project_worlds_wealthiest_people
---

Project notes:
What is a wealthy person?
a wealthy person has a name
a wealthy person has a ranking
a wealthy person has a description 
want an object that has these properties that the CLI can just use
go to website, find the people
extract the properties
instantiate a person 

I am on day 4! The first day, I made my flowchart and tried out some code while looking at a few references for similar projects. THAT WAS NOT THE RIGHT WAY TO GO! 

By day 2, I had code that I didn't full understand how to run. That was not the right way to approach building this. After talking to a friend on the slack channel, he told me it was imperative that I watch the videos on building basic CLI's that are provided to us. Thank goodness he told me to do that! 

On day 3, I watched half of the video, it was only 30 minutes but in order to code along, write notes, and understand what Avi was saying, I had to pause the video a bunch of times. So, 30 minutes in, but really, a couple hours in! It was so helpful, though. I understood more after watching that video than I did in a long time. Big win!

Day 4, I have a project that fully runs and works, after watching both of the videos and coding along - but there is something missing. My project, worlds wealthiest people, displays to the user a list of the 50 wealthiest people and their descriptions. The list shows their name and rankings. I want that data to be seperate, but I'm not sure what I did wrong with my CLI just yet. The user has the option to see all of that data together as a list, or exit. I'm just happy that it runs, and that I understand it up until this point! 

I was going to submit just that, because I think it still met all the requirements, but I decided to turn in a project help form to see what I could improve so that the user could interact with the project more.  Overall, I've put about...maybe 30 hours into this so far. And it has been...pretty fun and rewarding! I actually created new github repositories maybe 3 or 4 times...and even tried out an easier project idea! And I haven't been too frustrated yet...good sign I should keep going and keep practicing! 

STAY TUNED! 

https://github.com/DahliaBloomstone/Worlds_Wealthiest_People

TO RUN IN TERMINAL:
./bin/Worlds-Wealthiest-People

class WorldsWealthiestPeople::CLI
  
  def call 
    puts "These are the World's Wealthiest People!"
    list_billionaires
    menu 
    goodbye 
end

def list_billionaires   #Class method that returns list of people w their attributes/descriptions*
puts "2019 Billionaire List in order from least to greatest:"
@people = WorldsWealthiestPeople::Person.list     #person object that returns @people*
@people.each.with_index(1) do |person, i|   #*if you chain the index at 1 it will start with 1 soyou don't have to do i -1 all the time 
*
  *puts "#{i}. #{person.nameandranking} - #{person.descriptio*n}"
  end 
end 

def menu
   input = nil
     while input != "exit"
  puts "Continue to see the list of billionaires for 2019 with ranking, name, and description or type exit to enter or type list to see the full list of billionaires again or type exit:"
  input = gets.strip.downcase
 
  if input.to_i > 0 
    the_person = @people[input.to_i-1]
     puts "#{i}. #{the_person.name_and_ranking} - #{the_person.description}"
    elsif input == "list"
    list_billionaires 
     else 
        puts "Not sure what you want, type list or exit"
      end 
    end
  end 

def goodbye 
  puts "See you tomorrow to keep reading!"
  end 
end 

class WorldsWealthiestPeople::Person 
 attr_accessor :name_and_ranking, :description
 
 def self.list 
  self.scrape_people
 end 
      
def self.scrape_people  
  people = [] 
  
  people << self.scrape_url
    people
  end 
  
  def self.scrape_url 
    doc = Nokogiri::HTML(open("https://vocal.media/geeks/top-50-billionaires-in-the-world-for-2019"))
   
	 (Without putting .text it would show all of the html/css too)
   person = self.new 
   person.name_and_ranking = doc.search("h3.css-rv324f-Heading.em4arlq0").text.strip
   person.description = doc.search("p.css-1oblyum-P.e1ccqnho0").text.strip 
   person
  end 
end 
