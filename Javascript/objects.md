# OBJECTS

Obects are data structures in Javascript that lets you store data about a particular thing, and helps you keep track of that data by using a "key". An empty object can be created using:

```javascript
let object = {};
```

We can define someone using variables:

```javascript
let wifeName = "Julie";
let wifeAge = 34;
let wifeParents = ["Tom", "Donna"];
```

This can be converted to a object:

```javascript
let wife = {
  name: "Julie",
  age: 34,
  parents: ["Tom", "Donna"],
};
```

> This format is called **_object-literal notation_**

</br>

## Object-literal Notation

Important things to remember when structuring an object literal:

- The "key" (representing a **_property_** or **_method_** name) and its "value are separated from each other by a **_colon_**.
- The `key: value` pairs are separated by **_commas_**.
- The entire object is wrapped inside curly braces `{ }`.

Similar to how you would look up a word in the dictionary to find its definition, the `key` in a `key: value` pair allows you to look up a piece of information about an object.

```javascript
// two equivalent ways to use the key to return its value
sister["parents"]; // returns [ "alice", "andy" ]
sister.parents; // also returns ["alice", "andy"]
```

`sister["parents"]` is called **_bracket notation_**

`sister.parents` is called **_dot notation_**

</br>

## Methods

Creating a method is the same as defining a `key: value` pair except the `value` is a function.

```javascript
var sister = {
  name: "Sarah",
  age: 23,
  parents: ["alice", "andy"],
  siblings: ["julia"],
  favoriteColor: "purple",
  pets: true,
  paintPicture: function () {
    return "Sarah paints!";
  },
};

sister.paintPicture();
```

> **_Returns:_** "Sarah paints!"

</br>

## Naming Conventions

Object propeties (keys) should follow similar naming conventions to variable names.

- avoid using quotes around property names, can mask potential issues
- do not use a number as the first character `1stChild: "James"`
- do not use spaces in the property name `first name: "Chris"`
- do not use dashes in the property name `race-car: "red"`
