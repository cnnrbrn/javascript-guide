# JavaScript Variables

The old way to declare JavaScript variables was with the **var** keyword:

```js
var myString = "hello";
```

Nowadays you can also use **const** and **let**.

```js
const myString = "hei";

let myString = "hi!";
```

There are differences between all of these but we will get to those later.

## Types

Variables can have these types of values:

- `string`
- `number`
- `boolean`
- `null` and `undefined`
- `object`
- `arrays`
- `functions`

### Strings

Strings can range from one character to a whole book-load of characters. They're enclosed in either single `'` or double `"` quotes. You can use either but stick with one throughout your code.

Joining strings together is called **concatenation**:

```js
const myString = "chicken" + "feet";

console.log(myString);
// chickenfeet
```

Let's add another word:

```js
const myString = "chicken" + "feet";

const newString = "my" + myString;

console.log(newString);
// mychickenfeet
```

Let's redeclare `newString` and add a space:

```js
const newString = "my" + " " + myString;

// or
const newString = "my " + myString;

console.log(newString);
// my chickenfeet
```
