# JavaScript Data Types

A **data type** tells JavaScript what kind of value a variable contains.

For example:

```javascript
let name = "Sandip";
let age = 22;
let isStudent = true;
```

Here:

* `"Sandip"` → `String`
* `22` → `Number`
* `true` → `Boolean`

JavaScript is a **dynamically typed language**, which means a variable can hold values of different types during its lifetime.

```javascript
let value = "Hello";

value = 100;

value = true;
```

---

# 1. Types of JavaScript Data Types

JavaScript data types are commonly divided into two categories:

```text
Primitive Data Types
        +
Non-Primitive / Reference Types
```

## Primitive Types

JavaScript has 7 primitive data types:

| Type      | Example        |
| --------- | -------------- |
| String    | `"Hello"`      |
| Number    | `100`          |
| BigInt    | `100n`         |
| Boolean   | `true`         |
| Undefined | `undefined`    |
| Null      | `null`         |
| Symbol    | `Symbol("id")` |

## Non-Primitive / Reference Types

Common reference types include:

* Object
* Array
* Function
* Date
* Map
* Set
* and other objects

---

# 2. String

A string represents text.

Strings can be written using:

* Single quotes `'`
* Double quotes `"`
* Backticks `` ` ``

Example:

```javascript
let firstName = "Sandip";
let lastName = 'Kushwaha';
let message = `Hello`;
```

You can check the type using `typeof`:

```javascript
console.log(typeof firstName);
```

Output:

```text
string
```

---

## String Example

```javascript
let name = "Sandip";

console.log(name);
console.log(typeof name);
```

Output:

```text
Sandip
string
```

---

## String with Numbers

```javascript
let age = 22;

let message = "My age is " + age;

console.log(message);
```

Output:

```text
My age is 22
```

---

# 3. Number

The `number` type represents both integers and floating-point numbers.

```javascript
let age = 22;
let price = 499.99;
let temperature = -5;
```

All of these are `number`.

```javascript
console.log(typeof age);
console.log(typeof price);
```

Output:

```text
number
number
```

---

## Positive and Negative Numbers

```javascript
let positive = 100;
let negative = -100;
```

---

## Decimal Numbers

```javascript
let price = 99.99;
let rating = 4.5;
```

---

## Special Number Values

JavaScript numbers also include special values such as:

```javascript
Infinity
-Infinity
NaN
```

Example:

```javascript
console.log(10 / 0);
```

Output:

```text
Infinity
```

---

# 4. NaN

`NaN` means **Not-a-Number**.

It represents an invalid or unsuccessful numeric result.

Example:

```javascript
console.log("Hello" * 5);
```

Output:

```text
NaN
```

However, an important fact is:

```javascript
console.log(typeof NaN);
```

Output:

```text
number
```

So:

```text
NaN → special numeric value
```

You can check for `NaN` using:

```javascript
Number.isNaN(value);
```

Example:

```javascript
console.log(Number.isNaN(NaN));
```

Output:

```text
true
```

---

# 5. BigInt

`BigInt` is used for integers larger than the safe range of JavaScript's `Number` type.

A BigInt literal ends with `n`.

```javascript
let bigNumber = 123456789012345678901234567890n;

console.log(bigNumber);
console.log(typeof bigNumber);
```

Output:

```text
123456789012345678901234567890n
bigint
```

---

## BigInt Arithmetic

```javascript
let a = 100n;
let b = 200n;

console.log(a + b);
```

Output:

```text
300n
```

Do not directly mix `BigInt` and `Number` in arithmetic:

```javascript
let a = 10n;
let b = 5;

console.log(a + b);
```

This causes a `TypeError`.

Convert explicitly when needed:

```javascript
console.log(a + BigInt(b));
```

---

# 6. Boolean

A Boolean has only two values:

```javascript
true
false
```

Example:

```javascript
let isLoggedIn = true;
let isAdmin = false;
```

Check the type:

```javascript
console.log(typeof isLoggedIn);
```

Output:

```text
boolean
```

---

## Boolean Example

```javascript
let age = 22;

let isAdult = age >= 18;

console.log(isAdult);
```

Output:

```text
true
```

Boolean values are commonly used in:

* Conditions
* Authentication
* Validation
* Loops
* Permissions
* Application state

---

# 7. Undefined

`undefined` usually means a variable has been declared but has not been assigned a value.

```javascript
let name;

console.log(name);
```

Output:

```text
undefined
```

Check its type:

```javascript
console.log(typeof name);
```

Output:

```text
undefined
```

---

## Function Returning Undefined

A function that does not explicitly return a value returns `undefined`.

```javascript
function greet() {
    console.log("Hello");
}

