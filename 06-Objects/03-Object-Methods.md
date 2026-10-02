# JavaScript Object Methods

A **method** is a function stored inside an object.

For example:

```javascript
const user = {
  name: "Sandip",

  greet: function () {
    console.log("Hello!");
  }
};
```

Here:

* `name` is a property.
* `greet` is a method.
* `greet` contains a function.

---

# 1. What Is an Object Method?

A normal function:

```javascript
function greet() {
  console.log("Hello");
}
```

A function inside an object:

```javascript
const user = {
  greet: function () {
    console.log("Hello");
  }
};
```

The second one is called an **object method**.

---

# 2. Calling an Object Method

Use dot notation:

```javascript
const user = {
  name: "Sandip",

  greet: function () {
    console.log("Hello Sandip");
  }
};

user.greet();
```

Output:

```text
Hello Sandip
```

### Syntax

```javascript
object.method();
```

---

# 3. Method With Parameters

Methods can accept parameters just like normal functions.

```javascript
const user = {
  greet: function (name) {
    console.log(`Hello ${name}`);
  }
};

user.greet("Sandip");
```

Output:

```text
Hello Sandip
```

---

# 4. Method With a Return Value

A method can return a value.

```javascript
const calculator = {
  add: function (a, b) {
    return a + b;
  }
};

const result = calculator.add(10, 20);

console.log(result);
```

Output:

```text
30
```

---

# 5. Method Shorthand

Modern JavaScript provides a shorter syntax for methods.

Instead of:

```javascript
const user = {
  greet: function () {
    console.log("Hello");
  }
};
```

You can write:

```javascript
const user = {
  greet() {
    console.log("Hello");
  }
};
```

Both are object methods.

---

# 6. Multiple Methods

An object can have multiple methods.

```javascript
const calculator = {
  add(a, b) {
    return a + b;
  },

  subtract(a, b) {
    return a - b;
  },

  multiply(a, b) {
    return a * b;
  },

  divide(a, b) {
    return a / b;
  }
};

console.log(calculator.add(10, 5));
console.log(calculator.subtract(10, 5));
console.log(calculator.multiply(10, 5));
console.log(calculator.divide(10, 5));
```

Output:

```text
15
5
50
2
```

---

# 7. Method Access With Bracket Notation

You can also access methods using brackets.

```javascript
const user = {
  greet() {
    console.log("Hello");
  }
};

user["greet"]();
```

Output:

```text
Hello
```

---

# 8. Dynamic Method Access

A variable can contain the method name.

```javascript
const calculator = {
  add(a, b) {
    return a + b;
  },

  multiply(a, b) {
    return a * b;
  }
};

const operation = "add";

console.log(calculator[operation](10, 5));
```

Output:

```text
15
```

The following:

```javascript
calculator[operation](10, 5);
```

becomes:

```javascript
calculator["add"](10, 5);
```

---

# 9. Methods Can Use Object Properties

One of the most useful features of object methods is accessing other properties of the same object.

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(`Hello ${this.name}`);
  }
};

user.greet();
```

Output:

```text
Hello Sandip
```

Here:

```javascript
this.name
```

refers to the `name` property of the object when the method is called as `user.greet()`.

---

# 10. Understanding `this`

Inside a regular object method, `this` usually refers to the object that called the method.

```javascript
const user = {
  name: "Sandip",

  showName() {
    console.log(this.name);
  }
};

user.showName();
```

Output:

```text
Sandip
```

Here:

```text
this → user
```

So:

```javascript
this.name
```

means:

```javascript
user.name
```

---

# 11. Example With Multiple Properties

```javascript
const student = {
  name: "Sandip",
  age: 22,
  course: "BSc.CSIT",

  introduce() {
    console.log(
      `My name is ${this.name}. I am ${this.age} years old and study ${this.course}.`
    );
  }
};

student.introduce();
```

Output:

```text
My name is Sandip. I am 22 years old and study BSc.CSIT.
```

---

# 12. Methods Can Modify Properties

A method can change the object's properties.

```javascript
const user = {
  name: "Sandip",
  age: 22,

  increaseAge() {
    this.age++;
  }
};

user.increaseAge();

console.log(user.age);
```

Output:

```text
23
```

---

# 13. Method That Updates a Property

```javascript
const account = {
  balance: 1000,

  deposit(amount) {
    this.balance += amount;
  }
};

account.deposit(500);

console.log(account.balance);
```

Output:

```text
1500
```

---

# 14. Method That Uses Multiple Properties

```javascript
const product = {
  name: "Laptop",
  price: 80000,
  quantity: 2,

  getTotal() {
    return this.price * this.quantity;
  }
};

console.log(product.getTotal());
```

Output:

```text
160000
```

---

# 15. Hotel Management Example

Object methods are very useful in applications such as a hotel management system.

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "available",

  occupy() {
    this.status = "occupied";
  },

  makeAvailable() {
    this.status = "available";
  }
};
```

