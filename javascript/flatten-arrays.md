Some ways to flatten arrays...

Flatten Shallow:

```js
const flatten = (arr) => [].concat.apply([], arr)
const arr = [[1],[2,3],[4,5,6],[7,8,9,0]]
flatten(arr) // [1,2,3,4,5,6,7,8,9,9]
```

Flatten Deep:

```js
const flatten = (arr) => arr.reduce((accum, val) => accum.concat(Array.isArray(val) ? flatten(val) : val), [])
const arr = [[1],[[2,3]],[[[4,5,6]]],[[[[7,8,9,0]]]]]
flatten(arr) // [1,2,3,4,5,6,7,8,9,9]
```
