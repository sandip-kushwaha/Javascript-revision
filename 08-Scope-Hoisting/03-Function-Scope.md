# JavaScript Function Scope

**Function scope** means that variables declared inside a function are normally accessible only within that function.

A function creates its own scope.

```javascript
function login() {
  const username = "Sandip";

  console.log(username);
}

login();
```

Here, `username` belongs to the scope created by `login()`.

---

# 1. What Is Function Scope?

Consider:

```javascript
function calculateTotal() {
  const price = 500;
  const quantity = 2;

  console.log(price * quantity);
}

calculateTotal();
```

The variables:

```text
price
quantity
```

are available inside `calculateTotal()`.

They are not directly available outside the function.

---

# 2. Accessing a Function Variable Outside

```javascript
function createUser() {
  const username = "Sandip";
}

console.log(username);
```

This causes:

```text
ReferenceError
```

because `username` belongs to the function scope.

---

# 3. `var` Is Function-Scoped

The `var` keyword is function-scoped.

```javascript
function example() {
  var message = "Hello";

  console.log(message);
}

example();
```

This works.

Outside:

```javascript
console.log(message);
```

does not work because `message` exists only inside `example()`.

---

# 4. `let` and `const` Inside Functions

`let` and `const` are block-scoped, but when declared directly inside a function, they are also local to that function.

```javascript
function processOrder() {
  let status = "pending";
  const orderId = "ORD-1001";

  console.log(status);
  console.log(orderId);
}
```

Both variables are unavailable outside `processOrder()`.

---

# 5. Function Scope vs Block Scope

This distinction is important.

```javascript
function example() {
  var a = 10;
  let b = 20;
  const c = 30;

  if (true) {
    var x = 40;
    let y = 50;
    const z = 60;

    console.log(a);
    console.log(b);
    console.log(c);
    console.log(x);
    console.log(y);
    console.log(z);
  }

  console.log(x);
}
```

The important behavior is:

```text
a → function scope
b → function scope + block-scoped declaration
c → function scope + block-scoped declaration
x → function scope
y → block scope
z → block scope
```

So after the `if` block:

```javascript
console.log(x);
```

works.

But:

```javascript
console.log(y);
console.log(z);
```

does not.

---

# 6. Function Creates a Boundary

Think of a function as a boundary:

```text
Global Scope
│
├── globalVariable
│
└── function
    │
    ├── localVariable
    └── anotherVariable
```

Code outside the function cannot directly access its local variables.

---

# 7. Outer Variables Are Accessible

Function scope does not mean a function can only use its own variables.

A function can access variables from outer scopes.

```javascript
const appName = "Hotel App";

function startApp() {
  console.log(appName);
}

startApp();
```

Output:

```text
Hotel App
```

The function searches its own scope first and then moves outward.

---

# 8. Scope Chain

Example:

```javascript
const company = "Tech Corp";

function department() {
  const team = "Development";

  function employee() {
    const name = "Sandip";

    console.log(name);
    console.log(team);
    console.log(company);
  }

  employee();
}

department();
```

The scope chain is:

```text
employee scope
      ↓
department scope
      ↓
global scope
```

The inner function can access variables from the outer scopes.

---

# 9. Inner Functions

Functions can be declared inside other functions.

```javascript
function outer() {
  const message = "Hello";

  function inner() {
    console.log(message);
  }

  inner();
}

outer();
```

`inner()` can access `message`.

Why?

Because `inner()` was created inside the scope of `outer()`.

---

# 10. Outer Functions Cannot Access Inner Variables

Consider:

```javascript
function outer() {
  function inner() {
    const value = 100;
  }

  console.log(value);
}
```

This does not work.

`value` belongs to `inner()`.

The scope relationship is:

```text
outer()
│
└── inner()
    └── value
```

`inner()` can look outward toward `outer()`.

`outer()` cannot look inward into `inner()`.

---

# 11. Function Parameters Have Function Scope

Function parameters are also local to the function.

```javascript
function greet(name) {
  console.log(name);
}

greet("Sandip");
```

`name` is available inside the function.

Outside:

```javascript
console.log(name);
```

it is not available.

---

# 12. Parameters and Local Variables

Parameters and local variables can exist together.

```javascript
function createOrder(tableNumber) {
  const status = "pending";

  console.log(tableNumber);
  console.log(status);
}

createOrder(5);
```

Here:

```text
tableNumber → parameter
status      → local variable
```

Both belong to the function's local environment.

---

# 13. Function Parameters Can Shadow Outer Variables

```javascript
const name = "Global";

function greet(name) {
  console.log(name);
}

greet("Sandip");

console.log(name);
```

Output:

```text
Sandip
Global
```

The parameter `name` shadows the outer `name` inside the function.

---

# 14. Local Variables Can Shadow Outer Variables

```javascript
const status = "available";

function checkTable() {
  const status = "occupied";

  console.log(status);
}

checkTable();

console.log(status);
```

Output:

```text
occupied
available
```

The function has its own `status`.

---

# 15. `var` Inside a Function

Consider:

```javascript
function test() {
  var value = 10;

  if (true) {
    var value = 20;
  }

  console.log(value);
}

test();
```

Output:

```text
20
```

Both `var value` declarations refer to the same function-scoped variable.

The `if` block does not create a separate scope for `var`.

---

# 16. `let` Inside a Function

Now compare:

```javascript
function test() {
  let value = 10;

  if (true) {
    let value = 20;

    console.log(value);
  }

  console.log(value);
}

test();
```

Output:

```text
20
10
```

The `if` block has its own `let` binding.

---

# 17. `const` Inside a Function

The same principle applies to `const`.

```javascript
function test() {
  const value = 10;

  if (true) {
    const value = 20;

    console.log(value);
  }

  console.log(value);
}

test();
```

