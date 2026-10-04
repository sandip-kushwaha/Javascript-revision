# JavaScript Math

The JavaScript `Math` object provides built-in methods and constants for mathematical calculations.

It is commonly used for:

* Calculations
* Rounding numbers
* Finding minimum and maximum values
* Generating random numbers
* Working with percentages
* Pagination
* IDs and random values
* UI calculations
* Game logic

---

# 1. Math Object

`Math` is a built-in JavaScript object.

Example:

```javascript
console.log(Math.PI);
```

Output:

```text
3.141592653589793
```

You do not create a `Math` object:

```javascript
new Math(); // Error
```

Use it directly:

```javascript
Math.round();
Math.floor();
Math.random();
```

---

# 2. Math Constants

JavaScript provides several mathematical constants.

## `Math.PI`

Represents π.

```javascript
console.log(Math.PI);
```

Approximately:

```text
3.141592653589793
```

Example:

```javascript
const radius = 5;

const area = Math.PI * radius * radius;

console.log(area);
```

---

## `Math.E`

Euler's number.

```javascript
console.log(Math.E);
```

Approximately:

```text
2.718281828459045
```

---

## `Math.SQRT2`

Square root of 2.

```javascript
console.log(Math.SQRT2);
```

---

## `Math.SQRT1_2`

Square root of 1/2.

```javascript
console.log(Math.SQRT1_2);
```

---

# 3. `Math.round()`

Rounds a number to the nearest integer.

```javascript
console.log(Math.round(4.4));
```

Output:

```text
4
```

```javascript
console.log(Math.round(4.6));
```

Output:

```text
5
```

Exactly `.5` rounds toward positive infinity:

```javascript
console.log(Math.round(4.5));
// 5
```

For negative values:

```javascript
console.log(Math.round(-4.5));
// -4
```

---

# 4. `Math.floor()`

Rounds down toward negative infinity.

```javascript
console.log(Math.floor(4.9));
```

Output:

```text
4
```

Important with negative numbers:

```javascript
console.log(Math.floor(-4.1));
```

Output:

```text
-5
```

Because `-5` is lower than `-4.1`.

---

# 5. `Math.ceil()`

Rounds up toward positive infinity.

```javascript
console.log(Math.ceil(4.1));
```

Output:

```text
5
```

For negative values:

```javascript
console.log(Math.ceil(-4.9));
```

Output:

```text
-4
```

---

# 6. `Math.trunc()`

Removes the decimal part without rounding.

```javascript
console.log(Math.trunc(4.9));
```

Output:

```text
4
```

Negative example:

```javascript
console.log(Math.trunc(-4.9));
```

Output:

```text
-4
```

Comparison:

```text
Math.floor(4.9) → 4
Math.ceil(4.9)  → 5
Math.round(4.9) → 5
Math.trunc(4.9) → 4
```

---

# 7. Rounding Comparison

```javascript
const value = 4.7;

console.log(Math.floor(value));
console.log(Math.ceil(value));
console.log(Math.round(value));
console.log(Math.trunc(value));
```

Result:

```text
4
5
5
4
```

Use:

```text
floor  → down
ceil   → up
round  → nearest integer
trunc  → remove decimal
```

---

# 8. `Math.abs()`

Returns the absolute value.

```javascript
console.log(Math.abs(10));
```

Output:

```text
10
```

Negative:

```javascript
console.log(Math.abs(-10));
```

Output:

```text
10
```

Useful for calculating differences:

```javascript
const difference = Math.abs(100 - 75);

console.log(difference);
```

Output:

```text
25
```

---

# 9. `Math.max()`

Returns the largest value.

```javascript
console.log(
    Math.max(10, 20, 5, 30)
);
```

Output:

```text
30
```

---

# 10. `Math.min()`

Returns the smallest value.

```javascript
console.log(
    Math.min(10, 20, 5, 30)
);
```

Output:

```text
5
```

---

# 11. Using `Math.max()` with Arrays

`Math.max()` does not directly accept an array.

This does not work as expected:

```javascript
const numbers = [10, 20, 30];

Math.max(numbers);
```

Use spread:

```javascript
const numbers = [10, 20, 30];

console.log(
    Math.max(...numbers)
);
```

Output:

```text
30
```

Similarly:

```javascript
console.log(
    Math.min(...numbers)
);
```

Output:

```text
10
```

---

# 12. `Math.pow()`

Returns a number raised to a power.

```javascript
console.log(
    Math.pow(2, 3)
);
```

Output:

```text
8
```

Modern JavaScript can use the exponentiation operator:

```javascript
console.log(2 ** 3);
```

Output:

```text
8
```

Generally prefer:

```javascript
2 ** 3
```

for simple exponentiation.

---

# 13. `Math.sqrt()`

Returns the square root.

```javascript
console.log(
    Math.sqrt(25)
);
```

Output:

```text
5
```

Example:

```javascript
const number = 81;

const result = Math.sqrt(number);

console.log(result);
```

---

# 14. `Math.cbrt()`

Returns the cube root.

```javascript
console.log(
    Math.cbrt(27)
);
```

Output:

