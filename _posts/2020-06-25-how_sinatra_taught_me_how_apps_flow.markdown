---
layout: post
title:      "How Sinatra Taught Me How Apps Flow!"
date:       2020-06-25 23:04:44 -0400
permalink:  how_sinatra_taught_me_how_apps_flow
---


You ever hear a song by the great Frank Sinatra and just get so drawn in by the flow of song? It feels great because that's how his music is supposed to make you feel. How can I compare that with Sinatra MVC(Model, View, Controller)? All that Ruby code that probably didn't make too much sense at first was starting to flow better, because when you develop a web application its all about understanding the flow. 

The flow of a application is one of the most important things of an application or else you'll lose your user in unncessary complexity of your application. Sinatra help introduce the concept of RESTful resources RESTful api's. Before I discuss what some RESTful resources are what does REST stand for? REST stands for REpresentional State Transfer. REST is defined as "an architectural style and approach to communications often used in web services development. " . RESTful API design was first introduced by Dr. Roy Fieldin in his doctorate dissertation 2000. Dr. Fielding focused on six particular architectural constraints. For the purpose of this blog, I am only going to focus on "Use of uniform interface(UI)". Any applicaiton with utilizing RESTful API's which is probably about 99.9% of all apps, it's all about understanding HTTP methods and their codes. 

While learning how to develop a Sinatra MVC app, you are also introduced to a concept called CRUD(Create, Read, Update, Delete). This CRUD concept works hand in hand with HTTP methods such as POST(Create), GET(Read), PUT(Update/Replace) or PATCH(Update/Modify), and DELETE. This is simply called RESTful routes. 

GET/Read:
Typically the first operation in RESTful routes you are involved with is GET/read. Your essentially reading a route to go on to get a resource.

```
get "/" do
  erb :index
end
```

In the little bit of code rigth above here, usually the "/" is the index page or start page and we are just reading the the index file to view only.


POST/Create:
When you are making a post of a social media website you are creating something. In reference to code snippet above, there may be a form on that index page that you might have to make something.

```
<form method = "POST" action = "/create_something">
  <input type = "text">
	<input type = "submit">
</form>
```

```
post "/create_something" do
   #some redirect
end
```

When you fill something out on a form and submit it, you just created something and the redirect takes you to some page that will show you what you made.

PUT/Update
You may want to update or modify you social media post because you might have made a grammatical error or something else. You typically 

```
patch '/some_post/:id do
  #some modifying block of code
end
```

Also in your view page, you will need to add a line of code in your form
`<input id="hidden" type="hidden" name="_method" value="patch">`

The value attribute is taking the patch block from you controller and applying the changes to the parameters are there to be modified.


Lastly DELETE:

There might be a time that you want to get rid of a social media post, and I bet there is something on your facebook, or Instagram you want to get rid of. 

```
delete '/some_route/:id do
  #some block of code
	#some redirect for after the delete operation is fullfilled
end
```


There is so much more I can cover in what Sintara has taught me, but the most important thing I took away from this is RESTful routes









