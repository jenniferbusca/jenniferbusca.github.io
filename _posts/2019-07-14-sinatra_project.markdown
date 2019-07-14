---
layout: post
title:      "Sinatra Project"
date:       2019-07-14 09:43:08 -0400
permalink:  sinatra_project
---


For this project, I decided to build an app that allows users to track their favorite and completed hikes as well as create a new hike using Sinatra and Ruby.

## Planning
I started  by planning out what my models should look like and the type of associations that columns would be needed for the task.  Since a user could have many trails but a trail could also have many users, I had to use a has_many :through relationship and create a user_trails model. At this point, I double checked that my ideas met all of the project requirements. Here's what I initially had scoped out: 
![Imgur](https://i.imgur.com/J3AdQ5e.png)

## Implementation
1. **File Structure:** Once I had all of my ideas sketched out, I started building out the file structure. I did it from scratch, but there's a gem called  [Corneal](http://thebrianemory.github.io/corneal/) that makes it much easier. It even includes some pre-canned styling to help get you started. 
2. **Gems**: I made sure to include any gems needed in my gemfile such as Rake, Sinatra,ActiveRecord, SQLite3, shotgun and bcrypt. 
3. **Create Tables:** Since I had my columns planned out, it was easy to build migrations using Rake.  I created users, trails and user_trails tables.
4. **Initial Commit:** Once I had my basics setup, I created my Github repository and started committing.
5. **MVC**: Once all of the setup was completed, it was time to start building out my models, views and controllers. This took up the bulk of my time on the project. Thankfully there is some really great Rails documentation on [ActiveRecord ](https://guides.rubyonrails.org/active_record_querying.html)
6.  **Styling:** I found CSS a bit challenging to get the hang of. It's not very intuitive but [W3schools](https://www.w3schools.com/css/) and [CSS-Tricks](https://css-tricks.com/) are pretty great resources. As annoying as CSS is, it's really powerful and incorporating it into my project really helped to fine tune the appearance of my pages.

## Lessons Learned
* **Office hours and/ or pairing!** Even if you feel like your code is in a good place, it's good to run it by someone else. There could be an easier way to do something you've coded!
* **Planning** Planning out what my tables would need and what my pages should have on them helped me tremendously. 







