# MISC NOTES TO BE TRANSFERRED

## Generate Random Fractions

```javascript
function randomFraction() {
  return Math.random();
}

console.log(randomFraction());
```

To convert to whole numbers:

```javascript
function randomWholeNum() {
  return Math.floor(Math.random() * 10);
}
// will return a random number between 0 and 9 (will never be 10)
```

To generate a random number in a given range:

```javascript
function ourRandomRange(ourMin, ourMax) {
  return Math.floor(Math.random() * (ourMax - ourMin + 1)) + ourMin;
}
console.log(ourRandomRange(5, 15));
// will generate a number between 5 and 15
```

## Converting Strings to Numbers

```javascript
function convertToInteger(str) {
  return parseInt(str);
}

convertToInteger("56");
//will return the number 56
```
