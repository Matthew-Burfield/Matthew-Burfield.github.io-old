---
layout: page
title:  "Marvel App"
modified:
categories: project
excerpt:
tags: [JavaScript,React,Redux,React-Router]
image: 
  feature: marvel-app.jpg
  thumb: marvel-app.jpg
date:   2017-05-01 20:02:16
demo: https://matthew-burfield.github.io/marvel-app/
gitrepo: https://github.com/matthew-burfield/marvel-app
---

# About Marvel App

This Marvel App lets users search the database of all the marvel characters in the marvel universe to find out more information the character, including a description (if available) and the first comic that character appeared in as well as a list of comics that they appeared in sorted by year published.

# The Project

This project was part of the recruitment process for Rex Software. Their requirements were to construct a JavaScript application that allows users to explore the objects of the Marvel API and their relationships in a meaningful way.

The exact functionality was up to me to design, but there were limitations on style of code.

1. The Application must respond to mobile.
2. Must be able to traverse navigation history with the browsers back/forward buttons.
3. Must avoid treating the DOM as your application's state. Do note share data on DOM elements.
4. Avoid spaghetti code:
  4.1. Ensure your code is decoupled
  4.2. Use some kind of application architecture (e.g. Redux, Flux, MVVM, MVC etc)

And there were further restrictions:

1. You must not use a "full" framework in your implementation (e.g. Angular, Ember, Vue). We consider a full framework to be one that addresses multiple concerns: you can use a View library like React, but you cannot use a MVVM library like Vue.
2. You must not use jQuery or equivalent.
3. If you are familiar with the React ecosystem, you may use React, Redux, React Router and/or any other libraries from the ecosystem to complete this test - this is in line with the stated rules.
4. Note, you are free to use any libraries that you like as long as they are single purpose e.g. routing, templating, ajax requests.

Obviously I used React to build this solution, since I had already been developing in React for some time. I hadn't used Redux or React-Router v4 before though, so they were both new to me.

Overall I found the project to be really fun to do. I smashed it out relatively quickly (over the weekend) which I think is a sign I'm getting more and more comfortable with the React ecosystem.

The other thing I did differently this time as opposed to previous projects is that I didn't start with create-react-app and instead configured my own webpack configuration and pulling in all the modules I needed from scratch. Which was actually pretty fun and I plan on starting from scratch more often so I can get much more familiar with the tools that otherwise get abstracted with create-react-app.

# Problems I had to overcome

The first big issue I has was with React-Router, 90% of the app was a delight to use with the new version of React-Router. It was easy to pick up and implement. I originally started building a single-page app that didn't use routes. But quickly brought in React-Router because I knew I needed to be able to use the browsers back and forward buttons to navigate history.

One thing that took me hours to figure out how to do was to navigate to a new route upon submitting a form. I wrapped the search box on the landing page inside a form. This improves the user experience because the user can simply type something into the input box and then simply press the enter key initialise their search (i.e. the don't *have* to press the submit button)

This was hard.

React-Router has a convenient Link HOC (higher order component) that wraps anchor tags and easily navigates to the page that you specify with the "to" parameter that gets passed in.

Basically I wanted something similar with Form, but couldn't find one anywhere. I ended up writing my own HOC for form after stumbling around for ages trying to implement other peoples versions, or figure out how other peoples versions worked. Come to think of it, I probably should have just looking inside the React-Router implementation for Link, but I didn't think of that at the time.

# Another issue

Another issue I stumbled through was transitions. I really wanted to use my CSS transitions which gave the app some life and polish.

Traditionally, using CSS transitions in single-page apps has been relatively easy because I can just create action handlers that add/remove particular CSS classes, which initiate CSS transitions.

The issue was with using React-Router, I was actually mounting and unmounting entire components, so I couldn't just update the CSS had have the transactions work.

My solutions, although a bit hacky, was to have another HOC that surrounded the component that I wanted to transition, and give it the params of the class that needed to be added or removed to apply that transition. Then it would set a timeout for 100ms, (enough time for the component to be mounted) and then apply add or remove the class after the timeout.

This allowed the component to be mounted, and then the relevant classes were added/removed to enable the transitions that you see while navigating through the app.

Overall I think the effect looks really nice.