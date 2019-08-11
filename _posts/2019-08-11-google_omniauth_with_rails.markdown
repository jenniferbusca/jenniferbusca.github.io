---
layout: post
title:      "Rails Project: Google Omniauth with Rails"
date:       2019-08-11 00:44:03 -0400
permalink:  google_omniauth_with_rails
---


For this project, I decided to create an app called Travel Buddy that helps with scheduling all of the activities that you have coming up in your trip. One of the requirements was using some form of OmniAuth and I decided to use Google.  Setting up your app to login with Google OmniAuth is a bit tricky, but it's worth it since it makes the user's sign in process seamless.

## Google Developer console
1) Go to https://console.developers.google.com/api and click on the dropdown next to the Google API logo.

2) Select "New Project"

3) Type in the name of your project and submit

4) Open new project and click on "OAuth consent screen" on the left hand side

5) Enter your application name, email address and hit "Save"
![Imgur](https://imgur.com/okyZj40.png)

6) Go to "Credentials" and click on "Create Credentials" and select "OAuth Client ID" from the dropdown, then select Web Application. Under the "Authorized Redirect URI" section, add in the url that will be redirecting to your the Google callback url. For example, http://localhost:3000/auth/google_oauth2/callback since I am running this on a localhost. Hit "Create". Save the client id and client secret for later.
![Imgur](https://imgur.com/TsniQWA.png)

## Gemfile
In your gemfile, insert the below gems, then run `bundle install`.

`gem 'omniauth-google-oauth2'`

`gem 'omniauth'`

`gem 'dotenv-rails'`

## Initializers
In  `config/initializers/omniauth.rb` , add the following:

```
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :google_oauth2, ENV['GOOGLE_KEY'], ENV['GOOGLE_SECRET'],
  callback_path: '/auth/google_oauth2/callback',
end
```

Since this is a test app, I decided to bypass a couple security checks and used the below additional options:
 
 `provider_ignores_state: true` - this ignores CSRF failures
	
	`skip_jwt: true` - this ignores JWT failures
	
## .env File
In the root folder, create a file called `.env`. Inside this file, insert your Google key and secret from the credentials that we created earlier:
```
GOOGLE_KEY = your google key here
GOOGLE_SECRET = your google secret here
```

Be sure to add this file to your .gitignore file to avoid your keys and secret from being published!
	
##  Users Table

To your `:users` table, add the following columns as strings:

`google_token`

`google_refresh_token`

`image`

## Routes
	
In `config/routes.rb`
	
` get 'auth/google_oauth2/callback' => 'sessions#googleAuth'`

` get 'auth/failure', to: redirect('/')`

## View

 In your view for your app's login page, you can use to below link_to, to initiate the Google Omniauth login process:
 
 `<%= link_to "Login with Google", 'auth/google_oauth2/' %>`
 
## Sessions Controller

In `app/controllers/sessions_controller.rb`, add:

```
def googleAuth
   @user = User.find_or_create_by(uid: auth['uid']) do |u|
     u.name = auth['info']['name']
     u.email = auth['info']['email']
     u.image = auth['info']['image']
     access_token = auth
     u.google_token = auth.credentials.token
     refresh_token = auth.credentials.refresh_token
     u.google_refresh_token = refresh_token if refresh_token.present?
     u.password = SecureRandom.urlsafe_base64
  end
  YOUR LOGINS AND REDIRECT HERE
end
```
	
You should also have the below `private` method:
	
```
def auth
  request.env['omniauth.auth']
end
```
	

	
	
