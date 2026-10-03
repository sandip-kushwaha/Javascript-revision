# JavaScript Encapsulation

## What is Encapsulation?

**Encapsulation** means keeping an object's data and the operations that work with that data together, while controlling how outside code can access or modify the internal state.

In simple terms:

```text
Encapsulation
      ↓
Hide internal details
      ↓
Control access
      ↓
Protect object state
```

For example, instead of allowing anyone to directly change a bank account balance:

```js
account.balance = -50000;
```

we can control changes through methods or setters.

---

# 1. Simple Example

Without encapsulation:

```js
const user = {
  name: "Sandip",
  age: 20
};

user.age = -10;

console.log(user.age);
```

The object allows an invalid value.

With encapsulation:

```js
class User {
  #age;

  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  get age() {
    return this.#age;
  }

  set age(value) {
    if (value < 0) {
      throw new Error("Age cannot be negative");
    }

    this.#age = value;
  }
}

const user = new User("Sandip", 20);

console.log(user.age);
```

Now the age is controlled by the class.

---

# 2. Main Purpose of Encapsulation

Encapsulation helps you:

* protect internal data
* validate values
* control how data changes
* hide implementation details
* reduce accidental modifications
* make code easier to maintain

---

# 3. Public Properties

By default, JavaScript class properties are public.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user.name);

user.name = "Ram";

console.log(user.name);
```

Output:

```text
Sandip
Ram
```

The property can be accessed and changed directly.

---

# 4. Private Fields

Modern JavaScript provides private class fields using `#`.

```js
class User {
  #password;

  constructor(password) {
    this.#password = password;
  }
}

const user = new User("secret");
```

The field:

```js
#password
```

is private to the class.

You cannot access it from outside:

```js
console.log(user.#password);
```

This causes a syntax error.

---

# 5. Private Fields with Methods

Private data can be accessed through methods inside the class.

```js
class User {
  #password;

  constructor(password) {
    this.#password = password;
  }

  checkPassword(password) {
    return this.#password === password;
  }
}

const user = new User("secret");

console.log(user.checkPassword("secret"));
```

Output:

```text
true
```

The outside code never directly accesses:

```js
#password
```

---

# 6. Private Field with Getter

A private field can be exposed through a controlled getter.

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

The actual field remains private:

```text
#name
```

while the public interface is:

```text
name
```

---

# 7. Private Field with Setter

You can also control changes with a setter.

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

The setter prevents invalid values.

---

# 8. Encapsulation Using Methods

Encapsulation does not always require private fields.

A class can expose specific methods for changing internal state.

```js
class Counter {
  #count = 0;

  increment() {
    this.#count++;
  }

  decrement() {
    this.#count--;
  }

  getValue() {
    return this.#count;
  }
}

const counter = new Counter();

counter.increment();
counter.increment();

console.log(counter.getValue());
```

Output:

```text
2
```

Outside code cannot directly modify:

```js
#count
```

---

# 9. Bank Account Example

A bank account is a good example of encapsulation.

```js
class BankAccount {
  #balance = 0;

  deposit(amount) {
    if (amount <= 0) {
      throw new Error("Deposit must be greater than zero");
    }

    this.#balance += amount;
  }

  withdraw(amount) {
    if (amount <= 0) {
      throw new Error("Withdrawal must be greater than zero");
    }

    if (amount > this.#balance) {
      throw new Error("Insufficient balance");
    }

    this.#balance -= amount;
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount();

account.deposit(5000);
account.withdraw(1500);

console.log(account.getBalance());
```

Output:

```text
3500
```

The balance cannot be directly changed from outside.

---

# 10. Why Direct Access Can Be Dangerous

Suppose we have:

```js
class BankAccount {
  constructor(balance) {
    this.balance = balance;
  }
}
```

Then:

```js
const account = new BankAccount(5000);

account.balance = -100000;
```

The object has no protection against an invalid state.

With encapsulation:

