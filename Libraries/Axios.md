# AXIOS

[Axios Documentation](https://axios-http.com/docs/intro)

[Axios Github](https://github.com/axios/axios)

Axios is a `promise` based `HTTP client` for the browser and node.js

## Installing

```terminal
npm install axios
```

<br />

## Usage

Once installed, we import it like any other dependency. Once we have access to the Axios object, we can access the four most common methods:

- `axios.get(url[, config])`
- `axios.post(url[, config])`
- `axios.put(url[, config])`
- `axios.delete(url[, config])`

### Example of a `GET` request:

```jsx
axios.get('/api/appointments').then((response) => {
  console.log(response);
});
```

When we want to send data to the server, we need to provide a second argument.

```jsx
axios
  .put(`/api/appointments/2`, {
    id: 2,
    time: '1pm',
    interview: {
      student: 'Archie Cohen',
      interviewer: 9,
    },
  })
  .then((response) => {
    console.log(response);
  });
```

<br />

## Errors

There are situations where an API server responds with status codes that we treat as errors. With Axios we can use the Promise `catch` method to handle them.

```jsx
axios
  .get('/api/appointments')
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.log(error.response.status);
    console.log(error.response.headers);
    console.log(error.response.data);
  });
```

This pattern allows us to handle HTTP requests. When a user tries to login with the incorrect credentials, we would expect `error.response.status` to equal `401`. If they try to access a resource without permission, the response returns `403` status code.

<br/>

## Other Features

- We can cancel an in-progress request
- Set a timeout for a response
- Axios supports [CSRF](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.md) protection
