# ES6-features
**[ES6-features](http://es6-features.org/)**

###Constants
#####ECMAScript 6
``` js
const PI = 3.141593
PI > 3.0
```

#####ECMAScript 5
``` js
Object.defineProperty(typeof global === "object" ? global : window, "PI", {
    value:        3.141593,
    enumerable:   true,
    writable:     false,
    configurable: false
})
PI > 3.0;
```