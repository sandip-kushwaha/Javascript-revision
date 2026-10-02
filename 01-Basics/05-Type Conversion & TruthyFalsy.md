# JavaScript Type Conversion & Truthy/Falsy

JavaScript often needs to convert values from one data type to another.

For example:

```javascript
const age = "22";

console.log(typeof age);
```

Output:

```text
string
```

We can convert it to a number:

```javascript
const age = Number("22");

console.log(typeof age);
```

Output:

```text
number
```

Understanding type conversion is important when working with:

* Forms
* APIs
* JSON
* Databases
* User input
* Authentication
* Conditions
* Calculations

---

# 1. What is Type Conversion?

**Type conversion** means changing a value from one data type to another.

For example:

```text
String → Number
Number → String
String → Boolean
Boolean → Number
```

There are two major types:

```text
Explicit Conversion
        +
Implicit Conversion
```

---

# 2. Explicit Type Conversion

Explicit conversion happens when you intentionally convert a value.

Common functions include:

```javascript
Number()
String()
Boolean()
```

Example:

```javascript
const value = "100";

const number = Number(value);

console.log(number);
console.log(typeof number);
```

Output:

```text
100
number
```

---

# 3. Converting String to Number

Use `Number()`:

```javascript
const value = "100";

const result = Number(value);

console.log(result);
```

Output:

```text
100
```

Check the type:

```javascript
console.log(typeof result);
```

Output:

```text
number
```

---

# 4. `Number()` Conversion Examples

```javascript
console.log(Number("100"));
console.log(Number("10.5"));
console.log(Number(true));
console.log(Number(false));
console.log(Number(null));
```

Output:

```text
100
10.5
1
0
0
```

---

# 5. Converting an Empty String

An empty string converts to `0` using `Number()`:

```javascript
console.log(Number(""));
```

Output:

```text
0
```

Whitespace-only strings also become `0`:

```javascript
console.log(Number("   "));
```

Output:

```text
0
```

---

# 6. Invalid Number Conversion

If a string cannot be converted into a valid number:

```javascript
console.log(Number("Hello"));
```

Output:

```text
NaN
```

Example:

```javascript
const price = Number("abc");

console.log(price);
console.log(Number.isNaN(price));
```

Output:

```text
NaN
true
```

---

# 7. `Number()` vs `parseInt()`

These are not exactly the same.

```javascript
console.log(Number("42px"));
```

Output:

```text
NaN
```

But:

```javascript
console.log(parseInt("42px", 10));
```

Output:

```text
42
```

`parseInt()` reads an integer from the beginning of a string until it reaches a character that cannot be part of the number.

For modern code, include the radix:

```javascript
parseInt(value, 10);
```

---

# 8. `parseFloat()`

`parseFloat()` parses a floating-point number.

```javascript
console.log(parseFloat("10.50"));
```

Output:

```text
10.5
```

Example:

```javascript
console.log(parseFloat("10.50px"));
```

Output:

```text
10.5
```

---

# 9. `parseInt()`

`parseInt()` returns an integer.

```javascript
console.log(parseInt("100", 10));
```

Output:

```text
100
```

Decimal part is removed:

```javascript
console.log(parseInt("10.99", 10));
```

Output:

```text
10
```

---

# 10. String to Number Summary

| Method         | Example               | Result |
| -------------- | --------------------- | -----: |
| `Number()`     | `Number("100")`       |  `100` |
| `parseInt()`   | `parseInt("100", 10)` |  `100` |
| `parseFloat()` | `parseFloat("10.5")`  | `10.5` |

---

# 11. Converting Number to String

Use `String()`:

```javascript
const number = 100;

const value = String(number);

console.log(value);
console.log(typeof value);
```

Output:

```text
100
string
```

---

# 12. `String()` Conversion Examples

```javascript
console.log(String(100));
console.log(String(true));
console.log(String(false));
console.log(String(null));
console.log(String(undefined));
```

Output:

```text
100
true
false
null
undefined
```

All results are strings.

---

# 13. `toString()`

Numbers can also be converted using `.toString()`:

```javascript
const number = 100;

const value = number.toString();

console.log(value);
console.log(typeof value);
```

Output:

```text
100
string
```

Be careful with `null` and `undefined`:

