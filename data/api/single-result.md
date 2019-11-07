# Displaying a single result from an API call

To get a single, specific result from an API, we often need to send an `id` with the API call. This `id` often comes from the querystring (in the URL) on the page.

This code will get the `id` from the URL:

```js
function getQueryStringValue (key) {
    return decodeURIComponent(window.location.search.replace(new RegExp("^(?:.*[&\\?]" + encodeURIComponent(key).replace(/[\.\+\*]/g, "\\$&") + "(?:\\=([^&]*))?)?.*$", "i"), "$1"));
}

var id = getQueryStringValue("id");
```

Now we have the `id`:

```js
console.log(id);
// abcdefg
```

If we didn't get to the page by clicking on a card, there may not be an id to get from the URL. We can tell the user that:

```js
if(id === undefined) {
    alert("There is no id");
}
```

Now we have the id, we can build the URL that we will use to call the API.

If this is our base URL:

```js
const baseURL = "path/to/url/";
```

and this is our id:

```js
// abcdefg
```

We can add the id to the baseURL to get the full URL we need:

```js
const url = baseURL + id;
// path/to/url/abcdefg
```

If there is no `/` at the end of the `baseURL` we must add it when creating the `url`:

```js
const url = baseURL + "/" + id;
// path/to/url/abcdefg
```

Now that we have created the `url` we can make the call using fetch:

```js
//make the API call using fetch
fetch(url)
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        console.log(json);
        /*            
            { 
                dog: {
                    id: 1,
                    name: "Burt",
                    imageSrc: "path/to/image"
                } 
            }                               
        */
    });
```

Because we are making a specific call to get one result, we don't receive an array of objects but a single object. Remember to console log the result to see where that result object is.

Let's create a function to call from the second `then`:

```js
function displayDog(json) {
    console.log(json);
}
```

And call it from the then:

```js
fetch(url)
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        displayDog(json);       
    });
```

If we need to get the object from the json, we use `.` notation as usual:

```js
function displayDog(json) {
    const dog = json.dog;
}
```

We don't need a loop here as we only have one dog object. We can access the properties directly:

```js
function displayDog(json) {

    const dog = json.dog;

    console.log(dog.name);
    // Burt
}
```

If we wanted to use the object's properties to create HTML similar to this:

```html
<div class="dog-details">
    <div>
        <b>Id:</b> 3
    </div>
    <div>
        <b>Name:</b> Bob
    </div>
</div>
```

We would first find the element:

```js
// assuming a <div class="dog-details"> exists in our HTML
const dogDetails = document.querySelector(".dog-details");
```

And then create the HTML using `innerHTML`:

```js
function displayDog(json) {

    const dog = json.dog;

    const dogDetails = document.querySelector(".dog-details");

    dogDetails.innerHTML = `<div>
                                <b>Id:</b> ${dog.id}
                            </div>
                            <div>
                                <b>Name:</b> ${dog.name}
                            </div>`;
}
```

We only add the HTML between the element that we selected, so everything inside

```html
<div class="dog-details">

</div>
```

We don't use `+=` only `=` as we are not creating the HTML in a loop.


Here it is all together:

```js
function getQueryStringValue (key) {
    return decodeURIComponent(window.location.search.replace(new RegExp("^(?:.*[&\\?]" + encodeURIComponent(key).replace(/[\.\+\*]/g, "\\$&") + "(?:\\=([^&]*))?)?.*$", "i"), "$1"));
}

var id = getQueryStringValue("id");

const baseURL = "path/to/url/";

const url = baseURL + "/" + id;

fetch(url)
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        displayDog(json);       
    });

function displayDog(json) {

    const dog = json.dog;

    const dogDetails = document.querySelector(".dog-details");

    dogDetails.innerHTML = `<div>
                                <b>Id:</b> ${dog.id}
                            </div>
                            <div>
                                <b>Name:</b> ${dog.name}
                            </div>`;
}
```


