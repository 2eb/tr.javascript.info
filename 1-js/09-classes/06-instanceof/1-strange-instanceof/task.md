importance: 5

---

# Garip instanceof

<<<<<<< HEAD
Aşağıdaki `instanceof` neden `true` dönüyor? Aslında `a`'nın `B()` tarafından üretilmediği açık.
=======
In the code below, why does `instanceof` return `true`? We can easily see that `a` is not created by `B()`.
>>>>>>> cdf382de4cf3ed39ca70cb7df60c4c4886f2d22e

```js run
function A() {}
function B() {}

A.prototype = B.prototype = {};

let a = new A();

*!*
alert( a instanceof B ); // true
*/!*
```

