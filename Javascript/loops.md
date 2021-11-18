# LOOPS

## While Loops

### Parts of a While Loop

1. When to start
2. When to stop
3. How to get to the next item

Example:

```javascript
let start = 0;
while (start < 10) {
  console.log(start);
  start += 1;
}
```

> **_Prints:_** </br>
> 0 </br>
> 1 </br>
> 2 </br>
> ...</br>
> 9 </br>

If a loop is missing any of these three things, the loop is broken, and can result in a neverending loop.

</br>

## Do ... While Loops

This is different than a `while` loop as it will perform the action at least once, before checking the condition.

```javascript
let myArray = [];
let i = 10;

do {
  myArray.push(i);
  i++;
} while (i < 5);

console.log(i, myArray);
```

</br>

## For Loops

### Parts of a For Loop

Most common loop. The `for loop` explicitly forces you to define the start and stop points and each step of the loop. If you're missing any of these you will get an `Uncaught SyntaxError: Unexpected token`

```javascript
for (start; stop; step) {
  // do something
}
```

Example of a loop that counts from 0 - 5:

```javascript
for (let i = 0; i < 6; i++) {
  console.log(i);
}
```

> **_Prints:_** </br>
> 0 </br>
> 1 </br>
> ... </br>
> 5 </br>
> 6 </br>

</br>

### Nested Loops

Loops can be nested inside another loop, see example:

```javascript
for (var x = 0; x < 5; x = x + 1) {
  for (var y = 0; y < 3; y = y + 1) {
    console.log(x + "," + y);
  }
}
```

> **_Prints:_** </br>
> 0, 0 </br>
> 0, 1 </br>
> 0, 2 </br>
> 1, 0 </br>
> 1, 1 </br>
> 1, 2 </br>
> 2, 0 </br>
> 2, 1 </br>
> 2, 2 </br>
> 3, 0 </br>
> 3, 1 </br>
> 3, 2 </br>
> 4, 0 </br>
> 4, 1 </br>
> 4, 2 </br>

For each value of `x` in the outer loop, the inner loop executes completely. The outer loop startes with `x = 0`, and then the inner loop completes its cycle with all values of `y`.

Once the inner loop finishes iterating over `y`, the outer loop continues to the next value, `x = 1`, and the inner loop starts again.

</br>

## Increment and Decrement

**_Summary of operators_**

```javascript
x++; // x = x + 1
x--; // x = x - 1
x += 3; // x = x + 3
x -= 6; // x = x -6
x *= 2; // x = x * 2
x /= 5; // x = x / 5
```

</br>
</br>

# RECURSION

An alternative to loops.
[freeCodeCamp article on Recursion](https://www.freecodecamp.org/news/how-recursion-works-explained-with-flowcharts-and-a-video-de61f40cb7f9/)

In its simplest form, a recursive function is one that calls itself.

## Loops vs Recursion

### Iterative approach

```javascript
function multiply(arr, n) {
  let product = 1;
  for (let i = 0; i < n; i++) {
    product *= arr[i];
  }
  return product;
}
```

### Recursive approach

```javascript
function multiply(arr, n) {
  if (n <= 0) {
    return 1;
  } else {
    return multiply(arr, n - 1) * arr[n - 1];
  }
}
```

</br>

### Base Case & Recursive Case

To avoide an infinite loop you must include a base case. The base case tells the function to stop calling itself, preventing infinite loops. The recursive case tells the function to call itself.

```javascript
function countdown(i) {
  console.log(i);
  if (i <= 1) {
    // base case
    return;
  } else {
    // recursive case
    countdown(i - 1);
  }
}

countdown(5); // initial call of the function
```

![summary of coundown function](https://cdn-media-1.freecodecamp.org/images/1*rQ9Z3DmtGk1Bb6_Mx5W6rQ.png)

The function works like this:

We start by printing 5 to the console. Since 5 is not less than or equal to zero, we go to the else statement. There, we call the function again with the number 4 (5 - 1 = 4?).

We now log the number 4 and repeat the above sequence until i is equal to 1. We then hit the return statement and leave the function.

<br>

## The Call Stack

Recursive function use something called "the call stack". When a program calls a function, that function goes on top of the call stack. Similar to making a stack of books. You add one at a time and when you are ready, you take them off from the top.

Example using factorial function. 5! = 5 _ 4 _ 3 _ 2 _ 1.

```javascript
function fact(x) {
  if (x === 1) {
    return 1;
  } else {
    return x * fact(x - 1);
  }
}

fact(3);
```

The below illustration shows how the stack changes, line by line.

![Call stack illustration](https://cdn-media-1.freecodecamp.org/images/1*YRkMsMPRFAt8Y9BiC0QVDg.png)

Notice how each call to fact has its own copy of `x`. This is very important to making recursion work. You can't access a different function's copy of `x`.