let result = greet();

console.log(result);
```

Output:

```text
Hello
undefined
```

---

# 8. Null

`null` represents an intentional absence of a value.

```javascript
let selectedUser = null;
```

This means:

```text
There is intentionally no selected user.
```

Example:

```javascript
let currentUser = null;

console.log(currentUser);
```

Output:

```text
null
```

---

## `typeof null`

There is a famous JavaScript behavior:

```javascript
console.log(typeof null);
```

Output:

```text
object
```

This is a historical JavaScript behavior and is generally considered a language quirk.

It does **not** mean that `null` is actually an object.

---

# 9. Undefined vs Null

These values are different.

| `undefined`                              | `null`                       |
| ---------------------------------------- | ---------------------------- |
| Usually means no value has been assigned | Intentional absence of value |
| Often appears automatically              | Usually assigned explicitly  |
| `typeof` → `"undefined"`                 | `typeof` → `"object"`        |
| Example: `let x;`                        | Example: `let x = null;`     |

Example:

```javascript
let a;
let b = null;

console.log(a);
console.log(b);
```

Output:

```text
undefined
null
```

---

# 10. Symbol

`Symbol` creates a unique primitive value.

Example:

```javascript
const id = Symbol("id");

console.log(id);
console.log(typeof id);
```

Output:

```text
Symbol(id)
symbol
```

Even two Symbols with the same description are different:

```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");

console.log(id1 === id2);
```

Output:

```text
false
```

Symbols are commonly used when you need unique property keys.

Example:

```javascript
const userId = Symbol("userId");

const user = {
    name: "Sandip",
    [userId]: 101
};

console.log(user.name);
console.log(user[userId]);
```

---

# 11. Object

An object stores data in **key-value pairs**.

```javascript
const user = {
    name: "Sandip",
    age: 22,
    country: "Nepal"
};
```

Here:

```text
name    → "Sandip"
age     → 22
country → "Nepal"
```

Access properties:

```javascript
console.log(user.name);
console.log(user.age);
```

Output:

```text
Sandip
22
```

Check the type:

```javascript
console.log(typeof user);
```

Output:

```text
object
```

---

# 12. Array

An array stores multiple values in an ordered collection.

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango"
];
```

Access values using indexes:

```javascript
console.log(fruits[0]);
console.log(fruits[1]);
```

Output:

```text
Apple
Banana
```

Array indexes start from `0`.

```text
Apple  → 0
Banana → 1
Mango  → 2
```

---

## Array Type

An array is technically an object in JavaScript.

```javascript
console.log(typeof fruits);
```

Output:

```text
object
```

To correctly check whether a value is an array, use:

```javascript
Array.isArray(fruits);
```

Output:

```text
true
```

---

# 13. Function

Functions are objects in JavaScript, but `typeof` provides a special result for them.

```javascript
function greet() {
    console.log("Hello");
}
```

Check the type:

```javascript
console.log(typeof greet);
```

Output:

```text
function
```

Functions can be stored in variables:

```javascript
const greet = function () {
    console.log("Hello");
};
```

They can also be passed to other functions and returned from functions.

---

# 14. Primitive vs Reference Values

A useful distinction is between **primitive values** and **objects/reference values**.

### Primitive values

```text
string
number
bigint
boolean
undefined
null
symbol
```

### Reference values

Common examples:

```text
object
array
function
date
map
set
```

---

# 15. Primitive Values Are Immutable

Primitive values themselves cannot be modified.

For example:

```javascript
let message = "Hello";

message[0] = "Y";

console.log(message);
```

The original string is not changed.

Instead, you create a new string:

```javascript
message = "Yellow";
```

The variable now refers to a different string value.

---

# 16. Objects Are Mutable

Objects can have their properties changed.

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

This is why:

```javascript
const user = {};
```

does not mean the object itself is immutable.

It means the variable `user` cannot be reassigned to another object.

---

# 17. Dynamic Typing

JavaScript is dynamically typed.

This means a variable can hold different types of values.

```javascript
let value = "Hello";

console.log(typeof value);

value = 100;

console.log(typeof value);

value = true;

console.log(typeof value);
```

Output:

```text
string
number
boolean
```

The variable itself does not have a permanently fixed type.

---

# 18. `typeof` Operator

The `typeof` operator tells you the type of a value.

Examples:

```javascript
console.log(typeof "Hello");
console.log(typeof 100);
console.log(typeof true);
console.log(typeof undefined);
console.log(typeof 100n);
console.log(typeof Symbol("id"));
```

