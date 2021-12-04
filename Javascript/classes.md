# CLASSES

In OOP, classes are blueprints (templates) that we use to create instances of objects. A class describes what the object is going to be and we can create new objects using the class.

</br>

## Class

To declare a class, use the `class` keyword with the name of the class. ***Class names should be a noun.***

```js
class Pizza {

}
```

To create a new object from a class, we use the `new` keyword.

```js
let pizza1 = new Pizza();
let pizza2 = new Pizza();
```

`pizza1` and `pizza2` are pizza objects. When you create an object useing a class, it is an ***instance*** of that class. `pizza1` and `pizza2` are instances of the `Pizza` class.

Two objects of the same class are separate objects. Two houses made from the same blueprint are still separate houses.

```js
pizza1 !== pizza2
```

## Methods & Properties

Currently our pizza class is blank. Let's add some functionality.

```js
class Pizza {
  constructor() { // method
    this.toppings = ["cheese"];
  }
  addTopping(topping) {
    this.toppings.push(topping); // this.toppings => property
  }
}
```

</br>

## Intro to `constructor`

`constructor` is a special kind of method that gets executed when an object instance is created from a class. Everything inside the Pizza's constructor method will get run for the new instance of the class when we call `new Pizza();`. This is a great place to setup default state for new instances. In other words, the constructor is for setting default values for any new object's properties.

Above we used the `constructor` to setup the toppings array and add "cheese" as the first topping.

```js
let pizza1 = new Pizza();
console.log(pizza1.toppings); // ["cheese"]
pizza1.addTopping("mushrooms");
pizza1.addTopping("peppers");
console.log(pizza1.toppings); // ["cheese", "mushrooms", "peppers"]

let pizza2 = new Pizza();
console.log(pizza2.toppings); // ["cheese"]
pizza2.addTopping("more cheese");
console.log(pizza2.toppings); // ["cheese", "more cheese"];
```

</br>

## Customizing the Constructor

```js
class Pizza {

  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}
```

We can now pass in size and crust when we create a new object.

```js
let pizza = new Pizza('large', 'thin');
```

When this pizza get's created, it will look like this:

```js
let pizza = {
  size: 'large',
  crust: 'thin',
  toppings: ['cheese']
}
```

</br>

## Inheritance

### Duplication Problem 

```js
class Student {
  // this constructor is identical to that of a mentor!
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // here is a method that is specific to students
  enroll(cohort) {
    this.cohort = cohort;
  }

  // identical! Smells of code duplication
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor {
  // this constructor is identical to that of a student!
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }

  // identical! Smells of code duplication
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}
```

Here, the `student` and `mentor` classes have identical `constructor` and `bio` methods. They also share some properties (`name` and `quirkyFact`).

## A Solution with Inheritance

To solve the problem of duplication we can create new class that which contains elements that the two classes share.

```js
// This class represents all that is common between Student and Mentor
class Person {
  // moved here b/c it was identical
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  // moved here b/c it was identical
  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}

class Mentor extends Person {
  // specific to mentors
  goOnShift() {
    this.onShift = true;
  }

  // specific to mentors
  goOffShift() {
    this.onShift = false;
  }
}
```

Above, there is now a general `Person` class that contains shared code. `Student` and `Mentor` inherit ***behaviour*** and ***state*** information from `Person` using the keyword `extends`.

`Student` and `Mentor` are ***subclasses*** of the `Person` class. `Person` is the ***superclass*** in this relationship.

</br>

## Method Overriding and Super

### The problem:

You may want a sublass to have a slightly different behaviour to its superclass. What if we wanted the mentor bios to start with "I'm a mentor at Lighthouse." before saying "My name is..."

### Solution 1: Method Override

```js
// Superclass
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// Subclass
class Mentor extends Person {
  // Completely re-define the bio method since it has more to say
  bio() {
    return `I'm a mentor at Lighthouse Labs. My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// The Student class doesn't need to define bio since it can just use the one from Person

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

Here, we have overritten the superclass `bio()` method. This will solve the problem, but it's not the best solution as we are repeating code.

### Solution 2: Use `super`!

We can use `super` to call the `Person`'s superclass `bio` method.

```js
// Super class
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

</br>

## Getters and Setters

Getters and setters are special methods that are used to get the value of a property or set the value of a property.

```js
class Pizza {

  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

  setSize(size) {
    this.size = size;
  }

  getSize() {
    return this.size;
  }
}
// DRIVER CODE
const pizza = new Pizza();
pizza.setSize('m');
pizza.getSize(); // m
```

There are many reason you may want to use getters and setters. Here are two main reaons:

1. ***Validating*** data before assigning it to a property
2. ***Computing*** a value on the fly instead of simply pulling it out of the property

</br>

### Validating  Data

Our pizza should only have the following sizes: 's', 'm', 'l'. It would be bad if someont could set the size to '🍕'. Using a ***setter method*** we can validate the value before it gets set.

```js
// setSize now includes data validation
  setSize(size) {
    if (size === 's' || size === 'm' || size === 'l') {
      this.size = size;
    }
    // else we could throw an error, return false, etc.
    // We choose here to ignore all other values!
  }
```

### Computed Value

We could create a property to keep track of the price of a pizza. Every time the size or toppings change, we could update the price property. But that involves constantly keeping track of the price. It would be easier to compute the price when needed.

```js
getPrice() {
  const basePrice = 10;
  const toppingPrice = 2;
  return basePrice + (this.toppings.length * toppingPrice);
}
```

### There's a better way! `get` and `set`

The need for getters and setters is ver common in OOP. Javascript classes have special `get` and `set` keywords that we can use to implement getters and setters easily.

```js
get price() {
  const basePrice = 10;
  const toppingPrice = 2;
  return basePrice + this.toppings.length * toppingPrice;
}

set size(size) {
  if (size === 's' || size === 'm' || size === 'l') {
    this._size = size;
  }
}
```

We've adjusted the code to add `get` and `set` infront of the getter and setter methods. Now price and size are accessed as if they were value properties instead of method properties.

```js
let pizza = new Pizza();

pizza.price;      // instead of getPrice()
pizza.size = 's'; // instead of setSize(size)
```

