# OBJECT ORIENTED PROGRAMMING </br> BEST PRACTICES

## Goals & Best Practices

1. Reduce duplicated code (reusibility)
2. Breaking code up into sensibly-divided units (modularity)

OOP is about trying to make complex things simpler to read, write and maintain.

</br>

## Abstraction

> Abstraction is a technique for arranging complexity of computer systems. It works by establishing  a level of complexity on which a person inteacts with the system, suppressing the more complex details below the current level.

### Abstract Pizza Example

```js
class Pizza {
  constructor() {
    this.toppings = "";
  }
}
let pizza = new Pizza();

pizza.toppings = pizza.toppings + "cheese";
pizza.toppings = pizza.toppings + ", mushrooms";
```

We don't want to capture toppings in a string. An array would work better. To accomplish this we have to change to `this.toppins = []` but this also means we have to change how the toppings were being added. Here we just had to change the two lines of code to `push` into the array. Imagine we had 100s of lines of code we had to update... that would be a mess.

```js
class Pizza {
  constructor() {
    this.toppings = [];
  }
}

let pizza = new Pizza();

pizza.toppings.push("cheese");
pizza.toppings.push("mushrooms");
```

If we instead take away this external functionality and put it inside our method we only have to change the code inside the function.

```js
class Pizza {
  constructor() {
    this.toppings = [];
  }
  addTopping(topping) {
    this.toppings.push(topping);
  }
}

let pizza = new Pizza();

pizza.addTopping("cheese");
pizza.addTopping("mushrooms");
```

We could also update the function to ignore toppings that are already in the array. Again this is made easier by including the functionaly in the function, instead of relying on external factors.

```js
class Pizza {
  constructor() {
    this.toppings = [];
  }
  addTopping(topping) {
    if (this.toppings.indexOf(topping) > -1) {
      // Topping already exists, deny!
      return false;
    }
    this.toppings.push(topping);
    return true;
  }
}
```
</br>

## Private vs Public

All code using the pizza class should now use the `addTopping()` method instead of accessing `toppings` directly. But someone could still access the array directly using:

```js
pizza.toppings.push(`cheese`);
```

In some languages, properties can be made `private` and not accessible outside of the class they're created in but this is not possible in Javascript. But, we can add a `_` to the start of a property name and developers will know that they shouldn't access it directly.

```js
class Pizza {
  constructor() {
    this._toppings = [];
  }
  addTopping(topping) {
    this._toppings.push(topping); // "_toppings"
  }
}

let pizza = new Pizza();

pizza.addTopping("cheese");
pizza.addTopping("mushrooms");
```

By prefixing toppings with `_` we are letting other developers kon wthat they shouldn't access that property directly. They can still access it but they should know they're doing something wrong.

```js
pizza._toppings.add("pineapple");
```


</br>

## Single Responsibility Principle

The single responsibility principle states that a class should be responsible for a single part of the app's functionality, giving it only one reason to change. More simply, a class hould have ***ONE*** job.

Take a look at the following example:

```js
// Manage the state of a task
class Task {
  complete() {
    // Mark this task as complete
  }
  sendNotification() {
    // Send a notification to the user that their task is complete
  }
  saveToDatabase() {
    // Save this task to the database
  }
}

let task = new Task();
task.saveToDatabase();
task.complete();
task.sendNotification();
task.saveToDatabase();
```

This class's purpose is to manage the state of a task, but it's currently responsbile for 3 different things and has 3 separate reasons to change.

1. If the way a task's state is managed changes, like using a string instead of a boolean to mark a task as done, then the first method has to change.
2. If our in-app notification system changes, from browser notifications to email notifications, then the second method has to change.
3. If we need to change how it's persisted in the database, then the third method has to change.

Our class has too many raons to change and each mehtod has access to the entire internal state of the object. A change to the notifications could break the database method.

This violates the ***Single Responsibility Principle***. This object should be broken up into more objects that do one thing.

```js
// Manage the state of a task
class Task {
  complete() {
    // Mark this task as complete
  }
}

class NotificationManager {
  sendNotification(task) {
    // Send a notification to the user that their task is complete
  }
}

class DatabaseManager {
  saveToDatabase(task) {
    // Save this task to the database
  }
}

let task = new Task();
databaseManager.saveToDatabase(task);
task.complete();
notificationManager.sendNotification(task);
databaseManager.saveToDatabase(task);
```

Now each object has one reason to change. If we use abstraction and single responsibility principle, then a change to one part of our app won't affect other unrealted parts of the app. Changing from PostgreSQL to Mongo, for example, should not affect our notification system.

</br>

## Inheritance

When not using OO, we use functions and modules to reduce duplicate code and make our code more reusable. When using OO we can use inheritance to acheive this.

```js
class Flower {
  water() {
    console.log("Watering the flower");
    this.lastWatered = Date();
  }
}

class Tree {
  water() {
    console.log("Watering the tree");
    this.lastWatered = Date();
  }
}

class Bush {
  water() {
    console.log("Watering the bush");
    this.lastWatered = Date();
  }
}
```

We can get rid of the duplicate code above using inheritance.

```js
class Plant {
  water() {
    console.log(`Watering the ${this.type}`);
    this.lastWatered = Date();
  }
}

class Flower extends Plant {
  constructor() {
    super()
    this.type = "flower";
  }
}

class Tree extends Plant {
  constructor() {
    super()
    this.type = "tree";
  }
}

class Bush extends Plant {
  constructor() {
    super()
    this.type = "bush";
  }
}
```

Now if the water method changes, the code only has to be changed in one place. Use inheritance to reduce duplicate code and share behaviour between classes.