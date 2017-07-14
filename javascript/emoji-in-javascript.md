Sometimes you want to put an emoji in your JavaScript. One way to do that is to simply copy and paste the glyph. But what if you want to use unicode? And what if the unicode is greater than `FFFF`?

```js
('javascript is growing up! ').padEnd(35, `\u{1f62d}`);
// "javascript is growing up!😭😭😭😭😭"
```
