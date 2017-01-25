---
layout: post
title:  "React Series Part One: JSX"
modified:
categories: blog
excerpt:
tags: [JavaScript,React]
image:
date:   2017-01-25 6:02:16
---
### React Series Part One: JSX

In my road to learning React.JS, I've begun to feel a bit overwhelmed with all the additional tooling that has been required to get started using React.

For this reason, I decided I'd start a blog post series to go over specific areas of React. Breaking it down into smaller chunks so I can begin to understand it.

This is my first post in what will become a series, and figured I'd start with arguably one of the first things that is encounted when first starting with React.JS: JSX.

### JSX

At first glance, JSX could be mistaken for HTML inside of JavaScript code. That's what it looked like to me, and on the surface, it seems to behave similarly to a templating language.

```jsx
const element = <h1>Hello world!</h1>;
```

JSX is actually a syntax extension to JavaScript, and is highly recommended to use with React to describe what the UI should look like.

JSX gets compiled into React elements, which are used to render UI to the DOM. Although this doesn't happen natively, we use a JavaScript compiler such as Babel to do this for us.

### React Elements

What is a React element? A React element is just a regular JavaScript object.

For example:

```jsx
<div attribute="attributeValue" />
```

Compiles to:

```jsx
React.createElement(
  div,
  { attribute: attributeValue },
  null
);
```

Babel actually provide an [Online Babel Compiler][https://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015%2Creact%2Cstage-0&code=function%20hello()%20%7B%0A%20%20return%20%3Cdiv%3EHello%20world!%3C%2Fdiv%3E%3B%0A%7D] if you want to see the native JavaScript that different JSX components are compiled to.

### Adding Attributes To JSX Components

We have to remember that JSX is closer to JavaScript than it is to HTML, and it is for this reason that attributes are added to JSX components using camel case, as opposed to all lower case like in HTML. Similarly, some attribute names are different in JSX

Some of the common attributes that work differently between JSX and HTML are:
1. checked
2. className
3. dangerouslySetInnerHTML
4. style

There are a few more. The full list and descriptions of each can be found in the [official React documentation][https://facebook.github.io/react/docs/dom-elements.html]

Other than that though, adding attributes seems to be relatively straight forward. For example, if we wanted to add a button with a class of "button" and an onclick attribute that calls a function called `handleOnClick()` and some button text that says "Click Me" we would simply write:

```jsx
<button 
  className="button" 
  onClick={this.handleOnClick()}
>
  Click Me
</button>
```

This looks pretty much the same as regular HTML to me, the only differences are class becomes className, onclick becomes onClick, and the function call is in curly braces.

### Using Curly Braces In JSX

Because JSX is just JavaScript with a syntax extension to make it look similar to HTML, it's relatively easy to insert regular JavaScript directly into the JSX.

We do this by surrounding it with curly braces.

This isn't limited to just calling functions in onclick attributes, it's much more powerful.

Let's say we had an array of books with properties of title like so:

```JavaScript
const list = [
  {
    title: 'React',
    author: 'Jordan Walke',
    objectID: 0,
  },
  {
    title: 'Redux',
    author: 'Dan Abramov, Andrew Clark',
    objectID: 1,
  },
];
```

Now lets say we're rendering our JSX component and we want to display each of the items in the list. Using JavaScript inside the curly braces, we can use the Array.prototype.map() function.

```jsx
  <table>
    <tbody>
      {list.map(item =>
        <tr key={item.objectID}>
          <td>{item.title}</td>
          <td>{item.author}</td>
        </tr>
      )}
    </tbody>
  </table>
```

Notice how we surround the list.map function with curly braces, and then inside the function, we're returning more JSX, and use curly braces again, inline, to specify the `item.title` and `item.author` JavaScript object properties.

I haven't spoken about the key attribute yet, it's a special attribute in React, I'll go into further detail now.

### The Key Attribute

The key attribute is a special attribute in React. It is used specifically when we are building a list of JSX components.

Keys should be given to the elements inside an array to give the elements a stable identity.

React doesn't want to re-render everything to the DOM everytime the state of the app changes, that's resource intensive and takes too long. Instead, *React just iterates over both lists of children at the same time and generates a mutation whenever there's a difference*.

For example, converting between these two trees works poorly.

```JavaScript
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```

React will mutate every child instead of realizing it can keep the `<li>Duke</li>` and `<li>Villanova</li>` subtrees intact. This inefficiency can be a problem.


The key attribute solves this problem. For example, if we were to modify our above trees to have keys:

```JavaScript
<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
```

Now React knows that the element with key `'2014'` is the new one, and the elements with the keys `'2015'` and `'2016'` have just moved, and don't actually need to be mutated.

Another important note to make is that key should with explicit values, using something like the array index is not good practice.

The best way to pick a key is to use a string that uniquely identifies a list item among it's siblings. I.e. The id from your data.

### Conclusion

So far, I haven't found JSX too difficult to get my head around. Coming from HTML it seems relatively easy to take hold of. And with Babel doing all the compiling behind the scenes, I don't really need to concern myself too much with the compiled JavaScript React elements.

Tomorrow I want to dig deeper into Components, another React concept that as a beginner I'm introduced to right from the start, and they are used everywhere!