---
title: decodeJWT
tags: array,object,function, beginner
firstSeen: 2022-01-10T11:46:15+02:00
lastUpdated: 2022-01-10T11:46:15+02:00
---

decode a json-web-token (JWT).

- Check if a token is available within the `Decodejwt()` function making use of `! operator`.
- Make use of a `try{}catch{}` block to check if an error occured during executing the program which would prevent the program from crashing.
- Check the type of token given making use of the `typeof` opeartor.
- Convert the token into an array by making use of `array.split(delimeter)` function which takes a delimeter as an argument cause jwt token are concatinated by a dot, also extract item from the array making use of array index `[index_position] [1]`.
- Replace every `-` symbol with a `+` within the token and replace any `_` to `\` making use of `replace()` function.
- Decode the given string using `decodeUriComponent()` and `atob()` function.
- Convert the decoded string using `JSON.parse(string)` function which takes a `string` as a parameter.
- Return the result.

```js
function Decodejwt(token) {
  try {
    if (!token || token === "") {
      throw Error("token is missing, cant decode jwt");
    }
    if (typeof token !== "string") {
      throw Error("expected token to be a string but got functionor object");
    }
    var base64Url = token.split(".")[1];
    var base64 = base64Url.replace("-", "+").replace("_", "/");
    var jsonPayload = decodeURIComponent(atob(base64));
    return JSON.parse(jsonPayload);
  } catch (e) {
    return console.log("Something went wrong: Unable to decode jwt", e);
  }
}
```

```js
var decode = Decodejwt(
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
);
//  { sub: "1234567890", name: "John Doe", iat: 1516239022 }
```
