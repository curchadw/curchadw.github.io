---
layout: post
title:      "My Team Management System Sinatra Project"
date:       2020-07-05 22:27:39 -0400
permalink:  my_team_management_system_sinatra_project
---


To introduce what this blog is about is an overview of my project and key features that relates to what I've learned in the Sinatra Module. I based the idea of my project on the scenrio of managing a roster to a sports team and scouting other teams in whatever league it is. This project emphasized my overall understanding of how a MVC(Model, View, Controller) app works regardless of the framework in particular being even though they vary by convention and language. Another thing that this project got me used to is looking into the robust documentation of Ruby on Rails. There is still tons to learn but this project gave me a good headstart. There are a couple of features that I wanted to focus on, Dynamic Routes, and ActiveRecords Associations.


**Dynamic Routes**

A dynamic route is a http request that has the ability to conform to the attributes within a URL. Lets say for instance you are logged into your account and you want to access player with an ID of one and view their info. It doesn't matter if the player is part of their team or not for this example, so I thought I throw that technicallity out for this one. 
In my browser I will make a request like "www.tms.com/players/1". What is going on behind the scene with this? Looking at this from a higher level, I am typing in the URL address and making a http request to see player with an id of 1 to the webserver, and the webserver will reply  with a http code un the 200's and also a html document of the content back to your browser. The image below is an illustration on what is going on in a nutshell.

![](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP.png)

How does this process look under the hood? One thing to remember is the request in the browser calls a special method called a GET request within your controller of your MVC structure, which goes to the server to grab the content, in this case is the erb file at path "players/show

```
get '/players/:id' do
        
        @player = Player.find_by_id(params["id"])
        erb :"players/show"
    
end
```
Breakdown of the code above:

1) ```get '/players/:id do```
    - Grabbing the get method with the '/players/:id' route. 
    - The id attribute is designed to conform to whatever ID goes in the route.

2) ```@player = Player.find_by_id(params["id"])```
    - We have to assign this line to a **instance method** because we are going to render a erb document with the player we want

The dynamic part comes in play when you are able make the  requst with any id in the id attribute of the route that exist, without the application breaking.


**Assocations Straight Ruby Vs From Rails ActiveRecords Library**


I was forgetting what type of project I was doing when I was writng a code to gather players only associated with the current user. A case and point is when you are on a social media web app, you'll see other people's post, but you might want to just look at your own. You are dealing with a "has many" type of association in this example. The user has many post associated with it. In my project, your users will have many players associated with them. In my app, I made a part of it where the current user has the ability to create a player, and also has the ability to just view their own players.

When I was trying to figure this out I at first used the code below.

```
get '/user_players/:username' do
   @user_players = Player.all.select{|players| players.user_id == current_user.id }
	 erb : 'players/show_user_players'
end
```

The code in fact works the way it's supposed to, but one of the goals of this project is getting used to referencing Rails ActiveRecords documentation for this type of case reducing the amount of code in the long-run.

In your "User" model, you need to establish a "has many" relationship with players

```
class User <ActiveRecord::Base
    
    has_many :players

    
end
```

When you establish the "has_many" relationship like in the code above, you have access 17 different ActiveRecord methods. When refactoring I used  ```@players = @user.players``` which bascially returns a collection of players pertaining to that user and renders a view with the players like below.

```
get '/user_players/:username' do
        @players = current_user.players
        erb :'players/show_user_players'
 end
```










