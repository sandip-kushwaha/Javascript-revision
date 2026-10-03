# JavaScript Temporal Dead Zone (TDZ)

The **Temporal Dead Zone (TDZ)** is the period between entering a scope and the point where a `let` or `const` variable is initialized.

During this period, trying to access the variable causes a:

```text
ReferenceError
```

---

# 1. Simple Example

```javascript
console.log(username);

let username = "Sandip";
```

Output:

```text
ReferenceError
```

Why?

Because `username` exists in the scope, but it has not been initialized yet.

The area before the declaration is the **Temporal Dead Zone**.

---

# 2. Understanding the TDZ

Consider:

```javascript
{
  // TDZ starts

  console.log(name);

  let name = "Sandip";

  // TDZ ends
}
```

Conceptually:

```text
Block starts
     ↓
TDZ starts
     ↓
Accessing `name` → ReferenceError
     ↓
let name = "Sandip"
     ↓
TDZ ends
     ↓
name can be used
```

---

# 3. When Does the TDZ End?

The TDZ ends when the declaration is evaluated.

```javascript
{
  let username = "Sandip";

  console.log(username);
}
```

Output:

```text
Sandip
```

Here the variable has already been initialized before it is accessed.

---

# 4. `let` and TDZ

`let` variables have TDZ behavior.

```javascript
console.log(age);

let age = 22;
```

Result:

```text
ReferenceError
```

Compare this with `var`:

```javascript
console.log(age);

var age = 22;
```

Result:

```text
undefined
```

---

# 5. `const` and TDZ

`const` also has TDZ behavior.

```javascript
console.log(country);

const country = "Nepal";
```

Result:

```text
ReferenceError
```

The variable cannot be accessed before initialization.

---

# 6. TDZ Is Not the Same as "Not Hoisted"

A common misconception is:

> "`let` and `const` are not hoisted."

This is an oversimplification.

A better explanation is:

```text
let/const bindings are created for their scope,
but they remain uninitialized until execution reaches
their declaration.
```

Therefore:

```javascript
console.log(value);

let value = 100;
```

does not produce `undefined`.

It produces:

```text
ReferenceError
```

---

# 7. `var` vs `let`

### `var`

```javascript
console.log(value);

var value = 100;
```

Result:

```text
undefined
```

### `let`

```javascript
console.log(value);

let value = 100;
```

Result:

```text
ReferenceError
```

The major difference is the initialization behavior.

---

# 8. TDZ With `const`

```javascript
{
  console.log(price);

  const price = 500;
}
```

The access occurs before initialization.

Therefore:

```text
ReferenceError
```

Correct:

```javascript
{
  const price = 500;

  console.log(price);
}
```

Output:

```text
500
```

---

# 9. TDZ With Block Scope

TDZ applies within the variable's lexical scope.

```javascript
let value = "global";

{
  console.log(value);

  let value = "local";
}
```

This produces:

```text
ReferenceError
```

Why?

The inner `let value` creates a new binding for the block.

Inside the block, the inner `value` shadows the outer one.

Before the inner declaration is initialized, the inner `value` is in its TDZ.

---

# 10. Scope Shadowing + TDZ

Consider:

```javascript
const username = "Global";

function showUser() {
  console.log(username);

  const username = "Local";
}

showUser();
```

This causes:

```text
ReferenceError
```

It may look like JavaScript should use the global `username`.

But the function contains:

```javascript
const username = "Local";
```

Therefore, the local variable shadows the global variable throughout that lexical scope.

Before initialization, it is in the TDZ.

---

# 11. TDZ in `if`

```javascript
if (true) {
  console.log(status);

  let status = "active";
}
```

Result:

```text
ReferenceError
```

Correct:

```javascript
if (true) {
  let status = "active";

  console.log(status);
}
```

---

# 12. TDZ in Loops

TDZ can also occur inside loops.

