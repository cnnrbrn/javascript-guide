# forEach

The simplest way to loop through an array is to use the `forEach` method:

We will use this array of objects as an example:

```js
const dogArray = [
    {
        name: "Burt",
        breed: "Labrador"
    },
    {
        name: "Penny",
        breed: "Golden Retriever"
    }
];
```

We can loop over each object in the array by calling the `forEach` method on `dogArray`: 

```js
dogArray.forEach(function(item) {
    console.log(item);
});

// {name: "Burt", breed: "Labrador"}
// {name: "Penny", breed: "Golden Retriever"}
```

For each item in the array, a function is called that receives the item as an argument. We can then do what we want with the item. `item` there is a normal function argument, we can call it anything:

```js
dogArray.forEach(function(dog) {
    console.log(dog);
});
```

Because our dog array is an array of objects, we can use `.` notation to get to each property on the object:

```js
dogArray.forEach(function(dog) {
    console.log(dog.breed);
});

// Labrador
// Golden Retriever
```

More on [functions](../functions/README.md)