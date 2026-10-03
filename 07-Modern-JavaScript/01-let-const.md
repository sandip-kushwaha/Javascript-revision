# JavaScript `let` and `const`

`let` and `const` are modern ways to declare variables in JavaScript.

They were introduced with **ES6 (ECMAScript 2015)**.

Before `let` and `const`, JavaScript mainly used:

```javascript
var
```

Modern JavaScript generally prefers:

```javascript
let
const
```

---

# 1. `let`

Use `let` when a variable's value needs to change.

```javascript
let age = 22;

age = 23;

console.log(age);
```

Output:

```text
23
```

The value can be reassigned.

---

# 2. `const`

Use `const` when the variable should not be reassigned.

```javascript
const name = "Sandip";

console.log(name);
```

You cannot do:

```javascript
const name = "Sandip";

name = "Ram";
```

This causes an error because a `const` variable cannot be reassigned.

---

# 3. Basic Difference

```javascript
let age = 22;

age = 23;
```

Allowed.

```javascript
const age = 22;

age = 23;
```

Not allowed.

Simple rule:

```text
let   → value can be reassigned
const → value cannot be reassigned
```

---

# 4. `let` Can Be Reassigned

```javascript
let score = 50;

score = 70;
score = 90;

console.log(score);
```

Output:

```text
90
```

The same variable can receive a new value.

---

# 5. `const` Cannot Be Reassigned

```javascript
const score = 50;

score = 70;
```

This causes an error.

The variable binding created by `const` cannot point to a different value.

---

# 6. `const` Must Be Initialized

This is invalid:

```javascript
const name;
```

A `const` declaration must have an initial value.

Correct:

```javascript
const name = "Sandip";
```

---

# 7. `let` Can Be Declared Without a Value

This is allowed:

```javascript
let name;

console.log(name);
```

Output:

```text
undefined
```

You can assign a value later:

```javascript
let name;

name = "Sandip";

console.log(name);
```

Output:

```text
Sandip
```

---

# 8. `let` and `const` Are Block Scoped

`let` and `const` are **block-scoped**.

A block is usually represented by:

```javascript
{
  // block
}
```

Example:

```javascript
{
  let age = 22;

  console.log(age);
}
```

The variable exists inside that block.

---

# 9. Block Scope Example

```javascript
{
  let message = "Hello";

  console.log(message);
}

console.log(message);
```

The second `console.log()` causes an error because `message` only exists inside the block.

---

# 10. `const` Is Also Block Scoped

```javascript
{
  const name = "Sandip";

  console.log(name);
}
```

Outside the block:

```javascript
console.log(name);
```

The variable is not accessible.

---

# 11. Block Scope With `if`

```javascript
if (true) {
  let message = "Hello";

  console.log(message);
}
```

The variable belongs to the `if` block.

---

# 12. `let` in a Loop

`let` is commonly used with loops.

```javascript
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

Output:

```text
0
1
2
```

After the loop:

```javascript
console.log(i);
```

`i` is not available because it is block scoped.

---

# 13. `const` in a Loop

You can use `const` in a `for...of` loop:

```javascript
const fruits = [
  "Apple",
  "Mango",
  "Banana"
];

for (const fruit of fruits) {
  console.log(fruit);
}
```

Output:

```text
Apple
Mango
Banana
```

Each loop iteration gets its own `fruit` binding.

---

# 14. `let` vs `var`

Older JavaScript commonly used:

```javascript
var
```

Modern JavaScript commonly uses:

```javascript
let
const
```

One important difference is scope.

### `var`

`var` is function-scoped.

### `let`

`let` is block-scoped.

### `const`

`const` is block-scoped.

---

# 15. Example With `var`

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

`var` does not respect the `if` block in the same way `let` and `const` do.

---

# 16. Example With `let`

```javascript
if (true) {
  let message = "Hello";
}

console.log(message);
```

This causes an error because `message` is block-scoped.

---

# 17. Scope Comparison

| Keyword | Scope    | Reassign | Redeclare in Same Scope |
| ------- | -------- | -------- | ----------------------- |
| `var`   | Function | Yes      | Yes                     |
| `let`   | Block    | Yes      | No                      |
| `const` | Block    | No       | No                      |

---

# 18. Redeclaring `let`

This is not allowed in the same scope:

```javascript
let name = "Sandip";

let name = "Ram";
```

JavaScript reports an error.

But you can reassign it:

```javascript
let name = "Sandip";

name = "Ram";

console.log(name);
```

Output:

```text
Ram
```

---

# 19. Redeclaring `const`

This is also not allowed:

```javascript
const name = "Sandip";

const name = "Ram";
```

And reassignment is also not allowed:

```javascript
const name = "Sandip";

name = "Ram";
```

---

# 20. Different Blocks Can Have Same Name

Because `let` and `const` are block-scoped, the same variable name can exist in different blocks.

```javascript
let name = "Sandip";

{
  let name = "Ram";

  console.log(name);
}

