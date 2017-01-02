---
layout: post
title:  "CSS3 and Flexbox"
modified:
categories: blog
excerpt:
tags: [CSS3,JavaScript30,Flexbox,Transitions]
image:
  feature: css3-and-flexbox.jpg
date:   2017-01-02 6:02:16
---
### JavaScript30 tutorial 5

So I just finished the 5th tutorial in the JavaScript30, 30 day vanilla JS coding challenge. Created by [https://javascript30.com/](Wes Bos)

The challenge is titled 'Flex Panels Image Gallery', and is heavily based on using flex in CSS. There is only a tiny bit of JavaScript in the form of a couple of event listeners to tie it all together.

So I'd never seen flexbox before, and admitably, this tutorial only touched the surface, but I'm really liking what I'm seeing so far.

This is the end result of the tutorial can be seen on [http://codepen.io/Burfield/full/YNKOzR/](CodePen)

What we created was a series of 5 images that are all aligned horizontally across the screen and take up the entire vertical height of the browser window.

Each of those images, we refer to as a panel, and contain the panel class.

Inside each of the panels, we have three paragraph elements that contain text.

When we click on a panel, that panel expands using CSS3 transitions, and then the top and bottom text transition in aswell.

Finally, clicking on that panel again causes the panel to return to it's original state.

### Let's have a look at the code

First let's look at the CSS for our panels class.

```css
.panel {
  /* additional irrelavent properties */
  transition:
    font-size 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
    flex 0.7s cubic-bezier(0.61,-0.19, 0.7,-0.11),
    background 0.2s;
  flex: 1;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
}
```

Okay, so firstly I we put in the `display: flex;` propertly. This creates the flex box around our panels. By default, the flex boxes are stacked vertically.

This is why we added the `flex-direction: column;` property. This changes to flex boxes to be stacked horizonally (in columns).

`flex: 1;` is important, without it the flex boxes only use the amount of space that they need to use. So in this case it was only the length of the text. `flex: 1;` added to all of the flex boxes means that all of the flex boxes are split equally across the screen. We'll revisit this again later.

I also wanted to mention the transition, I didn't realise transitions could be written this way, all grouped under the `transition:` but it makes it way more readable. The cubic-bezier transition is also really cool. It makes the flex box get bigger, and then has this effect at the end where it snaps back. View it and see for yourself. I like the effect though.

### Nesting flex boxes

Flex boxes can be nested within other fex boxes. An example of this is the flex boxes surrounding the paragraph elements within the panels.

```css
.panel > * {
  margin:0;
  width: 100%;
  transition:transform 0.5s;
  border: 1px solid red;
  flex: 1 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

Here the `.panel > *` means to apply these styles to each of the child elements of the panel class. I.e. the three paragraph elements.

Notice that we've made these paragraph elements flex boxes as well by adding `display: flex;` to each of the child elements of the panel class. Adding `flex: 1 0 auto;` aligns the paragraph elements vertically.

### JavaScript

There isn't a lot of JavaScript used. We just add a couple of event handlers. On the `.panel` click event, the flex box is given the property of `flex: 5`. 

Remember earlier how we gave all the panels a `flex` property of 1? Well by giving a specific panel a `flex` property of 5, what we're saying is that that flex box is going to be 5 times the size of each of the other flex boxes.

All of the other flex boxes then get scaled accordingly.

One thing what was pretty helpful was this line:

```javascript
this.classList.toggle('open');
```

In a previous project, I was doing a conditional check to see if the classList included a specific class, if it did that I would remove it, if it didn't then I'd add it. Toggle is a much cleaner way to do that.

### End

I really enjoyed this tutorial. It gave me a glimpse into the power of using flex box. And I know I definitely need to look into flex box further.