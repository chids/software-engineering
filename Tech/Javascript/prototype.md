### Prototype

* http://dmitrysoshnikov.com/ecmascript/javascript-the-core/

```javascript
function Ninja() {
  this.swung = false
}
Ninja.prototype.swung = true;

var ninja1 = new Ninja(); // you can still exptend the prototype after instantiation

Ninja.prototype.swingSword = function(){
    return this.swung;
};

ninja1.constructor
> Ninja
ninja1.prototype
> undefined
ninja1.swung 
> false // constructor instantiated attributes are looked up first
ninja1.swingSword()
> false
ninja1 instanceof Ninja
> true

var ninja2 = new ninja1.constructor();
ninja2 instanceof Ninja
> true
```

### Prototype Chain & Inheritance

ninja1 -> constructor.prototype -> (prototype.constructor).prototype ... etc

```javascript
function Male() {
  this.gender = 'Male';
}
function Female() {
  this.gender = 'Female';
}
function Secret() {}
Secret.prototype.gender = 'Secret';

function Ninja() {
  this.ninjaInstance = true
}
Ninja.prototype.ninjaProto = true

ninja = new Ninja();
Ninja.prototype = new Male(); // prototype.constructor = Male
ninja.gender
> undefined // cannot change super once instantiated.
ninja instanceof Ninja
> true
ninja instanceof Male
> false
ninja1 = new Ninja();
ninja1.gender
> 'Male'
ninja1 instanceof Ninja
> true
ninja1 instanceof Male
> true

Ninja.prototype = new Female(); 
ninja2 = new Ninja();
ninja2.gender
> 'Female'
// Ninja.prototype's properties are lost.
ninja2.ninjaProto
> undefined
ninja2.ninjaInstance
> true

'gender' in ninja // inherited property
> true
ninja.hasOwnProperty('gender') 
> false
ninja.gender = 'Secret'
ninja.hasOwnProperty('gender')
> true

ninja3 = new Ninja();
ninja3.gender
> 'Secret'

Ninja.prototype.gender = 'Ninja' // this will be looked up first
ninja3.gender
> 'Ninja'
```

`constructor.prototype.constructor` is a circular reference

https://stackoverflow.com/questions/650764/how-does-proto-differ-from-constructor-prototype

```javascript
function Ninja() {}
ninja = new Ninja()
ninja.constructor
> [Function: Ninja]
ninja.constructor.prototype
> {}
ninja.constructor.prototype.constructor
> [Function: Ninja]

```

`__proto__` - refers directly to the prototype of the constructor of the instance of the object.

```javascript
ninja.__proto__ // constructor.prototype
> {}
ninja.__proto__.constructor
> [Function: Ninja]
ninja.__proto__.constructor.__proto__
> [Function: Empty]
ninja.__proto__.constructor.__proto__.__proto__
> {}
ninja.__proto__.constructor.__proto__.__proto__.__proto__
> null
ninja.__proto__.__proto__
> {} // .constructor == Object
ninja.__proto__.__proto__.__proto__
> null
ninja.__proto__.constructor.__proto__.constructor
> [Function: Function]
ninja.__proto__.constructor.__proto__.constructor.__proto__
> [Function: Empty]
```

```javascript
function Ninja() {}
Ninja.prototype.sword = true;
function Human() {}
Human.prototype.human = true;
ninja = new Ninja();
ninja.human
> undefined
ninja.sword
> true
Ninja.prototype.__proto__ = Human.prototype;
ninja.human
> true
ninja.sword
> true
```

### Inheritance

* http://www.crockford.com/javascript/inheritance.html

```javascript
function Human() {}
Human.prototype.human = true;

function Ninja() {};
Ninja.prototype = new Human();
Ninja.prototype.sword = true;

ninja = new Ninja();
ninja.sword;
> true
ninja.constructor
> [Function Human]

```

__Parasitic Combination Inheritance__

```javascript
function obj(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
 
function inheritPrototype(sub, sup) {
  var p = obj(sup.prototype);
  p.constructor = sub;
  sub.prototype = p;
}

function Human() {}
Human.prototype.human = true;

function Ninja() {};
inheritPrototype(Ninja, Human);
Ninja.prototype.sword = true;

ninja = new Ninja();
ninja.sword;
> true
ninja.constructor
> [Function Ninja]
```
