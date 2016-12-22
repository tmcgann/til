There are a number of ways to partially apply functions in JavaScript i.e. wrap functions in other functions with some or all of the arguments applied.

```js
// original function
function hello(first, last) {
  console.log(`hello ${first} ${last}`);
}

// use a function declaration to wrap the original function
function helloFunctionDeclaration() {
  hello('taylor', 'mcgann');
}

// use a function expression to wrap the original function
const helloFunctionExpressionA = () => hello('taylor', 'mcgann');
const helloFunctionExpressionB = function () { hello('taylor', 'mcgann'); };
const helloFunctionExpressionC = function helloFunctionExpressionC() { hello('taylor', 'mcgann'); };

// use bind to produce a new function with the applied arguments
const helloFunctionBind = hello.bind(null, 'taylor', 'mcgann');

// all yield the same output
hello('taylor', 'mcgann');
helloFunctionDeclaration();
helloFunctionExpressionA();
helloFunctionExpressionB();
helloFunctionExpressionC();
helloFunctionBind();
```

One place where this kind of function wrapping is useful is if you have a lot of known arguments and you want to hide them away inside a wrapper to make the code more readable.
