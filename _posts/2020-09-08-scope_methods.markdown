---
layout: post
title:      "Scope Methods"
date:       2020-09-08 18:18:25 -0400
permalink:  scope_methods
---


My project was a Flight Scheduler. The purpose of it was for the allocation of pilots on specific flights. I had a lot of fun with it due to some of the technical challeneges that came my way. One of the most important parts of my project was scope methods. 

Within my project I arranged the flights index page to seperate domestics flights from international flights. The mechanics of arranging this seemed a bit intimidating. First off, what are scope methods? Scope methods within rails are custom queries that you define with a particular model. 

This lesson goes back to the basics of SQL. 

Let's say you are trying to query where you are looking for the results in a table named puppies are breed pitbull.

Generally you would do something along these lines in SQL
`SELECT  * FROM puppies WHERE (breed = 'pitbull')`

In plain Ruby with key value pairs, it would look like this 

`puppy = Puppy.find_by(breed: 'pitbull')`


So breaking this down.....
1) We are selecting from a table called 'puppies'
2) We are focusing a a particular column called 'breed'
3) Lastly we are selecting any puppy id that has a breed classifiaction as pitbull.


How would you define this in your Puppy model using ActiveRecord?


```
class Puppy < ApplicationRecord
  scope :with_pitbull, -> { where("breed  = pitbull") }
end
```


When you do this you will get something called a ActiveRecord::Relation Object.


You will be able to chain this to an object with other methods in you puppies controller as such.

`@puppies = Puppy.with_pitbull.first`


How did I apply this in my project?

Well I wanted to seperate my international flights from my domestics flights based on on a rule of the number of characters in my the flight number. The rule have set up is if the flight numebr is above 3 chracters it is going to be classifed as a international flight, and below three characters is a domestice flight.

In my Flight model it goes as follows

```
class Flight < Actvie Record::Base
       #To sum this up I ordered by flight_number in ascending order then grabbed my results based on the length of the nunber
			 
       scope :order_by_flight_international, -> { order(flight_number: :asc).where("LENGTH(flight_number) > 3") }
       scope :order_by_flight_domestic, -> { order(flight_number: :asc).where("LENGTH(flight_number) <= 2 ") }

end
```

In my controller I defined the following for my index action....


```
def index
        @flights = Flight.order_by_flight_international
        @dom_flights = Flight.order_by_flight_domestic
 end
```


This is just a very short version of my view code.

International Flights:
```

<ul>
<% @flghts.each do |flight| %>
     <li><% flight.flight_number %></li>
<% end %>
</ul>

```

-------------------------------------------------------------------------------------------------------------

```
Domestics Flights:
<ul>
<% @dom_flights.each do |flight| %>
     <li><% flight.flight_number %></li>
<% end %>
</ul>
```





From here you will run you rails sever and see the result.

Basically you are defining the scope method in your model, attaching the method to desired object in your controller action, then you are displaying in your corresponding view as shown above. I hope this hleps some people understanding scopes methods in a simplified fashion.









