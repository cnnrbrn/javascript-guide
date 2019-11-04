# Objects and Arrays

## Objects

Objects are used to store related variables and functions. Variables inside objects are called properties. Everthing in an object lives inside curly braces: `{}`

```js
{
  name: "Burt", // name is a "property"
  breed: "labrador", // breed is a "property"
}
```

Let's store that object in a variable:

```js
const dog = {
    name: "Burt",
    breed: "labrador"
};
```

We can get properties from objects using dot `.` notation:

```js
console.log(dog.name);
// Burt

console.log(dog.breed);
// labrador
```

Data we get from APIs will usually be an object or an array of objects. If you make an API call to get a specific item it will come back as an object.

## Arrays

Arrays are lists of variables. Values in arrays live inside square brackets: `[]`

```js
["dog", "cat", "pig"];
```

That's an array of strings. Let's store it in a variable:

```js
const petArray = ["dog", "cat", "pig"];
```

Here's an array of numbers:

```js
const numberArray = [7, 34, 18];
```

Arrays can store different types of variables together:

```js
const thingsArray = [11, true, "cow"];
```

And they can store objects:

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

That's an array of two objects.

If you make an API call to get a list of items, this is how the data will come back.

### Looping through arrays

The simplest way to loop through an array is to use the `forEach` method:

```js
dogArray.forEach(function(item) {
    console.log(item);
});

// {name: "Burt", breed: "Labrador"}
// {name: "Penny", breed: "Golden Retriever"}
```

For each item in the array, a function is called that receives the item as argument. We can then do what we want with the item. `item` there is a normal function argument, we can call it anything:

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
