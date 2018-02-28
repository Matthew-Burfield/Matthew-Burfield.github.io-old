---
layout: post
title:  "Some things you might not know about React setState()"
modified:
categories: blog
excerpt:
tags: [JavaScript,React]
image:
date:   2018-02-28 6:02:16
---
### React State

Application state is no doubt a critical part of your React application, and setState is the built in React lifecycle method that lets you update and modify your state. You've probably used it a bunch of times already, but just incase you haven't, this is what it looks like.

```javascript
class MyCoolReactComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      myStateProperty: 'Hello everyone!',
    }
  }

  onClick() {
    this.setState({
      myStateProperty: 'Goodbye everyone',
    })
  }

  render() {
    return (
      <button onClick={ this.onClick }>Click me</button>
    )
  }
}
```

Alrighty, so there's a couple of different bits that make up our component above, but overall it should be pretty easy to follow.

1. The constructor just sets up our component and is the first function that is called when our component gets mounted and before it's first render. We can set any initial state values here. You can see I'm creating a state property called `myStateProperty` and giving it the initial value of `Hello everyone!`.
2. The onClick function is a simple function that takes no arguments, and calls the setState function that is provided by React. We have access to it because our class is extending React.Component. I won't go into detail on the setState function here, because we'll be covering it in detail later on. Just know for know that we are updating our `myStateProperty` property to `Goodbye everyone` when the onClick function is called.
3. Finally we have the render function, this is another lifecycle method given to us via our class extending React.Component, and contains all the JSX code that will eventually be rendered to the screen. Here we have a button that says "Click me", and when it is clicked, it calls the onClick function.

Okay, so that's each bit of the above component explained. Basically we have a Button, that when clicked is going to update our state to a new string. We aren't actually doing anything with our state, but that's okay, it's just for demonstration purposes :)

### Immutability

Okay! So now that we've seen setState in action, lets get into some of the nitty gritty of it. You may have noticed when we intialised our state in the above component, we were basically just creating an object and assigning it to a variable called `this.state`

```javascript
this.state = {
  myStateProperty: 'Hello everyone!',
}
```

Right-o, so state is just an object right? And objects can just be updated like so: `this.state.myStateProperty = 'Goodbye!'`. BOOM! State changed without even having to call `setState`....

Hmmm, well not exactly. The reason we can't do this is because React needs to watch for when your state changes so it can re-render your component when it updates, and the quickest way to this is by doing a quick comparison. React needs to know:

```javascript
this.previousState === this.newState
```

Is the previous version of your component state different from the new version of the component state? If it is, re-render the component with the new state changes, and if not, just move onto the next thing because we don't want to waste time re-rendering if we don't have to.

So what's the quickest way to compare two objects? For our simple object it's pretty easy, we can just compare the one property `myStateProperty` since it's just a string and there's only one property on the object. Essentially we'd be asking, does `'Hello everyone!' === 'Goodbye everyone!'`? No? Good, let's re-render this component.

But what happens if our state gets more complex? What happens if our state property was an array?

Have you ever tried to compare arrays? Open your browser console and type this: `[1, 2, 3] === [1, 2, 3]`. What would you expect it to return? They certainly look like the same array...

This actually returns false, because each of those arrays are stored in different locations in memory. So to property compare these arrays we'd have to go into each element of the array and compare each element separately.

And if there were more arrays, or nested arrays and objects, the amount of computation to compare each item in the state quickly adds up. And remember, React is comparing a lot of state changes, and will compare the same state multiple times over the lifetime of the application.

React wants to be as fast as possible, so it doesn't want to do all this comparing if it can help it.

Enter immutability.

State being immutable just means that the state value cannot me modified/updated/mutated. Instead, if we want to *change* the state, then we create a brand new state object, and reassign our state to point to the new state object we just created. This is what `setState` is doing for us.

Let's take a look at what immutability is doing with an example, we'll use the example of the array [1, 2, 3] again.

So before, *without* immutability, essentially what we were doing was this.

```javascript
var state = {
  myStateProperty: 'Hello everyone!'
}
var newState = state.myStateProperty = 'Goodbye'

state === newState // true
```

You can try that in your browser console and check the result. When react comes to do it's comparison of state, is returns true - it doesn't think the state has changed. This is because the state variable is still pointing to the same spot in memory, and state doesn't look inside the object, because it does what's called a shallow comparison - for speed reasons.

Now checkout the immutable equivalent!

```javascript
var state = {
  myStateProperty: 'Hello everyone!',
}
var newState = {
  myStateProperty: 'Goodbye',
}
state = newState // false
```

Notice the difference in the immutable example? State was assigned to an entire new object with just the change made. Because it's an entire new object, React doesn't need to compare every single item in the object tree, it knows straight away that *something* has changed, so it knows straight away to trigger a re-render.


### Component Rerender
### Using The Current State When Updating
### Asyncronise and Batching