# ES6-features
**[ES6-features](http://es6-features.org/)**

###Constants
####Constants
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

###Scoping
####Block-Scoped Variables
#####ECMAScript 6
``` js
for (let i = 0; i < a.length; i++) {
    let x = a[i]
    …
}
for (let i = 0; i < b.length; i++) {
    let y = b[i]
    …
}

let callbacks = []
for (let i = 0; i <= 2; i++) {
    callbacks[i] = function () { return i * 2 }
}
callbacks[0]() === 0
callbacks[1]() === 2
callbacks[2]() === 4
```

#####ECMAScript 5
``` js
var i, x, y;
for (i = 0; i < a.length; i++) {
    x = a[i];
    …
}
for (i = 0; i < b.length; i++) {
    y = b[i];
    …
}

var callbacks = [];
for (var i = 0; i <= 2; i++) {
    (function (i) {
        callbacks[i] = function() { return i * 2; };
    })(i);
}
callbacks[0]() === 0;
callbacks[1]() === 2;
callbacks[2]() === 4;
```

####Block-Scoped Functions
#####ECMAScript 6
``` js
{
    function foo () { return 1 }
    foo() === 1
    {
        function foo () { return 2 }
        foo() === 2
    }
    foo() === 1
}
```

#####ECMAScript 5
``` js
(function () {
    var foo = function () { return 1; }
    foo() === 1;
    (function () {
        var foo = function () { return 2; }
        foo() === 2;
    })();
    foo() === 1;
})();
```

###Arrow Functions
####Expression Bodies
#####ECMAScript 6
``` js
odds  = evens.map(v => v + 1)
pairs = evens.map(v => ({ even: v, odd: v + 1 }))
nums  = evens.map((v, i) => v + i)
```

#####ECMAScript 5
``` js
odds  = evens.map(function (v) { return v + 1; });
pairs = evens.map(function (v) { return { even: v, odd: v + 1 }; });
nums  = evens.map(function (v, i) { return v + i; });
```

####Statement Bodies
#####ECMAScript 6
``` js
nums.forEach(v => {
   if (v % 5 === 0)
       fives.push(v)
})
```

#####ECMAScript 5
``` js
nums.forEach(function (v) {
   if (v % 5 === 0)
       fives.push(v);
});
```

####Lexical this
#####ECMAScript 6
``` js
this.nums.forEach((v) => {
    if (v % 5 === 0)
        this.fives.push(v)
})
```

#####ECMAScript 5
``` js
var self = this;
this.nums.forEach(function (v) {
    if (v % 5 === 0)
        self.fives.push(v);
});

//  or
this.nums.forEach(function (v) {
    if (v % 5 === 0)
        this.fives.push(v);
}.bind(this));
```

###Extended Parameter Handling
####Default Parameter Values
#####ECMAScript 6
``` js
function f (x, y = 7, z = 42) {
    return x + y + z
}
f(1) === 50
```

#####ECMAScript 5
``` js
function f (x, y, z) {
    if (y === undefined)
        y = 7;
    if (z === undefined)
        z = 42;
    return x + y + z;
};
f(1) === 50;
```

`to be continued... go to[ES6-features](http://es6-features.org/)`