---
layout: post
title:      "Javascript/Rails API Project: OO Javascript"
date:       2019-09-15 12:24:15 -0400
permalink:  javascript_rails_api_project_oo_javascript
---


For my Javascript/Rails project, I decided to make an app called "Wine & Dine" where you can find food and wine pairings.  I'm using Javascript on the front end to render objects to the DOM and on the backend I'm using Rails as an API where food, wine and pairing data can be accessed by the front end. 

I used an object-oriented approach for building out my Javascript front end since we'll be dealing with this in the next and final project using React. Coming from Ruby, object-oriented programming was familiar, but applying it to Javascript was a bit tricky for me to grasp initially so I'm going to dive into it a bit here. 


## Front-end vs. Back-end
The front-end refers to the client side of the application - the part that a user would see and interact with. The back-end is the server-side where data is stored. Working on my Javascript/Rails project, I created Food, Wine and Pairing classes on both the front and back ends. It seemed a bit repetative, but they each serve different purposes. In Javascript, much like in Ruby, classes are used to create objects and assign properties to those objects.  However there are some differences in how these objects are used and how the data is accessed.


## Classes

### Adapter Class
For my app, I created an Adapter class that holds all of my app's properties and any properties that I may want to refer to later without having to repeat code throughout the classes methods.  This includes elements from the DOM that I'll want to access or add to as well as any event listeners that I want to add to the page when an element is clicked or changed.
```
class Adapter {
  constructor(baseURL){
    this.baseURL = baseURL
    this.wineURL = `${baseURL}/wines`
    this.foodURL = `${baseURL}/foods`
    this.pairingURL = `${baseURL}/pairings`
    this.newPairingURL = `${baseURL}/newpairing`
    this.pairingDropdowns = document.getElementById('pairing-dropdowns')
    this.pairTypeSelect = document.getElementById('pair-type-select')
    this.wineDropdown = document.getElementById('wine-dropdown')
    this.foodDropdown = document.getElementById('food-dropdown')
    this.winePairings= document.getElementById('wine-pairings')
    this.foodPairings = document.getElementById('food-pairings')
    this.pairingList = document.querySelector('.pairing-list')
    this.addPairForm = document.querySelector('.add-pairing-container')
    this.newPairButton = document.getElementById('new-pair-btn')
    this.selectedPairings = document.getElementById('selected-pairings')
    this.addPair = false // displayForm
    this.submitButton = document.querySelector('.submit'
    this.formInputs = document.querySelectorAll('.input-text')
    this.foods = []
    this.wines = []
    this.pairTypeSelect.addEventListener('click', this.handlePairChange)
    this.pairingDropdowns.addEventListener('change', this.handleChange)
    this.newPairButton.addEventListener('click', this.displayForm)
    this.submitButton.addEventListener('click', this.handleSubmitForm)
    this.headerObj = {
      "Content-Type": "application/json",
      "Accept": "application/json"
    }
  }
```

If I want to access any of the properties above in other methods within this class, I've got to use the `this` keyword. For instance the following code has references to many of the properties in the class constructor above:
```
  handlePairChange = (event) => {
    this.pairingList.innerHTML = ``
    let selection = event.target.value
    if (selection == "food") {
      this.foodPairings.style.display = 'block' // 
      this.winePairings.style.display = 'none'
    } else if (selection == "wine"){
      this.winePairings.style.display = 'block'
      this.foodPairings.style.display = 'none'
    }
  }

```



### Food Class
In Ruby, my Food class looks like the following:
```
class Food < ApplicationRecord
  has_many :pairings
  has_many :wines, through: :pairings
end

```
and I can access all Food objects by doing `Food.all` or search for a specific Food object by doing `Food.find(:id)`.

However on the front-end, the Food objects and their properties are stored in an array so that they can be accessed later.  My Food class in Javascript looks like:
```
class Food {
  constructor({id, name, category}){
    this.id = id
    this.name = name
		this.name = category
  }
}
```
New Food objects are created by calling `new Food(properties)` and then the newly created food object is pushed into `foods=[]`. The objects in the Javascript Array can be accessed by calling the foods array or by a find method `foods.find(food => food.id === objectId)`

You'll notice the difference in the find methods between Ruby and Javascript.  Due to Ruby's syntactic sugar, the code is much simpler than Javascript. 

## Conclusion
This project really just touched on object-oriented Javascript capabilities. For more information on OO Javascript, you can visit [MDN OO Javascript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS)




