# REGULAR EXPRESSIONS (REGEX)

[Notes taken from freeCodeCamp - Javascript Algorithms and Data Structures](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/regular-expressions)

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

Above, we've only checked to see if a pattern exists in a string or not. We can also extract the actual matches using `.match()`.

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

You can use the `g` flag on the regex to return an array containing only the word.

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

You can use the wild card character `.` to match any on character. For example, to match `hug`, `huh`, `hut`, and `hum`, you can use the regex `/hu./` to match all four words.

```js
let humStr = "I'll hum a song";
let hugStr = "Bear hug";
let huRegex = /hu./;
huRegex.test(humStr);
huRegex.test(hugStr);
// both tests would return true
```

</br>

## Match Single Character with Multiple Possibilities

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

Inside a `character set`, you can define a range of characters to match using a hyphen `-`. For example, to match lowercase characters a through e you would use `[a-e]`

```js
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex); // ['cat']
batStr.match(bgRegex); // ['bat']
matStr.match(bgRegex); // null
```

The `-` is not limited to letters, it can also work with a range of numbers. For example, `/[0-5]/` matches any numbers between, and including, `0` and `5`.

We can also combine a range of letters and numbers in a single character set.

```js
let jennyStr = 'Jenny8675309';
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex);
```

You can also create a `character set` of characters you do NOT want to match called, `negated character sets`.

To create a negated character set, you place a caret character `^` after the opening square bracket, before the characters you do not want to match.

```js
/[^aeiou]/gi
```

</br>

## Match Characters that Occur One or More Times

You can use the `+` character to check if a character appears one or more times in a row.

For example, `/a+/g` would find one match in `abc` and return `['a']`. Because of the `+`, it would also find a single match in `aabc` and return `['aa']`.

If we checked the string `abab`, it would return `['a', 'a']`.

</br>

There is also an option that matches characters that occur ***zero or more times***. This is the `*` character.

```js
let soccerWord = "gooooooooal!";
let gPhrase = "gut feeling";
let oPhrase = "over the moon";
let goRegex = /go*/;
soccerWord.match(goRegex); // ['goooooooo']
gPhrase.match(goRegex); // ['g']
oPhrase.match(goRegex); // null
```

</br>

## Find Characters with Lazy Matching

In regular expressions, a ***greedy*** match finds the longest possible part of a string that fits the regex pattern. The alternative is called a ***lazy*** match, which finds the smallest possible part of the string that satisfies the regex pattern.

You can apply the regex `/t[a-z]*i/` to the string 'titanic'. This regex is looking for a pattern that starts with 't', ends in 'i', and has some characters in between.

Regular expressions are ***greedy by default***, so it would return `['titani']`, finding the largest sub-string possible.

You can change the default to use lazy matching with the `?` character. `/t[a-z]*?i/` returns `['ti']`.


## Match Beginning String Patterns

The caret character `^` we used before to create a negated character set `[^thingsThatWillNotBeMatched]`. Outside a character set, the caret is used to search for patterns at the beginning of strings.

```js
let firstString = "Ricky is first and can be found.";
let firstRegex = /^Ricky/;
firstRegex.test(firstString); // true
let notFirst = "You can't find Ricky now.";
firstRegex.test(notFirst); // false
```

<br>

## Match Ending String Patterns

You can search for patterns at the end of strings using the `$` at the end of the regex.

```js
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding); // true
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding); // false
```