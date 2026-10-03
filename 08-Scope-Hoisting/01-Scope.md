# JavaScript Scope

**Scope** determines where a variable can be accessed in JavaScript.

In simple words:

> **Scope = the area of the program where a variable is available.**

Example:

```javascript
const name = "Sandip";

console.log(name);
```

Here, `name` can be accessed because it is available in the current scope.

---

# 1. Why Scope Matters

Consider:

```javascript
const username = "Sandip";

function showUser() {
  console.log(username);
}

showUser();
```

Output:

```text
Sandip
```

The function can access `username` because the variable exists in an outer scope.

But a variable created inside a function normally cannot be accessed outside it:

```javascript
function showUser() {
  const username = "Sandip";
}

console.log(username);
```

This produces an error because `username` only exists inside `showUser()`.

---

# 2. Types of Scope

JavaScript commonly has these scopes:

1. Global Scope
2. Function Scope
3. Block Scope
4. Module Scope

---

# 3. Global Scope

A variable declared outside functions and blocks can be available throughout the script.

```javascript
const appName = "Hotel Management System";

function showApp() {
  console.log(appName);
}

showApp();
```

Output:

```text
Hotel Management System
```

`appName` is in the outer/global scope.

---

# 4. Function Scope

Variables declared with `var`, `let`, or `const` inside a function are local to that function.

```javascript
function createUser() {
  const username = "Sandip";

  console.log(username);
}

createUser();
```

This works:

```javascript
console.log(username);
```

only **inside** the function.

Outside:

```javascript
console.log(username);
```

causes:

```text
ReferenceError
```

---

# 5. Block Scope

A block is code inside:

```text
{}
```

Examples include:

```javascript
if (true) {
  // block
}
```

and:

```javascript
for (let i = 0; i < 5; i++) {
  // block
}
```

`let` and `const` are block-scoped.

Example:

```javascript
if (true) {
  const message = "Hello";

  console.log(message);
}
```

This works.

Outside:

```javascript
console.log(message);
```

does not work.

---

# 6. `var` and Block Scope

`var` is **not block-scoped**.

Example:

```javascript
if (true) {
  var message = "Hello";
}

console.log(message);
```

Output:

```text
Hello
```

The `var` variable is not limited to the `if` block.

This is one reason modern JavaScript generally prefers:

```javascript
let
```

and:

```javascript
const
```

over `var`.

---

# 7. Function Scope vs Block Scope

Consider:

```javascript
function example() {
  if (true) {
    var a = 10;
    let b = 20;
    const c = 30;
  }

  console.log(a);
  console.log(b);
  console.log(c);
}
```

Result:

```text
10
ReferenceError
ReferenceError
```

Why?

```text
var   → function-scoped
let   → block-scoped
const → block-scoped
```

---

# 8. Scope Chain

JavaScript looks for variables through a **scope chain**.

Example:

```javascript
const company = "Tech Corp";

function outer() {
  const department = "Development";

  function inner() {
    const employee = "Sandip";

    console.log(employee);
    console.log(department);
    console.log(company);
  }

  inner();
}

outer();
```

The `inner()` function can access:

```text
employee   → inner scope
department → outer scope
company    → global/outer scope
```

JavaScript searches from the nearest scope outward.

---

# 9. How Scope Lookup Works

Suppose:

```javascript
const a = "global";

function outer() {
  const b = "outer";

  function inner() {
    const c = "inner";

    console.log(c);
    console.log(b);
    console.log(a);
  }

  inner();
}
```

When JavaScript evaluates:

```javascript
console.log(b);
```

it checks:

```text
1. inner scope
2. outer scope
3. global scope
```

It stops when it finds `b`.

---

# 10. Scope Lookup Goes Outward

Inner scopes can access outer variables.

```javascript
const app = "Hotel";

function start() {
  const server = "Express";

  function run() {
    console.log(app);
    console.log(server);
  }

  run();
}

start();
```

The inner function can access both:

```text
run scope
   ↓
start scope
   ↓
global scope
```

---

# 11. Outer Scope Cannot Access Inner Scope

