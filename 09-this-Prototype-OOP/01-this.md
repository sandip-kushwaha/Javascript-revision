# JavaScript `this`

`this` is a special keyword in JavaScript that refers to a value determined by **how a function is called**.

The meaning of `this` can change depending on the context.

The most important rule is:

> **For regular functions, `this` is generally determined by the call site.**

---

# 1. Simple Example

Inside an object method:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};

user.greet();
```

Output:

```text
Sandip
```

Here:

```javascript
this
```

refers to:

```javascript
user
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

# 2. What Is `this`?

`this` is not an ordinary variable.

You don't declare it like:

```javascript
const this = ...
```

Instead, JavaScript provides `this` automatically.

Its value depends on how the function is executed.

For example:

```javascript
const user = {
  name: "Sandip",

  showName() {
    console.log(this.name);
  }
};

user.showName();
```

The function is called as:

```javascript
user.showName();
```

Therefore:

```javascript
this === user
```

---

# 3. `this` in an Object Method

```javascript
const person = {
  name: "Sandip",

  introduce() {
    console.log(`My name is ${this.name}`);
  }
};

person.introduce();
```

Output:

```text
My name is Sandip
```

Here:

```javascript
this.name
```

refers to:

```javascript
person.name
```

---

# 4. `this` Refers to the Calling Object

Consider:

```javascript
const user1 = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};

const user2 = {
  name: "Ram",

  greet() {
    console.log(this.name);
  }
};

user1.greet();
user2.greet();
```

Output:

```text
Sandip
Ram
```

The same method style can work with different objects because `this` depends on the object used to call the method.

---

# 5. Important: `this` Is Not Determined by Where the Function Is Written

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

Here:

```javascript
this === user
```

because of the call:

```javascript
user.greet();
```

The important thing is **how the function is called**, not simply where it was defined.

---

# 6. Regular Function Called Normally

Consider:

```javascript
function showThis() {
  console.log(this);
}

showThis();
```

The result depends on whether the code is running in strict mode.

In modern JavaScript modules and strict mode:

```text
undefined
```

In non-strict browser scripts, a regular function called without an object may have:

```text
window
```

as its `this`.

Because behavior differs by execution mode, it is best to explicitly understand the environment rather than assume `this` is always `window`.

---

# 7. `this` in Strict Mode

```javascript
"use strict";

function showThis() {
  console.log(this);
}

showThis();
```

Output:

```text
undefined
```

In strict mode, a regular function called without an object has:

```javascript
this === undefined
```

ES modules are automatically strict mode.

---

# 8. `this` in Browser Global Context

In a classic browser script:

```javascript
console.log(this);
```

At the top level, `this` generally refers to:

```javascript
window
```

Example:

```javascript
console.log(this === window);
```

Output:

```text
true
```

This is different from `this` inside a regular function.

---

# 9. `this` in an Object Method

```javascript
const product = {
  name: "Laptop",
  price: 800,

  getDetails() {
    console.log(this.name);
    console.log(this.price);
  }
};

product.getDetails();
```

Output:

```text
Laptop
800
```

Here `this` refers to `product`.

---

# 10. Method Call Matters

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

Here:

```javascript
this === user
```

But if the method is extracted:

```javascript
const greet = user.greet;

greet();
```

The function is no longer called as:

```javascript
user.greet();
```

Therefore, the `this` value changes.

In strict mode:

```text
undefined
```

This is an important reason why methods can behave differently when passed around as callbacks.

---

# 11. `this` With Nested Objects

```javascript
const company = {
  name: "Tech Company",

  employee: {
    name: "Sandip",

    showName() {
      console.log(this.name);
    }
  }
};

company.employee.showName();
```

Output:

```text
Sandip
```

Here:

```javascript
this
```

refers to:

```javascript
company.employee
```

not:

```javascript
company
```

The object immediately used for the method call determines the `this` value.

---

# 12. `this` With Functions Inside Methods

Consider:

```javascript
const user = {
  name: "Sandip",

  greet() {
    function innerFunction() {
      console.log(this.name);
    }

    innerFunction();
  }
};

user.greet();
```

The inner regular function does not automatically inherit the outer method's `this`.

In strict mode:

```text
undefined
```

Therefore:

```javascript
this.name
```

does not refer to `user`.

---

# 13. Arrow Functions and `this`

Arrow functions behave differently.

Arrow functions do **not** create their own `this`.

Instead, they capture `this` from the surrounding lexical scope.

Example:

```javascript
const user = {
  name: "Sandip",

  greet() {
    const showName = () => {
      console.log(this.name);
    };

    showName();
  }
};

user.greet();
```

Output:

```text
Sandip
```

The arrow function uses the `this` from `greet()`.

---

# 14. Regular Function vs Arrow Function

