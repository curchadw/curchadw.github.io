---
layout: post
title:      "What is Thunk"
date:       2021-01-28 18:22:59 -0500
permalink:  what_is_thunk
---


I will start with a very direct purpose of thunk. Thunk or redux-thunk is a middleware that is commonly used to allow async logic to interact with your redux stores. To have a foundational understanding of the async logic, we need to understand the synchronus data flow of redux first.

Here is a flow chart as I start to describe the data flow in parts.

![](https://i.stack.imgur.com/HiNWO.jpg)


Step 1: An action is dispatched when the user initiates some type of action on the page


Step 2: The reducer is called in its current state with the dispatched action of the previous step


Step 3: Thestore then notifies the view which is what the user is looking at.


Step 4: The view's state is updated based on the user's interaction


Where the async call takes place is between the action phase and the store portion of the flow chart. This is where the middleware is applied to the store when created.

```
const store = createStore(manageRecipes,applyMiddleware(thunk))
```

A good example of this concept being applied is when on instagram and you are scrolling and you are seeing new post or old post. when you are scrolling the scroll action is setting off a perpetual GET request the the backend or api. The scroll is the action initated by the user.

How does this look in code?

On your index javascript file you want to import your reducer file, then use either npm or yarn to install react-redux.

```
import manageRecipes from './reducers/manageRecipes';
```

Then you need to create your redux store on you index javascript file. Once you create it your reducer, and you middleware function are you arguments. Whatever middleware you are using is going to used in your applyMiddleware() method.




```
import 'bootstrap/dist/css/bootstrap.min.css';


const store = createStore(manageRecipes,applyMiddleware(thunk))

ReactDOM.render(
  
    <Provider store={store}>
    <App />
    </Provider>,
   
  document.getElementById('root')
);

```


There is a great deal of significance of the code above. Thunk middleware verifies if an action is a function and excutes it.  Firstly an 'action' is an object that carries a type and a optional payload or in other words some kind of event that is triggered by user interaction. Here is an example
```
{
  type: ADD_RECIPE,
  payload: recipe
}
```
Actions are returned  by functions called action creators that are housed within a directory called actions. Action creators are associated to a component of the developers choosing based on what they are doing and can call them through the props. 


I'm am going to use my POST request when a recipe is entered. Just assuming I have my reducers setup, I will be dispatching my 'ADD_RECIPE' reducer.

```
export const postRecipes = (recipe) => {
  
    const BASE_URL = `http://localhost:3001`
    const RECIPES_URL =`${BASE_URL}/recipes`
    const config = {
        method: "POST",
        body:JSON.stringify(recipe),
        headers: {
        "Accept": "application/json",
        "Content-type": "application/json"
     }
    }

    return (dispatch) => {
      
      fetch(RECIPES_URL,config)
        .then(response =>{ return response.json()})
        .then(recipe => { dispatch({ type: 'ADD_RECIPE', payload: recipe })
        
    })
    .catch((error) => console.log.error(error))
       
        
    };

    
    
  }

```

Then once the snippet above is executed, the info being fected from the api will render in the recipe prop below:
```
import React, {Component} from 'react';
import Recipe from './Recipe.js'
import '../index.css'

class RecipeList extends Component {



render() {
  
   const { recipes } = this.props
   let flex ='flexitems'
   return (
    
      
    <div>
      <div className={flex}>
          {recipes.map(recipe => <Recipe recipe={recipe} deleteRecipe={this.props.deleteRecipe} key={recipe.id} /> )}
      </div>
    </div>
   )
    
  }
}


```


This Async call goes off after the action is iniaiated by the user, and once reponse is settled, it'll update the state accordingly. 











