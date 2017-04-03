---
layout: post
title:  "React Series Part Three: State And Props"
modified:
categories: blog
excerpt:
tags: [JavaScript,React]
image:
date:   2017-04-03 6:02:16
---
### State And Props

Similarly to what we covered in the first two posts of this react series, JSX and Components; State and Props are a critical part of the React ecosystem. And you will no doubt need to handle these concepts even with your very first React application.

Before going into detail about the differences, and how the two work together, let's first cover the commonalities. What are the common denominators between State and Props?

1. state and props are both just **plain JavaScript objects**

You'll see in the examples below that there is nothing special about State and Props from a JavaScript perspective. They aren't anything special or new to the language, they're only objects!

2. Changes to state and props both **trigger a re-render** of your component.

I use the word *changes* loosely here, we'll cover this in more detail later.

So with the commonalities out of the way, let's get stuck into the specifics!

### Props

# TL;DR

Props are just the properties that are passed to a component. While props can't be changed from inside a component, new values for props can be passed into components from their parent components.


What does props even mean? Is props a special/reserved word?

Nope, in the React ecosystem, props is just cool-kid speak for properties. Props are just the properties that get passed into your functions.

Take this example from the [official React docs](https://facebook.github.io/react/docs/components-and-props.html#rendering-a-component)

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

Firstly, we can see a stateless components called Welcome. We all ready know about stateless components from this post.

The stateless component accepts a parameter called props, which is then used to display a name, via `props.name`.

Second, we're assigning some JSX to the constant `element`. The JSX has the `<Welcome />` tag, and is passing in a property called `name`, with the value "Sara".

This is how we pass props to components. Simply adding the property to the component in JSX. Note that in this case, the `name` property is set to the hard coded string "Sara", but we could just as easily pass in a variable, or state, or the parent's components props. I'll cover some of those other scenarios in a second, they aren't complicated.

Lastly, `element` is rendered to the screen using the ReactDOM render method. You pass it in some JSX, in this case, the JSX referenced by the `element` constant, and the element in the DOM you want to append the React components to. In this case, it's an element with an id of "root".


## State

In React, state is what holds all your application's data information and can be passed down to child components as props.

Let's see that in action!

```javascript
class CounterContainer extends React.Component {
  constructor() {
    super();
    this.state = {
      counter: 0,
    };
    this.increaseCounter = this.increaseCounter.bind(this);
  }

  increaseCounter() {
    this.setState(prevState => {
      return {
        counter: prevState.counter + 1,
      };
    });
  }

  render() {
    <button text="Click to increase counter" onClick={increaseCounter} />
    <DisplayText counter={this.state.counter} />
  }
}

const DisplayText = props =>
  <div>The current counter value is {props.counter}</div>;
```

Soooo, what's quite a bit more code than last time, but there's nothing special going on here. Let's break it down!

## The components

We're looking at two components

```javascript
class CounterContainer extends React.Component {
}

const DisplayText = props =>
```

We've seen these before, the first, `CounterContainer`, is a stateful components, and the second, `DisplayText`, is a stateless component. Nothing new.


## The functions

Secondly, the `CounterContainer` component has three functions, `constructor()`, `increaseCounter()` and `render()`.

# constructor

constructor is called when the component is being initialized. Typically here you'll see a call to the `super()` function followed by initalizing the component state.

Remember, that state is just an object, there's nothing overly special about it. So here we're setting

```javascript
this.state = {
  counter: 0,
};
```

# increaseCounter

In increaseCounter, all we want to do in increase the counter value in state.
React helps us to update state by providing us with the `setState` function.

The reason we have access to `setState`, as well as some lifecycle methods that we'll cover in another post, is because our CounterContainer class is extending React.Component.

If you want to update your component's state (and you aren't using flux), then you need to use setState. This is because React has a few things happening behind the scenes to make sure components get re-rendered when state changes.

You may be tempted to mutate the state directly, i.e.

```javascript
this.state.counter += 1;
```

**Don't do this.** React won't know that the state has changed and your components won't be re-rendered.

The other thing I often see, is not using the `prevState` variable.

You might see examples on the internet like this:

```javascript
this.setState({
  counter: this.state.counter + 1,
});
```

**Don't do this either.** React updates your state in an asynchronous nature to be efficient. And updating your state in this way, while it won't throw any errors, doesn't take into account the asynchronous nature of how state is updated, and you could end up with weird side effects.

That's no different from defining and other simple object with a counter property anywhere else in JavaScript. The inialization is the only place you will ever set a value to `this.state` directly. To update the state later in the component lifecycle, you'll use the setState function.

State is immutable (although this isn't enforced by React). Which means that it can't be updated or modified. Instead, you should make a new object that is a clone of the current state, modify that, and then override the old state with the new state.

React gives a helper function to do this. The `setState()` function takes an object, and will update the state without mutating it.

# render

Render is the final function inside the CounterContainer class. React will call the render function when the component is first mounted, or needs to be re-rendered due to state changes.

In this case, we're rendering a simple button which will call our `increaseCounter()` function when it's clicked, and the DisplayText stateless component.

Notice how we have the counter property, and pass in `this.state.counter` as the value? This is how we pass **props** from one component (CounterContainer) to another component (DisplayText).

I told you it was easy, just pass in whatever properties you want.


## It all comes together!

So there we have it! We have a stateful component which initializes our state, and defines the function to update the counter value in our state via the setState method. And then passes that value to the DisplayText component via props in order to display it.