```javascript
const value = null;

value.toString();
```

This causes an error because `null` does not have a `toString()` method.

`String(value)` is safer for general-purpose explicit conversion.

---

# 14. Converting Boolean to Number

```javascript
console.log(Number(true));
console.log(Number(false));
```

Output:

```text
1
0
```

So:

```text
true  → 1
false → 0
```

---

# 15. Converting Number to Boolean

```javascript
console.log(Boolean(1));
console.log(Boolean(0));
```

Output:

```text
true
false
```

---

# 16. Converting String to Boolean

```javascript
console.log(Boolean("Hello"));
console.log(Boolean(""));
```

Output:

```text
true
false
```

An important point:

```javascript
Boolean("false");
```

returns:

```text
true
```

Why?

Because `"false"` is a **non-empty string**, and non-empty strings are truthy.

---

# 17. Boolean Conversion

The general rule is:

```javascript
Boolean(value)
```

converts a value into either:

```text
true
```

or:

```text
false
```

Example:

```javascript
console.log(Boolean("Hello"));
console.log(Boolean(100));
console.log(Boolean(true));
```

Output:

```text
true
true
true
```

---

# 18. Truthy and Falsy Values

JavaScript values can be classified as:

```text
Truthy
Falsy
```

A **truthy** value behaves like `true` in a Boolean context.

A **falsy** value behaves like `false`.

Example:

```javascript
if ("Hello") {
    console.log("Truthy");
}
```

Output:

```text
Truthy
```

---

# 19. Falsy Values

The main JavaScript falsy values are:

```text
false
0
-0
0n
""
null
undefined
NaN
```

These values become `false` when converted to Boolean.

Example:

```javascript
console.log(Boolean(false));
console.log(Boolean(0));
console.log(Boolean(""));
console.log(Boolean(null));
console.log(Boolean(undefined));
console.log(Boolean(NaN));
```

Output:

```text
false
false
false
false
false
false
```

---

# 20. Truthy Values

Almost everything else is truthy.

Examples:

```javascript
Boolean("Hello");   // true
Boolean("0");       // true
Boolean(100);       // true
Boolean(-10);       // true
Boolean([]);        // true
Boolean({});        // true
```

---

# 21. Empty String vs Empty Array

This is a common interview question.

An empty string is falsy:

```javascript
console.log(Boolean(""));
```

Output:

```text
false
```

But an empty array is truthy:

```javascript
console.log(Boolean([]));
```

Output:

```text
true
```

Similarly, an empty object is truthy:

```javascript
console.log(Boolean({}));
```

Output:

```text
true
```

Remember:

```text
""  → falsy
[]  → truthy
{}  → truthy
```

---

# 22. Checking Truthiness with `if`

Instead of:

```javascript
const username = "";

if (username === "") {
    console.log("No username");
}
```

You can often write:

```javascript
const username = "";

if (!username) {
    console.log("No username");
}
```

Output:

```text
No username
```

This works because an empty string is falsy.

---

# 23. `if` with Truthy Value

```javascript
const username = "Sandip";

if (username) {
    console.log("Username exists");
}
```

Output:

```text
Username exists
```

Because `"Sandip"` is truthy.

---

# 24. Double NOT `!!`

The `!!` operator is commonly used to convert a value to Boolean.

```javascript
console.log(!!"Hello");
```

Output:

```text
true
```

```javascript
console.log(!!0);
```

Output:

```text
false
```

Example:

```javascript
const username = "Sandip";

console.log(!!username);
```

Output:

```text
true
```

---

# 25. Implicit Type Conversion

Implicit conversion happens automatically when JavaScript needs to convert a value during an operation.

Example:

```javascript
console.log("10" + 5);
```

Output:

```text
105
```

The number `5` is converted to a string.

---

# 26. String Concatenation

The `+` operator behaves differently when strings are involved.

```javascript
console.log("10" + 5);
```

Result:

```text
"105"
```

But:

```javascript
console.log("10" - 5);
```

Result:

```text
5
```

The `-` operator performs numeric conversion.

---

# 27. More Implicit Conversion Examples

```javascript
console.log("10" * 2);
console.log("10" / 2);
console.log("10" - 2);
```

Output:

```text
20
5
8
```

