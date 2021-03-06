http://www.ebooks-it.net/ebook/javascript-the-good-parts

__Semicolon insertion__

returned before the object.
```
return 
{
  status: true
};
```

__Unicode__

JavaScript’s characters are 16 bits

__typeof__

`typeof null === 'object'`

__parseInt__

```
parseInt("16") === parseInt("16 tons") === 16
```

If the first character of the string is 0, then the string is evaluated in base 8 instead of base 10.
```
parseInt("08") === 0
parseInt("08", 10) === 8
```

__floating point__

```
0.1 + 0.2 !== 0.3
```

__NaN is Number__

```
typeof NaN === 'number'
NaN !== NaN

function isNumber(value) { 
  return typeof value === 'number' && isFinite(value);
}
```

__Falsy Values__

```
0
NaN
''
false
null
undefined
```

__==__

```
0 == '' // true
0 == '0' // true
false == 'false' // false
false == '0' // true
false == undefined // false
null == undefined // true
```

__For loops__
https://blogs.oracle.com/greimer/entry/best_way_to_code_a

```
for (var key in o) // iterate object key/value

for (var i = 0; i < a.length; i++) // array

array.forEach(function () {}) // 10 times slower!?

// lodash
// _.each() is not fully compatible to [].forEach(). See the following example:

var a = ['a0'];
a[3] = 'a3';
_.each(a, console.log); // runs 4 times
a.forEach(console.log); // runs twice -- that's just how [].forEach() is specified

// https://github.com/lodash/lodash/blob/master/lodash.js#L1112
// https://stackoverflow.com/questions/18881487/why-is-lodash-each-faster-than-native-foreach

function FastAlmostSpecForEach( fn, ctx ) {
    "use strict";
    if( arguments.length > 1 ) return slowCaseForEach();
    if( typeof this !== "object" ) return slowCaseForEach();
    if( this === null ) throw new Error("this is null or not defined");
    if( typeof fn !== "function" ) throw new Error("is not a function");
    var len = this.length;
    if( ( len >>> 0 ) !== len ) return slowCaseForEach();


    for( var i = 0; i < len; ++i ) {
        var item = this[i];
        //Semantics are not exactly the same,
        //Fully spec compliant will not invoke getters
       //but this will.. however that is an insane edge case
        if( item === void 0 && !(i in this) ) {
            continue;
        }
        fn( item, i, this );
    }
}

Array.prototype.fastSpecForEach = FastAlmostSpecForEach;

```
