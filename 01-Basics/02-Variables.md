# JavaScript Variables

Variables are used to **store data** in a JavaScript program.

For example:

```javascript
let name = "Sandip";
let age = 22;
```

Here:

* `name` is a variable.
* `age` is a variable.
* `"Sandip"` and `22` are the values stored in those variables.

---

## 1. What is a Variable?

A variable is a named reference to a value.

```javascript
let username = "Sandip";
```

You can think of it as:

```text
username → "Sandip"
```

The value can be used later:

```javascript
console.log(username);
```

Output:

```text
Sandip
```

---

# 2. Declaring Variables

JavaScript provides three keywords for declaring variables:

```javascript
var
let
const
```

Example:

```javascript
var name = "Sandip";
let age = 22;
const country = "Nepal";
```

Modern JavaScript mainly uses:

```javascript
let
const
```

`var` is an older way of declaring variables and is mostly encountered in older JavaScript code.

---

# 3. `let`

`let` is used when the variable's value may change.

```javascript
let age = 22;

age = 23;

console.log(age);
```

Output:

```text
23
```

The value can be reassigned:

```javascript
let city = "Birgunj";

city = "Kathmandu";
```

---

## 4. `const`

`const` is used when a variable should not be reassigned.

```javascript
const country = "Nepal";

console.log(country);
```

You cannot do:

```javascript
const country = "Nepal";

country = "India";
```

This produces an error because the `const` binding cannot be reassigned.

### Important

`const` does **not** make objects or arrays completely immutable.

For example:

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

The object can be mutated, but the variable cannot be reassigned to another object:

```javascript
const user = {
    name: "Sandip"
};

user = {
    name: "Ram"
};
```

This is not allowed.

---

# 5. `var`

`var` is the older way of declaring variables.

```javascript
var name = "Sandip";

name = "Ram";

console.log(name);
```

Output:

```text
Ram
```

`var` allows reassignment and redeclaration.

```javascript
var age = 22;

var age = 23;

console.log(age);
```

Output:

```text
23
```

Because of its scoping behavior, `var` can sometimes cause unexpected bugs.

Modern JavaScript generally prefers:

```javascript
let
const
```

instead of `var`.

---

# 6. `let` vs `const` vs `var`

| Feature                     | `var`         | `let` | `const` |
| --------------------------- | ------------- | ----- | ------- |
| Reassign                    | Yes           | Yes   | No      |
| Redeclare in same scope     | Yes           | No    | No      |
| Block scoped                | No            | Yes   | Yes     |
| Function scoped             | Yes           | Yes   | Yes     |
| Must initialize immediately | No            | No    | Yes     |
| Modern recommendation       | Usually avoid | Yes   | Yes     |

Example:

```javascript
let score = 10;

score = 20;
```

Valid.

```javascript
const score = 10;

score = 20;
```

Error.

---

# 7. Declaration vs Initialization

These are two different concepts.

## Declaration

Creating a variable without assigning a value:

```javascript
let age;
```

The variable exists, but its value is:

```javascript
undefined
```

Example:

```javascript
let age;

console.log(age);
```

Output:

```text
undefined
```

## Initialization

Giving a variable its first value:

```javascript
let age = 22;
```

Here:

```text
Declaration → let age
Initialization → = 22
```

---

# 8. Assignment

Assignment means changing the value stored in a variable.

```javascript
let age = 20;

age = 21;

console.log(age);
```

Output:

```text
21
```

The first assignment:

```javascript
let age = 20;
```

The second assignment:

```javascript
age = 21;
```

---

# 9. Variable Naming Rules

JavaScript variable names must follow certain rules.

### Rule 1: Names can contain letters

```javascript
let name = "Sandip";
```

### Rule 2: Names can contain numbers

```javascript
let user1 = "Sandip";
```

But a variable cannot start with a number:

```javascript
let 1user = "Sandip";
```

Invalid.

---

### Rule 3: Use `_`

Underscores are allowed:

```javascript
let user_name = "Sandip";
```

---

### Rule 4: Use `$`

Dollar signs are also allowed:

```javascript
let $price = 500;
```

---

### Rule 5: Variable names are case-sensitive

These are different variables:

```javascript
let name = "Sandip";
let Name = "Ram";
let NAME = "Hari";
```

JavaScript treats them as three different identifiers.

---

### Rule 6: Do not use reserved keywords

You cannot use keywords such as:

```javascript
let
const
class
function
return
if
else
for
while
```

as variable names.

Invalid:

```javascript
let class = "CSIT";
```

---

# 10. Naming Conventions

JavaScript commonly uses **camelCase**.

```javascript
let firstName = "Sandip";
let lastName = "Kushwaha";
let userAge = 22;
let totalPrice = 500;
```

Avoid unclear names:

```javascript
let x = 22;
let a = "Sandip";
```

Prefer meaningful names:

```javascript
let age = 22;
let userName = "Sandip";
```

