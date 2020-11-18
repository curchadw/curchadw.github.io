---
layout: post
title:      "Real Estate Listing App"
date:       2020-11-17 23:06:35 -0500
permalink:  real_estate_listing_app
---


I will admit that this particular project really got my nerves going just because of the nautue of this particular project. Its not perfect in anyway, but I learned a lot from it. This project really showed me how fullstack really works as there is a lot of coordination when it comes to data moving from the frontend to a rails backend api.

My project is bascially a real estate listing app. It tell's you the owner, address, the agent, sale price etc. for property listings. It gives you two forms. One for you to create an owner, and one to create a property and associate with an owner you created. When you look at the JSON file that the request are being sent to, you'll see data setup like in this example. 

```
{
  "exampleName": "John",
  "exampleName2": "Doe",
  "age": 30
}
```
Data in a JSON can expand out to more complicated trees

The question is how are he retriveing this data to display on the frontend?

Asynchronous Programming-------

Imagine you are clicking something in your browser and you have to wait for it to respond......well what if you had that also caused other operation outside of the browser to stop as well.....That would not make a great user experience in the slightest bit. Basically Asynchronous prorgamming the make your code work without interupting other processes going on.

In my project I have a form setup to create an owner. 


```
 <form id = "owner_form">
        <div>
          <label for='name'>Owner Name:</label>
          <input type='text' id='name' name='name' placeholder="John Doe" />
        </div>
        <div>
          <label for='phone_number'>Phone Number:</label>
          <input type='text' id='phone_number' name='phone_number' placeholder="Phone Number" />
        </div>
        <div>
          <label for='real_estate_agent'>Listing Agent:</label>
          <input type='text' id='real_estate_agent' name='real_estate_agent' placeholder="Agent"/>
        </div>
        <div>
          <input type='submit' id='owner_submit' value='Submit'/>
        </div>
      </form>
```

When the form is submitted.....I am running a function that is asynchronusly requesting a http request on form submission that 'POST' or creates the owner on the backend onto a JSON file, and I confirm with a console.log on the front to make sure the new resource was created.

 


	**The fetch function takes one mandatory argument, which is the path to the resource you want to fetch and returns a Promise that resolves to the Response of that request.**
	
	
>  	Armando Amador, How to make HTTP requests using Fetch API and Promises


My config object contains the payload on what I what to send to the back to get created.....In food ordering terms....you are placing an order and you are telling them what you want from McD's. In this case, My OWNER_URL is my menu.



```
const config ={
    method: 'post', 
    body:JSON.stringify(owner),
    headers: {
      "Accept": "application/json",
      "Content-type": "application/json"
    }
		

   
  }
  fetch(OWNERS_URL, config)  <----placing order
  .then(resp => resp.json()) <-----Your promise (like a food pager for when your order is ready)
  .then(resp =>{
    console.log(resp)<---------at this point, you either get your food or not.(resolved or rejected)
  })
 }
 
```
 
 In terms of my project, I entered info in a owner form to be created, then it lets me know if it was successful
 
 
  That new owner is then added to a dropdown I created in another form I am making my listing. The only way that can happen is if I performed a GET request in a spearate function to retrieve everything in my owner db. After I perform my request, my promises come back and then I am given a response in the form of a added html element in my dropdown menu.
	
	
	```

	const dropdownMenu = () =>{

  const dropdown = document.getElementById('owner_id');
  dropdown.innerHTML= ' '
  fetch(OWNERS_URL)
  .then(resp => resp.json())
  .then(owners => {
    owners.forEach(owner => {
    dropdown.innerHTML += `<option value = ${owner.id}>${owner.name}</option>`
    })
    
  })
}
```