The reverse is not true.

```javascript
function start() {
  const server = "Express";
}

console.log(server);
```

This fails because the outer scope cannot access variables created inside the function.

Think of scope like this:

```text
Outer Scope
┌───────────────────────────┐
│                           │
│   Inner Scope             │
│   ┌───────────────────┐   │
│   │ private variables │   │
│   └───────────────────┘   │
│                           │
└───────────────────────────┘
```

The inner scope can look outward, but the outer scope cannot look inward.

---

# 12. Same Variable Name in Different Scopes

Different scopes can contain variables with the same name.

```javascript
const name = "Global";

function showName() {
  const name = "Local";

  console.log(name);
}

showName();

console.log(name);
```

Output:

```text
Local
Global
```

The inner variable shadows the outer variable.

---

# 13. Variable Shadowing

**Shadowing** happens when an inner scope declares a variable with the same name as an outer variable.

```javascript
const role = "admin";

function checkRole() {
  const role = "waiter";

  console.log(role);
}

checkRole();
```

Output:

```text
waiter
```

The inner `role` shadows the outer `role`.

---

# 14. Block Shadowing

Shadowing can also happen with blocks.

```javascript
let status = "available";

if (true) {
  let status = "occupied";

  console.log(status);
}

console.log(status);
```

Output:

```text
occupied
available
```

There are two different `status` variables.

---

# 15. Lexical Scope

JavaScript uses **lexical scope**.

This means the scope of a variable is determined by where the code is written.

Example:

```javascript
const message = "Hello";

function showMessage() {
  console.log(message);
}
```

`showMessage()` can access `message` because of where the function is defined.

It does not depend on where the function is called.

---

# 16. Lexical Scope Example

```javascript
const username = "Sandip";

function outer() {
  const username = "Developer";

  function inner() {
    console.log(username);
  }

  return inner;
}

const result = outer();

result();
```

Output:

```text
Developer
```

`inner()` was defined inside `outer()`, so it uses the lexical environment where it was created.

This concept becomes especially important when learning **closures**.

---

# 17. Scope in `for` Loops

`let` creates a block-scoped variable.

```javascript
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

After the loop:

```javascript
console.log(i);
```

`i` is not available.

This helps prevent accidental access to loop variables outside the loop.

---

# 18. `var` in Loops

With `var`:

```javascript
for (var i = 0; i < 3; i++) {
  console.log(i);
}

console.log(i);
```

Output:

```text
0
1
2
3
```

Because `var` is function-scoped rather than block-scoped.

---

# 19. Nested Blocks

Blocks can be nested.

```javascript
{
  const a = 10;

  {
    const b = 20;

    console.log(a);
    console.log(b);
  }
}
```

The inner block can access `a`.

But the outer block cannot access `b`.

```text
Outer Block
│
├── a
│
└── Inner Block
    └── b
```

---

# 20. Global Scope Problems

Putting many variables in global scope can cause conflicts.

For example:

```javascript
const user = "Sandip";
const user = "Admin";
```

This causes an error because the same `const` name cannot be redeclared in the same scope.

Large applications should avoid unnecessary global variables.

Modules help solve this problem.

---

# 21. Module Scope

ES modules have their own scope.

Example:

### `config.js`

```javascript
const API_URL = "/api/v1";

export {
  API_URL
};
```

`API_URL` is not automatically a global variable.

Another module must import it:

```javascript
import { API_URL } from "./config.js";
```

This keeps module code isolated.

---

# 22. Scope and Functions

Every function creates its own function scope.

```javascript
function login() {
  const username = "Sandip";

  function validate() {
    console.log(username);
  }

  validate();
}
```

`validate()` can access `username` because it is inside the scope created by `login()`.

---

# 23. Scope and `const`

`const` is block-scoped.

```javascript
if (true) {
  const token = "abc123";

  console.log(token);
}
```

Outside the block:

```javascript
console.log(token);
```

causes a `ReferenceError`.

---

# 24. Scope and `let`

`let` is also block-scoped.

```javascript
let count = 0;

if (true) {
  let count = 10;

  console.log(count);
}

