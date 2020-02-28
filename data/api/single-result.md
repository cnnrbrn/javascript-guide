# Displaying a single result from an API call

Assign the path to the API to variable:

```js
const url = "path/to/api"
```

Use the variable in a fetch call:

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
const baseURL = "path/to/url/";

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


