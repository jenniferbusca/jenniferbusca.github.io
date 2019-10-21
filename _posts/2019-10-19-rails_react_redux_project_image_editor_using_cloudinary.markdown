---
layout: post
title:      "Rails/React/Redux Project: Image Editor using Cloudinary"
date:       2019-10-19 14:20:07 -0400
permalink:  rails_react_redux_project_image_editor_using_cloudinary
---


For my Rails/React project, my final project at Flatiron, I decided to build a photo editing application called 'Pixelate' where a user can upload an image, apply an image filter and save it. This was a bit of a challenge and took longer than any of my other projects to complete. In order to upload and store images, I used Cloudinary. Setting up Cloudinary was a bit tricky and I used it both on the frontend for image uploads and transformations and on the backend to upload images via the Cloudinary API. 


## Rails Api
A few setup details for the Pixelate Rails :
1. I'm only using Rails as an API here and using a Postgres database
2. In the Postgres database, there are two tables - `Images`  and `Users` . A user `has_many` images and an image `belongs_to` a user. In Images, I'm storing a reference to the `user_id` , `image_info` which holds all of the image details from Cloudinary and `transformations` so that I can save any changes to image filters that a user has made.  
3. I'm using Fast JSON API to serialize the data so that I can easily fetch it in my React frontend.

## Setting up Cloudinary
1. Create a [Cloudinary account]https://cloudinary.com/users/register/free).
2. Once you've got an account set up, you'll need to take note of your Cloud name and key and also download your YML file. You'll be using the cloud name in your Cloudinary widget and the YML in your Rails API setup
![Imgur](https://imgur.com/1LR0yA0.png)
3. Create an unsigned preset
* Go to your account settings > Scroll to "Upload Presets" > Click on "Add Upload Preset"
* Make sure signing mode is set to "Unsigned" and Save
    
## Cloudinary and Rails
1. Go to your Gemfile and add the below, then run `bundle install` or follow the [Cloudinary documentation](https://cloudinary.com/documentation/rails_integration#installation) instructions.
```
gem 'carrierwave'
gem 'cloudinary'
```
2. Place the YML file that you downloaded in the config folder of your Rails application. This should be all you need to do on the Rails side in order to get Cloudinary working.

## Cloudinary and React
On the front-end, I used Cloudinary in two ways. First I used their [upload widget](https://cloudinary.com/documentation/upload_widget) to easily upload images to their API and then I used the `cloudinary-react` library to wrap my image objects to easily manage.

### Cloudinary Widget Setup
1. In your index.html file, place the following script tag:
`    <script src="https://widget.cloudinary.com/v2.0/global/all.js" type="text/javascript"></script>`
2.  Then create an ImageUploader component.
![Imgur](https://imgur.com/X7nrpTb)
* In the render, we're rendering a button that `onClick` runs the showWidget function. This function then uses Cloudinary's `openUploadWidget` function which contains your CloudName and API key details that you saved from earlier.
* We're then calling `handleSubmit` to take the response from the Cloudinary upload using our an the action `this.props.postImages` to post the image data to our Rails API.  
![Imgur](https://imgur.com/39f94B2.png)
You should now have data from your upload saved to your database.

### Using the Cloudinary React SDK
I'm using the Cloudinary React SDK when displaying Cloudinary objects in my app and also to manage the image filters that a user has selected.
1. To start, run `npm install cloudinary-react`
2. You'll then have to import the cloudinary library within any components that will be displaying images.
 ![Imgur]https://imgur.com/ftXRMQI.png)
 * Here I'm rendering a list of all images that belong to a user. I'm using `Cloudinary Context` to reference my CloudName(you'll have to add your cloudName in here)
 * I'm then using `Image` and the `publicId` property that belongs to the Cloudinary Image object to dynamically populate all images in the list.
 * Lastly, I'm using `Transformations` to apply any transformation effects (more on this in a second). 
 
#### Cloudinary Transformations
Aside from the image upload solutions that Cloudinary has, they also have transformations which allow you to add a large number of filters and effects to your images.  I'm using the `Transformations`  `effect` property in the Image List to update how the image is rendering to the user. 
 ![Imgur]https://imgur.com/eWvKTuV.png)
 * I created a short list of filters that I wanted to include in my app using key:value pairs of the name that I want to display in a dropdown and the value that I want to dynamically send to the `Transformations` `effect` property.
 * I'm then mapping over the options to populate them in the dropdown.
 ![Imgur]https://imgur.com/UTtuuYc.png)
 
## Conclusion
There were a lot of moving parts to this project and this blog post is really just touching on one aspect of it. Cloudinary is a really useful and powerful tool once you get the hang of it.