console.log(name);
```

Output:

```text
Ram
Sandip
```

These are different variables.

---

# 21. Nested Blocks

```javascript
let name = "Sandip";

{
  let city = "Birgunj";

  {
    let country = "Nepal";

    console.log(name);
    console.log(city);
    console.log(country);
  }
}
```

Inner blocks can access variables from outer scopes when those variables are available there.

---

# 22. Outer Scope and Inner Scope

Example:

```javascript
let name = "Sandip";

{
  console.log(name);
}
```

Output:

```text
Sandip
```

The inner block can access `name` from the outer scope.

But the outer scope cannot access variables declared only inside the inner block.

```javascript
{
  let city = "Birgunj";
}

console.log(city);
```

This causes an error.

---

# 23. `const` With Objects

An important point:

`const` prevents **reassignment of the variable**, but it does not make an object completely immutable.

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22
};
```

You cannot do:

```javascript
user = {};
```

But you can change a property:

```javascript
user.age = 23;

console.log(user.age);
```

Output:

```text
23
```

---

# 24. Why Does This Work?

The variable:

```javascript
user
```

continues to reference the same object.

You are changing a property inside that object.

You are not assigning a completely new object to `user`.

```text
user
  ↓
{ name: "Sandip", age: 23 }
```

---

# 25. `const` With Arrays

The same rule applies to arrays.

```javascript
const fruits = [
  "Apple",
  "Mango"
];
```

You cannot reassign the array:

```javascript
fruits = [];
```

But you can modify the array:

```javascript
fruits.push("Banana");

console.log(fruits);
```

Output:

```text
["Apple", "Mango", "Banana"]
```

---

# 26. `const` Does Not Mean Immutable

This is an important concept.

```javascript
const user = {
  name: "Sandip"
};
```

`const` means:

```text
The variable cannot be reassigned.
```

It does **not** automatically mean:

```text
The object cannot be changed.
```

---

# 27. Reassigning vs Mutating

### Reassignment

```javascript
const user = {
  name: "Sandip"
};

user = {
  name: "Ram"
};
```

Not allowed.

### Mutation

```javascript
const user = {
  name: "Sandip"
};

user.name = "Ram";
```

Allowed.

---

# 28. `let` With Objects

`let` allows reassignment:

```javascript
let user = {
  name: "Sandip"
};

user = {
  name: "Ram"
};
```

This is allowed.

You can also mutate:

```javascript
user.name = "Shyam";
```

Both reassignment and mutation are possible with `let`.

---

# 29. Choosing Between `let` and `const`

Use `const` by default when the variable does not need reassignment.

```javascript
const name = "Sandip";
const age = 22;
```

Use `let` when the variable needs to change.

```javascript
let score = 0;

score = score + 10;
```

---

# 30. Example in a Function

```javascript
function calculateTotal() {
  const price = 500;
  const quantity = 2;

  let total = price * quantity;

  total = total + 100;

  return total;
}

console.log(calculateTotal());
```

Output:

```text
1100
```

Here:

* `price` does not change → `const`
* `quantity` does not change → `const`
* `total` changes → `let`

---

# 31. Hotel Management Example

```javascript
const tableNumber = "T-03";
const capacity = 6;

let status = "available";

status = "occupied";

console.log(tableNumber);
console.log(capacity);
console.log(status);
```

Output:

```text
T-03
6
occupied
```

`tableNumber` and `capacity` do not need reassignment, so `const` is appropriate.

`status` changes, so `let` is appropriate.

---

# 32. Food Example

```javascript
const foodName = "Chicken Momo";
const price = 180;

let isAvailable = true;

isAvailable = false;

console.log(foodName);
console.log(price);
console.log(isAvailable);
```

The food name and price are not reassigned.

The availability can change.

---

# 33. Order Example

```javascript
const orderId = "ORD-001";

let status = "pending";

status = "confirmed";
status = "preparing";
status = "ready";

console.log(orderId);
console.log(status);
```

Output:

```text
ORD-001
ready
```

This is a practical example of choosing `const` and `let`.

---

# 34. `let` Inside a Loop

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
```

The value of `i` changes during the loop.

Therefore:

```javascript
let i
```

is appropriate.

---

# 35. `const` Inside `for...of`

```javascript
const foods = [
  "Momo",
  "Pizza",
  "Burger"
];

for (const food of foods) {
  console.log(food);
}
```

The variable `food` does not need to be reassigned inside each iteration.

So `const` is appropriate.

---

# 36. `const` Inside `forEach()`

```javascript
const foods = [
  "Momo",
  "Pizza",
  "Burger"
];

foods.forEach((food) => {
  console.log(food);
});
```

The callback parameter behaves like a new binding for each callback invocation.

You do not need to reassign `food`.

---

# 37. Temporal Dead Zone

`let` and `const` are hoisted, but they cannot be accessed before their declaration is executed.

Example:

```javascript
console.log(name);

let name = "Sandip";
```

This causes a `ReferenceError`.

The period between entering the scope and reaching the declaration is called the **Temporal Dead Zone (TDZ)**.

The same applies to `const`:

```javascript
console.log(name);