```js
class BankAccount {
  #balance;

  constructor(balance) {
    if (balance < 0) {
      throw new Error("Invalid balance");
    }

    this.#balance = balance;
  }

  deposit(amount) {
    if (amount <= 0) {
      throw new Error("Invalid deposit");
    }

    this.#balance += amount;
  }

  get balance() {
    return this.#balance;
  }
}
```

Now the class controls its state.

---

# 11. Encapsulation with Getters and Setters

Getters and setters provide a controlled interface.

```js
class Product {
  #price;

  constructor(price) {
    this.price = price;
  }

  get price() {
    return this.#price;
  }

  set price(value) {
    if (value <= 0) {
      throw new Error("Price must be greater than zero");
    }

    this.#price = value;
  }
}

const product = new Product(500);

console.log(product.price);

product.price = 750;

console.log(product.price);
```

The price is private, but controlled access is available.

---

# 12. Encapsulation Does Not Mean Hiding Everything

Encapsulation does **not** mean that every property must be private.

For example:

```js
class Product {
  constructor(name, price) {
    this.name = name;
    this.#setPrice(price);
  }

  #setPrice(price) {
    if (price <= 0) {
      throw new Error("Invalid price");
    }

    this.price = price;
  }
}
```

Here:

* `name` is public.
* `price` is public.
* `#setPrice()` is private.

You decide which parts need controlled access.

---

# 13. Private Methods

JavaScript also supports private methods.

Use `#` before the method name.

```js
class User {
  #validateName(name) {
    return name.trim().length > 0;
  }

  constructor(name) {
    if (!this.#validateName(name)) {
      throw new Error("Invalid name");
    }

    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user.name);
```

The method:

```js
#validateName()
```

can only be called from inside the class.

---

# 14. Private Static Members

Private members can also be static.

```js
class User {
  static #count = 0;

  constructor(name) {
    this.name = name;
    User.#count++;
  }

  static getCount() {
    return User.#count;
  }
}

new User("Sandip");
new User("Ram");

console.log(User.getCount());
```

Output:

```text
2
```

The count belongs to the class rather than each individual object.

---

# 15. Encapsulation in a Hotel System

Consider a hotel table.

We don't want every part of the application to freely change its status to any value.

```js
class HotelTable {
  #status = "available";

  constructor(tableNumber, capacity) {
    this.tableNumber = tableNumber;
    this.capacity = capacity;
  }

  get status() {
    return this.#status;
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

    this.#status = value;
  }
}

const table = new HotelTable("T-03", 6);

console.log(table.status);

table.status = "occupied";

console.log(table.status);
```

Output:

```text
available
occupied
```

The status is protected from invalid values.

---

# 16. Better Control with Specific Methods

Sometimes methods communicate business rules better than a generic setter.

```js
class HotelTable {
  #status = "available";

  occupy() {
    if (this.#status !== "available") {
      throw new Error("Table is not available");
    }

    this.#status = "occupied";
  }

  clean() {
    this.#status = "cleaning";
  }

  makeAvailable() {
    this.#status = "available";
  }

  get status() {
    return this.#status;
  }
}

const table = new HotelTable();

table.occupy();

console.log(table.status);
```

Output:

```text
occupied
```

This approach makes the allowed operations explicit.

---

# 17. Encapsulation in a Food Order

```js
class Order {
  #items = [];

  addItem(item) {
    if (!item.name || item.price <= 0) {
      throw new Error("Invalid item");
    }

    this.#items.push(item);
  }

  removeItem(index) {
    if (index < 0 || index >= this.#items.length) {
      throw new Error("Invalid item index");
    }

    this.#items.splice(index, 1);
  }

  get items() {
    return [...this.#items];
  }

  get total() {
    return this.#items.reduce(
      (sum, item) => sum + item.price,
      0
    );
  }
}

const order = new Order();

order.addItem({
  name: "Pizza",
  price: 450
});

order.addItem({
  name: "Coffee",
  price: 120
});

console.log(order.items);
console.log(order.total);
```