console.log(count);
```

Output:

```text
10
0
```

---

# 25. Scope and `var`

`var` is function-scoped.

```javascript
function example() {
  if (true) {
    var value = 100;
  }

  console.log(value);
}

example();
```

Output:

```text
100
```

The `if` block does not create a separate `var` scope.

---

# 26. Scope Comparison

| Declaration |     Function Scoped | Block Scoped | Global/Module Scope |
| ----------- | ------------------: | -----------: | ------------------: |
| `var`       |                 Yes |           No |                 Yes |
| `let`       | Yes within function |          Yes |                 Yes |
| `const`     | Yes within function |          Yes |                 Yes |

The important difference is:

```text
var   → function scope
let   → block scope
const → block scope
```

---

# 27. Practical Example

Imagine a hotel application:

```javascript
const hotelName = "Grand Hotel";

function processOrder() {
  const orderId = "ORD-1001";

  if (orderId) {
    const status = "pending";

    console.log(hotelName);
    console.log(orderId);
    console.log(status);
  }

  console.log(hotelName);
  console.log(orderId);
}
```

Inside the `if` block:

```text
hotelName → available
orderId   → available
status    → available
```

After the `if` block:

```text
hotelName → available
orderId   → available
status    → unavailable
```

---

# 28. Scope Hierarchy

A simple way to visualize nested scope:

```text
Global Scope
│
├── hotelName
│
└── Function Scope
    │
    ├── orderId
    │
    └── Block Scope
        │
        └── status
```

Variable lookup moves outward:

```text
Block
  ↓
Function
  ↓
Global
```

---

# 29. Scope vs Lifetime

Scope and lifetime are related but different.

### Scope

Determines:

> Where can I access this variable?

### Lifetime

Determines:

> How long does the variable exist?

For example:

```javascript
function createOrder() {
  const orderId = "ORD-1001";

  console.log(orderId);
}
```

`orderId` is accessible only within its scope.

Its lifetime is associated with the execution of the function and the references that may keep related data alive.

---

# 30. Common Mistakes

### Mistake 1: Expecting block scope from `var`

```javascript
if (true) {
  var message = "Hello";
}

console.log(message);
```

`var` is not block-scoped.

---

### Mistake 2: Accessing local variables globally

```javascript
function test() {
  const value = 10;
}

console.log(value);
```

`value` only exists inside `test()`.

---

### Mistake 3: Accidentally shadowing variables

```javascript
const role = "admin";

function check() {
  const role = "user";

  console.log(role);
}
```

The inner `role` hides the outer one inside that scope.

---

# 31. Best Practices

Prefer:

```javascript
const
```

when a variable doesn't need reassignment.

Use:

```javascript
let
```

when reassignment is necessary.

Avoid unnecessary:

```javascript
var
```

Keep variables close to where they are used.

Use modules to organize larger applications.

Avoid unnecessary global variables.

Choose clear variable names to reduce confusion when scopes are nested.

---

# 32. Quick Reference

```text
Global Scope
    ↓
Function Scope
    ↓
Block Scope
```

Important rules:

```text
var   → function scoped
let   → block scoped
const → block scoped
```

Scope lookup:

```text
Inner → Outer → Global
```

Inner scopes can access outer scopes:

```javascript
const app = "Hotel";

function start() {
  console.log(app);
}
```

Outer scopes cannot access inner variables:

```javascript
function start() {
  const server = "Express";
}

console.log(server); // Error
```

---

# 33. Key Takeaways

* Scope controls where variables can be accessed.
* JavaScript uses lexical scope.
* Global scope is the outermost scope.
* Every function creates a function scope.
* Blocks create block scope for `let` and `const`.
* `var` is function-scoped.
* Inner scopes can access variables from outer scopes.
* Outer scopes cannot directly access variables inside inner scopes.
* The scope chain determines how JavaScript finds variables.
* Shadowing occurs when an inner scope uses the same variable name.
* ES modules have their own module scope.
* Understanding scope is essential for understanding **closures, `this`, hoisting, and asynchronous JavaScript**.

---
