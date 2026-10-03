# JavaScript Prototype

## What is a Prototype?

A **prototype** is an object that another object can use to inherit properties and methods.

JavaScript uses **prototype-based inheritance**.

Instead of copying the same method into every object, JavaScript can store the method on a prototype and let multiple objects share it.

```text
Object
  ↓
Prototype
  ↓
Inherited properties/methods
```

---

## 1. Simple Example

```js
const user = {
  name: "Sandip"
};

console.log(Object.getPrototypeOf(user));
```

Every normal JavaScript object has an internal connection to another object called its **prototype**.

You can inspect it with:

```js
Object.getPrototypeOf(user);
```

---

## 2. Prototype Chain

When JavaScript looks for a property, it checks:

```text
Object itself
      ↓
Its prototype
      ↓
Prototype's prototype
      ↓
null
```

Example:

```js
const user = {
  name: "Sandip"
};

console.log(user.toString());
```

There is no `toString` property directly inside `user`.

JavaScript searches its prototype chain and eventually finds `toString` through `Object.prototype`.

---

## 3. Object.prototype

Most normal JavaScript objects eventually inherit from:

```js
Object.prototype
```

For example:

```js
const user = {
  name: "Sandip"
};

console.log(Object.getPrototypeOf(user) === Object.prototype);
```

Output:

```text
true
```

`Object.prototype` contains commonly available methods such as:

```js
toString()
valueOf()
hasOwnProperty()
```

The top of the normal prototype chain is:

```js
console.log(Object.getPrototypeOf(Object.prototype));
```

Output:

```text
null
```

So:

```text
user
 ↓
Object.prototype
 ↓
null
```

---

# 4. Function `prototype` Property

Functions can have a special property called:

```js
prototype
```

This is especially important when using a function as a constructor.

```js
function User(name) {
  this.name = name;
}

console.log(User.prototype);
```

When we create an object using:

```js
const user = new User("Sandip");
```

the new object's prototype is connected to:

```js
User.prototype
```

---

## 5. Adding a Method to a Prototype

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  return `Hello ${this.name}`;
};

const user1 = new User("Sandip");
const user2 = new User("Ram");

console.log(user1.greet());
console.log(user2.greet());
```

Output:

```text
Hello Sandip
Hello Ram
```

Both objects use the same prototype method.

---

# 6. Why Use Prototypes?

Without prototypes:

```js
function User(name) {
  this.name = name;

  this.greet = function () {
    return `Hello ${this.name}`;
  };
}
```

Every new object gets a separate `greet` function.

With prototypes:

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  return `Hello ${this.name}`;
};
```

The method is shared through the prototype.

```text
User.prototype
      │
      ├── greet()
      │
      ├── ...
      │
      ↓
 ┌───────────┐
 │  user1    │
 └───────────┘

 ┌───────────┐
 │  user2    │
 └───────────┘
```

This is useful when creating many objects.

---

# 7. `Object.getPrototypeOf()`

Use:

```js
Object.getPrototypeOf(object);
```

to get an object's prototype.

Example:

```js
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(
  Object.getPrototypeOf(user) === User.prototype
);
```

Output:

```text
true
```

This is the important relationship:

```text
User.prototype
      ↑
      │
Object.getPrototypeOf(user)
```

---

# 8. `prototype` vs `Object.getPrototypeOf()`

These are related but different.

### Constructor's `prototype`

```js
User.prototype
```

This is the prototype object that instances created with:

```js
new User()
```

will inherit from.

### Object's actual prototype

```js
Object.getPrototypeOf(user)
```

This tells you which object `user` directly inherits from.

Example:

```js
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(User.prototype);
console.log(Object.getPrototypeOf(user));
```

They refer to the same prototype object:

```js
console.log(User.prototype === Object.getPrototypeOf(user));
```

Output:

```text
true
```

---

# 9. `isPrototypeOf()`

You can check whether an object is part of another object's prototype chain.

```js
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(User.prototype.isPrototypeOf(user));
```

Output:

```text
true
```

---

# 10. Property Lookup

Consider:

```js
function User(name) {
  this.name = name;
}

User.prototype.role = "User";

const user = new User("Sandip");
```

Now:

```js
console.log(user.name);
console.log(user.role);
```