```javascript
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

This is valid because `i` is initialized before the loop body uses it.

But:

```javascript
{
  console.log(i);

  let i = 10;
}
```

causes:

```text
ReferenceError
```

---

# 13. TDZ in Function Parameters

TDZ-related behavior can also appear with default parameters.

Consider:

```javascript
function example(value = count) {
  let count = 10;

  console.log(value);
}

example();
```

The `count` referenced by the default parameter is not the later local `count` in the function body.

The parameter environment is evaluated before the function body.

This can result in a `ReferenceError`.

The important point is that parameter initialization and the function body have different stages and scopes.

---

# 14. Default Parameter Example

This works:

```javascript
const defaultName = "Sandip";

function greet(name = defaultName) {
  console.log(name);
}

greet();
```

Output:

```text
Sandip
```

Here `defaultName` is already initialized.

---

# 15. TDZ With `typeof`

Many developers know that:

```javascript
typeof unknownVariable
```

usually returns:

```text
"undefined"
```

For example:

```javascript
console.log(typeof notDeclared);
```

Output:

```text
undefined
```

But `typeof` does **not** bypass the TDZ.

```javascript
console.log(typeof username);

let username = "Sandip";
```

This produces:

```text
ReferenceError
```

The difference is:

```text
undeclared variable → typeof can return "undefined"

declared let/const before initialization → ReferenceError
```

---

# 16. Undeclared vs TDZ Variable

### Undeclared

```javascript
console.log(typeof user);
```

Output:

```text
undefined
```

No `user` binding exists.

### TDZ

```javascript
console.log(typeof user);

let user = "Sandip";
```

Result:

```text
ReferenceError
```

The `user` binding exists, but it has not been initialized.

---

# 17. TDZ and `const` Initialization

A `const` declaration must initialize the variable.

This is invalid:

```javascript
const username;
```

It produces a:

```text
SyntaxError
```

Correct:

```javascript
const username = "Sandip";
```

After initialization, reassignment is not allowed:

```javascript
const username = "Sandip";

username = "Kushwaha";
```

This produces a:

```text
TypeError
```

---

# 18. TDZ Does Not Mean the Variable Is `undefined`

Consider:

```javascript
console.log(value);

let value = 100;
```

The variable is **not** temporarily:

```text
undefined
```

Instead, accessing it is illegal.

That is why the result is:

```text
ReferenceError
```

This is an important difference from `var`.

---

# 19. TDZ With Classes

Class declarations also have TDZ behavior.

```javascript
const user = new User();

class User {
  constructor(name) {
    this.name = name;
  }
}
```

This causes a:

```text
ReferenceError
```

The class declaration has not been initialized when `new User()` is executed.

Correct:

```javascript
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");
```

---

# 20. TDZ With Nested Blocks

```javascript
let message = "Outer";

{
  console.log(message);

  {
    let message = "Inner";
  }
}
```

Output:

```text
Outer
```

Why?

The inner `message` does not belong to the outer block.

Now consider:

```javascript
let message = "Outer";

{
  console.log(message);

  let message = "Inner";
}
```

This causes:

```text
ReferenceError
```

The inner declaration shadows the outer variable and is in its TDZ.

---

# 21. Practical Example

Imagine a hotel order system:

```javascript
function createOrder() {
  console.log(orderStatus);

  const orderStatus = "pending";

  return orderStatus;
}

createOrder();
```

This causes:

```text
ReferenceError
```

Correct:

```javascript
function createOrder() {
  const orderStatus = "pending";

  console.log(orderStatus);

  return orderStatus;
}

