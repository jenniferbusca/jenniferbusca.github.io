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

6) Click on "Credentials", enter a name and under the "Authorized Redirect URI" section, add in the url that will be redirecting to your the Google callback url. For example, 	http://localhost:3000/auth/google_oauth2/callback since I am running this on a localhost. Hit "Save"

7) Go back to "Credentials" and click on "Create Credentials" and select "OAuth Client ID" from the dropdown, then select Web Application and hit "Create". Save the client id and client secret for later.

![Imgur](https://imgur.com/S3vObVi)
