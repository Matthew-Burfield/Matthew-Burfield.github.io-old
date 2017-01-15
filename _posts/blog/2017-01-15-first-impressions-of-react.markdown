---
layout: post
title:  "First Impressions of React"
modified:
categories: blog
excerpt:
tags: [JavaScript,React]
image:
date:   2017-01-15 6:02:16
---
### React

I've just made my first few projects using React, a JavaScript library for building user interfaces. Although the two apps I've built so far have only been small, a markdown previewer, a pokedex, and a leaderboard, I can already start to see power of using this framework.

In React, we write components in JavaScript which return a block of html. Which can then be rendered to the screen using the ReactDOM.render method.

Components can be declared in a few different ways, but I've been using the ES6 method of creating classes. For example, if I wanted to create a component called navigation, it would be set out as follows.

```javascript
class Navigation extends React.Component {
  /* class stuff goes here */
  return <div></div>;
}
```

Note that the component needs to return html, and the html needs to be wrapped in a container.

The Navigation component can then be called within another component like this:

```html
<Navigation />
```

Easy as. It just becomes its own html tag.

This already makes code easier to maintain as all html can be broken up into separate components.

A component can also maintain internal state data and update/re-render certain aspects of the page when the state changes.

This is done by creating a state object in the class constructor.

For example:

```javascript
class Timer extends React.Component {
  constructor(props) {
    super(props);
    this.state = {secondsElapsed: 0};
  }

  tick() {
    this.setState((prevState) => ({
      secondsElapsed: prevState.secondsElapsed + 1
    }));
  }

  componentDidMount() {
    this.interval = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.interval);
  }

  render() {
    return (
      <div>Seconds Elapsed: {this.state.secondsElapsed}</div>
    );
  }
}

ReactDOM.render(<Timer />, mountNode);
```

Above is an example of a React component called Timer.

Inside is a constructor method, notice the `this.state = {secondsElapsed: 0};`.

This object is the state of the component.

The state can be changed using the `this.setState()` method, which takes an object and updates the state.

The state variables can be accessed using the `this.state.secondsElapsed`.

### Using React So Far

So that's pretty much what I know so far, which isn't a hell of a lot, but it's a start. I want to learn more about why things work the way the do. And how to modularize components, and if that's something worth doing.

### A few things I skipped over

So to get React to work, the JavaScript code that's been written in ES6 needs to be compiled into usable JavaScript by the browser, which uses something called Babel. And the tutorial I followed to help me set it up uses something called Webpack to automatically compile the React JavaScript and SASS whenever I update the files on my local server. This is something I've just kind of skipped over at this point, I have it working and don't really need to know exactly what's happening 'under the hood' right now. I can just concentrate on learning the React framework for now.

I don't want to get overwhelmed with all the new moving parts right now.

### Moving forward

Moving forward I really want to focus on making sure my React code is of a high standard. So far my apps have been quite small, so I've gotten away from making my React components relatively big. In the future I need to keep them smaller so they're each only doing one specific thing.

I'd also like to start modularising my React code if that's possible.

And I want to start using Redux with my React code to maintain a single global state. I've already had to sacrifice how I write my React code even for the smaller projects because of this.

Reach is great, and I can pass the state values of one component onto child components as properties (or props), but I can't share state values with sibling components.

I've already found this limiting and want to start using Redux with my next project.

One thing at a time, Matt. I'll get there.