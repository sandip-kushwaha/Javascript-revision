# JavaScript Prototype Chain

## What is a Prototype Chain?

A **prototype chain** is the sequence of objects JavaScript follows when searching for a property or method.

When JavaScript cannot find a property directly on an object, it checks the object's prototype, then the prototype's prototype, and continues until it reaches `null`.

```text
Object
  ↓
Prototype
  ↓
Prototype's Prototype
  ↓
null
```

This mechanism is the foundation of JavaScript inheritance.

---

# 1. Simple Example

```js
const user = {
  name: "Sandip"
};

console.log(user.name);
```

JavaScript finds `name` directly on `user`.

But:

```js
console.log(user.toString());
```

There is no `toString()` directly inside `user`.

JavaScript searches the prototype chain:

```text
user
 ↓
Object.prototype
 ↓
toString()
```

So the method can still be used.

---

# 2. Prototype Chain Structure

For a normal object:

```text
user
  │
  ↓
Object.prototype
  │
  ↓
null
```

For an object created from a constructor:

```text
user
  │
  ↓
User.prototype
  │
  ↓
Object.prototype
  │
  ↓
null
```

For multiple levels of inheritance:

```text
admin
  ↓
Manager.prototype
  ↓
Employee.prototype
  ↓
Object.prototype
  ↓
null
```

---

# 3. Checking the Prototype Chain

Use:

```js
Object.getPrototypeOf(object);
```

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

And:

```js
console.log(
  Object.getPrototypeOf(User.prototype) === Object.prototype
);
```

Output:

```text
true
```

Therefore:

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

# 4. Property Lookup

Suppose:

```js
function User(name) {
  this.name = name;
}

User.prototype.role = "User";

const user = new User("Sandip");
```

Now:

```js
console.log(user.role);
```

JavaScript searches:

```text
1. user.role
       ↓
2. User.prototype.role
       ↓
3. Object.prototype.role
       ↓
4. null
```

It finds:

```text
User.prototype.role
```

and returns:

```text
User
```

---

# 5. Property Found on the Object

```js
function User(name) {
  this.name = name;
}

User.prototype.role = "User";

const user = new User("Sandip");

console.log(user.name);
```

Search:

```text
user.name
   ↓
Found
```

JavaScript does not need to continue through the prototype chain.

---

# 6. Property Found on the Prototype

```js
console.log(user.role);
```

Search:

```text
user.role
   ↓
Not found
   ↓
User.prototype.role
   ↓
Found
```

So the value is returned from the prototype.

---

# 7. Property Not Found

```js
console.log(user.email);
```

Suppose `email` does not exist anywhere.

JavaScript searches:

```text
user
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

Nothing is found.

The result is:

```text
undefined
```

---

# 8. Prototype Chain with `Object.create()`

`Object.create()` makes prototype relationships easy to understand.

```js
const person = {
  type: "Person"
};

const employee = Object.create(person);

employee.job = "Developer";

const manager = Object.create(employee);

manager.department = "IT";
```

The chain is:

```text
manager
  ↓
employee
  ↓
person
  ↓
Object.prototype
  ↓
null
```

Now:

```js
console.log(manager.department);
console.log(manager.job);
console.log(manager.type);
```

Output:

```text
IT
Developer
Person
```

Each value is found at a different level.

---

# 9. Property Lookup Through Multiple Levels

```js
const company = {
  country: "Nepal"
};

const employee = Object.create(company);

employee.role = "Developer";

const user = Object.create(employee);

user.name = "Sandip";
```

Now:

```js
console.log(user.name);
```

Found here:

```text
user
 └── name
```

```js
console.log(user.role);
```

Found here:

```text
user
 ↓
employee
 └── role
```

And:

```js
console.log(user.country);
```

Found here:

```text
user
 ↓
employee
 ↓
company
 └── country
```

---

# 10. Prototype Chain Diagram

```text
┌──────────────────┐
│      user        │
│                  │
│ name: "Sandip"   │
└────────┬─────────┘
         │
         ↓
┌──────────────────┐
│    employee      │
│                  │
│ role: "Developer"│
└────────┬─────────┘
         │
         ↓
┌──────────────────┐
│     company      │
│                  │
│ country: "Nepal" │
└────────┬─────────┘
         │
         ↓
┌──────────────────┐
│ Object.prototype │
└────────┬─────────┘
         │
         ↓
       null
