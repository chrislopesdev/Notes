# REACT

[https://create-react-app.dev/](https://create-react-app.dev/)

To start, run this command:

```terminal
npx create-react-app my-app
```

To update:

```terminal
npm install react-script@latest
```

<br>

## Components

**_Create_** a navigation component called `Navigation.js` (Capital 'N')

```jsx
function Navigation() {
  return (
    <nav>
      <ul>
        <li>Nav Item 1</li>
        <li>Nav Item 2</li>
        <li>Nav Item 3</li>
      </ul>
    </nav>
  );
}

export default Navigation;
```

<br>

**_Import_** your components into your `App.js` file:

```jsx
import Navigation from './components/Navigation';
```

<br />

**_Show_** your components on the page:

```jsx
function App() {
  return <Navigation />;
}

export default App;
```

<br />

## Full App.js page

```jsx
import Navigation from './components/Navigation';
import Profile from './components/Profile';
import TweetList from './components/TweetList';
import TweetForm from './components/TweetForm';
import './App.css';

function App() {
  return (
    <div className='App'>
      <Navigation />
      <Profile />
      <TweetList />
      <TweetForm />
    </div>
  );
}

export default App;
```

<br />

## Replacing Hard-Coded Values with Variables

```jsx
// Before
function Profile() {
  return (
    <aside>
      <div className='profile'>
        <img className='profile__image' src='/profile-hex.png' />
      </div>
      <br />
      <div className='profile__name'>
        <h2>
          <span className='profile--bold'>Amy</span> Mansell
        </h2>
      </div>
    </aside>
  );
}

// After
function Profile() {
  const firstName = 'Amy';
  const lastName = 'Mansell';
  const avatar = '/profile-hex.png';

  return (
    <aside>
      <div className='profile'>
        <img className='profile__image' src={avatar} />
      </div>
      <br />
      <div className='profile__name'>
        <h2>
          <span className='profile--bold'>{firstName}</span> {lastName}
        </h2>
      </div>
    </aside>
  );
}
```

<br />

## State

State is the current status of something, for example a light that is either on or off. State in React allows us to dynamically change one or many elements based on one variable. To store state, we need to use a feature called "`hooks`" - specifically, the `useState` hook.

To use state, we have to import `useState` into the module. It is often imported on the same line as React:

```jsx
import React, { useState } from 'react';
//or
import { useState } from 'react';
```

The `useState` function receives an optional argument which is the default value for the state. `useState` returns an array - the first element is the current value of the state, the second is a function that can update teh state and cause a render.

Note how array destructuring is used to immediately create two variables from the array returned by `useState`.

```jsx
function Application(props) {
  const [count, setCount] = useState[0]; // Array destructuring

  return (
    <main>
      <Button onClick={(e) => setCount(count + 1)}>Increment</Button>
      <h1>Button was clicked {count} times.</h1>
    </main>
  );
}
```

> Do not call hooks inside conditionals, loops, or other functions. They need to be at the top of the component function.

The `useState` hook uses array destructuring syntax to return two different values. The pair of values returned in the array are related. One is used to **_get_** a value ("getter") and the other to **_set_** a value ("setter").

```jsx
const [reference, setReference] = useState();
//or
const [state, setState] = useState();
```

> The names uses in the destrcutred array have a rule: We can pick the name we want for the reference/state, but the setter function needs to start with the word `set` like the examples above.

<br/>

## Fragments

Since we can only return one component in a return statement:

```jsx
return (
  <h1>Heading</h1>
  <p>Paragraph</p>
)
```

The above code would cause an error. We could fix this with a `<div>`

```jsx
return (
  <div>
    <h1>Heading</h1>
    <p>Paragraph</p>
  </div>
);
```

Though the above code works, you may want to avoid adding additional unnecessary elements to the page. To fix this we can use a `<Fragment>`. Unlike a `<div>`, a React `<Fragment>` does not create any extra DOM nodes which can clutter up your HTML.

To use React `Fragment` we can import it:

```jsx
import { Fragment } from 'react';
```

We can then use it like this:

```jsx
return (
  <Fragment>
    <h1>Heading</h1>
    <p>Paragraph</p>
  </Fragment>
);
```

Alternatively we can also use shorthand `<>` and `</>`

```jsx
return (
  <>
    <h1>A heading</h1>
    <p>A paragraph</p>
  </>
);
```

> Note that shorthand method does not accept props. You must use the `<Fragment>` if you want to pass any props.
