# JavaScript Hoisting

**Hoisting** describes the behavior where JavaScript processes declarations before executing the code in a scope.

This can make some declarations appear usable before their written position, but **not all declarations behave the same way**.

The most important distinction is between:

```text
Function declarations
var
let
const
```

---

# 1. Simple Example

Consider:

```javascript
console.log(message);

var message = "Hello";
```

Output:

```text
undefined
```

It does not produce a `ReferenceError`.

Conceptually, JavaScript processes the declaration before execution:

```javascript
var message;

console.log(message);

message = "Hello";
```

The declaration is processed early, but the assignment happens where it was written.

---

# 2. Declaration vs Initialization

This distinction is important.

```javascript
var message = "Hello";
```

contains two main parts:

```text
Declaration   → var message
Initialization / assignment → "Hello"
```

Hoisting does not mean the complete line moves to the top.

Conceptually:

```javascript
var message;

console.log(message);

message = "Hello";
```

---

# 3. `var` Hoisting

`var` declarations are hoisted and initialized with:

```javascript
undefined
```

Example:

```javascript
console.log(name);

var name = "Sandip";
```

Output:

```text
undefined
```

After the assignment:

```javascript
console.log(name);

var name = "Sandip";

console.log(name);
```

Output:

```text
undefined
Sandip
```

---

# 4. `var` Declaration Is Hoisted

This:

```javascript
var username = "Sandip";
```

is conceptually similar to:

```javascript
var username;

username = "Sandip";
```

The declaration is processed before execution.

---

# 5. Function Declaration Hoisting

Function declarations are hoisted.

Example:

```javascript
greet();

function greet() {
  console.log("Hello");
}
```

Output:

```text
Hello
```

The function can be called before its written position.

---

# 6. Why Function Declaration Works

Consider:

```javascript
sayHello();

function sayHello() {
  console.log("Hello, Sandip");
}
```

The function declaration is available when the code executes the call.

This is different from a function expression.

---

# 7. Function Expression and Hoisting

Consider:

```javascript
greet();

const greet = function () {
  console.log("Hello");
};
```

This does not work.

`greet` is declared using `const`, so accessing it before initialization causes a `ReferenceError`.

---

# 8. Arrow Function and Hoisting

The same applies to arrow functions assigned to `const`.

```javascript
greet();

const greet = () => {
  console.log("Hello");
};
```

This causes a `ReferenceError`.

The function itself is not available before the `const` variable is initialized.

---

# 9. `let` and Hoisting

`let` declarations are also processed before execution, but they cannot be accessed before initialization.

Example:

```javascript
console.log(username);

let username = "Sandip";
```

This causes:

```text
ReferenceError
```

This behavior is connected to the **Temporal Dead Zone (TDZ)**.

---

# 10. `const` and Hoisting

The same applies to `const`.

```javascript
console.log(username);

const username = "Sandip";
```

This causes:

```text
ReferenceError
```

The `const` binding exists in the scope, but it cannot be accessed before initialization.

---

# 11. The Temporal Dead Zone

The period between entering a scope and reaching the declaration of a `let` or `const` variable is called the **Temporal Dead Zone**.

Example:

```javascript
console.log(name);

let name = "Sandip";
```

The access occurs inside the TDZ.

Therefore:

```text
ReferenceError
```

The TDZ will be covered in more detail in:

```text
08-Scope-Hoisting/06-Temporal-Dead-Zone.md
```

---

# 12. Hoisting Comparison

| Declaration                            | Hoisted?                             | Can Access Before Declaration? |
| -------------------------------------- | ------------------------------------ | ------------------------------ |
| Function declaration                   | Yes                                  | Yes                            |
| `var`                                  | Yes                                  | Yes, value is `undefined`      |
| `let`                                  | Yes, but uninitialized               | No                             |
| `const`                                | Yes, but uninitialized               | No                             |
| Function expression with `var`         | Variable is hoisted                  | No, value is `undefined`       |
| Function expression with `let`/`const` | Binding is hoisted but uninitialized | No                             |

