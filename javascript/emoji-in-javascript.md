Sometimes you want to put an emoji in your JavaScript. One way to do that is to simply copy and paste the glyph. But what if you want to use unicode? And what if the unicode value is greater than `\uFFFF`?

Use the curly brace shorthand:

```js
('javascript is growing up! ').padEnd(35, `\u{1f62d}`);
// "javascript is growing up!😭😭😭😭😭"
```
Otherwise you'd have to use a unicode surrogate pair...yuck!
