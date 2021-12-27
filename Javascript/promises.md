# PROMISES

A `Promise` is a constructor function and needs to use the `new` keyworkd to create it. It takes a function as it's argument, with two parameters: `resolve` and `reject`. The syntax loooks like this:

```js
const myPromise = new Promise((resolve, reject) => {

});
```

A promise has three states: `pending`, `fulfilled`, and `rejected`. While the function is working it is in pending. If the function suceedes it has fulfilled and if failed, rejected.

```js
const myPromise = new Promise((resolve, reject) => {
  if (true) {
    resolve('the promise was fulfilled');
  } else {
    reject('the promise was rejected');
  }
});
```

</br>

## Handle a Fulfilled Promise with `then`

Promises are most useful when you have a process that takes an unknown amount of time in your code (something asynchronous), often a server request. Making a server request can take some time to complete and afterwards, you usually want to do soemthing with the response from the server. The `then` method is executed immeditately after your promise is fulfilled with 'resolve`.

```js
myPromise.then(result => {

});
```

</br>

## Handle a Rejected Promise with `catch`

`catch` is the method used when your promise has been rejected. It is executed immediately after a promise's `reject` method is called.

```js
myPromise.catch(error => {

});
```

