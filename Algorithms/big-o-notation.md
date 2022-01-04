# BIG O NOTATION

[Notes from freeCodeCamp YouTube](https://youtu.be/Ee0HzlnIYWQ)

How code slows as data grows.

Terminology:

* O(blah blah N blah)
* N: how much data
* O: Order of

In order of best to worst case scenarios:

## O(1) - Constant Time

## O(log n) - Logarithmic

### Logarithms

In computer science, unless otherwise specified, we can assume the number we are raising to some power is `2`.

`2^? = 8 => Log₂8 = ? => ? = 3`

```js
// Recursive
function lognRecursive(n) {
  if (n === 0) return "Done";
  n = Math.floor(n/2);
  return lognRecursive(n);
}

// Iterative
function lognIterative(n) {
  while (n > 1) {
    n = Math.floor(n/2)
  }
}
```
In the example above, if we substitute n with 8, this fucntion will run 3x. `Log₂8 = 3`

<br>

### Binary Search & O(log n)

Must have an ***ordered*** array. Both ascending and descending will work. To perform a binary search we will cut the array in half and determine if our number is less than or greater than the mid point.

Example: We are looking for 100 in the following array.

[1, 2, 7, 12, 43, 44, 54, 100, 124]

The midway point is 43. 43 < 100 so we can remove everything to the right of and including 43 in our array.

[44, 54, 100, 124]

Array.length is now 4 => 4/2 = 2

Our 100 is now at index 2 and we've found our number 100.

<br>

Code Example:

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8];
let start = 0;
let end = arr.length - 1;
let target = 8;

function binarySearch(arr, start, end, target) {
  if (start > end) return false;
  let midIndex = Math.floor((start+end) / 2);
  if (arr[midIndex] === target) return true;

  if (arr[midIndex] > target) {
    return binarySearch(arr, start, midIndex - 1, target);
  } else {
    return binarySearch(arr, midIndex + 1, end, target);
  }
}
```

<br>

## O(n) - Linear

<br>

## O(n log n) - Linearithmic

```js
function nLogNFunc(n) {
  let y = n;
  while (n > 1) {
    n = Math.floor(n / 2);
    for (let i = 1; i <= y; i++) {
      console.log(i);
    }
  }
}
```

## O(n²) - Quadratic

Nested for loops are considered quadratic.

```js
function square(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++>) {
      console.log(i, j);
    }
  }
}
```

Replacing n with 4 in the code above would produce a 4 x 4 matrix. 4 x 4 = 16 which is the same as 4².

## O(n³) - Cubic

```js
function cube(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++>) {
      for (let k = 0; k < n; k++>) {
        console.log(i, j, k);
      }
    }
  }
}
```

## O(n!) - Factorial

O(n!) => O(3!) => 3 * 2 * 1 = 6 => O(3!) = 6


<br>

## Big-O

* complexity
* time complexity
* algorithmic complexity
* asymptotic complexity


## Determining Big-O

* Identify your code
* Identify N
* Count the steps in a ***typical*** run
* Keep the most significant part
  * remove insignificant coefficients