`name` exists directly on `user`.

```text
user
├── name
└── [[Prototype]]
       └── role
```

So JavaScript finds:

```text
name → user
role → User.prototype
```

---

# 11. Own Properties

An **own property** belongs directly to the object.

```js
function User(name) {
  this.name = name;
}

User.prototype.role = "User";

const user = new User("Sandip");

console.log(Object.hasOwn(user, "name"));
```

Output:

```text
true
```

But:

```js
console.log(Object.hasOwn(user, "role"));
```

Output:

```text
false
```

Because `role` comes from the prototype.

```text
user
├── name        ← own property
│
└── prototype
    └── role    ← inherited property
```

---

# 12. Prototype Inheritance with `Object.create()`

You can directly create an object using another object as its prototype.

```js
const admin = {
  role: "Admin"
};

const user = Object.create(admin);

user.name = "Sandip";

console.log(user.name);
console.log(user.role);
```

Output:

```text
Sandip
Admin
```

`role` is inherited from `admin`.

```text
user
├── name
│
└── admin
    └── role
```

---

# 13. Changing an Inherited Property

Example:

```js
const parent = {
  role: "User"
};

const child = Object.create(parent);

console.log(child.role);
```

Output:

```text
User
```

Now:

```js
child.role = "Admin";

console.log(child.role);
```

Output:

```text
Admin
```

The assignment creates an own property on `child`.

```text
Before:

child
  ↓
parent.role = "User"


After:

child.role = "Admin"
  ↓
parent.role = "User"
```

The child's property **shadows** the parent's property.

---

# 14. Property Shadowing

When an object has the same property name as its prototype, the object's own property takes priority.

```js
const parent = {
  role: "User"
};

const child = Object.create(parent);

child.role = "Admin";

console.log(child.role);
```

Output:

```text
Admin
```

JavaScript finds:

```text
child.role
```

first, so it does not need to use:

```text
parent.role
```

---

# 15. Modifying the Prototype

Example:

```js
function User(name) {
  this.name = name;
}

User.prototype.getName = function () {
  return this.name;
};

const user1 = new User("Sandip");
const user2 = new User("Ram");
```

Later:

```js
User.prototype.getRole = function () {
  return "User";
};
```

Now both objects can access the new method:

```js
console.log(user1.getRole());
console.log(user2.getRole());
```

Output:

```text
User
User
```

Because both objects use the same prototype.

---

# 16. Practical Example: Hotel Table

```js
function HotelTable(tableNumber, capacity) {
  this.tableNumber = tableNumber;
  this.capacity = capacity;
}

HotelTable.prototype.getInfo = function () {
  return `Table ${this.tableNumber} - Capacity: ${this.capacity}`;
};

const table1 = new HotelTable("T-01", 4);
const table2 = new HotelTable("T-02", 6);

console.log(table1.getInfo());
console.log(table2.getInfo());
```

Output:

```text
Table T-01 - Capacity: 4
Table T-02 - Capacity: 6
```

The `getInfo()` method is shared through:

```js
HotelTable.prototype
```

---

# 17. Prototype Chain Example

```js
const user = {
  name: "Sandip"
};

console.log(user.toString());
```

The lookup works approximately like this:

```text
user
 ↓
Object.prototype
 ↓
toString()
```

If JavaScript cannot find the property anywhere:

```js
console.log(user.someProperty);
```

the result is:

```text
undefined
```

The search eventually reaches:

```text
null
```

---

# 18. `Object.create(null)`

You can create an object with **no prototype**:

```js
const data = Object.create(null);

data.name = "Sandip";

console.log(data.name);
```

Its prototype is:

```js
console.log(Object.getPrototypeOf(data));
```

Output:

```text
null
```

This means it does not inherit methods from `Object.prototype`.

For example, methods such as:

```js
toString()
hasOwnProperty()
```

are not automatically available.

This can be useful for dictionary-like data where you want only your own keys.

---

# 19. Prototype and Classes

JavaScript `class` syntax still uses prototypes internally.

Example:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}
```

The `greet()` method is placed on:

```js
User.prototype
```

Conceptually:

```text
class User
    ↓
User.prototype
    ↓