---

# 13. `var` Function Expression

Consider:

```javascript
greet();

var greet = function () {
  console.log("Hello");
};
```

Conceptually:

```javascript
var greet;

greet();

greet = function () {
  console.log("Hello");
};
```

At the time of the call:

```javascript
greet();
```

`greet` is:

```javascript
undefined
```

Calling it causes:

```text
TypeError
```

because `undefined` is not a function.

---

# 14. Function Declaration vs Function Expression

### Function declaration

```javascript
greet();

function greet() {
  console.log("Hello");
}
```

Works.

### Function expression

```javascript
greet();

const greet = function () {
  console.log("Hello");
};
```

Does not work.

### Arrow function

```javascript
greet();

const greet = () => {
  console.log("Hello");
};
```

Does not work.

---

# 15. Hoisting Inside Functions

Hoisting also happens inside function scopes.

```javascript
function example() {
  console.log(value);

  var value = 100;
}

example();
```

Output:

```text
undefined
```

Conceptually:

```javascript
function example() {
  var value;

  console.log(value);

  value = 100;
}
```

---

# 16. Function Declaration Inside a Function

```javascript
function outer() {
  inner();

  function inner() {
    console.log("Inside inner");
  }
}

outer();
```

Output:

```text
Inside inner
```

The inner function declaration is available within the function scope.

---

# 17. Hoisting and Scope

Hoisting happens within the relevant scope.

Example:

```javascript
const globalValue = "Global";

function example() {
  var localValue = "Local";

  console.log(globalValue);
  console.log(localValue);
}

example();
```

The local declaration belongs to the function scope.

Hoisting does not move variables into a different scope.

---

# 18. Hoisting Does Not Ignore Scope

Consider:

```javascript
function example() {
  console.log(value);

  var value = 100;
}

console.log(value);
```

Inside the function:

```text
value → exists as a function-scoped variable
```

Outside:

```text
value → not available
```

Hoisting does not make `value` global.

---

# 19. Block Scope and Hoisting

`let` and `const` are block-scoped.

```javascript
if (true) {
  console.log(value);

  let value = 100;
}
```

This causes:

```text
ReferenceError
```

The declaration is associated with the block, but access before initialization is prohibited.

---

# 20. `var` Inside a Block

```javascript
if (true) {
  console.log(value);

  var value = 100;
}

console.log(value);
```

Output:

```text
undefined
100
```

In this example, `var` is not block-scoped.

---

# 21. Function Declaration Hoisting

Function declarations can be called before they appear.

```javascript
calculate();

function calculate() {
  console.log("Calculating...");
}
```

Output:

```text
Calculating...
```

This behavior is one reason older JavaScript code sometimes places function declarations below the code that uses them.

---

# 22. Function Declaration With Parameters

```javascript
const result = add(10, 20);

function add(a, b) {
  return a + b;
}

console.log(result);
```

Output:

```text
30
```

The function declaration is available when `add()` is called.

---

# 23. Hoisting Does Not Move Assignments

Consider:

```javascript
console.log(score);

var score = 100;
```

You get:

```text
undefined
```

Not:

```text
100
```

Only the declaration is processed before execution.

The assignment remains at its original execution point.

---

# 24. Multiple `var` Declarations

Consider:

```javascript
console.log(value);

var value = 10;
var value = 20;

console.log(value);
```

Output:

```text
undefined
20
```

Conceptually:

```javascript
var value;

console.log(value);

value = 10;
value = 20;

console.log(value);
```

The later assignment replaces the earlier value.

---

# 25. Function Declaration and `var` With Same Name

This is a more advanced case.

```javascript
console.log(value);

var value = 10;

function value() {
  console.log("Function");
}
```

Declaration processing rules can make interactions between function declarations and `var` surprising.

Avoid using the same identifier for unrelated declarations.

A clearer style is:

```javascript
function showValue() {
  console.log("Function");
}

const value = 10;
```

Use distinct names.

---

# 26. Hoisting and Best Practices

