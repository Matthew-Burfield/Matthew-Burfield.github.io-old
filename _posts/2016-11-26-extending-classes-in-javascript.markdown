---
layout: post
title:  "Extending Classes in JavaScript"
date:   2016-11-26 20:02:16 +1000
categories: jekyll update
---
I found an awesome article that explained JavaScript inheritence in a way I could understand, and had a great example that worked brilliantly.

What I wanted to do, was define a class in JavaScript that had some properties, and then have another class that extended the first class. The extended class would inherit some properties from the first class, and then have some additional functions.

For a bit more context; this came about while developing my latest project. The Tic Tac Toe game. I have a 'Player' class that is for a human player, it stores the player name, and which token they're using (X or O) and does a few error checks (i.e. to make sure a player can only have a token of X or O, and not any other characters for example.)

Now I want a ComputerPlayer class, that still has the same properties and error checks, but also has some additional functions that are only relevant to a computer player. I.e. making a move etc.

This is my Player class:

{% highlight javascript %}
function Player(playerName, playerToken) {
  this.name = playerName;
  this.token = playerToken;
  if (this.token !== "X" || this.token !== "O") {
    throw new "Player token must be X or O"
  }
}
{% endhighlight %}

When I create the ComputerPlayer class, I can re-use the contructor of the Player class by using the call() function:

{% highlight javascript %}
function ComputerPlayer(playerToken) {
  Player.call(this, "Computer", playerToken);
}
ComputerPlayer.prototype.move = function() {
  // code here.
}
{% endhighlight %}

By calling Player with the ComputerPlayer's this object, and passing in the other arguments of the Player constructor, we negate the need to repeat the code in the Player constructor.

Note that I don't need to assign the prototype of the 'ComputerPlayer' to the 'Player' prototype in this case, because I don't need the 'ComputerPlayer' to inherit any functions assigned to the prototype of the 'Player' class.

Read the full article at A Drip of JavaScript: [Basic Inheritance with JavaScript Constructors][article-link]

 [article-link]: http://adripofjavascript.com/blog/drips/basic-inheritance-with-javascript-constructors.html
