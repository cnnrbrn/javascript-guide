# Joining strings

We can join strings together using either concatenation with the `+` sign or template literals.

These two methods are often used with the `innerHTML` method to dynamically create HTML elements from data from an API call.

We will use this dummy data to look at both methods.

```js
// array of objects
const dogArray = [
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
];
```

This is the HTML we want to create for each object in the array:

```html
<div class="dog">
    <h1>Name</h1>
    <img src="path/to/image" />
    <a href="path/to/more/details/id">More details</a>
</div>
```

And we need a variable to store the HTML we are creating. We will give this variable an empty variable as its initial value and keep adding to this value.

```js
const newHTML = "";
```

We need to loop over the array and build an HTML string for each dog object:

```js
dogArray.forEach(function(dog) {
    // here we will have access to the dog object
    // we can access properties of the object like usual
    console.log(dog.name);
});
```

Let's create the HTML for each dog:

```js
dogArray.forEach(function(dog) {
    newHTML +=
        '<div class="dog">' +
        '<div class="dog">' +
        "<h1>Name</h1>" +
        '<img src="path/to/image">' +
        '<a href="path/to/more/details/id">More details</a>' +
        "</div>";
});
```

Each time we loop through the array, we are adding the HTML in that string to the `newHTML` variable. We are using the `+` sign to join the strings and allow us to use new lines.

We are using single quotes `'` for the strings as there are double quotes `"` inside them.

The `+=` signs means we want to keep what is already in the variable and add the new string to it. It is the same as saying:

```js
newHTML = newHTML + '<div class="dog">' +
```

If we just used the `=` sign we would replace the current value in `newHTML` with the new value and only end up with the last value.

If you logged `newHTML` you would see three `div`s with a class of "dog" and their contents.

But this is not useful, all the values are static. We need to replace the `id`, `name` and `image` `src` in the HTML.

## Method 1: concatenation

We will use concatenation with the `+` sign first.

We can get those properties from each object and join them together with the HTML using the `+` operator.

```js
dogArray.forEach(function(dog) {
    newHTML +=
        '<div class="dog">' +
        "<h1>" +
        dog.name +
        "</h1>" +
        '<img src="' +
        dog.imageSrc +
        '">' +
        '<a href="path/to/more/details/' +
        dog.id +
        '">More details</a>' +
        "</div>";
});
```

Now our `newHTML` variable will contain the dynamic properties from the objects in the array.

## Method 2: template literals

We need to use backticks

```
`
```

with template literals and we don't need the `+` operator.

We use embedded expressions made of the `$` sign and curly braces `{}` to access each property of the object.

```js
dogArray.forEach(function(dog) {
    //
    newHTML += `<div class="dog">
                    <h1>${dog.name}</h1>
                    <img src="${dog.imageSrc}">
                    <a href="path/to/more/details/${dog.id}">More details</a>
                </div>`;
});
```

---

Using either method, the `newHTML` variable will now contain a string we can assign to the `innerHTML` of an element in the DOM:

```js
// assuming there is a <div> with a class="container" on the HTML page
const container = document.querySelector(".container");
container.innerHTML = newHTML;
```