Output:

```text
string
number
boolean
undefined
bigint
symbol
```

For objects:

```javascript
console.log(typeof {});
```

Output:

```text
object
```

For arrays:

```javascript
console.log(typeof []);
```

Output:

```text
object
```

For functions:

```javascript
console.log(typeof function () {});
```

Output:

```text
function
```

---

# 19. `typeof` Quick Reference

| Value          | `typeof` Result |
| -------------- | --------------- |
| `"Hello"`      | `"string"`      |
| `100`          | `"number"`      |
| `100n`         | `"bigint"`      |
| `true`         | `"boolean"`     |
| `undefined`    | `"undefined"`   |
| `null`         | `"object"`      |
| `Symbol()`     | `"symbol"`      |
| `{}`           | `"object"`      |
| `[]`           | `"object"`      |
| `function(){}` | `"function"`    |

Remember:

```javascript
typeof null === "object"
```

This is a historical quirk.

---

# 20. Checking for an Array

Do not use:

```javascript
typeof [];
```

because it returns:

```text
object
```

Use:

```javascript
Array.isArray([]);
```

Example:

```javascript
const fruits = ["Apple", "Banana"];

console.log(Array.isArray(fruits));
```

Output:

```text
true
```

---

# 21. Type Checking Example

```javascript
const name = "Sandip";
const age = 22;
const isStudent = true;
const skills = ["JavaScript", "React"];
const user = {
    name: "Sandip"
};

console.log(typeof name);
console.log(typeof age);
console.log(typeof isStudent);
console.log(Array.isArray(skills));
console.log(typeof user);
```

Output:

```text
string
number
boolean
true
object
```

---

# 22. Common Data Type Examples

```javascript
// String
const name = "Sandip";

// Number
const age = 22;

// BigInt
const bigNumber = 12345678901234567890n;

// Boolean
const isStudent = true;

// Undefined
let address;

// Null
const selectedUser = null;

// Symbol
const id = Symbol("id");

// Object
const user = {
    name: "Sandip",
    age: 22
};

// Array
const skills = [
    "JavaScript",
    "React",
    "Node.js"
];

// Function
const greet = () => {
    console.log("Hello");
};
```

---

# 23. Important Comparison

```javascript
console.log(typeof "100");
console.log(typeof 100);
```

Output:

```text
string
number
```

Even though both visually contain `100`, they are different types.

```javascript
"100"
```

is a string.

```javascript
100
```

is a number.

---

# 24. Another Important Example

HTML form inputs commonly provide values as strings.

For example, if an input contains:

```text
22
```

JavaScript may receive:

```javascript
const age = "22";
```

Its type is:

```javascript
console.log(typeof age);
```

Output:

```text
string
```

If you need a number, convert it explicitly:

```javascript
const age = Number("22");

console.log(typeof age);
```

Output:

```text
number
```

---

# 25. Data Types in Real Applications

In a Hotel Management System, you might have:

```javascript
const hotelTable = {
    tableNumber: "T-03",
    capacity: 6,
    isAvailable: true,
    location: "rooftop",
    currentCustomer: null
};
```

Data types:

| Property          | Value       | Type    |
| ----------------- | ----------- | ------- |
| `tableNumber`     | `"T-03"`    | String  |
| `capacity`        | `6`         | Number  |
| `isAvailable`     | `true`      | Boolean |
| `location`        | `"rooftop"` | String  |
| `currentCustomer` | `null`      | Null    |

This is how different data types are used together in real applications.

---

# 26. Quick Revision

```text
JavaScript Data Types
        │
        ├── Primitive
        │   ├── String
        │   ├── Number
        │   ├── BigInt
        │   ├── Boolean
        │   ├── Undefined
        │   ├── Null
        │   └── Symbol
        │
        └── Reference / Object
            ├── Object
            ├── Array
            ├── Function
            ├── Date
            ├── Map
            └── Set
```

---

# Key Takeaways

* JavaScript has **primitive** and **reference/object** values.
* The 7 primitive types are `String`, `Number`, `BigInt`, `Boolean`, `Undefined`, `Null`, and `Symbol`.
* Objects, arrays, and functions are commonly treated as reference/object values.
* JavaScript is dynamically typed.
* `typeof` is useful for checking value types.
* `typeof null` returns `"object"` because of a historical language quirk.
* `typeof []` returns `"object"`; use `Array.isArray()` for arrays.
* `NaN` has the type `"number"`.
* `const` objects and arrays can still be mutated.
* `null` usually represents intentional absence of a value.
* `undefined` commonly represents an unassigned value.