Good variable names make code easier to understand.

---

# 11. Multiple Variables

You can declare multiple variables.

```javascript
let firstName = "Sandip";
let age = 22;
let city = "Birgunj";
```

You can also declare multiple variables in one statement:

```javascript
let name = "Sandip",
    age = 22,
    city = "Birgunj";
```

However, separate declarations are usually easier to read.

---

# 12. Reassigning Variables

With `let`:

```javascript
let score = 50;

score = 75;

console.log(score);
```

Output:

```text
75
```

You can change the value multiple times:

```javascript
let count = 0;

count = 1;
count = 2;
count = 3;

console.log(count);
```

Output:

```text
3
```

---

# 13. `const` Cannot Be Reassigned

```javascript
const pi = 3.14159;
```

This is invalid:

```javascript
pi = 3.14;
```

Because `const` variables cannot be reassigned.

---

# 14. `const` with Arrays

This is an important concept.

```javascript
const fruits = ["Apple", "Banana"];
```

You can modify the array:

```javascript
fruits.push("Mango");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

But you cannot replace the entire array:

```javascript
fruits = ["Orange", "Grapes"];
```

This causes an error.

### Remember

```text
const → cannot reassign the variable
```

It does not mean:

```text
const → everything inside the value can never change
```

---

# 15. `const` with Objects

Example:

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

You can modify a property:

```javascript
user.age = 23;
```

You can add a property:

```javascript
user.city = "Birgunj";
```

But you cannot reassign the variable:

```javascript
user = {};
```

---

# 16. Block Scope

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
    let message = "Hello";

    console.log(message);
}
```

This works inside the block.

But:

```javascript
{
    let message = "Hello";
}

console.log(message);
```

The variable is not accessible outside the block.

---

# 17. `var` and Block Scope

`var` is not block-scoped.

```javascript
{
    var message = "Hello";
}

console.log(message);
```

Output:

```text
Hello
```

This is one reason `let` and `const` are generally safer choices.

---

# 18. Function Scope

`var` is function-scoped.

```javascript
function test() {
    var message = "Hello";

    console.log(message);
}

test();
```

The variable exists inside the function.

But:

```javascript
function test() {
    var message = "Hello";
}

console.log(message);
```

This produces an error because `message` is local to the function.

---

# 19. Variable Scope Example

```javascript
let globalName = "Sandip";

function greet() {
    let message = "Hello";

    console.log(globalName);
    console.log(message);
}

greet();
```

Output:

```text
Sandip
Hello
```

The function can access variables from an outer scope.

But the outer scope cannot access variables declared inside the function:

```javascript
function greet() {
    let message = "Hello";
}

console.log(message);
```

Error.

---

# 20. Temporal Dead Zone (TDZ)

Variables declared with `let` and `const` are hoisted, but they cannot be accessed before their declaration.

Example:

```javascript
console.log(age);

let age = 22;
```

This produces a `ReferenceError`.

The period between entering the scope and reaching the declaration is called the **Temporal Dead Zone (TDZ)**.

The same applies to `const`:

```javascript
console.log(country);

const country = "Nepal";
```

Error.

---

# 21. `var` Hoisting

`var` behaves differently.

```javascript
console.log(age);

var age = 22;
```

Output:

```text
undefined
```

Conceptually, JavaScript behaves somewhat like:

```javascript
var age;

console.log(age);

age = 22;
```

This is simplified behavior; JavaScript's actual execution model is more detailed.

---

# 22. Best Practice

For modern JavaScript:

### Use `const` by default

```javascript
const name = "Sandip";
const country = "Nepal";
```

### Use `let` when the value needs to change

```javascript
let score = 0;

score++;
```

### Avoid `var` in new code

```javascript
// Prefer
const name = "Sandip";

// Instead of
var name = "Sandip";
```

---

# 23. Practical Example

```javascript
const userName = "Sandip";
const country = "Nepal";

let age = 22;

age = 23;

console.log(userName);
console.log(country);
console.log(age);
```

Output:

```text
Sandip
Nepal
23
```

---

# 24. Variables with Different Data Types

A JavaScript variable can hold different types of values.

```javascript
let value = "Hello";

value = 100;

value = true;

value = null;

console.log(value);
```

JavaScript is **dynamically typed**, so the type is associated with the value rather than being permanently fixed to the variable.

Example:

```javascript
let data = "Hello";

console.log(typeof data);

data = 100;

console.log(typeof data);

data = true;

console.log(typeof data);
```

Output:

```text
string
number
boolean
```

---

# 25. Quick Revision

```text
Variable
   ↓
Stores a value

var
   ↓
Function scoped
Older JavaScript

let
   ↓
Block scoped
Can be reassigned

const
   ↓
Block scoped
Cannot be reassigned
Must be initialized
```

### Modern JavaScript rule

```javascript
const → default choice
let   → when reassignment is needed
var   → generally avoid in new code
```

---
