---
layout: page
title:  "Nightlife Coordination"
modified:
categories: project
excerpt:
tags: [JavaScript,React,OAuth1.0,NodeJS,Express,Mongo,Travis]
image: 
  feature: nightlife.jpg
  thumb: nightlife.jpg
date:   2018-01-07 20:02:16
demo: https://burfield-nightlife.surge.sh/
gitrepo: https://github.com/Matthew-Burfield/fcc-nightlife-client
---

# About Nightlife Coordination

The Nightlife Coordination app is a full stack app that allows any user to search a location to find all the restaurants in that area. The user can then click to say that they are going to a particular restaurant which gets saved. All other users can then see the total number of people going to that restaurant.

# Project Requirements

The following user stories were used as requirements for this project.

1. User Story: As an unauthenticated user, I can view all bars in my area.

2. User Story: As an authenticated user, I can add myself to a bar to indicate I am going there tonight.

3. User Story: As an authenticated user, I can remove myself from a bar if I no longer want to go there.

4. User Story: As an unauthenticated user, when I login I should not have to search again.

# Building the Nightlife App

The nightlife coordination app felt a lot easier to do than the previous voting app project. I think this was due to a combination of having already having the foundational knowledge that I build up doing the voting app, and this project having a smaller scope.

Right from the start I had a better workflow than previously with the voting app. I wasn't procrastinating thinking about which to do first (frontend or backend) - I now know from experience that I find doing the backend first easier and so jumped straight on that. I also made sure to utilise Travis-CI right from the get-go, which meant that while it took me a little while longer to get set up, it saved so much effort later on with deployments, and it's awesome to be able to have your app in a deployed state during development.

I also didn't use create-react-app for this project. I instead used a boiler plate called simple-react-app, which still has the setup for hot module reloading and a basic webpack config, but I actually had access to the webpack config without needed to eject. I'm going to continue to do this in the future as I like having access to webpack, and ejecting from create-react-app gives a huge convoluted webpack config which is quite hard to understand and feels like there's a lot of unnecessary stuff in there for what I need.

It took me a little while to figure out the data structure but in the end I decided on getting the restaurant data from the YELP api, and then when a user clicks on that they are going to a restaurant, only then is that restaurant id, along with an array of user id's saved to my Mongo database. When a second user says that they are going to a restaurant, my app will append that users id, to the array of users that already exist for that restaurant.

Something that wasn't technically a user story, but was mentioned in the FreeCodeCamp video, was being able to login with Twitter's authentication api. This uses Auth 1.0 and I was keen to get it working. When the user clicks that they are going to a restaurant, the user is automatically redirected to Twitter so they can log in. This gives my app a token that can be used to validate requests.

I'm not sure if I implemented this the best way, since there are a lot of redirects. Like 6 redirects between the client, my server, and the twitter api. First I need to get a request token and request secret from twitter, then I also get a oauth verifier token on a separate call, then I do a third call to twitter to finally get the user access tokens. And with the user access tokens, I still need to do another validation call to twitter every time I want to validate a user and get their user data.

Lastly, on the frontend I experimented with parallax. Which is an effect where some elements scroll at different speeds than others. I used this is two areas, one in the header where the scene with three people overlooking a night time city, the objects further in the back don't move as quickly as the objects in the front. And the second place I used it, much less subtly, was after you search for restaurants - a giant pizza and nachos plate that look to be part of the background scroll at a different speed than the restaurant data.

# Improvements That Can Be Made

Like always, there are always room for improvements. I could definitely do a better job at displaying the restaurant data - I did this bit last and quite quickly just to finish off the project. One thing I wanted to play with, is returning as part of the restaurant data, whether that person (if they are logged in) have already registered at a given restaurant or not. This way, it would allow me to change the clickable button from "Click to say you are going" to "I changed my mind, I don't want to go here anymore", as opposed to just having a "Count" button that increases or decreases. This wouldn't be two hard to implement, I would only have to update my API call when it is searching the Mongo DB to also do a check to see if the current user Id is in the list of userIds for each restaurant.

I would like to get validation on the best way to implement the twitter authentication, because that many redirects seems too many, and the documentation doesn't explicitly say whether that's right or not.

# What I Liked About This Project

I liked that I was able to knock out this project fairly quickly. Building on many of the concepts that I did in the voting app, I was able to build much faster doing these things a second time. It helped that I didn't get stuck on building the Authentication for 6 months.

I did what I said I was going to do at the end of the voting app by branching away from create-react-app and setting up CI from the start. I did have a go at building tests, however many of the tests I need to write for this project involve the twitter api which I think I'd need to mock? I haven't done that yet, nor have I done any end-to-end tests, although I still have time to do some.

This project took be two weeks to build, which is significantly faster than the voting app. I'm keen to build further on these technologies, although the next project is charting the stock market, so it's still probably going to be another single page app - so still no SSR.