createOrder();
```

Output:

```text
pending
```

---

# 22. Another Practical Example

Consider a user session:

```javascript
function createSession() {
  console.log(sessionToken);

  let sessionToken = "abc123";

  return sessionToken;
}
```

The first access occurs before initialization.

Therefore:

```text
ReferenceError
```

Correct:

```javascript
function createSession() {
  let sessionToken = "abc123";

  console.log(sessionToken);

  return sessionToken;
}
```

---

# 23. TDZ and Closures

Consider:

```javascript
function createCounter() {
  console.log(count);

  let count = 0;

  return () => {
    count++;
    return count;
  };
}
```

The first `console.log(count)` happens before initialization.

Therefore:

```text
ReferenceError
```

Moving the declaration first fixes it:

```javascript
function createCounter() {
  let count = 0;

  return () => {
    count++;
    return count;
  };
}
```

The returned function can then access `count` through the closure.

---

# 24. TDZ Does Not Continue Forever

The TDZ only exists until initialization.

```javascript
{
  // TDZ

  let value = 100;

  // TDZ has ended

  console.log(value);
}
```

The variable can be used normally after initialization.

---

# 25. Common Errors Related to TDZ

### Error 1: Accessing `let` too early

```javascript
console.log(name);

let name = "Sandip";
```

Result:

```text
ReferenceError
```

---

### Error 2: Accessing `const` too early

```javascript
console.log(price);

const price = 500;
```

Result:

```text
ReferenceError
```

---

### Error 3: Using a shadowed variable

```javascript
const value = 10;

function test() {
  console.log(value);

  const value = 20;
}

test();
```

Result:

```text
ReferenceError
```

The local declaration shadows the outer variable.

---

### Error 4: Using `typeof` to bypass TDZ

```javascript
console.log(typeof value);

let value = 10;
```

Result:

```text
ReferenceError
```

`typeof` does not bypass the TDZ.

---

# 26. Best Practices

### Declare variables before using them

Prefer:

```javascript
const user = getUser();

console.log(user);
```

Instead of relying on declaration behavior.

---

### Prefer `const` by default

```javascript
const username = "Sandip";
```

Use `let` when reassignment is required:

```javascript
let count = 0;

count++;
```

Avoid `var` in modern JavaScript unless you specifically need its function-scoped behavior.

---

### Avoid confusing shadowing

Instead of:

```javascript
const user = "Admin";

function example() {
  const user = "Customer";
}
```

use descriptive names when appropriate:

```javascript
const currentUser = "Admin";

function example() {
  const customerUser = "Customer";
}
```

This can make scope relationships easier to understand.

---

# 27. `var`, `let`, and `const` Comparison

| Feature                                | `var`         | `let` | `const` |
| -------------------------------------- | ------------- | ----- | ------- |
| Scope                                  | Function      | Block | Block   |
| Declaration processed before execution | Yes           | Yes   | Yes     |
| Initialized before declaration access  | `undefined`   | No    | No      |
| TDZ                                    | No            | Yes   | Yes     |
| Can reassign                           | Yes           | Yes   | No      |
| Must initialize immediately            | No            | No    | Yes     |
| Recommended for modern code            | Usually avoid | Yes   | Yes     |

---

# 28. TDZ Mental Model

Think about:

```javascript
{
  // TDZ
  // `username` exists but cannot be accessed

  let username = "Sandip";

  // TDZ ends

  console.log(username);
}
```

A simple mental model:

```text
Enter scope
     ↓
Binding created
     ↓
TDZ
     ↓
Declaration evaluated
     ↓
Variable initialized
     ↓
TDZ ends
     ↓
Variable can be accessed
```

---

# 29. Key Takeaways

* **TDZ = Temporal Dead Zone**.
* It applies to `let` and `const`.
* A variable in the TDZ cannot be accessed.
* Accessing it causes a `ReferenceError`.
* TDZ begins when the scope is entered.
* TDZ ends when the declaration is initialized.
* `let` and `const` are not simply "not hoisted"; their bindings are created before execution but remain uninitialized.
* `var` does not have TDZ behavior.
* `var` is initialized with `undefined`.
* Shadowing can cause TDZ-related errors.
* `typeof` does not bypass the TDZ.
* Class declarations also have TDZ behavior.
* Declaring variables before using them makes code easier to understand.

---
