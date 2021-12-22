# ARRAYS

A data structure that you can use to store **_multiple values_**. Arrays are also **_organized_** like a numbered list.

```javascript
let donuts = ["glazed", "chocolate dip", "vanilla dip", "old fashioned"];
```

You can store multiple types of data including other arrays:

```javascript
let mixedData = ["abc", 123, true, undefined];

let arraysInArrays = [
  [1, 2, 3],
  ["chris", "lopes"],
  [true, false],
];
```

</br>

## Accessing Array Elements

Each item in an array is referred to as an element. They can be located by index starting at 0.

```javascript
console.log(donuts[1]);
// this will print "chocolate dip" to the console
```

If you try to access an element outside of the array you will return undefined.

```javascript
console.log(donuts[1000]);
// this will print undefined
```

</br>

## Properties and Methods

**_Methods_** are predefined functions built into Javascript. Examples include:

- `.length`
- `.reverse`
- `.sort`
- `.push` & `.pop`

Read more about arrays and their methods: [MDN - Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

</br>

### Array.length

You can find the **_length_** of an array by using the `length` property.

```javascript
let donuts = ["glazed", "chocolate dip", "vanilla dip", "old fashioned"];
console.log(dontus.length);
```

> **_Prints:_** 3

To access the `length` property, type the name of the array followed by a period `.` (the period is uded to access other properties and methods as well), and the word `length`. The `length` property will return the **_number of elements_** in an array.

</br>

### Array.push & Array.pop

You can use the `.push()` method to add elements to the end of an array.

```javascript
let numbers = [1, 2, 3];
numbers.push(4); // adds 4 to the end of the array
```

Notice that you must pass the value of the element you want to add into the `.push()` method. The `.push()` method will return the length of the array after the element has been added.

> The example above will return 4, the new length of the array.

Alternatively your can use `.pop()` to remove elements from the end of an array.

```javascript
let donuts = ["glazed", "chocolate dip", "vanilla dip", "old fashioned"];
donuts.pop(); // removes "old fashioned" from the array
```

> **_Returns:_** "old fashioned"

With the `.pop()` method you do not need to pass a value, instead, `.pop()` will always remove the last element of the array. It will also return the value of the item removed, in case you need to use it.

</br>

### Array.splice

`.splice()` is another handy method that allows you to add and remove elements from anywhere inside an array.

`.splice()` Syntax: [MDN - splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

```janascript
arrayName.splice(arg1, arg2, item1, item2, ..., itemLast);
```

- `arg1` = **_mandatory_** argument, specifies the starting index position to add/remove items. You can use a negative value to specify the position from the end of the array. Ex: -1 specifies the last element.
- `arg2` = optional argument, specifies the count of elements to be removed. If set to `0`, no items will be removed.
- `item1, ..., lastItem` are the elements to be added at the index of `arg1`

`.splice()` will return the elements that were removed.

```javascript
var donuts = ["cookies", "cinnamon sugar", "creme de leche"];
donuts.splice(-2, 0, "chocolate frosted", "glazed");
console.log(donuts);
// ['cookies', 'chocolate frosted', 'glazed', 'cinnamon sugar', 'creme de leche']
```

</br>
</br>

## Spread and Rest

Spread syntax (...) allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.

```js
const numbersToAdd = [4, 5 , 6];
const numbers = [0, 1, 2, 3, ...numbersToadd, 7, 8, 9];
```

> numbersToAdd is now "spread" into the numbers array </br>
> [0, 1, 2, 3, 4, 5, 6, 7 ,8 ,9]

It can be used to copy an array:

```js
const arr1 = [1, 2, 3];
const arr2 = [...arr1];
```
> creates a brand new array that is a copy off arr1

</br>

***REST*** turns elements into an array.

```js
function multiply(multiplier, ...theArgs) {
  return theArgs.map(function(element) {
    return multiplier * element;
  })
}
multiply(2, 1, 2, 3);

// returns [2, 4, 6]
```
> We can use array methods on REST

</br>
</br>

## Array Loops

To loop through an array, you can use a variaple to represent the index in the array, and then loop over that index to perform whatever manipulations your heart desires.

```javascript
var donuts = ["jelly donut", "chocolate donut", "glazed donut"];

// the variable `i` is used to step through each element in the array
for (let i = 0; i < donuts.length; i++) {
  donuts[i] += " hole";
  donuts[i] = donuts[i].toUpperCase();
}
```

> **_donuts array:_** ["JELLY DONUT HOLE", "CHOCOLATE DONUT HOLE", "GLAZED DONUT HOLE"]

</br>

### forEach() loop

The `forEach()` method gives you an alternative way to iterate over an array, and manipulate each element in the array with an inline function expression.

```javascript
var donuts = ["jelly donut", "chocolate donut", "glazed donut"];

donuts.forEach(function (donut) {
  donut += " hole";
  donut = donut.toUpperCase();
  console.log(donut);
});
```

> **_Prints:_** </br>
> JELLY DONUT HOLE </br>
> CHOCOLATE DONUT HOLE </br>
> GLAZED DONUT HOLE </br>

</br>

**_Parameters_**

The function that you pass to the `forEach()` method can take up to three parameters (`element`, `index`, and `array`).

The `forEach()` method will call this function once for each element in the array. Each time it will call the function with different arguments. The `element` parameter will get the value of the array element. The `index` will get you the index number of the element. The `array` parameter will get a reference to the whole array, which is handy if you want to modify the elements.

```javascript
words = ["cat", "in", "hat"];
words.forEach(function (word, num, all) {
  console.log("Word " + num + " in " + all.toString() + " is " + word);
});
```

> **_Prints:_** </br>
> Word 0 in cat,in,hat is cat </br>
> Word 1 in cat,in,hat is in </br>
> Word 2 in cat,in,hat is hat </br>

</br>

### .map()

Using `forEach()` is not useful if you want to permanently modify the original array. `forEach` always returns `undefined`. However, you can create a new array using the `map()` method. With the `map()` method, you can perform an operation on each element of the array, and return a new array.

```javascript
var donuts = ["jelly donut", "chocolate donut", "glazed donut"];

var improvedDonuts = donuts.map(function (donut) {
  donut += " hole";
  donut = donut.toUpperCase();
  return donut;
});
```

> **_donuts array:_** ["jelly donut", "chocolate donut", "glazed donut"] </br> > **_improvedDonuts array:_** ["JELLY DONUT HOLE", "CHOCOLATE DONUT HOLE", "GLAZED DONUT HOLE"]

</br>
</br>

## Arrays in Arrays

To loop over arrays in arrays you need a nested for loop. Look at a box of donuts:

```javascript
var donutBox = [
  ["glazed", "chocolate glazed", "cinnamon"],
  ["powdered", "sprinkled", "glazed cruller"],
  ["chocolate cruller", "Boston creme", "creme de leche"],
];
```

If you wanted to loop over the box and display each donut and its position in the box, you would start with a `for` loop to loop over each row of the box.

```javascript
var donutBox = [
  ["glazed", "chocolate glazed", "cinnamon"],
  ["powdered", "sprinkled", "glazed cruller"],
  ["chocolate cruller", "Boston creme", "creme de leche"],
];

// here, donutBox.length refers to the number of rows of donuts
for (var row = 0; row < donutBox.length; row++) {
  console.log(donutBox[row]);
}
```

> **_Prints:_** </br> > ["glazed", "chocolate glazed", "cinnamon"] </br> > ["powdered", "sprinkled", "glazed cruller"] </br> > ["chocolate cruller", "Boston creme", "creme de leche"] </br>

Since each row is an array of donuts, you next need to set up an inner-loop for each element in the row.

```javascript
for (var row = 0; row < donutBox.length; row++) {
  // here, donutBox[row].length refers to the length of the donut array currently being looped over
  for (var column = 0; column < donutBox[row].length; column++) {
    console.log(donutBox[row][column]);
  }
}
```

> **_Prints:_** </br>
> "glazed" </br>
> "chocolate glazed" </br>
> "cinnamon" </br>
> "powdered" </br>
> "sprinkled" </br>
> "glazed cruller" </br>
> "chocolate cruller" </br>
> "Boston creme" </br>
> "creme de leche" </br>