```

---

# 11. Property Shadowing

An object can have its own property with the same name as an inherited property.

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

Now add the same property:

```js
child.role = "Admin";
```

Then:

```js
console.log(child.role);
```

Output:

```text
Admin
```

The chain now looks like:

```text
child
 ├── role: "Admin"    ← found first
 │
 ↓
parent
 └── role: "User"
```

The child's own property **shadows** the inherited property.

---

# 12. Changing the Parent Property

Consider:

```js
const parent = {
  role: "User"
};

const child = Object.create(parent);
```

The child inherits the value:

```js
console.log(child.role);
```

Output:

```text
User
```

Now change the parent:

```js
parent.role = "Admin";
```

Then:

```js
console.log(child.role);
```

Output:

```text
Admin
```

Why?

Because `child` does not have its own `role`.

It still looks up the property from its prototype.

---

# 13. Own Property Stops the Search

```js
const parent = {
  role: "User"
};

const child = Object.create(parent);

child.role = "Admin";
```

Now change the parent:

```js
parent.role = "Manager";
```

What does the child return?

```js
console.log(child.role);
```

Output:

```text
Admin
```

Because the child has its own property:

```text
child.role
```

JavaScript stops searching immediately.

---

# 14. Prototype Chain with Constructor Functions

Consider:

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  return `Hello ${this.name}`;
};

const user = new User("Sandip");
```

The chain is:

```text
user
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

When we call:

```js
user.greet();
```

JavaScript finds:

```text
user
 ↓
User.prototype.greet()
```

and executes the method with `this` referring to `user`.

---

# 15. Built-in Prototype Chains

Arrays also use prototypes.

```js
const numbers = [10, 20, 30];
```

Conceptually:

```text
numbers
 ↓
Array.prototype
 ↓
Object.prototype
 ↓
null
```

Therefore:

```js
numbers.map(...)
numbers.filter(...)
numbers.push(...)
```

work because these methods are available through `Array.prototype`.

---

# 16. String Prototype Chain

For a string primitive:

```js
const name = "Sandip";
```

you can use:

```js
name.toUpperCase();
name.includes("a");
name.slice(0, 3);
```

JavaScript provides access to string methods through the corresponding built-in wrapper/prototype behavior.

You can inspect:

```js
console.log(String.prototype);
```

---

# 17. Function Prototype Chain

Functions are objects too.

```js
function greet() {
  return "Hello";
}
```

A function has its own prototype relationship.

```js
console.log(Object.getPrototypeOf(greet));
```

It points to:

```text
Function.prototype
```

And:

```text
greet
 ↓
Function.prototype
 ↓
Object.prototype
 ↓
null
```

This is separate from the function's `.prototype` property.

---

# 18. Two Meanings of `prototype`

This is one of the most important distinctions.

Consider:

```js
function User(name) {
  this.name = name;
}
```

### `User.prototype`

```js
User.prototype
```

This is a property of the constructor function.

It is used as the prototype of objects created by:

```js
new User();
```

### `Object.getPrototypeOf(user)`

```js
const user = new User("Sandip");

Object.getPrototypeOf(user);
```

This returns the actual prototype of `user`.

So:

```js
Object.getPrototypeOf(user) === User.prototype
```

is:

```text
true
```

---

# 19. Checking the Entire Chain

You can manually move through the chain:

```js
const user = {
  name: "Sandip"
};

let current = user;

while (current !== null) {
  console.log(current);
  current = Object.getPrototypeOf(current);
}
```

This walks through:

```text
user
 ↓
Object.prototype
 ↓
null
```

---

# 20. `isPrototypeOf()`

You can check whether one object appears in another object's prototype chain.

```js
const parent = {
  role: "User"
};

const child = Object.create(parent);

console.log(parent.isPrototypeOf(child));
```

Output:

```text
true
```

For a constructor:

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

# 21. `instanceof` and Prototype Chain

The `instanceof` operator checks whether a constructor's `prototype` exists somewhere in an object's prototype chain.

```js
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(user instanceof User);
```

Output:

```text
true
```

Because:

```text
user
 ↓
User.prototype
```

So:

```js
user instanceof User
```

is effectively checking whether `User.prototype` appears in the chain.

---

# 22. Inheritance with Constructor Functions

Prototype chains can create inheritance.

```js
function User(name) {
  this.name = name;
}

User.prototype.getName = function () {
  return this.name;
};

function Admin(name, permissions) {
  User.call(this, name);
  this.permissions = permissions;
}

Admin.prototype = Object.create(User.prototype);

