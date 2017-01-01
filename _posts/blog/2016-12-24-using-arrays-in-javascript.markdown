---
layout: post
title:  "Using Arrays In JavaScript"
modified:
categories: blog
excerpt:
tags: [CSS3,JavaScript,Javascript30]
image:
  feature:
date:   2016-12-24 20:02:16
---
### Array Cardio Day 1

Finished day 4 of the 30 day JavasScript tutorial series today. I started this tutorial earlier in the week but got distracted with other priorities and wasn't able to finish it until today.

Overall the tutorial was a good one and I learnt quite a few new things.

As the title suggests, we were getting more familiar with Arrays. In particular, using the filter, sort, reduce and map prototype functions of the array.

The map and filter function I was already quite familiar with, but one thing I did learn about were arrow functions.

### The Arrow Function

This is an example of using the Array's map function using a regular anonymous function

```javascript
const names = inventors.map(function(inventor) {
  `${inventor.first} ${inventor.last}`;
});
```
Here we're mapping the inventors array, which holds an array of inventor objects. Our mapped array will be an array of first name + last name strings, and saved into the names constant.

Note that we're also using ES6 here. By wrapping code up in back quotes \`, we're able to use the ${variable} notation. This is the equivalent to the code `inventor.first + " " + inventor.last;`

What I learnt is that we're able to do the exact same thing on one line using an arrow function.

```javascript
const names = inventors.map(inventor => `${inventor.first} ${inventor.last});
```

According to Modzilla Developer Network, "an arrow function expression has a shorter syntax compared to function expressions and does not bind its own this, arguments, super, or new.target. Arrow functions are always anonymous. These function expressions are best suited for non-method functions and they can not be used as constructors."

So an arrow function isn't going to always be the right way to go, but for small functions like this, the shorter syntax is nice. And I'm assuming it's faster if it doesn't need to bind its own this, arguments, super or new.target.

### console.table!

The other cool thing I learnt, was when you want to console.log an array of objects, the developer console will show you something like:

```
console.log(fifteen)
  - [Object, Object]
```

So, what we can do, is use console.table! The array of objects will be displayed in a beautiful table that's easy to view!

### Array.reduce()

Sort is a function that I thought I knew about but clearly didn't understand as well as I need to.

I knew that sort accepted a function with two parameters, usually labelled a and b like so..

```javascript
const reduce = inventors.sort(function(a,b) {
  // Reduce code goes here
});
```

I think I've used reduce before, but I never understood it's power or flexability. I probably still don't, but it's a little clearer now.

Modzilla Developer Network has this to say about the reduce function:

"The reduce() method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value."

I used the reduce function twice in this tutorial. The first time was to find out how many years did all the inventors live.

This was relatively easy, once I realised that in this case the parameter "a", would be the running total, and "b" would be the current item in the list.

Effectively, the same thing could be done with a for loop

```javascript
let count = 0;
for (var i = 0, i < inventors.length, i++) {
  count = count + (inventors[i].passed - inventor[i].year);
}
console.log(count);
```

Where passed refers to the year the inventor died, and year is the year they were born.

Reduced can do the same thing (I'll use the arrow function again)

```javascript
const count = inventors.reduced((total, inventor) => {
  return total + (inventor.passed - inventor.year);
});
```

So here is where it started to make more sense to me. Instead of using the generic a and b. We use more descriptive names that help me to understand. "a", or "total" is the running total of the reduce function, like the count variable in our for loop.

"b" or "inventor" is our current item that we're actioning.

One thing that I forgot though, and that I kept forgetting when trying to complete this tutorial, is that with the reduce function, you need to put an initializer for the running total. We do this with an additional parameter that I accidentally left out.

Here is the correct code for the above reduce function

```javascript
const count = inventors.reduced((total, inventor) => {
  return total + (inventor.passed - inventor.year);
}, 0);
```

notice the extra 0 on the end? This tells our reduce function that our running total is to start from 0.

### Conclusion

It's been a worthwhile tutorial! I know I need to get more comfortable using these functions. I'd be interested to see how much the reduce function is optimized compared to the for loop, and which is actually faster.
