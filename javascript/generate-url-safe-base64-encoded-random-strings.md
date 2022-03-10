# Generate URL-safe base64 encoded random strings

Standard Base64 encoded data is not URL safe because the `/`, `+` and `=` need to be encoded. A [standardized URL-safe Base64 encoding](https://en.wikipedia.org/wiki/Base64#RFC_4648) exists ([RFC-4648](https://datatracker.ietf.org/doc/html/rfc4648#section-5)).

```js
function generateRandomShortId(bytes = 7) {
  // Construct a typed array with a specified number of bytes
  const array = new Uint8Array(bytes)
  
  // Use `getRandomValues` to fill the array with random integer values
  crypto.getRandomValues(array)
  
  // Base64 encode the data; one way is to use a library like `base64url`
  return base64url.encode(array.buffer)
}

// One-liner
const generateRandomShortId = bytes => base64url.encode(crypto.getRandomValues(new Uint8Array(bytes)).buffer)
```
