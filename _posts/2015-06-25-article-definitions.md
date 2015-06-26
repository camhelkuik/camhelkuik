---
layout: post
title:  "Article: Definitions"
date:   2015-06-25
categories: code
---
#Class
A class is the blueprint for how individual objects should be made. An example would be if we had a class called Song. The attributes for this class would be artist, song name, genere and duration. Each individual object of the Song class would have an artist, a song name, a genere and a duration. 

#Model
A model is a class that is connected to a database. 

#Method
A method is a block of code that returns a value. We use methods for when we need to run the same code many times in a program. Methods belong to a class and can be used on a class object. 

Example of a method:
```ruby
  def hello
    puts "Hello! I am a method."
  end
```
#Variable
A variable is something that stores data. The data can be a variety of value types such as: integer, string, hash,etc. Variables are given individual names and they hold specific objects. For example: name = Cameron. Name is the given variable name and Cameron is the object that it is refering to. 

#Request
A request is the user input that has asked for our program to do something. It could me a click on a link to typing something into a form and hitting the submit button. The user is requesting our program to take their input and return something.  

#Route
A route is the way to connect the request to the controllers. It looks to see what the request is and matches it to the correct controller. The controller has the "action" that the program is supposed to due.

#Response
After the request is routed to the right controller and the program "gets" what was requested the program then sends the response. The response is what our program returns to the user. 
