# JavaScript `call()`, `apply()`, and `bind()`

JavaScript provides three important methods for controlling the `this` value of regular functions:

```javascript
call()
apply()
bind()
```

They are especially useful when working with:

* Objects
* Methods
* Constructors
* Function borrowing
* Callbacks
* Object-oriented JavaScript

---

# 1. Why `call()`, `apply()`, and `bind()`?

Consider:

```javascript
const user = {
  name: "Sandip"
};

function greet() {
  console.log(`Hello ${this.name}`);
}

greet();
```

The function does not automatically know that `this` should refer to `user`.

We can explicitly provide the `this` value:

```javascript
greet.call(user);
```

Output:

```text
Hello Sandip
```

---

# 2. `call()`

The `call()` method:

* Calls a function immediately
* Allows you to specify `this`
* Accepts function arguments individually

Basic syntax:

```javascript
functionName.call(thisValue, arg1, arg2, ...);
```

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

---

# 3. `call()` With Arguments

```javascript
function introduce(city, country) {
  console.log(
    `${this.name} lives in ${city}, ${country}`
  );
}

const user = {
  name: "Sandip"
};

introduce.call(user, "Birgunj", "Nepal");
```

Output:

```text
Sandip lives in Birgunj, Nepal
```

Arguments are passed normally:

```javascript
call(thisValue, argument1, argument2)
```

---

# 4. `call()` Changes `this`

```javascript
function showRole() {
  console.log(this.role);
}

const admin = {
  role: "Admin"
};

const waiter = {
  role: "Waiter"
};

showRole.call(admin);
showRole.call(waiter);
```

Output:

```text
Admin
Waiter
```

The same function can work with different objects.

---

# 5. Function Borrowing With `call()`

Function borrowing means using a method from one object with another object.

```javascript
const user1 = {
  name: "Sandip",

  greet() {
    console.log(`Hello ${this.name}`);
  }
};

const user2 = {
  name: "Ram"
};

user1.greet.call(user2);
```

Output:

```text
Hello Ram
```

The method comes from `user1`, but:

```javascript
this === user2
```

during the call.

---

# 6. `apply()`

`apply()` is similar to `call()`.

The main difference is how arguments are supplied.

Syntax:

```javascript
functionName.apply(thisValue, [arg1, arg2, ...]);
```

Example:

```javascript
function introduce(city, country) {
  console.log(
    `${this.name} lives in ${city}, ${country}`
  );
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

---

# 7. `call()` vs `apply()`

The main difference:

### `call()`

Arguments are passed individually.

```javascript
function greet(city, country) {
  console.log(this.name, city, country);
}

greet.call(user, "Birgunj", "Nepal");
```

### `apply()`

Arguments are passed as an array-like value.

```javascript
greet.apply(user, ["Birgunj", "Nepal"]);
```

Comparison:

| Method    | `this`         | Arguments  |
| --------- | -------------- | ---------- |
| `call()`  | First argument | Individual |
| `apply()` | First argument | Array      |
| `bind()`  | First argument | Individual |

---

# 8. `apply()` With an Existing Array

`apply()` can be useful when arguments are already stored in an array.

```javascript
function calculateTotal(a, b, c) {
  return a + b + c;
}

const numbers = [10, 20, 30];

const result = calculateTotal.apply(null, numbers);

console.log(result);
```

Output:

```text
60
```

Modern JavaScript often uses spread syntax instead:

```javascript
const result = calculateTotal(...numbers);
```

So `apply()` is less necessary for this particular use case today.

---

# 9. `bind()`

`bind()` works differently.

It does **not** immediately call the function.

Instead, it creates a new function with a bound `this` value.

Example:

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

# 10. `bind()` Does Not Execute Immediately

Consider:

```javascript
function greet() {
  console.log("Hello");
}

const newGreet = greet.bind(null);

console.log("Before");

newGreet();

console.log("After");
```

Output:

```text
Before
Hello
After
```

The function runs only when:

```javascript
newGreet();
```

is called.

---

# 11. `bind()` With Arguments

`bind()` can also pre-fill arguments.

```javascript
function introduce(city, country) {
  console.log(`${this.name} lives in ${city}, ${country}`);
}

const user = {
  name: "Sandip"
};

const boundIntroduce = introduce.bind(
  user,
  "Birgunj",
  "Nepal"
);

boundIntroduce();
```

Output:

```text
Sandip lives in Birgunj, Nepal
```

This technique is called **partial application** when some arguments are fixed in advance.

---

# 12. Partial Application

Consider:

```javascript
function multiply(a, b) {
  return a * b;
}

const double = multiply.bind(null, 2);

