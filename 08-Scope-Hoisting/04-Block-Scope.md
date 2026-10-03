# JavaScript Block Scope

**Block scope** means that a variable is available only inside the block where it was declared.

A block is code surrounded by curly braces:

```javascript
{
  // block
}
```

Blocks are commonly created by:

* `if`
* `else`
* `for`
* `while`
* `switch`
* standalone `{ }`

In modern JavaScript, `let` and `const` are block-scoped.

---

# 1. What Is a Block?

A block is a group of statements enclosed in `{}`.

```javascript
{
  const message = "Hello";

  console.log(message);
}
```

The variable `message` belongs to that block.

Outside:

```javascript
console.log(message);
```

causes a `ReferenceError`.

---

# 2. `let` Is Block-Scoped

```javascript
if (true) {
  let status = "active";

  console.log(status);
}
```

This works because `status` is used inside its block.

Outside:

```javascript
if (true) {
  let status = "active";
}

console.log(status);
```

`status` is not available outside the `if` block.

---

# 3. `const` Is Block-Scoped

The same rule applies to `const`.

```javascript
if (true) {
  const username = "Sandip";

  console.log(username);
}
```

Outside:

```javascript
console.log(username);
```

causes a `ReferenceError`.

---

# 4. `var` Is Not Block-Scoped

`var` behaves differently.

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

The `if` block does not create a separate scope for `var`.

Remember:

```text
var        → function-scoped
let        → block-scoped
const      → block-scoped
```

---

# 5. `if` Creates a Block

An `if` statement creates a block when `{}` are used.

```javascript
if (userLoggedIn) {
  const message = "Welcome";
  console.log(message);
}
```

`message` belongs to that block.

---

# 6. `else` Has Its Own Block

```javascript
if (isAdmin) {
  const role = "Admin";

  console.log(role);
} else {
  const role = "User";

  console.log(role);
}
```

The two `role` variables are separate.

Each belongs to its own block.

---

# 7. Same Variable Name in Different Blocks

Different blocks can contain variables with the same name.

```javascript
if (true) {
  const status = "available";

  console.log(status);
}

if (true) {
  const status = "occupied";

  console.log(status);
}
```

Output:

```text
available
occupied
```

Each block has its own `status`.

---

# 8. Block Shadowing

An inner block can create a variable with the same name as an outer variable.

```javascript
const status = "available";

if (true) {
  const status = "occupied";

  console.log(status);
}

console.log(status);
```

Output:

```text
occupied
available
```

The inner variable shadows the outer variable.

---

# 9. Nested Blocks

Blocks can exist inside other blocks.

```javascript
{
  const outer = "Outer";

  {
    const inner = "Inner";

    console.log(outer);
    console.log(inner);
  }
}
```

The inner block can access `outer`.

But `outer` cannot access `inner`.

```text
Outer Block
│
├── outer
│
└── Inner Block
    └── inner
```

---

# 10. Block Scope and `for`

A `for` loop creates a block scope.

```javascript
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

After the loop:

```javascript
console.log(i);
```

causes an error because `i` is scoped to the loop.

---

# 11. Block Scope and `for...of`

The same applies to `for...of`.

```javascript
const users = ["Sandip", "Ram", "Hari"];

for (const user of users) {
  console.log(user);
}
```

`user` belongs to the loop's scope.

Outside:

```javascript
console.log(user);
```

does not work.

---

# 12. Block Scope and `for...in`

```javascript
const user = {
  name: "Sandip",
  role: "admin"
};

for (const key in user) {
  console.log(key);
}
```

`key` is scoped to the loop.

---

# 13. Block Scope and `while`

A `while` loop can also contain a block.

```javascript
let count = 0;

while (count < 3) {
  const message = `Count: ${count}`;

  console.log(message);

  count++;
}
```

`message` is created inside the block of each loop iteration.

---

# 14. Block Scope and `switch`

`switch` uses case clauses, but declaring `let` or `const` directly across multiple cases can cause lexical declaration conflicts.

A safe pattern is to use braces around each case:

```javascript
const role = "admin";

