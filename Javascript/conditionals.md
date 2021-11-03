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

<code>
!value1
</code>
