---
layout: post
title:  "React Series Part Two: What Are Components?"
modified:
categories: blog
excerpt:
tags: [JavaScript,React]
image:
date:   2017-02-01 6:02:16
---
### What Are React Components

I've discovered that when building applications using React, each section or function of an application can and should, be broken down into components.

Using my latest project, [Build A Recipe Box][https://codepen.io/Burfield/pen/oBpOLm] as an example:

1. The list of recipes is a component
2. Each list of ingredients is one component
3. Each button is one component

Building the application in reusable components is what makes the React.js framework helps to reuse code, therefore making it easier to maintain.

For example, I don't need to maintain each list of ingredients, there is just one list. But I pass in an object that contains all the ingredients for that recipe, and it gets shaped using JSX and rendered when I call that component.

Basically we use components for everything. They are important.

### There Are Three Types Of Components

The next thing to tell you is that there are three types of components. Although one is deprecated now, so you only really need to worry about two.

## The Stateful Component

The first is the stateful component. It maintains some type of state for the application, and can pass on values of that state onto other components as props. A stateful component is defined using the class syntax, and calls the constructor method to set it's initial state.

```javascript
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state {
      stateAttribute: "stateValue",
    };
  }
  render() {
    <div>{this.state.stateAttribute}</div>
  }
}
```

This class definition is nothing special, that is, it's not specific to React, it's just regular ES6 JavaScript. Note however, that we are extending React.Component. Extending the React.Component class lets us inherit all of the lifecycle methods that React gives us. I'll talk more about lifecycle methods in a future post.

Here we are going to render a div that will contain the value of our state's "stateAttribute".

## The Stateless Component

The stateless component does not store any state of the application. For this reason, these components are sometimes referred to as "dumb components". Usually these components will be passed state values from a stateful component, which the stateless component will accept as props (short for properties) and use the values in rendering the component to the screen.

This is how we define a stateless component

```javascript
const StatelessComponent = (props) =>
  <div>props.value</div>
```

Note here that I'm using an arrow function. But the exact same JavaScript can be written as:

```javascript
function StatelessComponent(props) {
  return <div>props.value</div>;
}
```

The two sections of code are exactly the same. The first is just writted using the ES6 arrow function.

Both of these stateless components are displaying a div with a value that has been passed to the component as props.

Recall that we would do this in JSX like:

```javascript
<StatelessComponent value={value} />
```

### So Which Component Should I Use?

Most people seem to recommend writing as many components as you can as stateless components. And only have them evolve to be a stateful component as it's required in the application.

When I created my recipe box, I only had one stateful component that maintained the state of the entire app, and contained all of the logic. That stateful component then passed all of the required state and functions as props to stateless components. I'm not saying this is the best way, I'm just learning and I'm sure I'll get better as I write and read more code.

### So What Was That Third Component?

The third way of writing a component is

```
Const Component = React.createClass({
  render() {
    <div>Output</div>
  }
});
```

This method is how components used to have to be created before ES6. It's recommended to use the new ES6 method of creating components now, so I haven't really looked into this way, and don't plan to. It's not needed.