Even though JavaScript supports hoisting, don't rely on it unnecessarily.

Prefer writing code in a clear order:

```javascript
const user = getUser();

function getUser() {
  return {
    name: "Sandip"
  };
}
```

This works because the function declaration is hoisted, but you may also choose to place helper declarations where the structure is easy to follow.

For variables:

```javascript
const user = createUser();
```

is generally clearer than trying to use a variable before its declaration.

---

# 27. Recommended Style

Prefer:

```javascript
const calculateTotal = (items) => {
  // ...
};
```

and use it after its declaration:

```javascript
const calculateTotal = (items) => {
  return items.reduce((total, item) => total + item.price, 0);
};

const total = calculateTotal(items);
```

This makes the execution flow easy to read.

---

# 28. Practical Example

Consider a hotel order:

```javascript
const total = calculateTotal(orderItems);

function calculateTotal(items) {
  return items.reduce((sum, item) => {
    return sum + item.price;
  }, 0);
}
```

This works because `calculateTotal` is a function declaration.

For a function expression:

```javascript
const calculateTotal = function (items) {
  return items.reduce((sum, item) => {
    return sum + item.price;
  }, 0);
};

const total = calculateTotal(orderItems);
```

The function is initialized before it is used.

---

# 29. Common Mistakes

### Mistake 1: Thinking `var` is moved physically

Hoisting is not literally moving code to the top.

Instead, JavaScript processes declarations as part of creating the relevant execution environment before running statements.

---

### Mistake 2: Assuming `let` behaves like `var`

```javascript
console.log(value);

let value = 10;
```

This does not output `undefined`.

It throws a `ReferenceError`.

---

### Mistake 3: Calling a `const` function expression too early

```javascript
start();

const start = () => {
  console.log("Started");
};
```

This causes a `ReferenceError`.

---

### Mistake 4: Thinking assignments are hoisted

```javascript
console.log(value);

var value = 100;
```

Output:

```text
undefined
```

The value `100` is not available until the assignment executes.

---

# 30. A Simple Mental Model

Before executing a scope, think of JavaScript as preparing declarations.

For:

```javascript
var name = "Sandip";
```

think approximately:

```text
Declaration → prepared
Value       → assigned later
```

For:

```javascript
let name = "Sandip";
```

think:

```text
Declaration → known to the scope
Initialization → happens at the declaration
Before initialization → TDZ
```

For:

```javascript
function greet() {}
```

the function declaration is available during execution of its scope.

---

# 31. Quick Reference

### `var`

```javascript
console.log(value);

var value = 10;
```

Result:

```text
undefined
```

### `let`

```javascript
console.log(value);

let value = 10;
```

Result:

```text
ReferenceError
```

### `const`

```javascript
console.log(value);

const value = 10;
```

Result:

```text
ReferenceError
```

### Function declaration

```javascript
greet();

function greet() {
  console.log("Hello");
}
```

Works.

---

# 32. Hoisting Summary

```text
Function Declaration
        ↓
Available before written position

var
        ↓
Declaration available
        ↓
Initial value: undefined

let
        ↓
Declaration associated with scope
        ↓
TDZ before initialization

const
        ↓
Declaration associated with scope
        ↓
TDZ before initialization
        ↓
Must be initialized at declaration
```

---

# 33. Key Takeaways

* Hoisting describes how JavaScript processes declarations before executing statements.
* Function declarations can be called before their written position.
* `var` declarations are hoisted and initialized with `undefined`.
* `let` and `const` are hoisted in the sense that their bindings are created with the scope, but they remain uninitialized until their declaration is evaluated.
* Accessing `let` or `const` before initialization causes a `ReferenceError`.
* The period before initialization is the **Temporal Dead Zone**.
* Function expressions and arrow functions do not behave like hoisted function declarations.
* Assignments are not hoisted with their declarations.
* Hoisting does not change a variable's scope.
* Writing variables before using them generally makes code easier to understand.
* Understanding hoisting makes the behavior of `var`, `let`, `const`, and function declarations much clearer.

---