Admin.prototype.constructor = Admin;
```

Now:

```js
const admin = new Admin("Sandip", ["manage-users"]);
```

The chain becomes:

```text
admin
 ↓
Admin.prototype
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

Therefore the admin can access methods from `User.prototype`.

```js
console.log(admin.getName());
```

Output:

```text
Sandip
```

---

# 23. Why `constructor` Is Reset

When we do:

```js
Admin.prototype = Object.create(User.prototype);
```

`Admin.prototype` now points to a new object whose prototype is `User.prototype`.

The inherited `constructor` relationship should be restored:

```js
Admin.prototype.constructor = Admin;
```

This keeps:

```js
console.log(Admin.prototype.constructor === Admin);
```

as:

```text
true
```

---

# 24. Classes and Prototype Chains

The same concept works with classes.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

class Admin extends User {
  getRole() {
    return "Admin";
  }
}
```

Create an object:

```js
const admin = new Admin("Sandip");
```

The important prototype structure is approximately:

```text
admin
 ↓
Admin.prototype
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

So:

```js
admin.getRole();
```

comes from:

```text
Admin.prototype
```

while:

```js
admin.getName();
```

comes from:

```text
User.prototype
```

---

# 25. Prototype Chain in a Hotel System

Consider:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

class Waiter extends User {
  serveTable(tableNumber) {
    return `${this.name} is serving ${tableNumber}`;
  }
}

const waiter = new Waiter("Sandip");
```

The prototype chain is:

```text
waiter
 ↓
Waiter.prototype
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

Therefore:

```js
waiter.getName();
```

comes from `User.prototype`.

And:

```js
waiter.serveTable("T-03");
```

comes from `Waiter.prototype`.

---

# 26. Prototype Chain Lookup Rules

When accessing:

```js
object.property
```

JavaScript roughly follows this process:

```text
1. Check object itself
        ↓
2. Check object's prototype
        ↓
3. Check prototype's prototype
        ↓
4. Continue
        ↓
5. Reach null
        ↓
6. Return undefined if not found
```

Example:

```js
console.log(user.email);
```

If `email` does not exist anywhere:

```text
undefined
```

---

# 27. Prototype Chain vs Copying

Inheritance through prototypes does **not** copy properties into every object.

For example:

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  return `Hello ${this.name}`;
};

const user1 = new User("Sandip");
const user2 = new User("Ram");
```

The `greet` function is stored on:

```text
User.prototype
```

not separately copied into:

```text
user1
user2
```

Both objects can access it through the prototype chain.

---

# 28. Important Relationship

Remember these three concepts:

### Prototype property

```js
User.prototype
```

The prototype object associated with a constructor.

### Object prototype

```js
Object.getPrototypeOf(user)
```

The prototype directly linked to an object.

### Prototype chain

```text
user
 ↓
User.prototype
 ↓
Object.prototype
 ↓
null
```

The chain is the complete sequence JavaScript searches.

---

# 29. Prototype Chain Example

```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

Product.prototype.getPrice = function () {
  return this.price;
};

const product = new Product("Keyboard", 2500);

console.log(product.name);
console.log(product.getPrice());
console.log(product.toString());
```

The lookup is:

```text
product.name
    ↓
product

product.getPrice()
    ↓
Product.prototype

product.toString()
    ↓
Product.prototype
    ↓
Object.prototype
```

This demonstrates how JavaScript can find methods at different levels.

---

# 30. Key Takeaways

* A prototype chain is a sequence of linked objects.
* JavaScript uses the chain to find properties and methods.
* JavaScript checks an object's own properties first.
* If not found, it searches the prototype.
* The search continues until `null`.
* `Object.getPrototypeOf()` shows the direct prototype.
* `isPrototypeOf()` checks prototype relationships.
* `instanceof` uses the prototype chain.
* Constructor-created objects usually follow:

  ```text
  instance
   ↓
  Constructor.prototype
   ↓
  Object.prototype
   ↓
  null
  ```
* Classes also use prototype chains.
* Prototype inheritance does not copy methods into every object.
* An own property can shadow an inherited property.
* Arrays, functions, and other built-in objects also have prototype chains.

## Prototype Chain Summary

```text
              Object.prototype
                      ↑
                      │
               User.prototype
                      ↑
                      │
                   user
```

For inheritance:

```text
                 Object.prototype
                        ↑
                        │
                  User.prototype
                        ↑
                        │
                 Admin.prototype
                        ↑
                        │
                     admin
```
