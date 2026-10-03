# JavaScript Inheritance

## What is Inheritance?

**Inheritance** allows one class or object to reuse properties and methods from another class or object.

For example:

```text
User
  ↓
Admin
```

An `Admin` can inherit common behavior from `User` and also have its own behavior.

JavaScript supports inheritance through the **prototype chain** and the `extends` keyword.

---

# 1. Basic Inheritance

Use:

```js
extends
```

to create a child class.

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

const admin = new Admin("Sandip");

console.log(admin.getName());
console.log(admin.getRole());
```

Output:

```text
Sandip
Admin
```

`Admin` inherits `getName()` from `User`.

---

# 2. Parent and Child Classes

The class being inherited from is called the **parent class** or **base class**.

The class that inherits is called the **child class** or **derived class**.

```text
User
 │
 │ extends
 ↓
Admin
```

Example:

```js
class User {
  getName() {
    return "User";
  }
}

class Admin extends User {}
```

Here:

```text
User → Parent
Admin → Child
```

---

# 3. Inherited Methods

A child class automatically gets access to methods from its parent.

```js
class User {
  greet() {
    return "Hello";
  }
}

class Admin extends User {
  getRole() {
    return "Admin";
  }
}

const admin = new Admin();

console.log(admin.greet());
console.log(admin.getRole());
```

Output:

```text
Hello
Admin
```

`greet()` comes from the parent.

---

# 4. Prototype Chain in Inheritance

Consider:

```js
class User {
  getName() {
    return "User";
  }
}

class Admin extends User {
  getRole() {
    return "Admin";
  }
}

const admin = new Admin();
```

The prototype chain is approximately:

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

So JavaScript can find:

```text
getRole()
   ↓
Admin.prototype
```

and:

```text
getName()
   ↓
User.prototype
```

---

# 5. Inheritance of Properties

The child can also use properties initialized by the parent constructor.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {}

const admin = new Admin("Sandip");

console.log(admin.name);
```

Output:

```text
Sandip
```

The `name` property was initialized by the parent constructor.

---

# 6. Child Constructor

A child class can have its own constructor.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  constructor(name, permissions) {
    super(name);
    this.permissions = permissions;
  }
}

const admin = new Admin(
  "Sandip",
  ["manage-users", "manage-food"]
);

console.log(admin.name);
console.log(admin.permissions);
```

Output:

```text
Sandip
["manage-users", "manage-food"]
```

---

# 7. `super()`

When a derived class has a constructor, it must call:

```js
super();
```

before using `this`.

Example:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  constructor(name, permissions) {
    super(name);

    this.permissions = permissions;
  }
}
```

Here:

```js
super(name);
```

calls the parent constructor.

---

# 8. How `super()` Works

Consider:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  constructor(name, role) {
    super(name);
    this.role = role;
  }
}
```

The process is:

```text
new Admin("Sandip", "Admin")
        ↓
Admin constructor
        ↓
super("Sandip")
        ↓
User constructor
        ↓
this.name = "Sandip"
        ↓
Admin continues
        ↓
this.role = "Admin"
```

---

# 9. Why `super()` Must Come First

This is incorrect:

```js
class Admin extends User {
  constructor(name) {
    this.name = name;
    super(name);
  }
}
```

In a derived constructor, you cannot access `this` before calling `super()`.

Correct:

```js
class Admin extends User {
  constructor(name) {
    super(name);
    this.name = name;
  }
}
```

Usually, you don't need to assign `this.name` again because the parent already does it.

---

# 10. Parent Method Access

A child can explicitly call a parent method using:

```js
super.methodName()
```

Example:

```js
class User {
  greet() {
    return "Hello from User";
  }
}

class Admin extends User {
  greet() {
    return `${super.greet()} - Admin`;
  }
}

const admin = new Admin();

console.log(admin.greet());
```

Output:

```text
Hello from User - Admin
```

---

# 11. Method Overriding

A child can provide its own implementation of a parent method.

```js
class User {
  getRole() {
    return "User";
  }
}

class Admin extends User {
  getRole() {
    return "Admin";
  }
}

const admin = new Admin();

console.log(admin.getRole());
```

Output:

```text
Admin
```

The child method overrides the parent method.

---

# 12. Using `super` with Overridden Methods

You can still use the parent implementation.

```js
class User {
  getRole() {
    return "User";
  }
}

class Admin extends User {
  getRole() {
    const parentRole = super.getRole();

    return `${parentRole} → Admin`;
  }
}

const admin = new Admin();

