In JavaScript, the value of `this` depends on **how a function is called**, not where it is defined. 

---
#### 1. **Global Context**

- In the global scope, `this` refers to the global object (`window` in browsers).
- Example:
    
```javascript
var thisOutsideOfAFunction = this; // `this` is `window` console.log(thisOutsideOfAFunction === window); // true
```

---

#### 2. **Regular Function Calls**

- When a function is called without an object, `this` defaults to:
    - The global object (`window`) in non-strict mode.
    - `undefined` in strict mode.
- Example:
```javascript
function logThis() {   console.log(this); } logThis(); // `this` is `window` in non-strict mode, `undefined` in strict mode
```    
    
---

#### 3. **Methods in Objects**

- When a function is called as a method of an object, `this` refers to the object the method belongs to.
- "left of the dot rule" -> `one.two.hi()` `this = one.two`
- Example:
```javascript
var myObject = {   myMethod: function() {     console.log(this);   } }; myObject.myMethod(); // `this` is `myObject`
```
    
---

#### 4. **Constructors with `new`**

- When a function is called with `new`, `this` refers to the newly created object.
- Example:
```javascript
function Person(name) {   this.name = name; } var person = new Person('John'); console.log(person.name); // "John"
```
    
---

#### 5. **Explicit Binding with `bind`, `call`, and `apply`**

- The value of `this` can be explicitly set using `bind`, `call`, or `apply`.
- Example:
```javascript
function logThis() {   console.log(this); } var gordon = { name: 'Gordon' }; var boundLogThis = logThis.bind(gordon); boundLogThis(); // `this` is `gordon` 
```
    
---

#### 6. **Arrow Functions**

- Arrow functions do not have their own `this`. They inherit `this` from the surrounding lexical scope, aka what the value of `this` is where the arrow function is defined
- arrow functions have no control over the value of `this`
- Example:
```javascript
var obj = {   myArrowFunction: () => {     console.log(this);   } }; obj.myArrowFunction(); // `this` is `window` or `undefined` (in strict mode), not `obj`
```

---

### Key Takeaways from the Examples in This Chat:

1. **Global and Method Contexts:**
    
    - `this` in the global scope or regular functions is `window` (or `undefined` in strict mode).
    - Inside a method, `this` refers to the object the method belongs to.
2. **`new` Behavior:**
    
    - When a function is called with `new`, `this` is the newly created object.
3. **Explicit Binding:**
    
    - `this` can be explicitly set using `bind`, `call`, or `apply`.
4. **Arrow Functions:**
    
    - Arrow functions do not redefine `this` and use the surrounding context's `this`.

Understanding these rules ensures predictable behavior of `this` in various scenarios.