JavaScript converts the string `"10"` into a number for these numeric operations.

---

# 28. `+` Is Special

Consider:

```javascript
console.log("5" + 2);
```

Output:

```text
52
```

But:

```javascript
console.log("5" - 2);
```

Output:

```text
3
```

This happens because `+` can mean both:

```text
Addition
+
String concatenation
```

Other arithmetic operators such as `-`, `*`, and `/` generally perform numeric conversion.

---

# 29. Boolean Implicit Conversion

In conditions, JavaScript automatically converts values to Boolean.

```javascript
const username = "Sandip";

if (username) {
    console.log("User exists");
}
```

The string is truthy, so the condition succeeds.

Another example:

```javascript
const username = "";

if (username) {
    console.log("User exists");
} else {
    console.log("User does not exist");
}
```

Output:

```text
User does not exist
```

---

# 30. `null` and `undefined` in Conversion

```javascript
console.log(Number(null));
console.log(Number(undefined));
```

Output:

```text
0
NaN
```

This difference is important.

Also:

```javascript
console.log(Boolean(null));
console.log(Boolean(undefined));
```

Output:

```text
false
false
```

---

# 31. Arithmetic with `null`

JavaScript can convert `null` to `0` in numeric operations.

```javascript
console.log(null + 1);
```

Output:

```text
1
```

But:

```javascript
console.log(undefined + 1);
```

Output:

```text
NaN
```

This is one reason explicit conversion is often easier to understand.

---

# 32. Equality and Type Conversion

Loose equality `==` can perform type conversion.

```javascript
console.log(5 == "5");
```

Output:

```text
true
```

Strict equality `===` does not perform the same kind of coercion:

```javascript
console.log(5 === "5");
```

Output:

```text
false
```

### Best Practice

Prefer:

```javascript
===
```

and:

```javascript
!==
```

when you want predictable comparisons.

---

# 33. Common Conversion Table

| Value       | `Number()` | `String()`    | `Boolean()` |
| ----------- | ---------: | ------------- | ----------: |
| `"10"`      |       `10` | `"10"`        |      `true` |
| `""`        |        `0` | `""`          |     `false` |
| `"Hello"`   |      `NaN` | `"Hello"`     |      `true` |
| `true`      |        `1` | `"true"`      |      `true` |
| `false`     |        `0` | `"false"`     |     `false` |
| `null`      |        `0` | `"null"`      |     `false` |
| `undefined` |      `NaN` | `"undefined"` |     `false` |
| `0`         |        `0` | `"0"`         |     `false` |
| `1`         |        `1` | `"1"`         |      `true` |

---

# 34. User Input and Type Conversion

HTML form values are commonly received as strings.

For example:

```javascript
const quantity = "5";
const price = "100";
```

If you do:

```javascript
console.log(quantity + price);
```

You get:

```text
5100
```

because both values are strings.

Convert them first:

```javascript
const quantity = Number("5");
const price = Number("100");

console.log(quantity * price);
```

Output:

```text
500
```

This is extremely important when working with forms and APIs.

---

# 35. API Data and Type Conversion

Suppose an API returns:

```javascript
const response = {
    price: "499",
    quantity: "2"
};
```

If you need to calculate the total:

```javascript
const total =
    Number(response.price) *
    Number(response.quantity);

console.log(total);
```

Output:

```text
998
```

---

# 36. `||` and Truthy/Falsy

The `||` operator returns the first truthy operand.

```javascript
const username = "";

const displayName = username || "Guest";

console.log(displayName);
```

Output:

```text
Guest
```

Because:

```text
"" → falsy
```

So JavaScript uses `"Guest"`.

---

# 37. `??` and Nullish Values

`??` only checks:

```text
null
undefined
```

Example:

```javascript
const username = null;

const displayName = username ?? "Guest";

console.log(displayName);
```

Output:

```text
Guest
```

But:

```javascript
const username = "";

const displayName = username ?? "Guest";

console.log(displayName);
```

Output:

```text
""
```

Because an empty string is not nullish.

---

# 38. `||` vs `??`

This difference is very important.

```javascript
const count = 0;

console.log(count || 10);
```

Output:

```text
10
```

But:

```javascript
console.log(count ?? 10);
```

Output:

```text
0
```

Use:

