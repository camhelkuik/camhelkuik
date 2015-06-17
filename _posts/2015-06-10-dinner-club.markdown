---
layout: post
title:  "Dinner Club"
date:   2015-06-10
categories: code
---
# Dinner Club using Check Splitter

I need to build a program that would create a dinner club and would split a check between the dinner club members and hold certain information. The information that I need dinner club to store is the names of the members who are apart of the dinner club, the member's history of the total amount of money they have paid during their membership in dinner club, store a list of each outing with the restaurant name and which members went to that restaurant and finally allow for members of the dinner club to treat other members to meals. 


## CheckSplitter Class
I made a 'CheckSplitter' class to be able to take the check amount and tip percentage and divide that evenly between the paying members of the dinner club that attended that specific outing. The attributes I required are:

-total_cost_of_meal

-tip_percentage

-num_people

The methods are then finding necesary values. The method tip_as_decimal changes the tip percentage to a decimal. Tip_amount uses the decimal form and figures out the tip. Meal_plus_tip adds the total cost of the meal and the tip amount. Then finally even_split divides the final amount between the paying members. 


## Dinner Club Program
In my dinner club program when a dinner club is initialized, I set a few required attributes:

```ruby
def initialize(member_names)
    @total_outings = []
    @members = {}
    
    member_names.each do |name|
      @members[name] = 0
    end
end
```
I created @members as an empty hash and then iterated through the member_names to add each member name to the members hash and set each one equal to 0. This will end up being the tally for the history of how much each memeber has paid during their membership.

I use @total_outings later to hold a list of the restaurant name and which members went to the restaurant.


### go_out Method
My first method is go_out. This method uses my 'CheckSplitter' class to split the check between the paying members and then returns the members who attended and the history of the amount of each member. The parameters for this method are meal_cost, tip_percent, and who_paid. These parameters are the same values that are needed for the attributes in the 'CheckSplitter' class. However, I use the parameter who_paid instead of just the number of members who attended. I do this so it allows for members to treat each other. 

-meal_cost is an integer of how much the meal costs

-tip_percent is an integer of how much they tipped

-Who_paid is an array of member's names who paid for the meal.

```ruby
  def go_out(meal_cost, tip_percent, who_paid)    
    cs = CheckSplitter.new(meal_cost, tip_percent, who_paid.length)
    
    amount_per_person = cs.even_split
    
    who_paid.each do |a|
      @members[a] = @members[a] + amount_per_person
      
    end
    
    @members
  end
```

### club_outing Method
My next method is club_outing. This method returns the restaurant name and adds the member's name to that outing. The parameters of this method are restaurant_name and attendees. 

-restaurant_name is a string of the restaurant's name

-attendees is a string of the member's names who attended the outing. 

```ruby
  def club_outing(restaurant_name, attendees)
    outing = {}
    outing[restaurant_name] = attendees
    @total_outings.push outing
  end
end
```
The method club_outing takes the parameter restaurant_name and attendees and adds them into a hash. From there It pushes that hash to the total_outings array that was initalized at the beginning of the class. This gives us a list of all the different restaurants and the members who went to that restaurant. 