Use the methods:

```javascript
table.occupy();

console.log(table.status);
```

Output:

```text
occupied
```

Then:

```javascript
table.makeAvailable();

console.log(table.status);
```

Output:

```text
available
```

---

# 16. Food Example

```javascript
const food = {
  name: "Chicken Momo",
  price: 180,
  quantity: 2,

  getTotal() {
    return this.price * this.quantity;
  },

  increaseQuantity() {
    this.quantity++;
  }
};

console.log(food.getTotal());

food.increaseQuantity();

console.log(food.quantity);
```

Output:

```text
360
3
```

---

# 17. Order Example

```javascript
const order = {
  orderNumber: "ORD-001",
  status: "pending",

  confirm() {
    this.status = "confirmed";
  },

  cancel() {
    this.status = "cancelled";
  },

  getStatus() {
    return this.status;
  }
};

console.log(order.getStatus());

order.confirm();

console.log(order.getStatus());
```

Output:

```text
pending
confirmed
```

---

# 18. Methods Can Call Other Methods

A method can call another method of the same object using `this`.

```javascript
const user = {
  name: "Sandip",

  getName() {
    return this.name;
  },

  greet() {
    console.log(`Hello ${this.getName()}`);
  }
};

user.greet();
```

Output:

```text
Hello Sandip
```

Here:

```javascript
this.getName()
```

calls another method of the same object.

---

# 19. Method With Conditional Logic

Methods can contain normal JavaScript logic.

```javascript
const account = {
  balance: 5000,

  withdraw(amount) {
    if (amount <= this.balance) {
      this.balance -= amount;
      return "Withdrawal successful";
    }

    return "Insufficient balance";
  }
};

console.log(account.withdraw(2000));
console.log(account.balance);
```

Output:

```text
Withdrawal successful
3000
```

---

# 20. Method With an Array Property

An object method can work with an array stored in the same object.

```javascript
const cart = {
  items: ["Laptop", "Mouse", "Keyboard"],

  addItem(item) {
    this.items.push(item);
  },

  getItemCount() {
    return this.items.length;
  }
};

cart.addItem("Monitor");

console.log(cart.items);
console.log(cart.getItemCount());
```

---

# 21. Methods Can Return Objects

A method can return an object.

```javascript
const user = {
  name: "Sandip",
  age: 22,

  getProfile() {
    return {
      name: this.name,
      age: this.age
    };
  }
};

console.log(user.getProfile());
```

Result:

```javascript
{
  name: "Sandip",
  age: 22
}
```

---

# 22. Methods Can Accept Objects

A method can also receive objects as arguments.

```javascript
const calculator = {
  addNumbers(numbers) {
    return numbers[0] + numbers[1];
  }
};

console.log(
  calculator.addNumbers([10, 20])
);
```

Output:

```text
30
```

---

# 23. Regular Function vs Object Method

### Normal function

```javascript
function greet() {
  console.log("Hello");
}

greet();
```

### Object method

```javascript
const user = {
  greet() {
    console.log("Hello");
  }
};

user.greet();
```

The main difference is that the method belongs to the object.

---

# 24. Arrow Functions as Object Properties

You can store an arrow function in an object.

```javascript
const user = {
  greet: () => {
    console.log("Hello");
  }
};

user.greet();
```

This works.

However, arrow functions have **lexical `this`** and do not create their own `this`.

For object methods that need the object as `this`, prefer regular method syntax:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};
```

Instead of:

```javascript
const user = {
  name: "Sandip",

  greet: () => {
    console.log(this.name);
  }
};
```

The second example should not be used when you expect `this` to refer to `user`.

---

# 25. Method Shorthand vs Arrow Function

These are different:

### Method shorthand

```javascript
const user = {
  greet() {
    console.log(this.name);
  }
};
```

### Arrow function property

```javascript
const user = {
  greet: () => {
    console.log(this.name);
  }
};
```

The `this` behavior is different.

For object methods that depend on `this`, use:

```javascript
method() {}
```

---

# 26. Adding a Method Later

You can add a method after creating the object.

```javascript
const user = {
  name: "Sandip"
};

user.greet = function () {
  console.log(`Hello ${this.name}`);
};

user.greet();
```

Output:

```text
Hello Sandip
```

---

# 27. Deleting a Method

Because a method is a property containing a function, you can delete it.

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log("Hello");
  }
};

delete user.greet;
```

Now:

```javascript
console.log(user.greet);
```

Output:

```text
undefined
```

---

# 28. Checking Whether a Method Exists

You can use:

```javascript
Object.hasOwn(user, "greet");
```

Example:

```javascript
const user = {
  greet() {
    console.log("Hello");
  }
};

console.log(Object.hasOwn(user, "greet"));
```