```javascript
||
```

when you want a fallback for any falsy value.

Use:

```javascript
??
```

when you want a fallback only for `null` or `undefined`.

---

# 39. Practical Example — Login

```javascript
const username = "Sandip";
const password = "";

if (username && password) {
    console.log("Login allowed");
} else {
    console.log("Username and password are required");
}
```

Output:

```text
Username and password are required
```

Why?

```text
username → truthy
password → falsy
```

With `&&`, both conditions need to be truthy.

---

# 40. Practical Example — Hotel Booking

```javascript
const customerName = "Sandip";
const customerCount = 4;
const tableCapacity = 6;

if (customerName && customerCount <= tableCapacity) {
    console.log("Table can be booked");
} else {
    console.log("Table cannot be booked");
}
```

Output:

```text
Table can be booked
```

---

# 41. Practical Example — Default Value

```javascript
const customerName = "";

const displayName = customerName || "Guest";

console.log(displayName);
```

Output:

```text
Guest
```

Using nullish coalescing:

```javascript
const customerName = "";

const displayName = customerName ?? "Guest";

console.log(displayName);
```

Output:

```text
""
```

The difference matters when an empty string is a valid value.

---

# 42. Explicit vs Implicit Conversion

## Explicit

You intentionally convert:

```javascript
const age = Number("22");
```

This is usually easier to understand.

## Implicit

JavaScript converts automatically:

```javascript
console.log("22" * 2);
```

Output:

```text
44
```

---

# 43. Best Practices

### Prefer explicit conversion when the intent matters

Instead of relying on:

```javascript
const total = price * quantity;
```

when you know API/form values are strings, use:

```javascript
const total =
    Number(price) *
    Number(quantity);
```

### Prefer strict equality

Use:

```javascript
===
!==
```

instead of relying on:

```javascript
==
!=
```

### Understand truthiness

Know which values are falsy before writing conditions.

### Use `??` when zero, false, or empty string should remain valid

Example:

```javascript
const quantity = 0;

const result = quantity ?? 1;

console.log(result);
```

Output:

```text
0
```

---

# 44. Quick Revision

```text
Type Conversion
       │
       ├── Explicit
       │   ├── Number()
       │   ├── String()
       │   └── Boolean()
       │
       └── Implicit
           └── JavaScript converts automatically
```

---

## Falsy Values

```text
false
0
-0
0n
""
null
undefined
NaN
```

## Truthy Values

Examples:

```text
"Hello"
"0"
100
-10
[]
{}
function(){}
```

Remember:

```text
""  → falsy
[]  → truthy
{}  → truthy
```

---
# 45. Final Cheat Sheet

```javascript
// String → Number
Number("100");              // 100

// String → Integer
parseInt("100", 10);        // 100

// String → Decimal
parseFloat("10.5");         // 10.5

// Number → String
String(100);                // "100"

// Number → Boolean
Boolean(1);                 // true
Boolean(0);                 // false

// String → Boolean
Boolean("Hello");           // true
Boolean("");                // false

// Null → Number
Number(null);               // 0

// Undefined → Number
Number(undefined);          // NaN

// Truthy / Falsy
Boolean([]);                // true
Boolean({});                // true
Boolean("");                // false

// Loose equality
5 == "5";                   // true

// Strict equality
5 === "5";                  // false

// OR fallback
0 || 10;                    // 10

// Nullish fallback
0 ?? 10;                    // 0
null ?? 10;                 // 10
```

---

# Key Takeaways

* Type conversion changes a value from one type to another.
* Explicit conversion uses functions such as `Number()`, `String()`, and `Boolean()`.
* Implicit conversion happens automatically.
* `Number("100")` produces `100`.
* `String(100)` produces `"100"`.
* `Boolean(1)` is `true`; `Boolean(0)` is `false`.
* `Number("Hello")` produces `NaN`.
* `parseInt("42px", 10)` produces `42`, while `Number("42px")` produces `NaN`.
* The main falsy values are `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, and `NaN`.
* Empty arrays and objects are truthy.
* Prefer `===` and `!==` for predictable equality checks.
* `||` falls back for any falsy value.
* `??` falls back only for `null` and `undefined`.
* Explicit conversion is often clearer than relying on implicit conversion.