console.log(admin.getRole());
```

Output:

```text
User → Admin
```

---

# 13. Multi-Level Inheritance

Inheritance can have multiple levels.

```js
class User {
  getUserType() {
    return "User";
  }
}

class Employee extends User {
  getEmployeeType() {
    return "Employee";
  }
}

class Manager extends Employee {
  getManagerType() {
    return "Manager";
  }
}
```

Create an object:

```js
const manager = new Manager();
```

The chain is:

```text
manager
   ↓
Manager.prototype
   ↓
Employee.prototype
   ↓
User.prototype
   ↓
Object.prototype
   ↓
null
```

The manager can access methods from all parent levels.

---

# 14. Multi-Level Example

```js
class User {
  getName() {
    return "User";
  }
}

class Employee extends User {
  getDepartment() {
    return "Development";
  }
}

class Manager extends Employee {
  getLevel() {
    return "Manager";
  }
}

const manager = new Manager();

console.log(manager.getName());
console.log(manager.getDepartment());
console.log(manager.getLevel());
```

Output:

```text
User
Development
Manager
```

---

# 15. Practical Hotel Inheritance

A hotel system can use inheritance for different staff types.

```js
class Staff {
  constructor(name) {
    this.name = name;
  }

  getInfo() {
    return this.name;
  }
}

class Waiter extends Staff {
  serveTable(tableNumber) {
    return `${this.name} is serving ${tableNumber}`;
  }
}

class KitchenStaff extends Staff {
  prepareOrder(orderId) {
    return `${this.name} is preparing ${orderId}`;
  }
}
```

Create objects:

```js
const waiter = new Waiter("Sandip");
const kitchenStaff = new KitchenStaff("Ram");

console.log(waiter.getInfo());
console.log(waiter.serveTable("T-03"));

console.log(kitchenStaff.getInfo());
console.log(kitchenStaff.prepareOrder("ORD-101"));
```

The common behavior is defined in `Staff`.

---

# 16. Another Hotel Example

```js
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  getProfile() {
    return `${this.name} - ${this.email}`;
  }
}

class Admin extends User {
  constructor(name, email, permissions = []) {
    super(name, email);
    this.permissions = permissions;
  }

  manageUsers() {
    return `${this.name} can manage users`;
  }
}

class Waiter extends User {
  serveTable(tableNumber) {
    return `${this.name} serves ${tableNumber}`;
  }
}
```

Now:

```js
const admin = new Admin(
  "Sandip",
  "sandip@example.com",
  ["users", "food"]
);

const waiter = new Waiter(
  "Ram",
  "ram@example.com"
);
```

Both inherit:

```text
getProfile()
```

from `User`.

But each child has its own behavior.

---

# 17. Inheritance of Static Members

Static members can also be inherited.

```js
class User {
  static type() {
    return "User";
  }
}

class Admin extends User {}

console.log(Admin.type());
```

Output:

```text
User
```

The child class can access the inherited static method.

---

# 18. Overriding Static Methods

A child class can override a static method.

```js
class User {
  static type() {
    return "User";
  }
}

class Admin extends User {
  static type() {
    return "Admin";
  }
}

console.log(Admin.type());
```

Output:

```text
Admin
```

---

# 19. `instanceof` with Inheritance

Consider:

```js
class User {}

class Admin extends User {}

const admin = new Admin();
```

Now:

```js
console.log(admin instanceof Admin);
console.log(admin instanceof User);
console.log(admin instanceof Object);
```

Output:

```text
true
true
true
```

Why?

Because the prototype chain contains:

```text
Admin.prototype
      ↓
User.prototype
      ↓
Object.prototype
```

---

# 20. Checking Prototype Relationships

```js
class User {}

class Admin extends User {}

const admin = new Admin();

console.log(
  User.prototype.isPrototypeOf(admin)
);
```

Output:

```text
true
```

And:

```js
console.log(
  Admin.prototype.isPrototypeOf(admin)
);
```

Output:

```text
true
```

Both prototypes exist in the chain.

---

# 21. Inheritance Is Not Copying

When:

```js
class Admin extends User {}
```

is used, JavaScript does not simply copy every method from `User` into `Admin`.

Instead, a prototype relationship is created.

```text
Admin.prototype
       ↓
User.prototype
```

So methods can be found through the prototype chain.

---

# 22. Inheritance vs Composition

Inheritance:

```text
Admin
  ↓
User
```

Composition:

```text
Order
 ├── Customer
 ├── Table
 └── Payment
