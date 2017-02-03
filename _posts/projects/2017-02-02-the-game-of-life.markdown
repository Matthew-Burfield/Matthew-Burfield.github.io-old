---
layout: page
title:  "The Game Of Life"
modified:
categories: project
excerpt:
tags: [JavaScript,React]
image: 
  feature: the-game-of-life.jpg
  thumb: the-game-of-life.jpg
date:   2017-02-02 20:02:16
codepen: https://codepen.io/Burfield/pen/QdmmJe
gitrepo: https://github.com/Matthew-Burfield/TheGameOfLife
---

# About The Game Of Life

The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970.[1]

The "game" is a zero-player game, meaning that its evolution is determined by its initial state, requiring no further input. One interacts with the Game of Life by creating an initial configuration and observing how it evolves, or, for advanced "players", by creating patterns with particular properties.

For more information, including the games rules. Please check out the [wikipedia entry][https://en.wikipedia.org/wiki/Conway's_Game_of_Life]

# Project Requirements

The following user stories were used as requirements for this project.

1. User Story: When I first arrive at the game, it will randomly generate a board and start playing.

2. User Story: I can start and stop the board.

3. User Story: I can set up the board.

4. User Story: I can clear the board.

5. User Story: When I press start, the game will play out.

6. User Story: Each time the board changes, I can see how many generations have gone by.

# Improvements That Can Be Made

Firstly, should be able to make my algorithm for calculating the next generation much more efficient. At the moment I'm just using for loops to loop through my two-dimensional array game board and for each square, count the number of active neighbouring cells.

I feel like this should be able to be optimzed in a big way.

1. I used objects inside each array item thinking I'd need to store more data in each square. But there is only an on/off state. A simple 1 or 0 would require less memory.

2. I also don't see why I should have to loop through the entire array. Many squares don't need to be updated since none of their surrounding neighbours are changing. I.e. they're just static squares. I'd love to be able to have each square simply watch for an event (their neighbours changing state) which would trigger them to update. This means I wouldn't have to loop through the entire array when only a third of the squares are actually changing etc.

3. I'd like to add a feature where I can easily add onto the game board specific configurations like gliders, glider guns, static items and oscillating items etc.

4. I don't like how I have to re-create the game board new generation. This can't be very efficient. Cloning an immutable array would surely be better. Would be interesting to test the speed differences for different sized game boards.

# What I Liked About This Project

I'm getting much better/more comfortable using the create-react-app tools now, and more am efficient.

I'm really surprised at how quickly I was able to finish the requirements for this project. Considering how long it took me to finish the Build A Recipe project - which felt like a grind.

I think this means I'm getting much more comfortable using React, and designing my components in the right ways.

I also started using eslint with airbnb rules for this project, which gives me more confidence that I'm writing my code to a high standard.

