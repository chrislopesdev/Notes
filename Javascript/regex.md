# REGULAR EXPRESSIONS (REGEX)

[Regular Expressions on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

## Test Method

Regular expressions are used in programming languages to match parts of strings. You create patterns to help you do that matching.

[More on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)

To find the word `the` in the string `The dog chased the cat`, you could use the following regex `/the/`.

There are multiple ways to use regexes. One way to test a regex is to use the `.test()` method. The `.test()` method takes a regex applies a string to it (placed in the parentheses), and returns `true` or `false`.

```js
let testStr = 'freeCodeCamp';
let testRegex = /Code/;
testRegex.test(testStr);
// this will return true
```

If you want to search for multiple patterns you can use the `alternation` or `OR` operator `|`.

This will match patterns before or after the alternation operator. For example, if you wanted to match the strings `yes` or `no`, the regex would be `/yes|no/`. You can search for more than two patterns using multiple OR operators, `/yes|no|maybe/`.

Above, our search would only return true if the character's case matched. Example: /Dog/ => 'Dog'.

We can use the can `append` our search with the `i` flag to ignore case in our search.

```js
let myString = "freeCodeCamp";
let fccRegex = /freecodecamp/i; // we add the i here
let result = fccRegex.test(myString);
// this would return true because we added /i to the end of our regex
```

</br>

## Extract Matches

Above, we've only checked to see if a pattern exists in a string or not. We can also extract the actaul matches using `.match()`.

[Read more on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match)

```js
let ourStr = "Regular expressions";
let ourRegex = /expressions/;
ourStr.match(ourRegex);
```

> Note: the .match() syntax is the opposite of the .test() method

```js
'string'.match(/regex/);
/regex/.test('string');
```

The match method will create an array containing the matched word.

```js
[ 'coding', // matched word
  index: 18, // starting character index
  input: 'Extract the word \'coding\' from this string.', // input string
  groups: undefined ]
```

You can use the `g` flag on the regex to return an arry containing only the word.

```js
['coding']
```

The `g` flag will also return more than just the first match.

```js
let testStr = "Repeat, Repeat, Repeat";
let ourRegex = /Repeat/;
testStr.match(ourRegex);
// returns ['Repeat']
```

```js
let repeatRegex = /Repeat/g;
testStr.match(repeatRegex);
// returns ['Repeat', 'Repeat', 'Repeat']
```

</br>

## Match Anything with Wildcard Period

You can use the whild card character `.` to match any on character. For example, to match `hug`, `huh`, `hut`, and `hum`, you can use the regex `/hu./` to match all four words.

```js
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr);
huRegex.test(hugStr);
// both tests would return true
```

</br>

## Match Single Character with Muliple Possibilites

You can search for a literal pattern with some flexibility using character classes. Character classes allow you to define a group of characters you wish to match by placing them inside square brackets `[ ]`.

For example, to match `bag`, `big`, and `bug` but not `bog` - create the regex `/b[aiu]g/`.

```js
let bigStr = "big";
let bagStr = "bag";
let bugStr = "bug";
let bogStr = "bog";
let bgRegex = /b[aiu]g/;
bigStr.match(bgRegex); // true
bagStr.match(bgRegex); // true
bugStr.match(bgRegex); // true
bogStr.match(bgRegex); // null
```

The above works great with only a couple characters but would be tedious for large sets of characters. Fortunately, there is a built-in feature that makes this short and simple.

Inside a character set, you can define a range of characters to match ussing a hyphen `-`. For example, to match lowercase characters a through e you would use `[a-e]`

```js
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex); // ['cat']
batStr.match(bgRegex); // ['bat']
matStr.match(bgRegex); // null
```