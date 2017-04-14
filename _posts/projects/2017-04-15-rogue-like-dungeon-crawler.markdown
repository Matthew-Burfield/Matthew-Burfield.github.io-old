---
layout: page
title:  "Rogue-like Dungeon Crawler"
modified:
categories: project
excerpt:
tags: [JavaScript,React]
image: 
  feature: rogue-like-dungeon-crawler.jpg
  thumb: rogue-like-dungeon-crawler.jpg
date:   2017-04-15 20:02:16
demo: https://matthew-burfield.github.io/roguelike-dungeon-crawler/
gitrepo: https://github.com/Matthew-Burfield/roguelike-dungeon-crawler
---

# About The Rogue-like Dungeon Crawler

The Rogue-like dungeon crawler is a game where the hero much navigate his way through a dungeon, killing all the monsters to gain experience and discovering items, and finally killing the boss to get the next level.

Each level instance is randomly generated based off a BSP Tree algorithm that I also wrote and can be found [here](https://www.npmjs.com/package/random-dungeon-generator)

# Project Requirements

The following user stories were used as requirements for this project.

1. User Story: I have health, a level, and a weapon. I can pick up a better weapon. I can pick up health items.

2. User Story: All the items and enemies on the map are arranged at random.

3. User Story: I can move throughout a map, discovering items.

4. User Story: I can move anywhere within the map's boundaries, but I can't move through an enemy until I've beaten it.

5. User Story: Much of the map is hidden. When I take a step, all spaces that are within a certain number of spaces from me are revealed.

6. User Story: When I beat an enemy, the enemy goes away and I get XP, which eventually increases my level.

7. User Story: When I fight an enemy, we take turns damaging each other until one of us loses. I do damage based off of my level and weapon. The enemy does damage based off it's level. Damage is somewhat random within a range.

8. User Story: When I find an beat the boss, I win.

9. User Story: The game should be challenging, but theoretically winnable.

# Improvements That Can Be Made

I spent a lot of time on this game, polishing the finish so it looked nice. I want to use it as a show piece for where I'm currently at with my coding.

That being said, there are a few things I'd like to improve, given the time.

1. It would be nice to pre-load all the images. I fiddled around with this a little bit, but couldn't get it working as I wanted it. The (very minor) issue is that when the hero first turns left or right, or you discover a new item or monster for the first time. Often the image with render as a black square for a split second, as the resource is downloading.

2. The game gets (in my opinion) fairly easy towards the end of the game when the player grows in level, and the items get better. I would like to increase the difficulty of the monsters in the later levels. This is super easy to do, but would require additional testing/play throughs of the entire game to ensure the game is still winnable.

3. I used a fair few CSS transitions in this project which make the game look more polished. I would like to add a few more - one when the going to the next level. Another when a weapon or shield is discovered/equipped.

4. I would like to fix the experience bar. The issue is, if you level up and have additional experience in the next level, instead of the experience bar CSS transitioning to 100%, then back to 0%, then up to the addition experience %, it just goes directly from point A to point B.

# What I Liked About This Project

It's interesting reading over what I learnt from my previous project, The Game of Life. So much of that stuff is just second nature now. create-react-app, especially after having to tweak the npm global install is not even mentionable now, it's that easy. Similarly to other tooling like eslint.

I was able to successfully implement a setInterval in this project, which is significant because that's really what I got stuck on with a previous fitness tracking project that I ended up abandoning for that reason. I'd like to have another go at it now.

I created my first ever npm package! That was a pretty awesome feeling, uploading it to npm and then doing an npm install of my own package. And not only that, but its also had 2,657 downloads in the past month! That's kinda wow!

I think I did a lot better in commenting my code for this project, as well as structuring/nesting my javascript files in an easy to understand way.
