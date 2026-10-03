# JavaScript Getters and Setters

## What are Getters and Setters?

**Getters** and **setters** allow you to control how properties are read and changed.

* **Getter** → reads or calculates a value.
* **Setter** → controls how a value is assigned.

They are useful when you want a property to have custom behavior.

```text
Getter → read a property
Setter → change a property
```

---

# 1. Basic Getter

A getter uses the `get` keyword.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  get username() {
    return this.name;
  }
}

const user = new User("Sandip");

console.log(user.username);
```

Output:

```text
Sandip
```

Notice that we use:

```js
user.username
```

not:

```js
user.username()
```

A getter is accessed like a normal property.

---

# 2. Basic Setter

A setter uses the `set` keyword.

```js
class User {
  set username(value) {
    this.name = value;
  }
}

const user = new User();

user.username = "Sandip";

console.log(user.name);
```

Output:

```text
Sandip
```

The setter runs when you assign:

```js
user.username = "Sandip";
```

---

# 3. Getter and Setter Together

A common pattern is to use both.

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

The setter cleans the value before storing it.

---

# 4. Why Use `_name`?

Consider:

```js
class User {
  get name() {
    return this.name;
  }

  set name(value) {
    this.name = value;
  }
}
```

This causes recursive calls.

The getter calls itself:

```text
name
 ↓
getter
 ↓
name
 ↓
getter
 ↓
...
```

Instead, use a different internal property:

```js
this._name
```

Example:

```js
class User {
  constructor(name) {
    this._name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value;
  }
}
```

Here:

```text
name → public interface
_name → internal storage
```

> `_name` is only a naming convention. It is not a JavaScript private field. If you need true private storage, use `#name`.

---

# 5. Getter for a Calculated Value

A getter does not have to return a stored property.

It can calculate a value.

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.width * this.height;
  }
}

const rectangle = new Rectangle(10, 5);

console.log(rectangle.area);
```

Output:

```text
50
```

There is no separate `area` property being stored.

It is calculated when accessed.

---

# 6. Getter with Full Name

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

const user = new User(
  "Sandip",
  "Kushwaha"
);

console.log(user.fullName);
```

Output:

```text
Sandip Kushwaha
```

The getter creates the value from:

```text
firstName + lastName
```

---

# 7. Getter with Array Data

```js
class Order {
  constructor(items = []) {
    this.items = items;
  }

  get itemCount() {
    return this.items.length;
  }
}

const order = new Order([
  "Pizza",
  "Burger",
  "Coffee"
]);

console.log(order.itemCount);
```

Output:

```text
3
```

The getter calculates the number of items.

---

# 8. Getter for Total Price

```js
class Order {
  constructor(items = []) {
    this.items = items;
  }

  get total() {
    return this.items.reduce(
      (sum, item) => sum + item.price,
      0
    );
  }
}

const order = new Order([
  { name: "Pizza", price: 450 },
  { name: "Coffee", price: 120 }
]);

console.log(order.total);
```

Output:

```text
570
```

This is useful when a value depends on current object data.

---

# 9. Setter for Validation

Setters are useful for validation.

```js
class Product {
  constructor(price) {
    this.price = price;
  }

  set price(value) {
    if (value < 0) {
      throw new Error("Price cannot be negative");
    }

    this._price = value;
  }

  get price() {
    return this._price;
  }
}

const product = new Product(2500);

console.log(product.price);
```

The setter controls what values can be stored.

---

# 10. Setter for String Cleanup

```js
class User {
  constructor(name) {
    this.name = name;
  }

  set name(value) {
    this._name = value.trim();
  }

  get name() {
    return this._name;
  }
}

const user = new User("  Sandip  ");

console.log(user.name);
```

Output:

```text
Sandip
```

The setter automatically removes extra spaces.

---

# 11. Setter for Type Conversion

A setter can also normalize values.

```js
class Product {
  set price(value) {
    this._price = Number(value);
  }

  get price() {
    return this._price;
  }
}

const product = new Product();

product.price = "2500";

console.log(product.price);
console.log(typeof product.price);
```

Output:

```text
2500
number
```

The setter converts the value to a number.

---

# 12. Setter with Multiple Conditions

```js
class User {
  set age(value) {
    if (!Number.isInteger(value)) {
      throw new Error("Age must be an integer");
    }

    if (value < 0) {
      throw new Error("Age cannot be negative");
    }

    this._age = value;
  }

  get age() {
    return this._age;
  }
}

const user = new User();

user.age = 20;

console.log(user.age);
```

The setter ensures that only valid values are stored.

---

# 13. Read-Only Property

You can create a getter without a setter.

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

const user = new User(
  "Sandip",
  "Kushwaha"
);

console.log(user.fullName);
```

There is no:

```js
set fullName()
```

So `fullName` is effectively read-only through this interface.

In strict mode, attempting to assign to it throws a `TypeError`.

---

# 14. Write-Only Property

A setter can exist without a getter.

```js
class User {
  set password(value) {
    this._password = value;
  }
}