const name = "Sandip";
```

This also causes a `ReferenceError`.

The TDZ is covered in more detail in:

```text
08-Scope-Hoisting/06-Temporal-Dead-Zone.md
```

---

# 38. `var` and Hoisting Difference

With `var`:

```javascript
console.log(name);

var name = "Sandip";
```

The declaration is hoisted, and the value before assignment is:

```text
undefined
```

With `let` and `const`:

```javascript
console.log(name);

let name = "Sandip";
```

This results in a `ReferenceError` because of the Temporal Dead Zone.

---

# 39. Best Practice

A common modern JavaScript approach is:

```text
Use const by default.
Use let when reassignment is required.
Avoid var in modern code unless there is a specific reason to use it.
```

Example:

```javascript
const name = "Sandip";
const country = "Nepal";

let age = 22;

age = 23;
```

---

# 40. Multiple Declarations

You can declare multiple variables:

```javascript
let firstName = "Sandip";
let lastName = "Kushwaha";
```

You can also write:

```javascript
let firstName = "Sandip",
    lastName = "Kushwaha";
```

However, separate declarations are often easier to read.

---

# 41. Constants With Uppercase Names

For values that represent application-wide constants, uppercase naming is sometimes used:

```javascript
const API_URL = "https://example.com/api";
const MAX_USERS = 100;
```

This is a naming convention, not a JavaScript requirement.

You can also use normal camelCase:

```javascript
const apiUrl = "https://example.com/api";
```

Choose a consistent style for your project.

---

# 42. `const` With Functions

You can store a function in a `const` variable:

```javascript
const greet = () => {
  console.log("Hello");
};

greet();
```

You cannot later assign another function to `greet`:

```javascript
greet = () => {
  console.log("Hi");
};
```

because `greet` is a `const` binding.

---

# 43. `const` With Arrays

```javascript
const numbers = [1, 2, 3];

numbers.push(4);

console.log(numbers);
```

Output:

```text
[1, 2, 3, 4]
```

But:

```javascript
numbers = [5, 6, 7];
```

is not allowed.

---

# 44. `const` With Objects

```javascript
const user = {
  name: "Sandip"
};

user.name = "Ram";

console.log(user.name);
```

Output:

```text
Ram
```

But:

```javascript
user = {
  name: "Ram"
};
```

is not allowed.

---

# 45. Quick Comparison

```text
┌──────────┬──────────────┬──────────────┐
│          │ let          │ const        │
├──────────┼──────────────┼──────────────┤
│ Scope    │ Block        │ Block        │
│ Reassign │ Yes          │ No           │
│ Redeclare│ No           │ No           │
│ Must     │ No           │ Yes          │
│ initialize│             │              │
└──────────┴──────────────┴──────────────┘
```

---

# 46. Common Mistakes

## Mistake 1: Using `const` and then reassigning

```javascript
const age = 22;

age = 23;
```

Use `let` if reassignment is required:

```javascript
let age = 22;

age = 23;
```

---

## Mistake 2: Declaring `const` without a value

```javascript
const name;
```

Use:

```javascript
const name = "Sandip";
```

---

## Mistake 3: Thinking `const` makes objects immutable

```javascript
const user = {
  name: "Sandip"
};

user.name = "Ram";
```

This is allowed.

`const` prevents reassignment of the variable, not normal mutation of the referenced object.

---

## Mistake 4: Using `var` unnecessarily

Modern JavaScript code generally prefers:

```javascript
const
let
```

instead of:

```javascript
var
```

---

# 47. Cheat Sheet

### `let`

```javascript
let age = 22;

age = 23;
```

Use when reassignment is needed.

### `const`

```javascript
const name = "Sandip";
```

Use when reassignment is not needed.

### Block scope

```javascript
{
  let x = 10;
  const y = 20;
}
```

Both are limited to the block.

### Object mutation with `const`

```javascript
const user = {
  name: "Sandip"
};

user.name = "Ram";
```

Allowed.

### Object reassignment with `const`

```javascript
const user = {
  name: "Sandip"
};

user = {};
```

Not allowed.

---

# 48. Key Takeaways

* `let` and `const` were introduced in ES6.
* `let` allows reassignment.
* `const` does not allow reassignment.
* Both are block-scoped.
* `const` must be initialized when declared.
* `let` can be declared without initialization.
* Neither `let` nor `const` can be redeclared in the same scope.
* `const` does not make objects or arrays immutable.
* Object and array properties/elements can still be changed when declared with `const`.
* `let` is useful for values that change.
* `const` is usually preferred for values that do not need reassignment.
* `let` and `const` have a Temporal Dead Zone before their declaration is reached.
* Modern JavaScript generally prefers `const` and `let` over `var`.

---

## Simple Rule

```text
Does the variable need reassignment?
        │
        ├── Yes → let
        │
        └── No  → const
```

Example:

```javascript
const name = "Sandip";

let score = 0;

score = 10;
```

---
