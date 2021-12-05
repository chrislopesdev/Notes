# cURL

[15 practical Linux cURL examples](https://www.thegeekstuff.com/2012/04/curl-examples/)

## Download a single file

The following code will print the content of the url to the terminal. Use the flag -i to inspect the resonse headers 

```js
curl www.amazon.ca
```

To save the results to a file use:

```js
curl www.amazon.ca > amazon.html
```