Output:

```text
[
  { name: "Pizza", price: 450 },
  { name: "Coffee", price: 120 }
]

570
```

---

# 18. Why Return a Copy?

Consider:

```js
get items() {
  return this.#items;
}
```

Outside code could then modify the original array:

```js
order.items.push({
  name: "Invalid Item",
  price: -500
});
```

Instead:

```js
get items() {
  return [...this.#items];
}
```

returns a shallow copy.

Now changes to the returned array do not directly modify the internal array.

```text
Private array
     │
     ↓
   copy
     │
     ↓
Outside code
```

This is an important part of protecting internal state.

---

# 19. Encapsulation vs Private Fields

These concepts are related but not identical.

### Encapsulation

A design principle:

```text
Control access to object state
```

### Private field

A JavaScript language feature:

```js
#balance
```

Private fields are one way to implement encapsulation.

Other techniques include:

* methods
* getters/setters
* closures
* modules
* controlled APIs

---

# 20. Encapsulation with Closures

Before private class fields existed, closures were commonly used to hide data.

```js
function createCounter() {
  let count = 0;

  return {
    increment() {
      count++;
    },

    getValue() {
      return count;
    }
  };
}

const counter = createCounter();

counter.increment();
counter.increment();

console.log(counter.getValue());
```

Output:

```text
2
```

`count` cannot be directly accessed from outside.

```text
createCounter()
      │
      ├── count → private
      │
      ├── increment()
      │
      └── getValue()
```

---

# 21. Encapsulation with Modules

Modules can also hide implementation details.

```js
const secret = "internal value";

export function getSecret() {
  return secret;
}
```

Other files can use:

```js
import { getSecret } from "./security.js";
```

But they cannot directly access:

```js
secret
```

because it was not exported.

---

# 22. Encapsulation and Abstraction

These concepts are related but different.

### Encapsulation

Controls access to data and implementation.

```text
How can data be accessed?
```

### Abstraction

Hides unnecessary complexity and exposes what is needed.

```text
What does the user need to know?
```

For example:

```js
account.withdraw(1000);
```

The caller does not need to know every internal step used to update the balance.

---

# 23. Encapsulation and Inheritance

Private fields belong to the class that declares them.

```js
class User {
  #password;

  constructor(password) {
    this.#password = password;
  }
}

class Admin extends User {
  showPassword() {
    // Cannot directly access User's #password
  }
}
```

A child class cannot directly access a parent's private field.

Instead, the parent class can expose controlled methods:

```js
class User {
  #password;

  constructor(password) {
    this.#password = password;
  }

  checkPassword(value) {
    return this.#password === value;
  }
}

class Admin extends User {
  verify(value) {
    return this.checkPassword(value);
  }
}
```

The child uses the parent's public/protected-style interface rather than the private field itself.

---

# 24. Encapsulation Does Not Mean Security by Itself

Private fields provide JavaScript-level access control.

They should not be confused with complete application security.

For example:

```js
class User {
  #password;

  constructor(password) {
    this.#password = password;
  }
}
```

This does not automatically mean that a real application should store passwords as plain text.

In a backend application, passwords should be handled using appropriate password hashing and authentication practices.

Encapsulation protects object design; application security requires additional measures.

---

# 25. Good Encapsulation Design

A good class generally:

```text
                Class
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
    Internal State       Public API
        │                   │
      private          methods/getters
        │                   │
        └──── controlled ───┘
             access
```

Example:

```js
class BankAccount {
  #balance = 0;

  deposit(amount) {
    if (amount <= 0) {
      throw new Error("Invalid amount");
    }

    this.#balance += amount;
  }

  get balance() {
    return this.#balance;
  }
}
```

The internal state is protected while useful operations remain available.

---

# 26. Common Encapsulation Mistakes

### Mistake 1: Making everything public

```js
class Account {
  constructor() {
    this.balance = 0;
  }
}
```

If the balance must follow business rules, uncontrolled public access may be undesirable.

