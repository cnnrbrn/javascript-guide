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

We can join strings together with the `+` operator. This is called **concatenation**:

```js
const myString = "sheep" + "dog";

console.log(myString);
// sheepdog
```

Let's add another word:

```js
const myString = "sheep" + "dog";

const newString = "my" + myString;

console.log(newString);
// mysheepdog
```

Let's redeclare `newString` and add a space:

```js
const newString = "my" + " " + myString;

// or
const newString = "my " + myString;

console.log(newString);
// my sheepdog
```

### Numbers

We add numbers with the `+` operator:

```js
const total = 2 + 2;
```

If we try to add the `string` `"2"` and the `number` `2`, we'll end up with a `string`:

```js
const total = "2" + 2;
console.log(total);
// "22"
```

To convert a string to a number we can use the Number() method:

```js
const total = Number("2") + 2;
console.log(total);
// 4
```
