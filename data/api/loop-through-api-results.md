# Looping through API results

```js
//make the API call using fetch
fetch("/path/to/api/")
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        console.log(json);
        /*
            {
                dogs: [
                    {
                        id: 1,
                        name: "Burt",
                        imageSrc: "path/to/image"
                    },
                    {
                        id: 2,
                        name: "Penny",
                        imageSrc: "path/to/image"
                    },
                    {
                        id: 3,
                        name: "Harold",
                        imageSrc: "path/to/image"
                    }
                ]
            }
        */
    });
```

In the second `then` method, we have the json data from the server. Within that function we can now do something with that data.

> All APIs return data differently. Inspect (console.log) what is returned from the API to see how to access the properties you need.

When we logged our json argument above, we can see that it is an object with one property called `dogs` which has a value of an array of objects.

Let's create a function we can can call from the final `then` method to loop through that array.

```js
function loopThroughDogs(ourArgument) {
    console.log(ourArgument);
}
```

Now we can call that from the `then`:

```js
fetch("/path/to/api/")
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
        // we pass json to loopThroughDogs
        // this will become the argument we receive in that function
        loopThroughDogs(json);
    });
```

Let's change our argument name to something more meaningful:

```js
function loopThroughDogs(dogObject) {
    console.log(dogObject);
}
```

We saw above that response from the API is an object with one property called `dogs`. That's the array we need to loop through. Let's get that array:

```js
function loopThroughDogs(dogObject) {
    const dogArray = dogObject.dogs;
}
```

Now we can loop through that array:

```js
function loopThroughDogs(dogObject) {
    //get the array
    const dogArray = dogObject.dogs;

    //loop through the array
    dogArray.forEach(function(dog) {
        // we have access to each dog object inside this function
        console.log(dog);
    });
}
```

Let's create a variable we can add the HTML in a string to, then add to it inside the loop:

```js
function loopThroughDogs(dogObject) {
    const dogArray = dogObject.dogs;

    const newHTML = "";

    dogArray.forEach(function(dog) {
        // add to the HTML
        newHTML += `<div class="dog">
                        <h1>${dog.name}</h1>
                        <img src="${dog.imageSrc}">
                        <a href="path/to/more/details/${dog.id}">More details</a>
                    </div>`;
    });
}
```

Our variable `newHTML` now has all the HTML we can add to an element in our HTML page, using `innerHTML`:

```js
// assuming there is a <div> with a class="container" on the HTML page
const container = document.querySelector(".container");
container.innerHTML = newHTML;
```

---
