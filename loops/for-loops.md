# For loops

```js
for (let i = 0; i <= 9; i++) {
  console.log(i);
  // 1
  // 2
  // ...
  // 9
}
```

Let's break it down.

The variable `i` is a normal variable and could be called anything. We could rewrite the loop like this:

```js
for (let frog = 0; frog <= 9; frog++) {
  console.log(frog);
}
```

Normally `i` is used for the variable name, though you may see `k`, `j` or `count` used. 

---

Below we are saying we want to start our loop count at 0.

```js
let i = 0;

//  can also be written as
var i = 0; // the older way
```

We want to keep doing this loop while `i` is `less than` or `equal` to 9.

```js
i <= 9;
```

We're **incrementing** `i` by 1 every time we go through the loop.

```js
i++;
```

This could be written like this:

```js
i = i + 1;
```