---

### Mistake 2: Exposing private data directly

```js
get items() {
  return this.#items;
}
```

If callers can mutate the returned array, internal state may be changed indirectly.

Consider:

```js
get items() {
  return [...this.#items];
}
```

when appropriate.

---

### Mistake 3: Using `_` as if it were private

```js
this._password = password;
```

The underscore is only a convention.

This is still accessible:

```js
user._password;
```

True private fields use:

```js
this.#password;
```

---

### Mistake 4: Adding unnecessary getters/setters

Not every property needs a getter and setter.

This may be unnecessary:

```js
get name() {
  return this._name;
}

set name(value) {
  this._name = value;
}
```

If there is no validation, transformation, or controlled access requirement, a normal property may be simpler.

---

# 27. Encapsulation Example with Validation

```js
class Product {
  #name;
  #price;

  constructor(name, price) {
    this.name = name;
    this.price = price;
  }

  get name() {
    return this.#name;
  }

  set name(value) {
    const name = value.trim();

    if (!name) {
      throw new Error("Product name is required");
    }

    this.#name = name;
  }

  get price() {
    return this.#price;
  }

  set price(value) {
    const price = Number(value);

    if (!Number.isFinite(price) || price <= 0) {
      throw new Error("Invalid product price");
    }

    this.#price = price;
  }
}

const product = new Product(
  " Chicken Pizza ",
  "450"
);

console.log(product.name);
console.log(product.price);
```

Output:

```text
Chicken Pizza
450
```

The class handles:

* trimming
* validation
* type conversion
* private storage

---

# 28. Benefits of Encapsulation

### 1. Data protection

Internal state cannot be changed freely.

### 2. Validation

Invalid values can be rejected.

### 3. Maintainability

Internal implementation can change without changing the public API.

### 4. Reduced coupling

Other parts of the application depend on a controlled interface.

### 5. Clear responsibilities

The class controls its own state.

### 6. Safer modifications

Changes happen through defined methods or setters.

---

# 29. Simple Real-World Analogy

Think about an ATM.

You can:

```text
Insert card
     ↓
Enter PIN
     ↓
Choose operation
     ↓
Withdraw money
```

You cannot directly access the bank's internal database.

The ATM provides a controlled interface.

Similarly:

```js
account.withdraw(1000);
```

is a controlled interface to the internal balance.

```text
Public API
    ↓
withdraw()
    ↓
Validation
    ↓
Private balance
```

---

# 30. Encapsulation Summary

| Concept         | Meaning                                               |
| --------------- | ----------------------------------------------------- |
| Encapsulation   | Control access to internal state                      |
| Public property | Accessible from outside                               |
| Private field   | Declared using `#`                                    |
| Private method  | Method declared using `#`                             |
| Getter          | Controlled reading                                    |
| Setter          | Controlled writing                                    |
| Closure         | Can hide data through lexical scope                   |
| Module          | Can hide non-exported data                            |
| Validation      | Prevents invalid state                                |
| Copy            | Helps prevent direct mutation of internal collections |

---

# Key Takeaways

* **Encapsulation** means controlling access to an object's internal state.
* JavaScript supports true private class fields using `#`.
* Private methods also use `#`.
* Getters and setters can provide controlled access.
* Methods can enforce business rules.
* Returning copies can protect internal arrays and objects from direct mutation.
* Closures and modules can also hide implementation details.
* `_property` is a convention, not real privacy.
* Private fields are not directly accessible from child classes.
* Encapsulation is a design principle, while private fields are one language feature used to implement it.
* Encapsulation improves maintainability, validation, and control over object state.
* Encapsulation is not a replacement for application-level security.

## Simple Mental Model

```text
        Object
          │
    ┌─────┴─────┐
    ↓           ↓
 Private      Public
  State        API
    │           │
    │      ┌────┴────┐
    │      ↓         ↓
    │   Methods   Getters
    │      │         │
    └──────┴─────────┘
          Controlled
            Access
```