greet()
```

So classes provide a cleaner syntax for JavaScript's prototype-based system.

---

# 20. Prototype Methods vs Instance Properties

### Instance property

```js
function User(name) {
  this.name = name;
}
```

Each object gets its own `name`.

### Prototype method

```js
User.prototype.greet = function () {
  return `Hello ${this.name}`;
};
```

The method is shared.

A common pattern is:

```js
function User(name, role) {
  this.name = name;
  this.role = role;
}

User.prototype.getInfo = function () {
  return `${this.name} - ${this.role}`;
};
```

Use instance properties for object-specific data and prototypes for behavior that can be shared.

---

# 21. Prototype Diagram

```text
             Object.prototype
                    ↑
                    │
              User.prototype
                    ↑
                    │
             ┌──────────────┐
             │    user      │
             │              │
             │ name         │
             │ role         │
             └──────────────┘
```

When JavaScript cannot find a property on `user`, it checks:

```text
user
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

---

# 22. Important Prototype Methods

### Get prototype

```js
Object.getPrototypeOf(object);
```

### Set prototype

```js
Object.setPrototypeOf(object, prototype);
```

Example:

```js
const parent = {
  role: "Admin"
};

const user = {
  name: "Sandip"
};

Object.setPrototypeOf(user, parent);

console.log(user.role);
```

Output:

```text
Admin
```

> `Object.setPrototypeOf()` exists, but changing prototypes after object creation can hurt performance. Prefer `Object.create()` or constructor/class patterns when designing objects.

### Check prototype relationship

```js
prototype.isPrototypeOf(object);
```

---

# 23. `__proto__`

You may see:

```js
user.__proto__
```

in older tutorials.

It refers to the object's prototype in many environments, but modern code should generally prefer:

```js
Object.getPrototypeOf(user);
```

instead.

Use:

```js
Object.getPrototypeOf(user);
```

for clearer and more explicit code.

---

# 24. Prototype vs Own Property

```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

Product.prototype.getPrice = function () {
  return this.price;
};

const product = new Product("Keyboard", 2500);
```

Here:

```js
console.log(Object.hasOwn(product, "name"));
```

Output:

```text
true
```

And:

```js
console.log(Object.hasOwn(product, "getPrice"));
```

Output:

```text
false
```

Because:

```text
name
 ↓
product

getPrice
 ↓
Product.prototype
```

---

# 25. Why Prototypes Matter

Prototypes are important because they allow JavaScript to:

* share methods between objects
* reduce unnecessary function duplication
* implement inheritance
* create object relationships
* support constructor functions
* power JavaScript classes
* build prototype chains
* provide built-in object methods

---

# 26. Best Practices

### Prefer:

```js
Object.getPrototypeOf(obj);
```

instead of relying on:

```js
obj.__proto__;
```

### Share reusable methods through prototypes

```js
User.prototype.getInfo = function () {
  return this.name;
};
```

### Keep object-specific data on the instance

```js
this.name = name;
```

### Avoid unnecessary prototype mutation

Design the prototype structure before creating many objects.

### Use classes when they make code easier to understand

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}
```

Classes still use prototypes internally.

---

# 27. Key Takeaways

* A prototype is an object used for inheritance.
* Objects can inherit properties and methods from their prototypes.
* JavaScript searches the prototype chain when a property is not found directly.
* `Object.getPrototypeOf(obj)` returns an object's prototype.
* Constructor functions have a `.prototype` property.
* Objects created with `new Constructor()` inherit from `Constructor.prototype`.
* `Object.prototype` is near the top of the normal prototype chain.
* The prototype chain eventually ends at `null`.
* Own properties belong directly to an object.
* Inherited properties come from the prototype chain.
* An own property can shadow an inherited property.
* `Object.create()` can create an object with a chosen prototype.
* JavaScript classes use prototypes internally.
* Prototypes are useful for sharing methods between objects.

### Prototype Relationship

```text
Constructor Function
        │
        ↓
Constructor.prototype
        │
        ↓
new Constructor()
        │
        ↓
Object instance
```

### Property Lookup

```text
Object
  ↓
Own Property?
  ↓
No
  ↓
Prototype
  ↓
No
  ↓
Prototype's Prototype
  ↓
...
  ↓
null
```