```text
3
```

---

# 15. `Math.sign()`

Returns the sign of a number.

Possible results:

```text
1
-1
0
-0
NaN
```

Examples:

```javascript
console.log(Math.sign(10));
// 1

console.log(Math.sign(-10));
// -1

console.log(Math.sign(0));
// 0
```

---

# 16. `Math.random()`

Returns a pseudo-random number between:

```text
0 inclusive
1 exclusive
```

Example:

```javascript
console.log(Math.random());
```

Possible output:

```text
0.3849271
```

It will never return exactly `1`.

---

# 17. Random Integer from 0 to 9

```javascript
const number = Math.floor(
    Math.random() * 10
);

console.log(number);
```

Possible values:

```text
0
1
2
3
4
5
6
7
8
9
```

---

# 18. Random Integer from 1 to 10

```javascript
const number =
    Math.floor(Math.random() * 10) + 1;

console.log(number);
```

Possible values:

```text
1
2
3
...
10
```

---

# 19. Random Integer Between Two Numbers

A reusable function:

```javascript
function randomInteger(min, max) {
    return Math.floor(
        Math.random() * (max - min + 1)
    ) + min;
}
```

Example:

```javascript
console.log(
    randomInteger(1, 100)
);
```

Possible values:

```text
1 through 100
```

The formula is:

```text
Math.floor(
    Math.random() * (max - min + 1)
) + min
```

---

# 20. Random Array Element

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];

const randomFruit =
    fruits[
        Math.floor(
            Math.random() * fruits.length
        )
    ];

console.log(randomFruit);
```

This selects one random element from the array.

---

# 21. Random Color

```javascript
function randomColor() {
    const number = Math.floor(
        Math.random() * 16777216
    );

    return `#${number
        .toString(16)
        .padStart(6, "0")}`;
}

console.log(randomColor());
```

This can generate values such as:

```text
#4a7bc2
#ff2098
#12aa45
```

For security-sensitive tokens, passwords, or authentication values, do not use `Math.random()`.

---

# 22. `Math.log()`

Returns the natural logarithm.

```javascript
console.log(
    Math.log(Math.E)
);
```

Output:

```text
1
```

---

# 23. `Math.log10()`

Returns the base-10 logarithm.

```javascript
console.log(
    Math.log10(100)
);
```

Output:

```text
2
```

Because:

```text
10² = 100
```

---

# 24. `Math.log2()`

Returns the base-2 logarithm.

```javascript
console.log(
    Math.log2(8)
);
```

Output:

```text
3
```

Because:

```text
2³ = 8
```

---

# 25. `Math.exp()`

Returns Euler's number raised to a power.

```javascript
console.log(
    Math.exp(1)
);
```

This is approximately:

```text
2.718281828459045
```

because:

```text
e¹ = e
```

---

# 26. Trigonometric Methods

JavaScript provides trigonometric functions:

```javascript
Math.sin();
Math.cos();
Math.tan();
```

Example:

```javascript
console.log(
    Math.sin(0)
);
```

Output:

```text
0
```

These methods use radians, not degrees.

---

# 27. Degrees to Radians

To convert degrees to radians:

```javascript
const degrees = 90;

const radians =
    degrees * Math.PI / 180;

console.log(radians);
```

Output:

```text
1.5707963267948966
```

---

# 28. Radians to Degrees

```javascript
const radians = Math.PI;

const degrees =
    radians * 180 / Math.PI;

console.log(degrees);
```

Output:

```text
180
```

---

# 29. `Math.hypot()`

Returns the square root of the sum of squares.

```javascript
console.log(
    Math.hypot(3, 4)
);
```

Output:

```text
5
```

This is useful for calculating distance:

```text
√(3² + 4²) = 5
```

---

# 30. `Math.clz32()`

Counts leading zero bits in the 32-bit representation of a number.

```javascript
console.log(
    Math.clz32(1)
);
```

Output:

```text
31
```

This is an advanced method and is rarely needed in normal web development.

---

# 31. `Math.imul()`

Performs 32-bit integer multiplication.

```javascript
console.log(
    Math.imul(2, 4)
);
```

Output:

```text
8
```

It is mainly useful for low-level or performance-oriented calculations.

---

# 32. Handling `NaN`

Some Math operations can produce `NaN`.

```javascript
console.log(
    Math.sqrt(-1)
);
```

Output:

```text
NaN
```

Check it with:

```javascript
const result = Math.sqrt(-1);

console.log(
    Number.isNaN(result)
);
```

Output:

```text
true
```

---

# 33. Handling Infinity

JavaScript can represent positive and negative infinity.

```javascript
console.log(
    Math.max()
);
```

Output:

```text
-Infinity
```

And:

```javascript
console.log(
    Math.min()
);
```

Output:

```text
Infinity
```

Check infinity:

```javascript
console.log(
    Number.isFinite(100)
);
```

Output:

```text
true
```

---

# 34. `Number.isFinite()` vs Infinity

```javascript
console.log(
    Number.isFinite(100)
);
// true

console.log(
    Number.isFinite(Infinity)
);
// false

