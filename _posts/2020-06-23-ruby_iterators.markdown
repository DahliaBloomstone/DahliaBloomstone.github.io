---
layout: post
title:      "Ruby Iterators!"
date:       2020-06-23 16:36:28 -0400
permalink:  ruby_iterators
---


![](https://jellygummies.tumblr.com/image/182033912973)


## Reviewing iterators and return values with examples with the help of Relp.it

```
#Example 1: Using Split, Join, and Collect. This will return a new array but reversed.

def reverse_words(string)
array = string.split(" ") 
new_array = []
array.collect do |string|
  new_array << string.reverse 
end 
new_array.join(" ") 
end 
reverse_words("I AM HUNGRY")
 
 RETURNS: 
 => "I MA YRGNUH"

#Example 2: Using Collect to return a new array with all elements 

fruits = ["apples", "pears", "plums", "bananas"]
fruits.collect do |fruit|
  fruit
  end 
end 

RETURNS: 
=> ["apples", "pears", "plums", "bananas"]


#Example 3: Using each and a phrase  to return the phrase and original array of fruits 

fruits = ["apples", "pears", "plums", "bananas"]
fruits.each do |fruit|
  puts "this fruit sucks: #{fruit}!
end 

RETURNS: 
=>   this fruit sucks: apples
       this fruit sucks: pears
       this fruit sucks: plums
       this fruit sucks: bananas  
			 ["apples", "pears", "plums", "bananas"]

 
#Example 4: Using each to return the original array, no change in return value 

fruits = ["apples", "pears", "plums", "bananas"]
fruits.each do |fruit|
  puts fruit 
end 

RETURNS:
=> ["apples", "pears", "plums", "bananas"]

#Example 5: Using map to change the return value and return a new array 

fruits = ["apples", "pears", "plums", "bananas"]
fruits.map do |fruit|
  puts fruit 
end 

RETURNS: 
=> ["apples", "pears", "plums", "bananas"]


#Example 6: Using each with reverse method to return the original array and sorted elements 

fruits = ["apples", "pears", "plums", "bananas"]
fruits.each do |fruit|
  puts fruit.reverse
end

RETURNS: 
=> 
selppa
sraep
smulp
sananab 
["apples", "pears", "plums", "bananas"]


#Example 7:  using each and sort to return sorted (alphabetical) elements and the original array 

fruits = ["apples", "pears", "plums", "bananas"]
fruits.sort.each do |fruit|
  puts fruit 
end 

RETURNS: 
apples
bananas 
pears 
plums 
["apples", "pears", "plums", "bananas"]














