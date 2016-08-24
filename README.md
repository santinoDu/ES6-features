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

####Rest Parameter
#####ECMAScript 6
``` js
function f (x, y, ...a) {
    return (x + y) * a.length
}
f(1, 2, "hello", true, 7) === 9
```

#####ECMAScript 5
``` js
function f (x, y) {
    var a = Array.prototype.slice.call(arguments, 2);
    return (x + y) * a.length;
};
f(1, 2, "hello", true, 7) === 9;
```

####Spread Operator
#####ECMAScript 6
``` js
var params = [ "hello", true, 7 ]
var other = [ 1, 2, ...params ] // [ 1, 2, "hello", true, 7 ]
f(1, 2, ...params) === 9

var str = "foo"
var chars = [ ...str ] // [ "f", "o", "o" ]
```

#####ECMAScript 5
``` js
var params = [ "hello", true, 7 ];
var other = [ 1, 2 ].concat(params); // [ 1, 2, "hello", true, 7 ]
f.apply(undefined, [ 1, 2 ].concat(params)) === 9;

var str = "foo";
var chars = str.split(""); // [ "f", "o", "o" ]
```

###Template Literals
####String Interpolation
#####ECMAScript 6
``` js
var customer = { name: "Foo" }
var card = { amount: 7, product: "Bar", unitprice: 42 }
var message = `Hello ${customer.name},
want to buy ${card.amount} ${card.product} for
a total of ${card.amount * card.unitprice} bucks?`
```

#####ECMAScript 5
``` js
var customer = { name: "Foo" };
var card = { amount: 7, product: "Bar", unitprice: 42 };
var message = "Hello " + customer.name + ",\n" +
"want to buy " + card.amount + " " + card.product + " for\n" +
"a total of " + (card.amount * card.unitprice) + " bucks?";
```

####Custom Interpolation
#####ECMAScript 6
``` js
get`http://example.com/foo?bar=${bar + baz}&quux=${quux}`
```

#####ECMAScript 5
``` js
get([ "http://example.com/foo?bar=", "&quux=", "" ],bar + baz, quux);
```

####Raw String Access
#####ECMAScript 6
``` js
function quux (strings, ...values) {
    strings[0] === "foo\n"
    strings[1] === "bar"
    strings.raw[0] === "foo\\n"
    strings.raw[1] === "bar"
    values[0] === 42
}
quux `foo\n${ 42 }bar`

String.raw `foo\n${ 42 }bar` === "foo\\n42bar"
```

#####ECMAScript 5
``` js
//  no equivalent in ES5
```

###Extended Literals
####Binary & Octal Literal
#####ECMAScript 6
``` js
0b111110111 === 503
0o767 === 503
```

#####ECMAScript 5
``` js
parseInt("111110111", 2) === 503;
parseInt("767", 8) === 503;
0767 === 503; // only in non-strict, backward compatibility mode
```

####Unicode String & RegExp Literal
#####ECMAScript 6
``` js
"𠮷".length === 2
"𠮷".match(/./u)[0].length === 2
"𠮷" === "\uD842\uDFB7"
"𠮷" === "\u{20BB7}"
"𠮷".codePointAt(0) == 0x20BB7
for (let codepoint of "𠮷") console.log(codepoint)
```

#####ECMAScript 5
``` js
"𠮷".length === 2;
"𠮷".match(/(?:[\0-\t\x0B\f\x0E-\u2027\u202A-\uD7FF\uE000-\uFFFF][\uD800-\uDBFF][\uDC00-\uDFFF][\uD800-\uDBFF](?![\uDC00-\uDFFF])(?:[^\uD800-\uDBFF]^)[\uDC00-\uDFFF])/)[0].length === 2;
"𠮷" === "\uD842\uDFB7";
//  no equivalent in ES5
//  no equivalent in ES5
//  no equivalent in ES5
```




`to be continued...` go to[ES6-features](http://es6-features.org/)