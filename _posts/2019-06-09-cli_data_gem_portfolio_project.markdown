---
layout: post
title:      "CLI Data Gem Portfolio Project"
date:       2019-06-09 04:52:50 +0000
permalink:  cli_data_gem_portfolio_project
---

For this gem of a project, I decided to scrape the Bon Appétit recipe site for featured recipes and ingredients. Cooking is one of my passions so I thought that it would be a good subject matter to work on.

## Planning
I started by planning out what I wanted the gem to do: 
* Launch the program by typing in "recipe-finder"
* Upon launching the program, the user should be presented with a list of featured recipes
* A user can then select a recipe by typing in a number to get more details
* There should always be an option to quit the program or go back to the main menu
* Invalid input is handled properly

## Setup
Once I decided on the user flow for the gem, I worked on creating my [new gem with Bundler](http://railscasts.com/episodes/245-new-gem-with-bundler). This made setup super easy and created the folder structure along with all of the required files to create the gem. After that, I went to the recipe_finder.gemspec file to add in the required information and dependencies like Nokogiri for scraping the website and pry for testing. I also updated the environment file to include all of the required gems and files were included.

## Creating the methods
The methods for recipe-finder are organized among 4 files:
* **CLI** - this contains the methods that run the program
* **Scraper** - this contains the scraper class that extracts all of the CSS information from the Bon Appetit pages and creates new instances in the Recipe and Ingredient classes
* **Recipe** - this is the recipe class file that stores all of the recipes and the ingredients that they contain
* **Ingredients** - this class contains methods that store all of the ingredients and the recipes that they belong to

Building out the methods took up the bulk of the time on this project. I found that this project was really helpful in solidifying some of the concepts that I was uncertain of since I created the plan for how I wanted the gem to work. 

## Pushing to Github
I built out the bulk of my project locally before making my initial commit to Github.  Pushing to my Github repository took a couple of tries because I didn't have the correct email address set up initially. 

## Lessons learned
Overall, I really felt that this project was fun and I enjoyed working on a subject matter of my choosing since the concepts and relationships made a lot more sense to me.  Below are some of key take aways: 

* **Create methods initially with static data** - Creating the methods with the data that you want it to return helps make the concepts less abstract and also allows you to test functionality with real data. Once this is done,  you can swap in dynamic data within the solid foundation that you've already built.
* **Testing** - While this project didn't include any rspec tests, I found it really helpful to use pry to make sure that my assumptions the objects that I was working with were correct. Often when I was having trouble making a method work, it was because I thought an object was a string but it was really an array or something along those lines. This project also helped me get more clever about where to place the binding.pry to test the exact object that I wanted to. 
* **Take a break** - You'll eventually start spinning after being stuck on something for too long. Take a break, walk away, rest your mind and come back with a clear head.

