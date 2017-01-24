---
layout: post
title:  "The Beginnings Of A React Series"
modified:
categories: blog
excerpt:
tags: [JavaScript,React]
image:
date:   2017-01-24 6:02:16
---
### The Beginnings Of A React Series

Okay, so I've been working more with React.JS over the past couple of weeks and sometimes I feel like I'm beginning to wrap my head around it, and other times I feel like I'm completely lost!

One of the proplems I'm having is that there's so much information to take in, but it's not just React, it's all this extra stuff that plugs in around it. 

For example, I was recently working through a tutorial on building a voting system using the react framework. The app would take a list of 'things' you wanted to vote against, and then starting with the first two 'things' in the list, people could start voting for one or the other. The winning 'thing' would go through to the next round and people would start voting on the next two items in the list. Pretty straight forward and it was a really thorough and well done tutorial. It can be found here: [Full-Stack Redux Tutorial][1]

Actually the reason I started this tutorial in the first place was because I wanted to learn how to use Redux with React.

All well and good, however...

The stack introduced a bunch of other frameworks and technologies that I needed to learn, the tutorial explained why to use them, and it all made sense, and they're all things that I do want to learn eventually and probably should be using. I just need to remember to start with the basics, otherwise I just keep getting overwhelmed.

Firstly, it also introduced me to 

1. TDD, and using the Mocha test framework with the Chai assertion/expectation libraries.
2. The Immutable library to ensure the data structures remained immutable.
3. Redux (which is what I was wanting to learn anyway)
4. Routing

Which is all good, it just gets a bit overwhelming. I need to get back to basics, which is why this series is going to take one question I've had regarding the react and redux frameworks and attempt to answer that question.

I'm going to start today by writing what I learnt about the Virtual DOM used by React.JS

### The Virtual DOM

The power of React.JS comes from being able to quickly compare a virtual DOM, with the actual DOM in the browser, and only making the necessary changes it needs to.

In this sense, the name React makes perfect sense, as when the view renders to the virtual DOM, the React framework will 'react' to the updated virtual DOM and update the real DOM accordingly.

The way the view renders to the virtual DOM in React.JS is different to how a view in the MVC world updates the DOM.

In MVC, a view needs to maintain a reference to all of the elements that *might* need to be updated at some point. Then it as the model spoon feeds the view small bits of information, i.e. only the DOM elements that need to be updated, the view will search it's list of references to find the right element to update.

Apparently, that approach can get cumbersome. With so many references with so many elements.

With the virtual DOM in react however, instead of the model telling the view only the bits that need to be updated, the model will just hand the view the current state of the entire application. The view then creates a complete DOM. A virtual DOM. The view doesn't need to care about the previous states, or what's been changed, it just takes the current state, and creates the virtual DOM from it.

Then it hands the virtual DOM to React.JS, which can very quickly do a diff between the virtual DOM and the real DOM and update only the real DOM elements that have changed.

I think that's it. That's how the virtual DOM works anyway. Tomorrow I'll research another question I have, or something else that I've been stuck on. It's all part of the learning process.

[1]: https://teropa.info/blog/2015/09/10/full-stack-redux-tutorial.html#the-client-application