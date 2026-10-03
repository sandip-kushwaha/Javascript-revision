# JavaScript Classes

## What is a Class?

A **class** is a cleaner syntax for creating objects and working with inheritance in JavaScript.

Classes were introduced in **ES6 (ECMAScript 2015)**.

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

const user = new User("Sandip");

console.log(user.greet());
```

Output:

```text
Hello Sandip
```

---

# 1. Basic Class Structure

A class usually contains:

```text
Class
 ├── constructor()
 ├── properties
 └── methods
```

Example:

```js
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  getInfo() {
    return `${this.name} - ${this.email}`;
  }
}
```

Create an object:

```js
const user = new User("Sandip", "sandip@example.com");

console.log(user.getInfo());
```

---

# 2. Creating a Class

Use the `class` keyword:

```js
class User {
  // class body
}
```

The class name normally follows **PascalCase**:

```js
class User {}
class HotelTable {}
class FoodItem {}
class Order {}
```

---

# 3. Constructor

The `constructor()` method runs automatically when an object is created with `new`.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user.name);
```

Output:

```text
Sandip
```

The constructor is mainly used to initialize object data.

---

# 4. Constructor Parameters

A constructor can receive multiple values.

```js
class User {
  constructor(name, email, role) {
    this.name = name;
    this.email = email;
    this.role = role;
  }
}

const user = new User(
  "Sandip",
  "sandip@example.com",
  "admin"
);

console.log(user);
```

The created object contains:

```text
name
email
role
```

---

# 5. `this` Inside a Class

Inside a constructor, `this` refers to the newly created object.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");
```

Conceptually:

```text
new User("Sandip")
        ↓
new object
        ↓
this = new object
        ↓
this.name = "Sandip"
```

---

# 6. Creating Multiple Objects

One class can create many objects.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user1 = new User("Sandip");
const user2 = new User("Ram");
const user3 = new User("Hari");

console.log(user1.name);
console.log(user2.name);
console.log(user3.name);
```

Each object has its own data.

```text
user1 → Sandip
user2 → Ram
user3 → Hari
```

---

# 7. Class Methods

Methods are defined directly inside the class body.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}

const user = new User("Sandip");

console.log(user.greet());
```

You don't need to write:

```js
function greet() {}
```

inside the class.

---

# 8. Methods Are Shared Through the Prototype

Consider:

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

The `greet()` method is associated with:

```js
User.prototype
```

You can verify:

```js
console.log(
  Object.hasOwn(User.prototype, "greet")
);
```

Output:

```text
true
```

So classes still use JavaScript's prototype system internally.

---

# 9. Class and Prototype Relationship

```text
class User
     │
     ↓
User.prototype
     │
     ├── greet()
     ├── getName()
     └── ...
     ↑
     │
   user
```

When:

```js
user.greet();
```

JavaScript can find `greet()` through:

```text
user
 ↓
User.prototype
```

---

# 10. Class Properties

You can create properties in the constructor:

```js
class Product {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }
}

const product = new Product("Keyboard", 2500);

console.log(product.name);
console.log(product.price);
```

These are instance properties.

Each object gets its own values.

---

# 11. Class Fields

Modern JavaScript also supports class fields.

```js
class User {
  role = "User";

  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user.name);
console.log(user.role);
```

Output:

```text
Sandip
User
```

Class fields are useful when a property has a default value.

---

# 12. Methods with Parameters

Class methods can accept parameters.

```js
class Calculator {
  add(a, b) {
    return a + b;
  }

  multiply(a, b) {
    return a * b;
  }
}

const calculator = new Calculator();

console.log(calculator.add(10, 20));
console.log(calculator.multiply(5, 4));
```

Output:

```text
30
20
```

---

# 13. Updating Object Data

Class methods can modify instance properties.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  rename(newName) {
    this.name = newName;
  }
}

const user = new User("Sandip");

user.rename("Sandip Kushwaha");

console.log(user.name);
```

Output:

```text
Sandip Kushwaha
```

---

# 14. Default Values

You can provide default values.

```js
class User {
  constructor(name, role = "User") {
    this.name = name;
    this.role = role;
  }
}

const user1 = new User("Sandip");
const user2 = new User("Ram", "Admin");

console.log(user1.role);
console.log(user2.role);
```

Output:

