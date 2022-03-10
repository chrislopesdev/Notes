# TESTING

> "Write tests. Not too many. Mostly integration." - Kent C. Dodds

<br />

## Testing Frameworks

[Mocha](https://mochajs.org/#installation) - Javascript testing for Node.js and browser

[Chai](https://www.chaijs.com/) - Assertion Library (Used with Mocha)

[Jest](https://jestjs.io/docs/getting-started) - JavaScript Testing Framework with a focus on simplicity

[Jest with Create React App](https://create-react-app.dev/docs/running-tests) - Pre-installed JS testing for React

<br />

## Jest with Create-React-App

### Writing Tests

To create tests, add `it()` blocks with the name of the test and its code. Jest provides a built-in `expect()` global function for making assertions.

```js
import sum from './sum';

it('sums numbers', () => {
  expect(sum(1, 2)).toEqual(3);
  expect(sum(2, 3)).toEqual(5);
});
```

All `expect()` matchers supported by Jest are [documented here](https://jestjs.io/docs/expect).