const user = new User();

user.password = "secret";
```

The property can be assigned through the setter, but there is no getter to read it through `user.password`.

However, this does **not** make `_password` truly private:

```js
console.log(user._password);
```

For real private data, use a private field such as:

```js
#password
```

---

# 15. Getters and Setters with Private Fields

Modern JavaScript allows private fields with getters and setters.

```js
class BankAccount {
  #balance = 0;

  get balance() {
    return this.#balance;
  }

  set balance(value) {
    if (value < 0) {
      throw new Error("Balance cannot be negative");
    }

    this.#balance = value;
  }
}

const account = new BankAccount();

account.balance = 1000;

console.log(account.balance);
```

Output:

```text
1000
```

The actual balance remains private.

---

# 16. Getter with Private Field

```js
class User {
  #name;

  constructor(name) {
    this.#name = name;
  }

  get name() {
    return this.#name;
  }
}

const user = new User("Sandip");

console.log(user.name);
```

The outside code can read the name through the getter but cannot directly access:

```js
user.#name;
```

---

# 17. Setter with Private Field

```js
class User {
  #name;

  constructor(name) {
    this.name = name;
  }

  get name() {
    return this.#name;
  }

  set name(value) {
    if (!value.trim()) {
      throw new Error("Name cannot be empty");
    }

    this.#name = value.trim();
  }
}

const user = new User("Sandip");

user.name = "Ram";

console.log(user.name);
```

The setter provides controlled access to the private field.

---

# 18. Getter vs Normal Method

Getter:

```js
class User {
  get fullName() {
    return "Sandip Kushwaha";
  }
}
```

Usage:

```js
user.fullName;
```

Normal method:

```js
class User {
  getFullName() {
    return "Sandip Kushwaha";
  }
}
```

Usage:

```js
user.getFullName();
```

Choose a getter when the operation conceptually behaves like a property.

---

# 19. Getter Should Usually Be Lightweight

A getter is accessed like a property:

```js
user.fullName;
```

Because of that, it is usually best for simple calculations or controlled property access.

Good:

```js
get fullName() {
  return `${this.firstName} ${this.lastName}`;
}
```

Less suitable:

```js
get report() {
  // expensive database request
  // network operation
  // large computation
}
```

For expensive or asynchronous operations, a normal method is generally clearer.

---

# 20. Setters Are Synchronous

A JavaScript setter cannot be declared with `async`.

This is not valid:

```js
class User {
  async set name(value) {
    // ...
  }
}
```

If an operation needs asynchronous behavior, use a normal method:

```js
class User {
  async updateName(value) {
    // asynchronous work
  }
}
```

---

# 21. Getter and Setter Naming

Usually, the getter and setter use the same property name:

```js
class User {
  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value;
  }
}
```

This allows natural syntax:

```js
user.name;
```

and:

```js
user.name = "Sandip";
```

---

# 22. Practical Hotel Table Example

```js
class HotelTable {
  constructor(tableNumber, capacity) {
    this.tableNumber = tableNumber;
    this.capacity = capacity;
    this.status = "available";
  }

  get isAvailable() {
    return this.status === "available";
  }

  set status(value) {
    const allowedStatuses = [
      "available",
      "occupied",
      "reserved",
      "cleaning",
      "maintenance"
    ];

    if (!allowedStatuses.includes(value)) {
      throw new Error("Invalid table status");
    }

    this._status = value;
  }

  get status() {
    return this._status;
  }
}

const table = new HotelTable("T-03", 6);

console.log(table.status);
console.log(table.isAvailable);

table.status = "occupied";

console.log(table.status);
console.log(table.isAvailable);
```

Output:

```text
available
true
occupied
false
```

The setter validates the table status.

The getter calculates availability.

---

# 23. Practical Food Example

```js
class Food {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }

  set price(value) {
    if (value <= 0) {
      throw new Error("Price must be greater than zero");
    }

    this._price = Number(value);
  }

  get price() {
    return this._price;
  }

  get displayPrice() {
    return `Rs. ${this._price}`;
  }
}

const food = new Food("Chicken Pizza", 450);

console.log(food.price);
console.log(food.displayPrice);
```

Output:

```text
450
Rs. 450
```

---

# 24. Practical User Example

```js
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  set email(value) {
    const email = value.trim().toLowerCase();

    if (!email.includes("@")) {
      throw new Error("Invalid email");
    }

    this._email = email;
  }

  get email() {
    return this._email;
  }

  get profile() {
    return `${this.name} - ${this.email}`;
  }
}

const user = new User(
  "Sandip",
  " SANDIP@EXAMPLE.COM "
);