```text
User
Admin
```

---

# 15. Class with a Practical Hotel Example

```js
class HotelTable {
  constructor(tableNumber, capacity, status = "available") {
    this.tableNumber = tableNumber;
    this.capacity = capacity;
    this.status = status;
  }

  occupy() {
    this.status = "occupied";
  }

  makeAvailable() {
    this.status = "available";
  }

  getInfo() {
    return `${this.tableNumber} - ${this.status}`;
  }
}

const table = new HotelTable("T-03", 6);

console.log(table.getInfo());

table.occupy();

console.log(table.getInfo());
```

Output:

```text
T-03 - available
T-03 - occupied
```

---

# 16. Class Inheritance

A class can inherit from another class using:

```js
extends
```

Example:

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

The `Admin` class inherits from `User`.

---

# 17. `super()`

When a child class has its own constructor, it must call:

```js
super();
```

before using `this`.

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
  ["manage-users"]
);

console.log(admin.name);
console.log(admin.permissions);
```

`super(name)` calls the parent class constructor.

---

# 18. Calling Parent Methods

`super` can also call methods from the parent class.

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

# 19. Method Overriding

A child class can provide its own version of a parent method.

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

The child method overrides the inherited method.

---

# 20. Static Methods

A `static` method belongs to the class itself, not to its instances.

```js
class MathHelper {
  static add(a, b) {
    return a + b;
  }
}

console.log(MathHelper.add(10, 20));
```

You call it using:

```js
MathHelper.add();
```

Not:

```js
const helper = new MathHelper();

helper.add();
```

---

# 21. Static Properties

Classes can also have static properties.

```js
class User {
  static role = "User";
}

console.log(User.role);
```

Output:

```text
User
```

The property belongs to the class:

```text
User.role
```

not to each instance.

---

# 22. Instance vs Static

### Instance

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}

const user = new User("Sandip");

console.log(user.greet());
```

### Static

```js
class User {
  static getType() {
    return "User";
  }
}

console.log(User.getType());
```

Think of it as:

```text
Instance method
     ↓
object.method()

Static method
     ↓
Class.method()
```

---

# 23. Private Fields

Modern JavaScript supports private class fields using `#`.

```js
class BankAccount {
  #balance = 0;

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount();

account.deposit(500);

console.log(account.getBalance());
```

Output:

```text
500
```

This will not work:

```js
console.log(account.#balance);
```

Private fields can only be accessed inside the class.

---

# 24. Private Methods

Methods can also be private.

```js
class User {
  #validateName(name) {
    return name.length > 0;
  }

  setName(name) {
    if (this.#validateName(name)) {
      this.name = name;
    }
  }
}

const user = new User();

user.setName("Sandip");

console.log(user.name);
```

`#validateName()` is accessible only inside the class.

---

# 25. Getters

A getter allows a method to be accessed like a property.

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

const user = new User("Sandip", "Kushwaha");

console.log(user.fullName);
```

Notice:

```js
user.fullName
```

not:

```js
user.fullName()
```

---

# 26. Setters

A setter allows controlled assignment to a property.

```js
class User {
  set username(value) {
    this.name = value.trim();
  }
}

const user = new User();

user.username = " Sandip ";

console.log(user.name);
```

Output:

```text
Sandip
```

---

# 27. Getter and Setter Together

```js
class User {
  constructor(name) {
    this._name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value.trim();
  }
}

const user = new User("Sandip");

console.log(user.name);

user.name = " Ram ";

console.log(user.name);
```

Output:

```text
Sandip
Ram
```

---

# 28. Checking an Instance

Use:

```js
instanceof
```

Example:

```js
class User {}

const user = new User();

console.log(user instanceof User);
```

Output:

```text
true
```

With inheritance:

```js
class User {}

class Admin extends User {}

const admin = new Admin();

console.log(admin instanceof Admin);
console.log(admin instanceof User);
```

Output:

```text
true
true
```

Because `User.prototype` appears in the prototype chain.

---

# 29. Classes Cannot Be Called Like Normal Functions

This is incorrect:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = User("Sandip");
```

It throws an error because classes must be used with:

```js
new User("Sandip");
```

---

# 30. Class Declaration

