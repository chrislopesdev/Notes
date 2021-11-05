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
x - +6; // x = x -6
x *= 2; // x = x * 2
x /= 5; // x = x / 5
```