Output:

```text
20
10
```

There are two separate bindings.

---

# 18. Function Scope With Loops

Consider:

```javascript
function showNumbers() {
  for (let i = 0; i < 3; i++) {
    console.log(i);
  }

  console.log(i);
}
```

The last line causes an error because `i` belongs to the `for` block.

With `var`:

```javascript
function showNumbers() {
  for (var i = 0; i < 3; i++) {
    console.log(i);
  }

  console.log(i);
}
```

The final `console.log(i)` works because `var` is function-scoped.

---

# 19. Function Scope and `var`

A useful rule:

```text
var
↓
function scope
```

Example:

```javascript
function example() {
  if (true) {
    var username = "Sandip";
  }

  console.log(username);
}

example();
```

The variable is available throughout the function.

---

# 20. Function Scope and `let` / `const`

For `let` and `const`, remember:

```text
let / const
↓
block scope
```

Example:

```javascript
function example() {
  if (true) {
    const username = "Sandip";

    console.log(username);
  }

  console.log(username);
}
```

The second `console.log()` fails because `username` belongs to the `if` block.

---

# 21. Function Scope and Closures

Function scope is closely connected to **closures**.

Example:

```javascript
function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter = createCounter();

console.log(counter());
console.log(counter());
```

Output:

```text
1
2
```

The returned function continues to access `count` even after `createCounter()` has finished.

This behavior is called a **closure**.

Closures are covered later in:

```text
16-Advanced-JavaScript/01-Closures.md
```

---

# 22. Function Scope and Callbacks

A callback function also has its own scope.

```javascript
const users = ["Sandip", "Ram"];

users.forEach(function (user) {
  const message = `Hello ${user}`;

  console.log(message);
});
```

`user` and `message` belong to the callback's local scope.

They are not directly available outside the callback.

---

# 23. Arrow Functions Also Have Scope

Arrow functions create their own lexical scope for local variables.

```javascript
const calculate = (price, quantity) => {
  const total = price * quantity;

  return total;
};

console.log(calculate(500, 2));
```

`total` is local to the arrow function.

---

# 24. Function Expression Scope

A function expression can also have local variables.

```javascript
const calculateTotal = function (price, quantity) {
  const total = price * quantity;

  return total;
};
```

`price`, `quantity`, and `total` are associated with the function's local execution context.

---

# 25. Nested Function Example

```javascript
function login(username) {
  const isValid = true;

  function verify() {
    return isValid && username.length > 0;
  }

  return verify();
}

console.log(login("Sandip"));
```

The nested `verify()` function can access:

```text
username → parameter of login()
isValid  → variable of login()
```

because both belong to an outer scope.

---

# 26. Practical Hotel Example

Suppose you process an order:

```javascript
function createOrder(tableNumber, items) {
  const orderStatus = "pending";

  function calculateTotal() {
    return items.reduce((total, item) => {
      return total + item.price;
    }, 0);
  }

  return {
    tableNumber,
    orderStatus,
    total: calculateTotal()
  };
}
```

Here:

```text
createOrder()
│
├── tableNumber
├── items
├── orderStatus
│
└── calculateTotal()
```

`calculateTotal()` can access `items` because it is nested inside `createOrder()`.

---

# 27. Avoid Unnecessary Global Variables

Instead of:

```javascript
let currentUser;
let currentOrder;
let total;
let status;
```

at global scope, keep variables close to where they are needed.

For example:

```javascript
function processOrder(order) {
  const total = calculateTotal(order);

  return total;
}
```

This reduces accidental changes from unrelated code.

---

# 28. Function Scope in Modules

Modules already provide an additional scope boundary.

Example:

```javascript
// userService.js

const secret = "internal";

export function getUser() {
  return "Sandip";
}
```

`secret` is not automatically available to other modules.

Only exported values are available for importing.

---

# 29. Common Mistakes

### Mistake 1: Expecting function variables to be global

```javascript
function start() {
  const message = "Hello";
}

console.log(message);
```

`message` is local to `start()`.

---

### Mistake 2: Confusing `var` with block scope

```javascript
function test() {
  if (true) {
    var value = 100;
  }

  console.log(value);
}
```

This works because `var` is function-scoped.

---

### Mistake 3: Forgetting parameter scope

```javascript
function greet(name) {
  console.log(name);
}

console.log(name);
```

`name` is only available inside the function.

---

# 30. Quick Reference

### Function-local variable

```javascript
function example() {
  const value = 100;
}
```

`value` is local to the function.

### Function parameter

```javascript
function greet(name) {
  console.log(name);
}
```

`name` is local to the function.

### Outer variable

```javascript
const app = "Hotel";

function start() {
  console.log(app);
}
```

The function can access `app`.

### `var`

```javascript
function test() {
  var value = 10;
}
```

`var` is function-scoped.

### `let` / `const`

```javascript
function test() {
  if (true) {
    let value = 10;
    const name = "Sandip";
  }
}
```

They are block-scoped.

---

# 31. Scope Structure

A typical nested function structure can be visualized as:

```text
Global Scope
│
└── outer()
    │
    ├── outerVariable
    │
    └── inner()
        │
        └── innerVariable
```

Lookup from `inner()`:

```text
inner scope
    ↓
outer scope
    ↓
global scope
```

---

# 32. Key Takeaways

* Every function creates its own function scope.
* Variables declared inside a function are normally local to that function.
* Function parameters are also local to the function.
* A function can access variables from outer scopes.
* An outer function cannot directly access variables inside an inner function.
* `var` is function-scoped.
* `let` and `const` are block-scoped.
* Nested functions can access variables from their outer functions.
* Function scope is an important foundation for understanding closures.
* Keeping variables inside the smallest necessary scope makes code easier to maintain.

---