### Regular function

```javascript
const user = {
  name: "Sandip",

  greet() {
    function showName() {
      console.log(this.name);
    }

    showName();
  }
};
```

The inner regular function has its own `this` behavior.

### Arrow function

```javascript
const user = {
  name: "Sandip",

  greet() {
    const showName = () => {
      console.log(this.name);
    };

    showName();
  }
};
```

The arrow function uses the surrounding `this`.

---

# 15. Arrow Function as an Object Method

Be careful with this:

```javascript
const user = {
  name: "Sandip",

  greet: () => {
    console.log(this.name);
  }
};

user.greet();
```

This does **not** make `this` refer to `user`.

Arrow functions do not get their `this` from the object method call.

For object methods, prefer:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(this.name);
  }
};
```

---

# 16. Why Arrow Functions Behave Differently

Regular functions:

```javascript
function greet() {
  console.log(this);
}
```

get `this` based on how they are called.

Arrow functions:

```javascript
const greet = () => {
  console.log(this);
};
```

capture `this` from their surrounding lexical scope.

They do not have their own `this`.

---

# 17. `this` in Constructor Functions

Before classes became common, constructor functions were widely used.

```javascript
function User(name, email) {
  this.name = name;
  this.email = email;
}

const user = new User("Sandip", "sandip@example.com");

console.log(user.name);
```

Output:

```text
Sandip
```

When using:

```javascript
new User(...)
```

JavaScript creates a new object and `this` refers to that new object inside the constructor.

---

# 18. `this` With `new`

Consider:

```javascript
function Product(name, price) {
  this.name = name;
  this.price = price;
}

const product = new Product("Laptop", 800);
```

Conceptually:

```text
new
 ↓
Create new object
 ↓
Set prototype
 ↓
Bind `this` to new object
 ↓
Execute constructor
 ↓
Return object
```

Therefore:

```javascript
this.name
```

becomes a property of the newly created object.

---

# 19. `this` in Classes

Classes also use `this`.

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello ${this.name}`);
  }
}

const user = new User("Sandip");

user.greet();
```

Output:

```text
Hello Sandip
```

Here:

```javascript
this
```

refers to the object created by:

```javascript
new User("Sandip")
```

---

# 20. `this` in Class Methods

```javascript
class Hotel {
  constructor(name) {
    this.name = name;
  }

  showName() {
    console.log(this.name);
  }
}

const hotel = new Hotel("Everest Hotel");

hotel.showName();
```

Output:

```text
Everest Hotel
```

The method is called through:

```javascript
hotel.showName();
```

so `this` refers to the `hotel` instance.

---

# 21. `this` With `call()`

JavaScript provides:

```javascript
call()
```

to explicitly specify the `this` value for a regular function.

Example:

```javascript
function greet() {
  console.log(`Hello ${this.name}`);
}

const user = {
  name: "Sandip"
};

greet.call(user);
```

Output:

```text
Hello Sandip
```

Here:

```javascript
this === user
```

---

# 22. `this` With `apply()`

`apply()` is similar to `call()`.

```javascript
function introduce(city, country) {
  console.log(`${this.name} lives in ${city}, ${country}`);
}

const user = {
  name: "Sandip"
};

introduce.apply(user, ["Birgunj", "Nepal"]);
```

Output:

```text
Sandip lives in Birgunj, Nepal
```

The difference is mainly how arguments are provided.

---

# 23. `call()` vs `apply()`

### `call()`

Arguments are provided individually:

```javascript
function greet(city, country) {
  console.log(this.name, city, country);
}

greet.call(user, "Birgunj", "Nepal");
```

### `apply()`

Arguments are provided as an array:

```javascript
greet.apply(user, ["Birgunj", "Nepal"]);
```

| Method    | Arguments            |
| --------- | -------------------- |
| `call()`  | Individual arguments |
| `apply()` | Array of arguments   |

---

# 24. `this` With `bind()`

`bind()` creates a new function with a permanently specified `this` value.

```javascript
function greet() {
  console.log(`Hello ${this.name}`);
}

const user = {
  name: "Sandip"
};

const boundGreet = greet.bind(user);

boundGreet();
```

Output:

```text
Hello Sandip
```

---

# 25. `call`, `apply`, and `bind`

```text
call()
   ↓
Calls function immediately

apply()
   ↓
Calls function immediately

bind()
   ↓
Creates a new function
```

Example:

```javascript
greet.call(user);
greet.apply(user, []);
const newGreet = greet.bind(user);
newGreet();
```

---

# 26. Practical Example: Hotel Order

```javascript
const order = {
  orderId: "ORD-101",
  tableNumber: 5,

  showOrder() {
    console.log(`Order: ${this.orderId}`);
    console.log(`Table: ${this.tableNumber}`);
  }
};

