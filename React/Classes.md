# CLASS BASED COMPONENTS

Class based components gained popularity between 2016 and 2019. They have been replaced with React Hooks, but may appear in legacy code.

## Classes

ES6 provides a new Class syntax that resembles some of the most popular OOP languages. React replaced the usage of their custom `React.createClass` function with official ES6 Class syntax. A React component declared using ES6 class must now follow additional rules.

### Structure of a class

```jsx
import React, { Component } from 'react';

class Application extends Component {
  render() {
    return <div></div>;
  }
}
```

This `Application` component renders a single `div` element and represents a basic example of a class-based component. It returns an empty `div`, which isn't useful, but it follows `two rules`.

1. All class-based React components must `extend` the `React.Component` class
2. All class-based React components must override the `render` method of the `React.Component` superclass that they `extend`

<br>

## Constructors

We are not required to override the constructor method, but if we do, then we must follow an important rule to ensure that our component works properly.

We must call the `super()` method, and we must pass it the `props` object.

```jsx
import React, { Component } from 'react';

class Application extends Component {
  constructor(props) {
    // If we add a constructor to our class, we must pass props to the super class
    super(props);
  }

  render() {
    return <div></div>;
  }
}
```

The constructor does not perform any operation, but it is still performing its only required responsibility. A constructor must call the `super(props)` method.

<br>

## Class Properties
