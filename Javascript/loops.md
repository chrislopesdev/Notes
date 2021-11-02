# LOOPS

## While Loops

### Parts of a While Loop

1. When to start
2. When to stop
3. How to get to the next item

Example:

```
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

```
for (start; stop; step) {
  // do something
}
```

Example of a loop that counts from 0 - 5:

```
for (let i = 0; i < 6; i++) {
  console.log(i)
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
