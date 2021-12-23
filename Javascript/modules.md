# MODULES

[freeCodeCamp notes on Javascript Modules](https://www.freecodecamp.org/news/javascript-modules-beginners-guide/)

## The Export Keyword 

To make a module available to other files, you can use the `export` keyword.

```js
// math.js
function add(a, b) => a + b;

export default add;
```

Alternatively the `export` keyword can be used before the function definition:

```js
export default function add(a, b) => a + b;
```

</br>

## The Import Keyword

We can use the `import` keyword to add the funciton to our other js files.

```js
// script.js
import add from './math.js';
```

Our add function is now available inside the script.js file.

</br>

## Named Exports vs Default Exports

With ES modules you can use either named or default exports. When using the ***default*** (as in our example above) you can rename your import.

```js
// change name from add to addition
import addition from './math.js';
```

***Named*** exports are used to export multiple values from a module.

```js
// math.js
export function subtract(a, b) => a - b;
export function multiply(a, b) => a * b;
```

```js
// script.js
import { multiply, subtract } from './math.js';
```

We can import both named and default together:

```js
import add, { multiply, subtract } from './math.js';
```

We can also rename our named exports using the `as` keyword:

```js
import { subtract as subtractNumbers } from './math.js';
```