console.log(user.email);
console.log(user.profile);
```

Output:

```text
sandip@example.com
Sandip - sandip@example.com
```

---

# 25. Getter and Setter Inheritance

Getters and setters can be inherited.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  get displayName() {
    return this.name;
  }
}

class Admin extends User {}

const admin = new Admin("Sandip");

console.log(admin.displayName);
```

The getter is inherited through the prototype chain.

---

# 26. Overriding a Getter

A child class can provide its own getter.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  get role() {
    return "User";
  }
}

class Admin extends User {
  get role() {
    return "Admin";
  }
}

const admin = new Admin("Sandip");

console.log(admin.role);
```

Output:

```text
Admin
```

---

# 27. Using `super` with Getters

A child can access a parent getter with `super`.

```js
class User {
  get role() {
    return "User";
  }
}

class Admin extends User {
  get role() {
    return `${super.role} → Admin`;
  }
}

const admin = new Admin();

console.log(admin.role);
```

Output:

```text
User → Admin
```

---

# 28. Setter and Inheritance

A child class can also define its own setter.

```js
class User {
  set name(value) {
    this._name = value.trim();
  }

  get name() {
    return this._name;
  }
}

class Admin extends User {
  set name(value) {
    this._name = `Admin: ${value.trim()}`;
  }
}

const admin = new Admin();

admin.name = "Sandip";

console.log(admin.name);
```

Output:

```text
Admin: Sandip
```

The child setter overrides the parent setter.

---

# 29. Getters and Setters on Objects

Getters and setters are not limited to classes.

They can also be defined in object literals.

```js
const user = {
  _name: "Sandip",

  get name() {
    return this._name;
  },

  set name(value) {
    this._name = value.trim();
  }
};

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

# 30. Getters and Setters with `Object.defineProperty()`

JavaScript also provides:

```js
Object.defineProperty()
```

Example:

```js
const user = {
  _name: "Sandip"
};

Object.defineProperty(user, "name", {
  get() {
    return this._name;
  },

  set(value) {
    this._name = value.trim();
  }
});

console.log(user.name);

user.name = " Ram ";

console.log(user.name);
```

This is useful when defining property behavior dynamically.

---

# 31. Getter/Setter Descriptor

A getter and setter are part of a property's **property descriptor**.

Example:

```js
const user = {
  _name: "Sandip"
};

Object.defineProperty(user, "name", {
  get() {
    return this._name;
  },

  set(value) {
    this._name = value;
  }
});
```

You can inspect the descriptor:

```js
console.log(
  Object.getOwnPropertyDescriptor(user, "name")
);
```

It contains properties such as:

```text
get
set
enumerable
configurable
```

---

# 32. Getter/Setter vs Public Property

Simple public property:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}
```

Getter/setter:

```js
class User {
  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value.trim();
  }
}
```

Use getters/setters when you need behavior such as:

* validation
* formatting
* normalization
* calculated values
* controlled access
* encapsulation

For simple data, a normal property is often enough.

---

# 33. Common Mistake: Calling a Getter

Incorrect:

```js
console.log(user.fullName());
```

If `fullName` is a getter, use:

```js
console.log(user.fullName);
```

Remember:

```text
Getter → property syntax
Method → function syntax
```

---

# 34. Common Mistake: Recursive Setter

Avoid:

```js
class User {
  set name(value) {
    this.name = value;
  }
}
```

This calls the setter again:

```text
name setter
   ↓
this.name
   ↓
name setter
   ↓
...
```

Use separate storage:

```js
class User {
  set name(value) {
    this._name = value;
  }

  get name() {
    return this._name;
  }
}
```

Or use a private field:

```js
class User {
  #name;

  set name(value) {
    this.#name = value;
  }

  get name() {
    return this.#name;
  }
}
```

---

# 35. Key Takeaways

* A getter controls how a property is read.
* A setter controls how a property is assigned.
* Getters use the `get` keyword.
* Setters use the `set` keyword.
* Getters are accessed without `()`.
* Setters are triggered by assignment.
* Getters can calculate values dynamically.
* Setters can validate or normalize values.
* A getter without a setter can provide a read-only interface.
* `_name` is a convention, not true privacy.
* `#name` provides a real private field.
* Getters and setters can be inherited and overridden.
* `super` can access a parent getter or setter.
* Getters should generally be lightweight.
* Use normal methods for operations that are expensive or asynchronous.

## Simple Mental Model

```text
              Object
                │
        ┌───────┴───────┐
        ↓               ↓
      Getter          Setter
        │               │
        ↓               ↓
      Read            Write
        │               │
        ↓               ↓
   user.name       user.name = value
```

## Common Pattern

```js
class User {
  #name;

  constructor(name) {
    this.name = name;
  }

  get name() {
    return this.#name;
  }

  set name(value) {
    this.#name = value.trim();
  }
}
```

This gives you:

```js
user.name;
```

for reading and:

```js
user.name = "Sandip";
```

for controlled writing.
