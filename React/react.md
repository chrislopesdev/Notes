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

***Create*** a navigation component called `Navigation.js` (Capital 'N')

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
  )
}

export default Navigation
```

<br>

***Import*** your components into your `App.js` file:

```jsx
import Navigation from './components/Navigation'
```

<br />

***Show*** your components on the page:

```jsx
function App() {
  return (
    <Navigation />
  )
}

export default App;
```

<br />

## Full App.js page

```jsx
  import Navigation from './components/Navigation'
  import Profile from './components/Profile'
  import TweetList from './components/TweetList'
  import TweetForm from './components/TweetForm'
  import './App.css';

  function App() {
    return (
      <div className="App">
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
        <div className="profile">
          <img className="profile__image" src="/profile-hex.png" />
        </div>
        <br />
        <div className="profile__name">
          <h2><span className="profile--bold">Amy</span> Mansell</h2>
        </div>
      </aside>
    )
  }

  // After
  function Profile() {
    const firstName = "Amy"
    const lastName = "Mansell"
    const avatar = "/profile-hex.png"

    return (
      <aside>
        <div className="profile">
          <img className="profile__image" src={avatar} />
        </div>
        <br />
        <div className="profile__name">
          <h2><span className="profile--bold">{firstName}</span> {lastName}</h2>
        </div>
      </aside>
    )
  }
```