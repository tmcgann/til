# Overview

Was reading this JS perf post today and stumbled upon some insightful comments related to how indexed and named properties work in JavaScript, at least in the V8 engine.

# Original Transcript

What follows is an exchange of comments from a blog post I was reading on basic JavaScript performance optimization principles.

The "list trick" referenced in the first comment is as follows:

```js
// To avoid an array as a possible performance optimization you index the object itself
class EventEmitter {
    //constructor() {
    //    this.listeners = [];
    //}

    //addListener(fn) {
    //    this.listeners.push(fn);
    //}
    
    constructor() {
        this.length = 0;
    }

    addListener(fn) {
        var index = this.length;
        this.length++;
        this[index] = fn;
    }
}
```

---

> The other technique I'm suspicious about without measurements to show for is the list trick (ie. the EventEmitter example) - I imagine a javascript array is highly optimized and when you replace it with index properties of an object you end up with a less optimized implementation (eg. hash table). So you may have faster inserts and removes, but when you loop over the eventEmitters you end up with a slower loop. Perhaps you can extend an Array prototype instead? [1]

---

> At spec level JavaScript array is just an object whose `.length` property has to be updated when indexed properties change. Hash table wouldn't be faster than plain array for any operation.

> You can tell if an implementation (a reasonable mainstream one I.E. one that doesn't do unreasonable things just to mess with me) uses arrays to back up indexed properties if it retains insertion order for named properties but cannot do it for indexed properties:

> ```js
var o = {};
o.value = 1;
o.anotherValue = 2;
o[5] = 3;
o[0] = 4;
o.thirdValue = 5;
console.log(Object.keys(o));
```

> The result should either be `0, 5, value, anotherValue, thirdValue` or `value, anotherValue, thirdValue, 0, 5`. The insertion order of indexed properties cannot be retained in simple array implementation and you get 0, 5 instead of the expected 5, 0. The usual implementation for named properties is "hidden class" so you get them in insertion order as the hidden class has evolved the in the same order. [2]

---

> Does this mean that index properties does not affect an objects hidden class? I.e. I can add all the index properties I want to an object created by a class constructor without it affecting the objects hidden class and still get fast lookup for it's non-index keys?" [3]

---

> ...indexed properties are tracked completely separately in V8 and most likely in other implementations too." [4]

---

**References**

- [1] https://reaktor.com/blog/javascript-performance-fundamentals-make-bluebird-fast/?utm_source=javascriptweekly&utm_medium=email#comment-2874297142
- [2] https://reaktor.com/blog/javascript-performance-fundamentals-make-bluebird-fast/?utm_source=javascriptweekly&utm_medium=email#comment-2874315478
- [3] https://reaktor.com/blog/javascript-performance-fundamentals-make-bluebird-fast/?utm_source=javascriptweekly&utm_medium=email#comment-2875636352
- [4] https://reaktor.com/blog/javascript-performance-fundamentals-make-bluebird-fast/?utm_source=javascriptweekly&utm_medium=email#comment-2875675429

# Takeway #1

A JavaScript Array is just an object whose `length` property has to be updated when indexed properties change (but not named properties). Try it for yourself:

```js
var arr = [1,2,3];
console.log(arr.length); //3
arr.foo = 'bar';
console.log(arr.length); //3
arr[5] = 0;
console.log(arr.length); //6
```

# Takeway #2

You can add **indexed** properties to an object WITHOUT affecting the object's hidden class and therefore NOT affect the performance optimizations of the object's named properties.
