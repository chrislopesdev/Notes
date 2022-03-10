# REACT PROPS

In React, we pass data to components as "props" (short for properties).

## Passing Props

We can pass props to components in two different ways.

First, to list each as a `key=value` pair:

```jsx
<Profile firstName="Amy" lastName="Mansel" avatar="/profile-hex.png" />
```

The second way uses the `spread operator` to destructure the object `{...{key: value}}`. It seems more complicated at first, but it is useful if we want to pass all the properties of an object as individual variables. Destructuring the `user` object when passing it to the `Profile` component will have the same effect as the above example.

```jsx
const user = { firstName = "Amy", lastName = "Mansel", avatar = "/profile-hex.png" };

<Profile {...user} />
```

<br />

## Using Props

The props you pass to a component are automatically stored in an object. The object is available as a parameter in the component definition and is commonly named `props` by React developers.

The example below shows how the `Profile` component receives and uses the `props` that were passed to it.

```jsx
  function Profile (props) {
    // props will contain an object: 
    // { firstName: "Amy", lastName: "Mansel", avatar: "/profile-hex.png" }
    const firstName = props.firstName;
    const lastName = props.lastName;
    const avatar = props.avatar;

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
    );
  }
```

> ⚠️ It's common for a prop to be an entire function definition. Remember ***not*** to call the function when it's being passed down. Pass only the referenc eot the component.

```jsx
  function doStuff () {
    console.log("This is the doStuff function.");
    // do stuff
  }

  // CORRECT: doStuff is passed as a reference!
  <Profile doStuff={doStuff} />
```

