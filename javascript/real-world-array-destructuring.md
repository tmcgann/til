# Real World Array Destructuring

## Introduction

If you're new to desctructuring it can be hard to know when it can be really helpful, i.e. when it can make your code more readable, concise, and maintainable. You could argue that in some instances or when overused, destructuring can make code harder to read or understand.

One of the best real world use cases for destructuring arrays is when using `Promise.all`.

## Example

Let's say we have a number of async data requests that return promises, we want to execute all of them in parallel, and we want to wait for all of them to resolve before continuing.

```js
// For simplicity, let's NOT fetch real data and instead return some resolved promises :)
const promises = [
  Promise.resolve('foo'),
  Promise.resolve('bar'),
  Promise.resolve('baz'),
]
```

WITHOUT desctructuring, we might do something like this:

```js
Promise.all(promises)
  .then(values => {
    console.log(values[0]) // foo
    console.log(values[1]) // bar
    console.log(values[2]) // baz
  }, err => {
    console.error(err)
  })
```

In a attempt to make the code more intelligible, we could do something like this:

```js
Promise.all(promises)
  .then(values => {
    const foo = values[0];
    const bar = values[1];
    const baz = values[2];
    console.log(foo)
    console.log(bar)
    console.log(baz)
  }, err => {
    console.error(err)
  })
```

I would argue destructuring is much more readable and concise--you can accomplish the same thing in fewer lines of code AND make sense of it quicker.

WITH desctructuring, we would do this:

```js
Promise.all(promises)
  .then(([foo, bar, baz]) => { // <-- destructure the array of resolved promises for more readable code
    console.log(foo)
    console.log(bar)
    console.log(baz)
  }, err => {
    console.error(err)
  })
```

With destructuring, it becomes immediately apparent what the promise resolution values represent in a concise and easy-to-read format.

Play around with [this Babel REPL example](https://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015%2Ces2016%2Cstage-3&targets=&browsers=&builtIns=false&experimental=false&loose=false&spec=true&code=const%20promises%20%3D%20%5B%0A%20%20Promise.resolve('foo')%2C%0A%20%20Promise.resolve('bar')%2C%0A%20%20Promise.resolve('baz')%2C%0A%20%20%2F%2F%20Promise.reject(new%20Error('baz'))%2C%0A%5D%0A%0A%2F%2F%20WITH%20desctructuring%0APromise.all(promises)%0A%20%20.then((%5Bfoo%2C%20bar%5D)%20%3D%3E%20%7B%20%2F%2F%20%3C--%20desctructure%20the%20array%20of%20resolved%20promises%20for%20more%20readable%20code%0A%20%20%20%20console.log(foo)%0A%20%20%20%20console.log(bar)%0A%20%20%20%20console.log(baz)%0A%20%20%7D%2C%20err%20%3D%3E%20%7B%0A%20%20%20%20console.error(err)%0A%20%20%7D)).

Original source: https://philna.sh/blog/2017/02/09/toast-to-es2015-destructuring/
