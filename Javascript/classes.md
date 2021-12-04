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