A class can be declared like this:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}
```

The class is block-scoped and behaves differently from traditional function declarations.

---

# 31. Class Expression

A class can also be stored in a variable.

```js
const User = class {
  constructor(name) {
    this.name = name;
  }
};

const user = new User("Sandip");

console.log(user.name);
```

This is called a **class expression**.

---

# 32. Class Expressions with a Name

You can also give the class expression an internal name:

```js
const User = class UserClass {
  constructor(name) {
    this.name = name;
  }
};
```

Usually, the simpler form is enough unless you need the internal class name.

---

# 33. Class Methods Are Not Enumerable

Methods defined in a class are non-enumerable on the prototype.

```js
class User {
  greet() {
    return "Hello";
  }
}

console.log(
  Object.keys(User.prototype)
);
```

Output:

```text
[]
```

The method still exists:

```js
console.log(
  Object.hasOwn(User.prototype, "greet")
);
```

Output:

```text
true
```

---

# 34. Class vs Constructor Function

### Constructor function

```js
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  return `Hello ${this.name}`;
};
```

### Class

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

The class syntax is generally easier to read.

Both use JavaScript's prototype system.

---

# 35. Class Prototype Structure

For:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}

const user = new User("Sandip");
```

The relationship is:

```text
user
 ↓
User.prototype
 ├── constructor
 └── greet()
 ↓
Object.prototype
 ↓
null
```

---

# 36. Practical Example: Order

```js
class Order {
  constructor(id, items = []) {
    this.id = id;
    this.items = items;
    this.status = "pending";
  }

  addItem(item) {
    this.items.push(item);
  }

  confirm() {
    this.status = "confirmed";
  }

  getSummary() {
    return {
      id: this.id,
      items: this.items,
      status: this.status
    };
  }
}

const order = new Order("ORD-001");

order.addItem("Pizza");
order.confirm();

console.log(order.getSummary());
```

The class keeps related data and behavior together.

---

# 37. Practical Example: Hotel Staff

```js
class Staff {
  constructor(name, role) {
    this.name = name;
    this.role = role;
  }

  getInfo() {
    return `${this.name} - ${this.role}`;
  }
}

class Waiter extends Staff {
  serveTable(tableNumber) {
    return `${this.name} is serving ${tableNumber}`;
  }
}

const waiter = new Waiter("Sandip", "Waiter");

console.log(waiter.getInfo());
console.log(waiter.serveTable("T-03"));
```

Output:

```text
Sandip - Waiter
Sandip is serving T-03
```

---

# 38. Important Rules

### Constructor

A class can have one constructor:

```js
constructor() {}
```

### `new`

Create an instance with:

```js
new User();
```

### `this`

Refers to the current instance when called as an instance method.

### `extends`

Creates inheritance:

```js
class Admin extends User {}
```

### `super`

Calls the parent constructor or method:

```js
super();
super.method();
```

### `static`

Creates class-level members:

```js
static method() {}
```

### `#`

Creates private fields or methods:

```js
#balance;
#validate();
```

---

# 39. Best Practices

* Use **PascalCase** for class names.
* Keep constructors focused on initialization.
* Put reusable behavior into methods.
* Use `extends` when there is a genuine parent-child relationship.
* Use `super()` when a child constructor extends a parent constructor.
* Use private fields when internal state should not be directly accessed.
* Use static methods for behavior related to the class itself.
* Avoid unnecessarily large classes.
* Keep each class responsible for a clear purpose.

---

# 40. Key Takeaways

* A class is a convenient syntax for creating objects.
* Classes were introduced in ES6.
* `constructor()` initializes an instance.
* `new` creates an instance of a class.
* `this` refers to the current object.
* Methods are shared through the class prototype.
* `extends` creates class inheritance.
* `super()` accesses the parent class.
* Methods can be overridden in child classes.
* `static` members belong to the class itself.
* `#` creates private fields and methods.
* Getters behave like properties.
* Setters control property assignment.
* `instanceof` checks the prototype chain.
* Classes still use prototypes internally.

## Class Structure

```text
             User Class
                 │
        ┌────────┴────────┐
        │                 │
   constructor()       methods
        │                 │
        ↓                 ↓
   instance data     User.prototype
        │
        ↓
      user
```

## Inheritance Structure

```text
Admin instance
      ↓
Admin.prototype
      ↓
User.prototype
      ↓
Object.prototype
      ↓
null
```
