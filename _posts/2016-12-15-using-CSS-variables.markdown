---
layout: post
title:  "Using CSS variables"
date:   2016-12-15 20:02:16 +1000
categories: CSS JavaScript30
---
Just finished the 3rd tutorial in the JavaScript30 series (30 tutorials in 30 days by Wes Bos).

I want to capture what I learnt in the tutorial as a reference for myself.

In the tutorial, we created three CSS variables under the :root element of the CSS stylesheet, updated the three variables in JavaScript based on various HTML inputs.

Creating the variables in CSS was relatively easy, they were created under the :root element like so:

```css
:root {
  --base: #ffc6BB;
  --spacing: 20px;
  --blur: 10px;
}
```

Obviously the three variables here are called base, spacing and blur. The -- before the variable name is what indicates a variable in vanilla CSS and the values specified here indicate the default values given to the variables.

Variables are then used within the stylesheet like so:

```css
.className {
  color: var(--base);
  padding: var(--spacing);
  filter: blur(var(--blur));
}
```

Next up was then to update the variables in JavaScript. The main line used to do this was to update the documentElement.style like so:

```javascript
document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
```

documentElement returns the Element that is the root element of the document. For example, the <html> element in this case.

When we defined the CSS variables under the :root, those elements were added to the html tag. So by setting the document.documentElement.style.setProperty, we're really just updating the style attribute of the <html> tag.

This is the final JavaScript we used in the tutorial:

```javascript
const inputs = document.querySelectorAll('.controls input');

function handleUpdate() {
  const suffix = this.dataset.sizing || '';
  document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
}

inputs.forEach(input => input.addEventListener('change', handleUpdate));
inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
```

As a side note, Wes explained that the document.querySelectorAll doesn't actually return an Array, it instead returns a NodeList which is very similar, except it's prototype doesn't have as many of the properties and methods as the Array prototype.

Everything else was pretty straight forward, the inputs are listening for the change and mousemove events. 

The change event isn't enough, because the event will only be involked when the input slider has changed and the mouse button is released. Not when the mouse button is pressed in and currently sliding.

The variables aren't updated when only hovering over the inputs though, because there is obviously no change in input values unless the mouse button is also being pressed down.