Output:

```text
true
```

---

# 29. Methods Are Functions

You can store a method in a variable and call it.

```javascript
const user = {
  greet() {
    console.log("Hello");
  }
};

const greetFunction = user.greet;

greetFunction();
```

The function is called, but there is an important difference: calling it this way does not provide the same `this` receiver as `user.greet()`.

For example:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};

user.greet();
```

Here `this` refers to `user`.

But:

```javascript
const greet = user.greet;

greet();
```

The `this` value is no longer automatically the `user` object.

The exact behavior depends on strict mode and how the function is called.

---

# 30. Method Call Determines `this`

Consider:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};

user.greet();
```

The call:

```javascript
user.greet();
```

gives the method an object receiver.

Therefore:

```javascript
this === user
```

for that call.

This concept becomes very important when learning JavaScript `this`, prototypes, and classes.

---

# 31. Practical Example: Shopping Cart

```javascript
const cart = {
  items: [],

  addItem(item) {
    this.items.push(item);
  },

  removeItem(item) {
    const index = this.items.indexOf(item);

    if (index !== -1) {
      this.items.splice(index, 1);
    }
  },

  getItems() {
    return this.items;
  },

  getCount() {
    return this.items.length;
  }
};

cart.addItem("Laptop");
cart.addItem("Mouse");

console.log(cart.getItems());
console.log(cart.getCount());

cart.removeItem("Mouse");

console.log(cart.getItems());
```

This demonstrates how methods can manage an object's internal data.

---

# 32. Practical Example: Hotel Table

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "available",

  isAvailable() {
    return this.status === "available";
  },

  occupy() {
    if (this.isAvailable()) {
      this.status = "occupied";
      return true;
    }

    return false;
  },

  release() {
    this.status = "available";
  }
};

console.log(table.isAvailable());

table.occupy();

console.log(table.status);

table.release();

console.log(table.status);
```

Methods allow the object to contain both:

* data
* behavior

This is one of the important ideas behind **object-oriented programming**.

---

# 33. Data + Behavior

An object can combine data and behavior.

```javascript
const user = {
  // Data
  name: "Sandip",
  age: 22,

  // Behavior
  greet() {
    console.log(`Hello, I am ${this.name}`);
  }
};
```

Think of it as:

```text
Object
│
├── Data
│   ├── name
│   └── age
│
└── Behavior
    └── greet()
```

---

# 34. Common Mistakes

### Mistake 1: Forgetting `()`

Incorrect:

```javascript
user.greet;
```

This accesses the function.

To execute it:

```javascript
user.greet();
```

---

### Mistake 2: Calling a non-function property

```javascript
const user = {
  name: "Sandip"
};

user.name();
```

This causes an error because `name` contains a string, not a function.

---

### Mistake 3: Incorrect arrow function `this`

Avoid:

```javascript
const user = {
  name: "Sandip",

  greet: () => {
    console.log(this.name);
  }
};
```

when you expect `this` to refer to `user`.

Prefer:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};
```

---

### Mistake 4: Losing the object receiver

```javascript
const greet = user.greet;

greet();
```

This is not equivalent to:

```javascript
user.greet();
```

The way a function is called affects its `this` value.

---

# 35. Object Methods Cheat Sheet

| Concept             | Example                           |
| ------------------- | --------------------------------- |
| Method              | `greet() {}`                      |
| Call method         | `user.greet()`                    |
| Method parameter    | `greet(name) {}`                  |
| Return value        | `getName() { return this.name; }` |
| Access property     | `this.name`                       |
| Modify property     | `this.age++`                      |
| Call another method | `this.getName()`                  |
| Bracket method      | `user["greet"]()`                 |
| Dynamic method      | `user[methodName]()`              |
| Check method        | `Object.hasOwn(user, "greet")`    |
| Delete method       | `delete user.greet`               |

---

# 36. Key Takeaways

* A **method is a function stored in an object**.
* Methods represent an object's behavior.
* Call a method using `object.method()`.
* Methods can accept parameters.
* Methods can return values.
* Methods can read and modify object properties.
* `this` commonly refers to the object used as the receiver of a method call.
* Use method shorthand:

```javascript
method() {}
```

* Arrow functions have lexical `this`, so they should not normally be used as object methods when you need `this` to refer to the object.
* A method can call another method using `this`.
* Methods can work with arrays, nested objects, and other values.
* Objects can combine **data + behavior**.

---

## Quick Example

```javascript
const user = {
  name: "Sandip",
  age: 22,

  greet() {
    return `Hello, I am ${this.name}`;
  },

  increaseAge() {
    this.age++;
  }
};

console.log(user.greet());

user.increaseAge();

console.log(user.age);
```

Output:

```text
Hello, I am Sandip
23
```

---
