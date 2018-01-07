---
layout: page
title:  "Voting App"
modified:
categories: project
excerpt:
tags: [JavaScript,React,OAuth 2.0,React-Router,NodeJS,Express,Mongo]
image: 
  feature: voting-app.jpg
  thumb: voting-app.jpg
date:   2017-12-20 20:02:16
demo: https://fcc-voting-app.surge.sh/
gitrepo: https://github.com/Matthew-Burfield/FCC-voting-app
---

# About The Voting App

The voting app is a full stack app that allows a user to vote on different polls shared by their friends. Users are able to create an account and create polls that they can save as a draft, or publish and let the public vote on them.

# Project Requirements

The following user stories were used as requirements for this project.

1. User Story: As an authenticated user, I can keep my polls and come back later to access them.

2. User Story: As an authenticated user, I can share my polls with my friends.

3. User Story: As an authenticated user, I can see the aggregate results of my polls.

4. User Story: As an authenticated user, I can delete polls that I decide I don't want anymore.

5. User Story: As an authenticated user, I can create a poll with any number of possible items.

6. User Story: As an unauthenticated or authenticated user, I can see and vote on everyone's polls.

7. User Story: As an unauthenticated or authenticated user, I can see the results of polls in chart form. (This could be implemented using Chart.js or Google Charts.)

8. User Story: As an authenticated user, if I don't like the options on a poll, I can create a new option.

# Improvements That Can Be Made

There is a lot that can be improved on with this app, and it's hard to make that decision on how much longer to I spend updating and refining this app vs starting on the next project.

I'm not very happy with the final look and feel of the app and I think I could improve the design a lot, however at the same time, I've learnt so much in building this app that I feel ready to take the learnings from this project and apply them and build on them in my next project.

The server and client work really well together, however the front-end doesn't really handle error messages very well, like if the user tries to create a poll and isn't logged in - the app will just hang after the network request comes back with an error.

I think the form works pretty well though and was able to use to same form component for creating, editing drafts, and adding new poll options which I though was pretty neat.

The view published poll page leaves a lot for improvement, in the end I just chucked in a basic delete and add new poll options buttons to get the functionality working. Similarly the voting options could be layed out better.

I wanted to also add polish around the pie charts, hover effects and matching up colors to poll options.

One thing that is kind of preventing me from making improvements is that I had to change a lot in the build step to deploy the project. The front end was deployed to surge.sh and the backend to Heroku. Now if I want to continue to work on the project, I have to change it all back which is tedious. This could have been prevented by setting up a continuous integration method early into the project.

# What I Liked About This Project

I actually started this project twice, this was the second attempt. In the first attempt I started with the front-end framework first, passing in mock objects to display, and I actually found that really hard to do, constantly changing the mock objects as I realised additional properties that they needed. In the second attempt I started with the server first, creating all the API end points and using postman to validate them. I found this much easier as it forced me to get the database objects correct from the start.

This project took me 6 months to finish! I was stuck on authentication for a long time. I wanted to use auth0.com which is an authentication as a service which allows me to outsource the security aspect of the site which makes me feel better. This was my introduction into JWT tokens and how to create and handle them, and also I was able to set up one click authentication (logging in with facebook, google plus or twitter) which was something that I wanted to achieve.

Being my first ever full stack app, I'm quite happy with the results, I've learnt a lot and have a strong foundation now that I can build on.

In my next project I'm going to branch away from create-react-app because I want access to the webpack config. I'm also going to setup CI right from the start, and concentrate a lot more on writing integration tests and end-to-end tests.

I'm going to stick with auth0.com now that I have that figured out, and I'm going to stick with express on the server and mongodb for the database. This will allow me to build on those foundations and learn new technologies that will help me grow as a full stack developer.