switch (role) {
  case "admin": {
    const message = "Administrator";
    console.log(message);
    break;
  }

  case "waiter": {
    const message = "Waiter";
    console.log(message);
    break;
  }
}
```

Each case has its own block.

---

# 15. Standalone Block

You can create a block without `if`, `for`, or another statement.

```javascript
{
  const apiUrl = "/api/v1";

  console.log(apiUrl);
}
```

After the block:

```javascript
console.log(apiUrl);
```

does not work.

Standalone blocks can be useful when you intentionally want to limit the lifetime and visibility of temporary variables.

---

# 16. Block Scope With `let`

```javascript
{
  let count = 10;

  count++;

  console.log(count);
}
```

Output:

```text
11
```

Outside the block:

```javascript
console.log(count);
```

causes an error.

---

# 17. Block Scope With `const`

```javascript
{
  const appName = "Hotel App";

  console.log(appName);
}
```

`appName` is only accessible inside the block.

---

# 18. `const` Can Still Mutate Objects

Block scope and immutability are different concepts.

Consider:

```javascript
{
  const user = {
    name: "Sandip"
  };

  user.name = "Ram";

  console.log(user.name);
}
```

Output:

```text
Ram
```

`const` prevents reassignment of the variable binding:

```javascript
user = {};
```

but it does not make the object itself immutable.

---

# 19. Block Scope and Functions

Functions can be declared inside blocks.

```javascript
if (true) {
  function greet() {
    console.log("Hello");
  }

  greet();
}
```

For predictable modern JavaScript behavior, avoid relying on block-level function declaration behavior across older environments. If you specifically need a function local to a block, a function expression or arrow function with `const` is often clearer:

```javascript
if (true) {
  const greet = () => {
    console.log("Hello");
  };

  greet();
}
```

---

# 20. Block Scope and `try...catch`

`catch` creates a scope for its parameter.

```javascript
try {
  throw new Error("Something went wrong");
} catch (error) {
  console.log(error.message);
}
```

`error` is available inside the `catch` block.

Outside:

```javascript
console.log(error);
```

does not work.

---

# 21. Block Scope in `try...finally`

```javascript
try {
  const message = "Processing";

  console.log(message);
} finally {
  const cleanup = "Cleaning up";

  console.log(cleanup);
}
```

`message` and `cleanup` belong to their respective blocks.

---

# 22. Block Scope and Closures

Block-scoped variables are especially useful with callbacks.

For example:

```javascript
const buttons = document.querySelectorAll("button");

for (let i = 0; i < buttons.length; i++) {
  buttons[i].addEventListener("click", () => {
    console.log(i);
  });
}
```

`let` creates the appropriate per-iteration binding for the loop.

This makes it easier for callbacks to use the correct iteration value.

---

# 23. Why `let` Works Better in Loops

Consider:

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 100);
}
```

The output is:

```text
0
1
2
```

Each iteration gets its own binding for `i`.

This is one practical benefit of `let` in loops.

---

# 24. Comparing `var` and `let` in Loops

With `var`:

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 100);
}
```

The callbacks typically print:

```text
3
3
3
```

because `var` uses one function-scoped binding.

With `let`:

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 100);
}
```

the callbacks print:

```text
0
1
2
```

because each iteration gets its own `let` binding.

---

# 25. Block Scope in Real Applications

Suppose a hotel application checks a table:

```javascript
function checkTable(table) {
  if (table.status === "available") {
    const message = "Table can be assigned";

    console.log(message);
  }

  console.log(table.status);
}
```

`message` is only needed inside the `if` block.

Keeping it there makes its scope smaller and clearer.

---

# 26. Another Practical Example

```javascript
function processPayment(amount) {
  if (amount > 0) {
    const transactionId = "TXN-1001";

    console.log(`Processing ${transactionId}`);
  }

  console.log(amount);
}
```

