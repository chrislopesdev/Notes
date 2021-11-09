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

This can be converted to a object: the variables become properties of the wife object.

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

## Updating & Adding Object Properties

We can update object properties using dot notation.

```javascript
let ourDog = {
  name: "Camper",
};

ourDog.name = "Happy Camper";

// ourDog.name has been changed to "Happy Camper"
```

We can use the same method to add new properties.

```javascript
let ourDog = {
  name: "Camper",
};

ourDog.bark = true;

// ourDog obj now includes bark: true
```

 </br>

## Deleting Object Properties

We can use the `delete` keyword to remove a property from an object:

```javascript
delete ourDog.bark;
```

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

</br>

## Accessing Object Properties with Variables

```javascript
// setup
let testObj = {
  12: "Namath",
  16: "Montana",
  19: "Unitas",
};
// only change code below this line
let playerNumber = 16;
let player = testObj[playerNumber];
// player = "Montana
```

</br>

## Using Objects for Lookups

```javascript
//setup
function phoneticLookup(val) {
  let result = "";

  // use object for lookup vs switch below
  let lookup = {
    alpha: "Adams",
    bravo: "Boston",
    charlie: "Chicago",
  };

  result = lookup[val];

  return result;

  // switch lookup
  // switch(val) {
  //   case "alpha":
  //     result = "Adams";
  //     break;
  //   case "bravo":
  //     result = "Boston";
  //     break;
  //   case "charlie":
  //     result = "Chicago";
  //     break
  // }
}

console.log(phoneticLookup("charlie"));
```

</br>

## Testing Objects for Properties

You can check if an object has a property with the `hasOwnProperty` method.

```javascript
let myObj = {
  gift: "pony",
  pet: "kitten",
  bed: "sleigh",
};

function checkObj(checkProp) {
  if (myObj.hasOwnProperty(checkProp)) {
    return myObj[checkProp];
  } else {
    return "Not Found";
  }
}

//test code
console.log(checkObj("gift"));
```