console.log(double(10));
```

Output:

```text
20
```

The first argument has already been provided:

```javascript
2
```

Then:

```javascript
double(10);
```

supplies the remaining argument.

---

# 13. `call()` vs `bind()`

### `call()`

```javascript
greet.call(user);
```

The function runs immediately.

### `bind()`

```javascript
const newGreet = greet.bind(user);
```

A new function is created.

Then:

```javascript
newGreet();
```

runs it.

---

# 14. `apply()` vs `bind()`

### `apply()`

```javascript
greet.apply(user, ["Birgunj"]);
```

Immediately calls the function.

### `bind()`

```javascript
const newGreet = greet.bind(user, "Birgunj");

newGreet();
```

Creates a new function first.

---

# 15. Simple Comparison

```text
call()
  ↓
Set this
  ↓
Execute now

apply()
  ↓
Set this
  ↓
Execute now

bind()
  ↓
Set this
  ↓
Create new function
  ↓
Execute later
```

---

# 16. Practical Object Example

```javascript
const admin = {
  name: "Sandip",
  role: "Admin"
};

function showUser() {
  console.log(`${this.name} - ${this.role}`);
}

showUser.call(admin);
```

Output:

```text
Sandip - Admin
```

---

# 17. Using the Same Function With Multiple Objects

```javascript
const admin = {
  name: "Sandip",
  role: "Admin"
};

const waiter = {
  name: "Ram",
  role: "Waiter"
};

function showUser() {
  console.log(`${this.name} - ${this.role}`);
}

showUser.call(admin);
showUser.call(waiter);
```

Output:

```text
Sandip - Admin
Ram - Waiter
```

One function is reused for different objects.

---

# 18. Practical Hotel Example

Suppose different staff members have the same structure:

```javascript
const admin = {
  name: "Sandip",
  role: "Admin"
};

const waiter = {
  name: "Ram",
  role: "Waiter"
};

function showStaff() {
  return `${this.name} is a ${this.role}`;
}

console.log(showStaff.call(admin));
console.log(showStaff.call(waiter));
```

Output:

```text
Sandip is a Admin
Ram is a Waiter
```

---

# 19. Using `apply()` With Hotel Data

```javascript
function createOrder(tableNumber, total) {
  return {
    staff: this.name,
    tableNumber,
    total
  };
}

const waiter = {
  name: "Ram"
};

const order = createOrder.apply(
  waiter,
  [5, 1500]
);

console.log(order);
```

Output:

```javascript
{
  staff: "Ram",
  tableNumber: 5,
  total: 1500
}
```

---

# 20. Using `bind()` for a User

```javascript
const user = {
  name: "Sandip",
  role: "Admin"
};

function showProfile() {
  console.log(this.name);
  console.log(this.role);
}

const showUserProfile = showProfile.bind(user);

showUserProfile();
```

Output:

```text
Sandip
Admin
```

The new function remembers the bound `this`.

---

# 21. `bind()` With Event Handlers

`bind()` is useful when passing a method as a callback.

Example:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(`Hello ${this.name}`);
  }
};

const button = document.querySelector("#loginButton");

button.addEventListener(
  "click",
  user.greet.bind(user)
);
```

The bound function keeps:

```javascript
this === user
```

when the event occurs.

Without binding, a method passed as a callback may receive a different `this`.

---

# 22. `bind()` With `setTimeout()`

Consider:

```javascript
const user = {
  name: "Sandip",

  greet() {
    console.log(`Hello ${this.name}`);
  }
};

setTimeout(user.greet.bind(user), 1000);
```

After one second:

```text
Hello Sandip
```

`bind()` ensures that `this` remains the `user` object.

---

# 23. `bind()` vs Arrow Function

Both can help preserve context, but they work differently.

### `bind()`

```javascript
const greet = user.greet.bind(user);
```

Creates a new function with a bound `this`.

### Arrow function

```javascript
setTimeout(() => {
  user.greet();
}, 1000);
```

The arrow function captures `this` from its surrounding scope, while the method call explicitly uses `user`.

Another common pattern is:

```javascript
class User {
  constructor(name) {
    this.name = name;

    this.greet = this.greet.bind(this);
  }

  greet() {
    console.log(this.name);
  }
}
```

---

# 24. `call()` With No Extra Arguments

You can use:

```javascript
function showName() {
  console.log(this.name);
}

const user = {
  name: "Sandip"
};

showName.call(user);
```

No additional function arguments are required.

---

# 25. `apply()` With No Arguments

You can also use:

```javascript
showName.apply(user);
```

The second argument is optional.

---

# 26. `bind()` Without Arguments

You can create a bound function:

```javascript
const boundShowName = showName.bind(user);

boundShowName();
```

The returned function can be stored and called later.

---

# 27. Important Difference With Arrow Functions

`call()`, `apply()`, and `bind()` cannot replace the lexical `this` of an arrow function.

Example:

```javascript
const greet = () => {
  console.log(this);
};

greet.call(user);
```