console.log(
    Number.isFinite(NaN)
);
// false
```

This is useful when validating numeric input.

---

# 35. Percentage Calculation

Math methods are often used with percentages.

```javascript
const price = 1000;
const discount = 20;

const discountAmount =
    price * discount / 100;

const finalPrice =
    price - discountAmount;

console.log(finalPrice);
```

Output:

```text
800
```

---

# 36. Average Calculation

```javascript
const marks = [70, 80, 90, 85];

const total =
    marks.reduce(
        (sum, mark) => sum + mark,
        0
    );

const average =
    total / marks.length;

console.log(average);
```

Output:

```text
81.25
```

Round the result:

```javascript
console.log(
    Math.round(average)
);
```

Output:

```text
81
```

---

# 37. Pagination Calculation

Suppose:

```text
Total items = 95
Items per page = 10
```

Calculate pages:

```javascript
const totalItems = 95;
const itemsPerPage = 10;

const totalPages =
    Math.ceil(
        totalItems / itemsPerPage
    );

console.log(totalPages);
```

Output:

```text
10
```

`Math.ceil()` is useful because even a partially filled final page needs to exist.

---

# 38. Price Rounding

```javascript
const price = 499.987;

const rounded =
    Math.round(price * 100) / 100;

console.log(rounded);
```

Output:

```text
499.99
```

For displaying currency, `Intl.NumberFormat` is often preferable:

```javascript
const formatter =
    new Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "USD"
    });

console.log(
    formatter.format(499.987)
);
```

---

# 39. Finding the Closest Number

```javascript
const target = 50;

const numbers = [20, 45, 60, 80];

const closest = numbers.reduce(
    (previous, current) => {
        return Math.abs(current - target) <
            Math.abs(previous - target)
            ? current
            : previous;
    }
);

console.log(closest);
```

Output:

```text
45
```

---

# 40. Math Method Summary

| Method          | Purpose             |
| --------------- | ------------------- |
| `Math.round()`  | Nearest integer     |
| `Math.floor()`  | Round down          |
| `Math.ceil()`   | Round up            |
| `Math.trunc()`  | Remove decimal part |
| `Math.abs()`    | Absolute value      |
| `Math.max()`    | Largest value       |
| `Math.min()`    | Smallest value      |
| `Math.pow()`    | Power               |
| `Math.sqrt()`   | Square root         |
| `Math.cbrt()`   | Cube root           |
| `Math.sign()`   | Number sign         |
| `Math.random()` | Random number       |
| `Math.log()`    | Natural logarithm   |
| `Math.log10()`  | Base-10 logarithm   |
| `Math.log2()`   | Base-2 logarithm    |
| `Math.exp()`    | e raised to a power |
| `Math.sin()`    | Sine                |
| `Math.cos()`    | Cosine              |
| `Math.tan()`    | Tangent             |
| `Math.hypot()`  | Hypotenuse          |

---

# 41. Most Important Math Methods

For everyday JavaScript development, focus mainly on:

```text
Math.round()
Math.floor()
Math.ceil()
Math.trunc()
Math.abs()
Math.max()
Math.min()
Math.sqrt()
Math.random()
Math.pow()
```

These are commonly useful in:

* React applications
* Node.js applications
* APIs
* Pagination
* Shopping carts
* Calculators
* Games
* Data processing
* UI calculations

---

# 42. Quick Cheat Sheet

```javascript
// Constants
Math.PI;
Math.E;

// Rounding
Math.round(4.6); // 5
Math.floor(4.6); // 4
Math.ceil(4.2);  // 5
Math.trunc(4.9); // 4

// Absolute value
Math.abs(-10); // 10

// Minimum / Maximum
Math.min(10, 20, 5); // 5
Math.max(10, 20, 5); // 20

// Power
Math.pow(2, 3); // 8
2 ** 3;         // 8

// Roots
Math.sqrt(25); // 5
Math.cbrt(27); // 3

// Sign
Math.sign(-10); // -1
Math.sign(10);  // 1

// Random
Math.random();

// Logarithms
Math.log(Math.E); // 1
Math.log10(100);  // 2
Math.log2(8);     // 3

// Trigonometry
Math.sin(0);
Math.cos(0);
Math.tan(0);
```

---

# Key Takeaways

* `Math` provides built-in mathematical operations.
* `Math.round()` rounds to the nearest integer.
* `Math.floor()` rounds toward negative infinity.
* `Math.ceil()` rounds toward positive infinity.
* `Math.trunc()` removes the decimal part.
* `Math.abs()` returns an absolute value.
* `Math.min()` and `Math.max()` find the smallest and largest values.
* Use spread syntax when passing an array to `Math.min()` or `Math.max()`.
* `Math.sqrt()` calculates square roots.
* `Math.random()` returns a value from `0` inclusive to `1` exclusive.
* Use `Math.floor()` with `Math.random()` to generate random integers.
* `Math.PI` is useful for circle calculations.
* Trigonometric methods use radians.
* `Math.random()` is not suitable for security-sensitive random values.
* `Number.isFinite()` and `Number.isNaN()` are useful when validating calculations.
