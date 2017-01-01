---
layout: post
title:  "Event Listeners and Transitions"
modified:
categories: blog
excerpt:
tags: [CSS3,JavaScript]
image:
  feature:
date:   2016-12-22 20:02:16 +1000
---
Working on the Simon Game, which is the last project I need to finish to complete the front end developer certificate of Free Code Camp.

The game lights up one of four colours in a sequence, and then the player needs to repeat that sequence to proceed to the next level.

From what I've read in the forums, everyone else has been looping through their sequence array, lighting up the current colour in the sequence, then use the `setTimeout()` function to wait for a second, before looping to the next colour in the sequence and lighting it up.

The reason for waiting inbetween each sequence colour, is because otherwise the colours will look like they're all activating at the same time, and the player won't be able to distinguish the sequence.

My solution has been different to any that I've seen thus far. I've been using CSS3 transitions to transform the colours to be slightly larger and with a lighter colour when they're the current colour in the sequence. And then using an event handler to watch for the'transitionend' event which will trigger the next item in the sequence.

I'm not finished yet, but it's working pretty well so far.

One problem I've been having and could potentially stuff me up in other browsers, is that the transitionevent event handler needs to be watching for the final transition, otherwise it stuffs up when the same colour is twice or more in a row in the sequence.

For example, if my CSS3 transtition is increasing the size and changing the colour. Then there the transitionend event is fired three times per sequence item. The first time for the height, the second time for the width, and the third time for the colour.

The order is consistent, but seems to change based on the order they're defined in my CSS file which could render differently in different browsers which I'll have to check.

My CSS is just stock standard transitions. Here I've set the game squares to be 100px, and for each sequence item I add the class "current" which sets up the transition.

```css
.game-square {
  height: 100px;
  width: 100px;
}
.current {
  width: 110px;
  height: 110px;
  -webkit-transition-property: width height;
  -webkit-transition-duration: 0.5s;
  -webkit-transition-delay: 2s;
  -webkit-transition-timing-function: linear;
  transition-property: width height;
  transition-duration: 0.5s;
  transition-delay: 0.5s;
  transition-timing-function: linear;
}
```

Note that instead of using the `setTimeout()` function, I can simply add the transition-delay property to the CSS. This will have the same effect to the end user, as the transition will be delayed, and the next sequence item won't be effected until after the previous transitionend event is triggered.

```javascript
const gameSquares = document.querySelectorAll('.game-square');
gameSquares.forEach(gameSquare => gameSquare.addEventListener('transitionend', handleTransitionEndEvent));
```

Here I loop through all the the game-squares and add the transitionend event listener. On the transitionend, the function `handleTranstitionEndEvent() is called.

```javascript
function handleTransitionEndEvent(e) {
  // The transition has ended on this element, so we can remove the current class now
  this.classList.remove('current');
  
  // // This line is to make the class remove and re-add so the transition will run again
  void this.offsetWidth;
  
  /* We only want to call computerSequence once per element.
     Without this condition, transitionend is called for each transition
     I.e. transitions for width, height, color, size etc */
  
  if (e.propertyName === "background-color") {
      computerSequence();
    }
  }
}

function setupComputerTurn() {
  const nextMove = Math.floor(Math.random() * 4 + 1); // Pick a random number between 1 and 4.
  gameArray.push(nextMove);
  gameIterator = gameArray[Symbol.iterator]();
  computerSequence();
}

function computerSequence() {
  let currIterator = gameIterator.next();

  /* add the current class to sequence item which begins the transition */
}
```

A couple of points to note. The `void this.offsetWidth` is a line that I found on StackOverflow that 
will refresh the element once the current class has been removed. The only reason that's there,
is because if in a sequence there are two of the same colours in a row, then the class will get removed and then re-added
in JavaScript, but it won't be updated in the browser, so the browser doesn't see the class getting re-added and just
thinks it's been there the whole time, thus the transition isn't triggered again and the sequence comes to a grinding
halt.

The second thing to note is the interator obviously I'm not looking through the array that contains all the sequence data, but I am able to
store the iterator in a global variable that I can reference each time the transitionend event is fired. This is what allows me to
store where I'm up to in the current sequence.

Lastly, I know this is a third point, but it's probably just also worth noting the conditional `if (e.propertyName === "background-color")`, 
this is to ensure the `computerSequence()` function is only called once per transition. I.e. we don't want to call it three times,
once for the width transition, once for the height, and again for the background-color.

Interestingly, in chrome at least, if the transition that calls the `computerSequence()` function isn't the last transition that's run,
then the sequence comes to a halt.

I.e. if I were to have the conditional to check for the `width` property, and then the transitionend event was triggered for `height` and `background-color`, the sequence would break down. I don't know why this is yet.