The `call()` method does not make the arrow function's `this` become `user`.

Arrow functions capture `this` from their surrounding scope.

---

# 28. `call()` With Methods

You can temporarily borrow a method.

```javascript
const user1 = {
  name: "Sandip",

  greet() {
    console.log(`Hello ${this.name}`);
  }
};

const user2 = {
  name: "Ram"
};

user1.greet.call(user2);
```

Output:

```text
Hello Ram
```

This is called **method borrowing**.

---

# 29. A Common Array Example

Before modern spread syntax became common, `apply()` was sometimes used with array methods.

```javascript
const numbers = [10, 20, 30, 40];

const maximum = Math.max.apply(null, numbers);

console.log(maximum);
```

Output:

```text
40
```

Modern JavaScript is simpler:

```javascript
const maximum = Math.max(...numbers);
```

So prefer spread syntax when it clearly expresses the intent.

---

# 30. `call()` for Method Borrowing

Another example:

```javascript
const person1 = {
  name: "Sandip",

  introduce() {
    console.log(`My name is ${this.name}`);
  }
};

const person2 = {
  name: "Ram"
};

person1.introduce.call(person2);
```

Output:

```text
My name is Ram
```

The function uses `person2` as its `this`.

---

# 31. `bind()` and Reusable Functions

Suppose you frequently need the same object:

```javascript
const user = {
  name: "Sandip",
  role: "Admin"
};

function showRole() {
  console.log(`${this.name}: ${this.role}`);
}

const showUserRole = showRole.bind(user);

showUserRole();
showUserRole();
```

The bound function can be reused.

---

# 32. `bind()` Does Not Change the Original Function

```javascript
function greet() {
  console.log(this.name);
}

const user = {
  name: "Sandip"
};

const boundGreet = greet.bind(user);
```

The original:

```javascript
greet
```

is unchanged.

The bound function is:

```javascript
boundGreet
```

---

# 33. Bound Functions Can Be Called Later

This is useful when working with asynchronous code:

```javascript
const user = {
  name: "Sandip",

  showName() {
    console.log(this.name);
  }
};

const showName = user.showName.bind(user);

setTimeout(showName, 1000);
```

The callback runs later but retains the bound `this`.

---

# 34. `call()`, `apply()`, and `bind()` Syntax

### `call()`

```javascript
function.call(thisValue, arg1, arg2);
```

### `apply()`

```javascript
function.apply(thisValue, [arg1, arg2]);
```

### `bind()`

```javascript
const newFunction = function.bind(
  thisValue,
  arg1,
  arg2
);
```

---

# 35. Comparison Table

| Feature                    | `call()`   | `apply()`        | `bind()`    |
| -------------------------- | ---------- | ---------------- | ----------- |
| Sets `this`                | Yes        | Yes              | Yes         |
| Executes immediately       | Yes        | Yes              | No          |
| Returns new function       | No         | No               | Yes         |
| Arguments                  | Individual | Array/array-like | Individual  |
| Useful for callbacks       | Sometimes  | Sometimes        | Very useful |
| Supports partial arguments | No         | No               | Yes         |

---

# 36. When to Use Each

### Use `call()`

When you want to:

* Execute a function immediately
* Specify `this`
* Pass arguments individually
* Borrow a method

Example:

```javascript
showUser.call(user);
```

### Use `apply()`

When you want to:

* Execute a function immediately
* Specify `this`
* Pass arguments from an array

Example:

```javascript
showUser.apply(user, args);
```

### Use `bind()`

When you want to:

* Create a reusable function
* Preserve `this`
* Pass the function as a callback
* Pre-fill arguments

Example:

```javascript
const boundFunction = showUser.bind(user);
```

---

# 37. Modern JavaScript Alternatives

Some older uses of `apply()` can now be replaced with spread syntax.

Instead of:

```javascript
Math.max.apply(null, numbers);
```

use:

```javascript
Math.max(...numbers);
```

Instead of:

```javascript
function.call(null, ...args);
```

modern syntax may make the intent clearer depending on the situation.

However, `call()`, `apply()`, and `bind()` remain important for understanding JavaScript's function behavior and `this`.

---

# 38. Key Takeaways

* `call()`, `apply()`, and `bind()` control the `this` value of regular functions.
* `call()` executes the function immediately.
* `apply()` executes the function immediately.
* `bind()` creates a new function without executing it immediately.
* `call()` receives arguments individually.
* `apply()` receives arguments as an array/array-like value.
* `bind()` can pre-fill arguments.
* `call()` and `apply()` are useful for method borrowing.
* `bind()` is useful when passing methods as callbacks.
* Arrow functions have lexical `this`.
* `call()`, `apply()`, and `bind()` cannot replace the lexical `this` of an arrow function.
* Modern spread syntax can replace some older `apply()` use cases.

---
