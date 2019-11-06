# Providing default values for missing data

Sometimes objects returned from an API will have missing properties.

In the data below, the second object's `imageSrc` property is undefined and the third is missing its `name` property entirely.

```js
const dogArray = [
    {
        id: 1,
        name: "Burt",
        imageSrc: "path/to/image"
    },
    {
        id: 2,
        name: "Penny",
        imageSrc: undefined
    },
    {
        id: 3,
        imageSrc: "path/to/image"
    }
];
```

We can provide default values for the missing properties before trying to use them.

```js

// we create these before the loop

// provide a default path for the image
let imageUrl = "path/to/a/default/image";

// provide default text for the dog name
let name = "This dog has no name";

dogArray.forEach(function(dog) {

    //inside the loop we check the properties
    // check if dog.imageSrc exists and it is "truthy" - not null, undefined or an empty string
    if(dog.imageSrc) {
        imageUrl = dog.imageSrc;
    }

    // check if dog.name exists and it is "truthy"
    if(dog.name) {
        name = dog.name;
    }

    // now we use the variables we created, not the properties on the object

    // this will print "path/to/a/default/image" if dog.imageSrc is missing
    // and whatever is in dog.imageSrc if it is not missing
    console.log(imageUrl) 

    // this will print "This dog has no name" if dog.name is missing
    // and whatever is in dog.name if it is not missing
    console.log(name)

    // we didn't create a default value for dog.id as we assume it always exists
    // so we access it directly on the dog object
    console.log(dog.id);

})

```

Let's see how we can apply that when creating an HTML string in a loop:

```js
   
    let newHTML = "";

    let imageUrl = "path/to/a/default/image";
    let name = "This dog has no name";

    dogArray.forEach(function(dog) {

        if(dog.imageSrc) {
            imageUrl = dog.imageSrc;
        }

        if(dog.name) {
            name = dog.name;
        }

        // now we use imageUrl instead of dog.imageSrc
        // and name instead of dog.name
        // we still use dog.id
        
        newHTML += `<div class="dog">
                        <h1>${name}</h1>
                        <img src="${imageUrl}">
                        <a href="path/to/more/details/${dog.id}">More details</a>
                    </div>`;
    });

    // after the loop, newHTML will contain the properties from each object and
    // their default values if they are missing

```