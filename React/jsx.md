# JSX (JavaScript XML)

## Rules:

### All tags must be closed!

* Open and close tags (`<div>...</div>`)
* Self-closing tag (`<img />`)

<br>

### Child tags must be closed before its parent

```jsx
<div>
  <ul>
    <li>
    </li>
  </ul>
</div>
```

<br>

### All JSX expressions must result in one root level element

A function can only return one value. A component is defined using JavaScript function so the same rules apply.

***Good:***
```jsx
return (
  <div> {/* root element */}
    <input />
  </div>
)

/* becomes */

return React.createElement('div', null, React.createElement('input', null))
```

***Bad:***
```jsx
return (
  <div>
  </div>
  <input />
)

/* becomes? */

return (
  React.createElement("div", null)
  React.createElement("input", null)
)

/* Nope. Functions can't return multiple values like that. */
```

<br>

### No HTML comments

```jsx
return (
  <div>
    <!-- not allowed -->
    {/* allowed */}
  </div>
)
```