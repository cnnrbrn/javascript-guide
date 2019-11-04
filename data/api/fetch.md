# In progress

# Using fetch to make API calls

First, we make the API call with the URL to the API as the argument to the fetch method:

```js
const url = "path/to/api";

fetch(url);
```

`fetch` uses promises, so when the API call returns successfully a `then` method is called. The argument received by the function in the `then` method is the response from the server:

```js
fetch(url).then(function(response) {
    // this function is called when the API call returns
    // the function argument (response) is what is returned from the API
    console.log(response);
});
```
