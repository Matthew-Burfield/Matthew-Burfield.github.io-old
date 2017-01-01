---
layout: post
title:  "Finishing The Front End Developer Course"
modified:
categories: blog
excerpt:
tags: [CSS3,JavaScript,FreeCodeCamp]
image:
  feature:
date:   2016-12-29 6:02:16
---
### Free Code Camp

Today marks the day that I finished the Free Code Camp front end developer certificate. I'm really happy with my last project, a Simon game replica which I will talk about in a minute.

For the most part, the front end lessons have been pretty easy since I already knew most of what was required, and I probably would have been able to finish all the projects, without doing any of the lessons. I have however, learnt quite a bit from the lessons, and I can notice quite a difference in my code.

I think it's much cleaner now, and I'm starting to utilise much more helper functions, like the Map, Reduce, Filter functions of the Array for example.

Another example would be the approach I took to solve the Simon game. I think had I done this a few months ago, I would've been using `setTimeout()` functions everywhere. However with the knowledge I have now, I was able to come up with a much cleaner solution - using CSS animations and `animationed` event listeners.

Now that I've finish the front end certificate, I'm keen to continue on with the back end cert. This is where the fun begins for me!

### My Simon Game

My Simon game is hosted on CodePen at [http://codepen.io/Burfield/full/woLYVZ/](http://codepen.io/Burfield/full/woLYVZ/).

I had a few additional goals when I set out to create my Simon game

1. I wanted to use vanilla CSS3 and JavaScript code. I.e. no frameworks like AngularJS or jQuery, and no preprocessors like LESS or SASS.
1. Modularise my code
1. I didn't want to use any `setTimeout()` functions
1. I wanted to be proud of my work

I've accomplished my goals, and I'm really happy with the final product.

### Using CSS Animations and Transitions

This was my solution to animating the Simon game button clicks, and revealing the computer sequence. I got stuck for a while using CSS transitions and ended up looking on the Free Code Camp forums for some help. This is when I realised that pretty much everyone else were using `setTimeout()` functions in their code to animate their Simon games.

This game me more determination to persevere with my solution. In my opinion, using Transitions and the `transitionend` event listener looked cleaner and I was determined to get it working.

### Issues and Limitations with Transitions

The main limitation I had with transitions, is that I didn't have as much control over the timing of the transitions, and the wait time between each transition.

I needed some wait time inbetween each transition, to make the animation sequence look nice. Ideally, I would like the transition to scale the game shape a bit bigger on click, then hold that scale for a second, before snapping back to the original size, waiting another few miliseconds, and then continuing on to the next sqeuence.

Unfortunately with the transition, the only controls I had were the transition time, and the delay time. So I could delay the transition from starting, which kind of worked, at least there was wait time inbetween each transition, and I could increase the length of the transition, which also kind of worked, but it made the game look unpolished and clunky, as the transitions were slow moving and not snappy like I wanted.

### Animations to the Rescue

Animations solved my problem. Animations get defined in CSS and it gives you more control of what transforms happen at each point throughout the animation. I.e. I can scale the image in the first 5% of the animation, and then hold that scale for the rest of the 95% of the animation. This alone made the while animation much better than using transitions. They look more snappy, while also giving the effect of having a delay between each animation.

Another added benefit of the animation, is that I can easily check the animation name when the `animationend` event is triggered.

```javascript
function gameButtonAnimationHandler(e) {
  transitionModule.removeTransitionClasses(this);
  if (e.animationName === "gameButtonPress") {
    // ...
  }
}
```

Here, within the this `gameButtonAnimationHandler` function, I can easily check the animationName before proceeding accordingly. This is a much cleaner scenario that what I had to do when using CSS3 transitions. Given that the `transitionend` event will be called after all transforms and transitions end, each game button in the sequence would have three `transitionend` events called. One for the increased width, one for the increased height, and one for the change in colour.

It wasn't too bad, as I could just check for a specific one and then proceed, so that my code would only be triggered once per sequence event. However there are two issues that arose when attemping that. Firstly, if I had any transitions on any other elements, the `transitionend` event would also trigger. I.e. if I highlighted a button on hover with a transition for example; and secondly, the code wouldn't trigger at all, unless the transition that I was listening for was the last transition called.

For example, I had three transitions. width, height and colour. Each would trigger the `transitionend` event after the transition finished. Depending on which order they were in in the CSS, would depend on the the order of the transitions occuring. However, everything would come to a grinding holt, unless the check that I was making to ensure the code wasn't being called for each transition, was the last transition to end.

I wasn't very comfortable with this, and could envision problems. I didn't test it too much, because I found the animation solution which solved this problem. But it felt like a bit of a hack. The animation solution is much better, and feels cleaner. All the different transitions are now encapsulated within one animation.

### Modularising My Code

Due to the prototype nature of JavaScript, there are no Classes. Modules are a means to keeping units of code for a project cleanly separated and organised.

I'm really proud of is how I've modularised my code. Unfortunately, JavaScript doesn't have a standard way to do this, and so there are a number of different solutions that probably all have their strengths and weaknesses. I haven't looked too much into why I might use different ways of modularising for different scenarios yet, I just wanted to decouple as much of my code that I could, and leave the main.js looking as clean as I could.

After looking on numerous sites to try and find how to do this, I finally found the book [Learning JavaScript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript) by Addy Osmani.

It had a good reference for creating Modules in JavaScript, and also explained about different ways to do it. For now, I just chose the way that looked the nicest to me, but I plan on reading this book cover to cover.

### End

I think that's all I wanted to say about Simon game for now. I plan to post my solution to the Free Code Camp forums, so I might have something else to write about after my code has been peer reviewed.