importance: 5

---

# Garip instanceof

<<<<<<< HEAD
Aşağıdaki `instanceof` neden `true` dönüyor? Aslında `a`'nın `B()` tarafından üretilmediği açık.
=======
In the code below, why does `instanceof` return `true`? We can easily see that `a` is not created by `B()`.
>>>>>>> e01998baf8f85d9d6cef9f1add6c81b901f16d69

```js run
function A() {}
function B() {}

A.prototype = B.prototype = {};

let a = new A();

*!*
alert( a instanceof B ); // true
*/!*
```

