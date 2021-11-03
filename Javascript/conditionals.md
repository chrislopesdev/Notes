# CONDITIONALS

![Flow Chart](https://d17h27t6h515a5.cloudfront.net/topher/2016/December/584853f3_buy-the-item-cropped/buy-the-item-cropped.jpg)

```
let price = 15 // price of hammer;
let money = 20 // how much money I have;

if (money >= price) {
  console.log('buy the hammer');
} else {
  console.log('don't buy the hammer');
}
```

## if...else statements

These let you execute code based on a condition or set of conditions being met.

```
if ( true ) {
  // run this code;
} else {
  // run this code;
}
```

```
var a = 1;
var b = 2;

if (a > b) {
  console.log("a is greater than b");
} else {
  console.log("a is less than or equal to b");
}
```

> Prints "a is less than or equal to b"

### Important things about `if...else` statements:

The value inside the `if` statment is always converted to `true` or `false`. Depending on the value, the code inside the `if` statement is run or the code inside the `else` statement is run, but not both.

</br>

## Else...if Statements

In some situations, two conditionals aren't enough.

![Flow chart](https://video.udacity-data.com/topher/2016/November/5834ac48_what-to-wear-cropped/what-to-wear-cropped.jpeg)

In Javascript, you can represent the secondary check by using and extra `if` statement called an `else if` statement.

```
let weather = "sunny";

if (weather === "snow") {
  console.log("Bring a coat.");
} else if (weather === "rain") {
  console.log("Bring a rain jacket.");
} else {
  console.log("Wear what you have on.");
}
```

</br>

## Logical Operators

Logical operators include:

`&&` => logical AND => returns `true` only if both sides of expression are `true`

```
value1 && value2
```

`||` => logical OR => returns `true` if **_either or both_** sides of the expression are `true`

```
value1 || value2
```

`!` => logical NOT ("bang") => returns the **_pposite_** of `value1`. If `value1` is `true`, then `!value1` is `false`.

```
!value1
```

</br>

## Truthy and Falsy

Every value in JavaScript has an inherent boolean value. When that value is evaluated in the context of a boolean expression, the value will be transformed into that inherent boolean value.

### Falsy Values

A value is **_falsy_** if it converts to `false` when evaluated in a boolean context.

**_Falsy Values:_**

1. the Boolean value `false`
2. the `null` type
3. the `undefined` type
4. the nmber `0`
5. an empty sting `""`
6. the odd value `NaN` "not a number"

**_Truthy Values_**
Everything not falsy is truthy!

</br>

## Ternary Operator

Example conditonal:

```
var isGoing = true;
var color;

if (isGoing) {
  color = "green";
} else {
  color = "red";
}

console.log(color);
```

This is too long for simply assigning a value to a variable.

> **_Tip:_** using `if(isGoing)` is the same as using `if(isGoing === true)`. Alternatively, using `if(!isGoing)` is the same as using `if(isGoing === false)`

The **_ternary operator_** provides a shortcut to if...else statements.

```
conditonal ? (if condition true) : (if condition false)
```

To use the ternary operator, first provide a conditional statement on the left-side of the `?`. Then, between the `?` and `:` write the code that would run if the condition is `true` and on the right-hand side of the `:` write the code that would run if the condition is `false`. For example, you can rewrite the example code above as:

```
var isGoing = true;
var color = isGoing ? "green" : "red";
console.log(color);
```

</br>

## Switch Statements

If you find yourself repeating `else if` statements where each condition is based on the same value, you should consider a switch statement.

```
if (option === 1) {
  console.log("You selected option 1.");
} else if (option === 2) {
  console.log("You selected option 2.");
} else if (option === 3) {
  console.log("You selected option 3.");
} else if (option === 4) {
  console.log("You selected option 4.");
} else if (option === 5) {
  console.log("You selected option 5.");
} else if (option === 6) {
  console.log("You selected option 6.");
}
```

A **_switch statement_** is another way to chain multiple `else if` statements that are basedon the same value **_without using conditional statements_**. Instead you _switch_ which piece of code is executed based on a value.

```
switch (option) {
  case 1:
    console.log("You selected option 1.");
    break;
  case 2:
    console.log("You selected option 2.");
    break;
  case 3:
    console.log("You selected option 3.");
    break;
  case 4:
    console.log("You selected option 4.");
    break;
  case 5:
    console.log("You selected option 5.");
    break;
  case 6:
    console.log("You selected option 6.");
    break; // technically, not needed
}
```

### Breat Statement

The **_break statement_** can be used to terminate a switch statement and transfer control to the code following the terminated statement. By adding a `break` to each `case` clause, you fix the issue of the switch statement falling-through to other case clauses.

Some situations may call for "falling-through". For example, a hierarchical-type structure.

```
var tier = "nsfw deck";
var output = "You’ll receive "

switch (tier) {
  case "deck of legends":
    output += "a custom card, ";
  case "collector's deck":
    output += "a signed version of the Exploding Kittens deck, ";
  case "nsfw deck":
    output += "one copy of the NSFW (Not Safe for Work) Exploding Kittens card game and ";
  default:
    output += "one copy of the Exploding Kittens card game.";
}

console.log(output);
```

> **_Prints:_** You’ll receive one copy of the NSFW (Not Safe for Work) Exploding Kittens card game and one copy of the Exploding Kittens card game.

The `default` case will be used if none of the values above match the value of the switch expression.