Here:

```text
amount         → function scope
transactionId  → if-block scope
```

This is a good example of using the smallest necessary scope.

---

# 27. Block Scope and Modules

ES modules have module scope, and blocks inside modules still follow normal block-scope rules.

```javascript
const API_URL = "/api";

if (true) {
  const timeout = 5000;

  console.log(API_URL);
  console.log(timeout);
}
```

`API_URL` belongs to the module's top-level scope.

`timeout` belongs to the `if` block.

---

# 28. Scope Hierarchy

A block can be nested inside a function:

```text
Global / Module Scope
│
└── Function Scope
    │
    └── Block Scope
        │
        └── Nested Block Scope
```

Variable lookup moves outward:

```text
Nested Block
     ↓
Outer Block
     ↓
Function
     ↓
Global / Module
```

---

# 29. Block Scope vs Function Scope

| Feature    | Function Scope                        | Block Scope             |
| ---------- | ------------------------------------- | ----------------------- |
| Created by | Function                              | `{}` blocks             |
| `var`      | Yes                                   | No                      |
| `let`      | Local to function when declared there | Yes                     |
| `const`    | Local to function when declared there | Yes                     |
| Example    | `function test() {}`                  | `if (...) {}`           |
| Lookup     | Can search outer scopes               | Can search outer scopes |

---

# 30. `var` vs `let` vs `const`

```javascript
function example() {
  var a = 10;
  let b = 20;
  const c = 30;

  if (true) {
    var x = 40;
    let y = 50;
    const z = 60;
  }

  console.log(a); // 10
  console.log(b); // 20
  console.log(c); // 30
  console.log(x); // 40

  // y → unavailable
  // z → unavailable
}
```

The key difference:

```text
var
└── function scope

let
└── block scope

const
└── block scope
```

---

# 31. Common Mistakes

### Mistake 1: Assuming `var` is block-scoped

```javascript
if (true) {
  var value = 100;
}

console.log(value);
```

This works because `var` is not block-scoped.

---

### Mistake 2: Using a `let` variable outside its block

```javascript
if (true) {
  let value = 100;
}

console.log(value);
```

This causes a `ReferenceError`.

---

### Mistake 3: Assuming `const` makes objects immutable

```javascript
if (true) {
  const user = {
    name: "Sandip"
  };

  user.name = "Ram";
}
```

The property can still be changed.

`const` controls reassignment of the binding, not deep immutability of the object.

---

# 32. Best Practices

### Use `const` by default

```javascript
const user = getUser();
```

### Use `let` when reassignment is required

```javascript
let count = 0;

count++;
```

### Keep variables close to their usage

Instead of:

```javascript
let message;

if (success) {
  message = "Success";
}
```

you can often write:

```javascript
if (success) {
  const message = "Success";

  console.log(message);
}
```

### Avoid unnecessary `var`

Prefer:

```text
const → let → var
```

depending on the requirement.

---

# 33. Quick Reference

### Block

```javascript
{
  // block
}
```

### `let`

```javascript
if (true) {
  let value = 10;
}
```

Block-scoped.

### `const`

```javascript
if (true) {
  const value = 10;
}
```

Block-scoped.

### `var`

```javascript
if (true) {
  var value = 10;
}

console.log(value);
```

Not block-scoped.

### Nested block

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

---

# 34. Key Takeaways

* A block is code surrounded by `{}`.
* `let` is block-scoped.
* `const` is block-scoped.
* `var` is function-scoped, not block-scoped.
* `if`, `for`, `while`, and `switch` commonly contain blocks.
* Variables inside a block are not normally available outside it.
* Inner blocks can access variables from outer scopes.
* Different blocks can contain variables with the same name.
* `let` provides a separate binding for each `for` loop iteration.
* Block scope helps keep variables limited to where they are actually needed.
* Smaller scopes generally make code easier to understand and maintain.

---