order.showOrder();
```

Output:

```text
Order: ORD-101
Table: 5
```

Here:

```javascript
this === order
```

---

# 27. Practical Example: User

```javascript
const user = {
  name: "Sandip",
  role: "Admin",

  showProfile() {
    return {
      name: this.name,
      role: this.role
    };
  }
};

console.log(user.showProfile());
```

Output:

```javascript
{
  name: "Sandip",
  role: "Admin"
}
```

---

# 28. Practical Example: Class

```javascript
class Order {
  constructor(orderId, total) {
    this.orderId = orderId;
    this.total = total;
  }

  getSummary() {
    return `${this.orderId}: Rs. ${this.total}`;
  }
}

const order = new Order("ORD-101", 1500);

console.log(order.getSummary());
```

Output:

```text
ORD-101: Rs. 1500
```

---

# 29. `this` in Event Handlers

In a traditional DOM event handler:

```javascript
button.addEventListener("click", function () {
  console.log(this);
});
```

`this` generally refers to the element that received the listener.

For example:

```javascript
button.addEventListener("click", function () {
  console.log(this.textContent);
});
```

This can print the button's text.

With an arrow function:

```javascript
button.addEventListener("click", () => {
  console.log(this);
});
```

the arrow function does not create its own `this`.

It uses the surrounding lexical `this`.

---

# 30. Arrow Functions in Callbacks

Arrow functions are useful when you want to preserve surrounding `this`.

```javascript
const user = {
  name: "Sandip",

  showName() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};

user.showName();
```

Output after one second:

```text
Sandip
```

The arrow function captures the `this` from `showName()`.

---

# 31. Regular Function in Callback

Compare:

```javascript
const user = {
  name: "Sandip",

  showName() {
    setTimeout(function () {
      console.log(this.name);
    }, 1000);
  }
};

user.showName();
```

The callback is a regular function.

Its `this` is not automatically the `user` object.

Using an arrow function is often simpler when you want the surrounding `this`:

```javascript
setTimeout(() => {
  console.log(this.name);
}, 1000);
```

---

# 32. Four Important `this` Rules

A useful way to remember regular-function `this`:

### 1. Method call

```javascript
object.method();
```

Usually:

```javascript
this === object
```

### 2. Plain function call

```javascript
functionName();
```

In strict mode:

```javascript
this === undefined
```

### 3. `new`

```javascript
new Constructor();
```

`this` refers to the newly created object.

### 4. `call`, `apply`, `bind`

These allow explicit control of `this`.

---

# 33. `this` Priority

When multiple mechanisms appear, a useful simplified order for regular functions is:

```text
new
 ↓
call/apply/bind
 ↓
object method call
 ↓
plain function call
```

For example:

```javascript
function User(name) {
  this.name = name;
}
```

When called with:

```javascript
new User("Sandip");
```

`this` refers to the new object.

---

# 34. Arrow Functions Have Different Rules

Arrow functions:

* Do not have their own `this`
* Do not get `this` from an object method call
* Capture `this` from the surrounding scope
* Cannot change `this` using `call()`
* Cannot change `this` using `apply()`
* Cannot change `this` using `bind()`

For example:

```javascript
const greet = () => {
  console.log(this);
};

greet.call(user);
```

`call()` does not replace the arrow function's lexical `this`.

---

# 35. Common Mistake

Avoid:

```javascript
const user = {
  name: "Sandip",

  greet: () => {
    console.log(this.name);
  }
};
```

if your intention is for `this` to refer to `user`.

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

# 36. `this` Quick Comparison

| Situation                     | Regular Function `this` |
| ----------------------------- | ----------------------- |
| `object.method()`             | `object`                |
| Plain function in strict mode | `undefined`             |
| `new Function()`              | New object              |
| `call(object)`                | Explicit object         |
| `apply(object)`               | Explicit object         |
| `bind(object)`                | Bound object            |
| Arrow function                | Lexical `this`          |

---

# 37. Important Points

* `this` is a special JavaScript keyword.
* Its value depends on execution context.
* Regular function `this` is generally determined by how the function is called.
* In an object method call, `this` normally refers to the object before the dot.
* In strict-mode plain function calls, `this` is `undefined`.
* `new` makes `this` refer to the new instance.
* `call()` explicitly sets `this` for regular functions.
* `apply()` explicitly sets `this` for regular functions.
* `bind()` creates a function with a bound `this`.
* Arrow functions do not have their own `this`.
* Arrow functions capture `this` from the surrounding scope.
* Arrow functions are useful inside callbacks when you want to preserve surrounding `this`.
* Avoid arrow functions as object methods when you expect `this` to refer to the object.
* Classes commonly use `this` to access instance properties and methods.

---