```

Inheritance represents an **is-a** relationship.

Example:

```text
Admin is a User
Waiter is a Staff member
```

Composition represents a **has-a** relationship.

Example:

```text
Order has a Customer
Order has Items
Order has a Table
```

Both approaches are useful depending on the design.

---

# 23. Avoid Unnecessary Inheritance

Not every class needs to extend another class.

For example, these are not automatically good inheritance relationships:

```text
Order → User
Food → User
Table → User
```

If two objects don't have a genuine parent-child relationship, composition or separate classes may be clearer.

---

# 24. Inheritance with Getters

Parent getters can be inherited.

```js
class User {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

class Admin extends User {
  get role() {
    return "Admin";
  }
}

const admin = new Admin("Sandip", "Kushwaha");

console.log(admin.fullName);
console.log(admin.role);
```

Output:

```text
Sandip Kushwaha
Admin
```

---

# 25. Inheritance with Private Fields

Private fields belong to the class that declares them.

```js
class User {
  #id;

  constructor(id) {
    this.#id = id;
  }

  getId() {
    return this.#id;
  }
}

class Admin extends User {
  showId() {
    return this.getId();
  }
}

const admin = new Admin("USR-01");

console.log(admin.showId());
```

The child does not directly access:

```js
admin.#id
```

because the private field belongs specifically to `User`.

It can use the public/protected-style API provided by the parent, such as `getId()`.

---

# 26. Inheritance with Constructor Defaults

```js
class User {
  constructor(name, role = "User") {
    this.name = name;
    this.role = role;
  }
}

class Admin extends User {
  constructor(name) {
    super(name, "Admin");
  }
}

const admin = new Admin("Sandip");

console.log(admin.role);
```

Output:

```text
Admin
```

The child can provide specific values to the parent constructor.

---

# 27. Traditional Prototype Inheritance

Before classes, inheritance was commonly created directly with prototypes.

```js
function User(name) {
  this.name = name;
}

User.prototype.getName = function () {
  return this.name;
};

function Admin(name) {
  User.call(this, name);
}

Admin.prototype = Object.create(User.prototype);
Admin.prototype.constructor = Admin;

Admin.prototype.getRole = function () {
  return "Admin";
};

const admin = new Admin("Sandip");

console.log(admin.getName());
console.log(admin.getRole());
```

The chain is:

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

Modern code commonly uses `class` and `extends` because the syntax is clearer.

---

# 28. Class Inheritance Structure

```text
              Object
                 ↑
                 │
              User
                 ↑
                 │
              Staff
                 ↑
                 │
              Waiter
```

For an instance:

```text
waiter
   ↓
Waiter.prototype
   ↓
Staff.prototype
   ↓
User.prototype
   ↓
Object.prototype
   ↓
null
```

---

# 29. Complete Example

```js
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  getProfile() {
    return `${this.name} - ${this.email}`;
  }
}

class Staff extends User {
  constructor(name, email, department) {
    super(name, email);
    this.department = department;
  }

  getDepartment() {
    return this.department;
  }
}

class Waiter extends Staff {
  constructor(name, email, shift) {
    super(name, email, "Restaurant");
    this.shift = shift;
  }

  serveTable(tableNumber) {
    return `${this.name} is serving ${tableNumber}`;
  }
}

const waiter = new Waiter(
  "Sandip",
  "sandip@example.com",
  "Morning"
);

console.log(waiter.getProfile());
console.log(waiter.getDepartment());
console.log(waiter.serveTable("T-03"));
```

The inheritance structure is:

```text
User
 ↓
Staff
 ↓
Waiter
```

---

# 30. Key Takeaways

* Inheritance allows a class to reuse another class's behavior.
* Use `extends` to create class inheritance.
* The parent class provides common behavior.
* The child class can add new behavior.
* `super()` calls the parent constructor.
* `super.method()` calls a parent method.
* A child can override parent methods.
* Inheritance works through the prototype chain.
* Multiple levels of inheritance are possible.
* Static members can also be inherited.
* `instanceof` works through the prototype chain.
* Private fields remain private to the class that declares them.
* Inheritance represents an **is-a** relationship.
* Composition represents a **has-a** relationship.
* Avoid inheritance when the relationship does not naturally fit.

## Simple Mental Model

```text
Parent Class
     │
     │ extends
     ↓
Child Class
     │
     ↓
Child Object
```

## Example

```text
User
  │
  ├── name
  ├── email
  └── getProfile()
       ↑
       │
Staff
  │
  ├── department
  └── getDepartment()
       ↑
       │
Waiter
  │
  ├── shift
  └── serveTable()
```
