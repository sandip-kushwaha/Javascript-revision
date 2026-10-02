# JavaScript Array Destructuring

Array destructuring is a JavaScript feature that allows you to **extract values from an array and store them in variables**.

It is commonly used in modern JavaScript and React.

---

## 1. Basic Example

Without destructuring:

```javascript
const colors = ["red", "green", "blue"];

const first = colors[0];
const second = colors[1];

console.log(first);
console.log(second);
```

With destructuring:

```javascript
const colors = ["red", "green", "blue"];

const [first, second] = colors;

console.log(first);
console.log(second);
```

Output:

```text
red
green
```

---

## 2. How Array Destructuring Works

Values are assigned based on their **position**.

```javascript
const numbers = [10, 20, 30];

const [a, b, c] = numbers;

console.log(a); // 10
console.log(b); // 20
console.log(c); // 30
```

The relationship is:

```text
Array position       Variable

numbers[0]     →     a
numbers[1]     →     b
numbers[2]     →     c
```

---

## 3. Extract Only the First Value

```javascript
const fruits = ["Apple", "Banana", "Orange"];

const [first] = fruits;

console.log(first);
```

Output:

```text
Apple
```

---

## 4. Skip Values

You can skip elements using commas.

```javascript
const fruits = ["Apple", "Banana", "Orange"];

const [first, , third] = fruits;

console.log(first);
console.log(third);
```

Output:

```text
Apple
Orange
```

Here:

```javascript
[first, , third]
```

means:

```text
first  → index 0
skip   → index 1
third  → index 2
```

---

## 5. Extract More Values

```javascript
const numbers = [10, 20, 30, 40];

const [a, b, c, d] = numbers;

console.log(a);
console.log(b);
console.log(c);
console.log(d);
```

Output:

```text
10
20
30
40
```

---

## 6. Missing Values

If the array does not contain enough values:

```javascript
const numbers = [10, 20];

const [a, b, c] = numbers;

console.log(a);
console.log(b);
console.log(c);
```

Output:

```text
10
20
undefined
```

---

## 7. Default Values

You can provide default values.

```javascript
const numbers = [10, 20];

const [a, b, c = 30] = numbers;

console.log(a);
console.log(b);
console.log(c);
```

Output:

```text
10
20
30
```

The default value is used when the array value is `undefined`.

---

## 8. Default Value Is Not Used for `null`

```javascript
const values = [null];

const [value = 100] = values;

console.log(value);
```

Output:

```text
null
```

Default values apply when the value is `undefined`, not `null`.

---

## 9. Rest Pattern

You can collect the remaining values using `...`.

```javascript
const numbers = [10, 20, 30, 40];

const [first, ...rest] = numbers;

console.log(first);
console.log(rest);
```

Output:

```text
10
[20, 30, 40]
```

Here:

```javascript
first
```

gets the first value.

```javascript
...rest
```

collects the remaining values into an array.

---

## 10. Rest Must Be Last

Correct:

```javascript
const [first, ...rest] = numbers;
```

Incorrect:

```javascript
const [...rest, last] = numbers;
```

The rest element must always be the **last element** in an array destructuring pattern.

---

## 11. Destructuring Nested Arrays

You can destructure nested arrays.

```javascript
const numbers = [1, [2, 3]];

const [first, [second, third]] = numbers;

console.log(first);
console.log(second);
console.log(third);
```

Output:

```text
1
2
3
```

---

## 12. Swapping Variables

Array destructuring makes swapping values easy.

Without destructuring:

```javascript
let a = 10;
let b = 20;

let temp = a;
a = b;
b = temp;
```

With destructuring:

```javascript
let a = 10;
let b = 20;

[a, b] = [b, a];

console.log(a);
console.log(b);
```

Output:

```text
20
10
```

---

## 13. Destructuring in Function Returns

Functions can return arrays.

```javascript
function getUser() {
    return ["Ram", 22];
}

const [name, age] = getUser();

console.log(name);
console.log(age);
```

Output:

```text
Ram
22
```

This pattern is commonly used in JavaScript libraries and React.

---

## 14. React Example

React hooks commonly return arrays.

For example:

```javascript
const [count, setCount] = useState(0);
```

This is array destructuring.

Conceptually, `useState()` returns something like:

```javascript
[
    currentValue,
    functionToUpdateValue
]
```

Then:

```javascript
const [count, setCount] = useState(0);
```

extracts those two values.

---

## 15. Destructuring Function Results

```javascript
function getCoordinates() {
    return [27.7172, 85.3240];
}

const [latitude, longitude] = getCoordinates();

console.log(latitude);
console.log(longitude);
```

Output:

```text
27.7172
85.324
```

---

## 16. Using `const`

You can use `const`:

```javascript
const numbers = [10, 20];

const [a, b] = numbers;
```

The variables cannot be reassigned.

---

## 17. Using `let`

You can also use `let`:

```javascript
let numbers = [10, 20];

let [a, b] = numbers;

a = 100;

console.log(a);
```

Output:

```text
100
```

---

## 18. Destructuring with Strings

Strings are iterable, so they can also be destructured.

```javascript
const name = "Sandip";

const [first, second, third] = name;

console.log(first);
console.log(second);
console.log(third);
```

Output:

```text
S
a
n
```

---

## 19. Destructuring with `Set`

Iterable values such as `Set` can also be destructured.

```javascript
const numbers = new Set([10, 20, 30]);

const [a, b, c] = numbers;

console.log(a);
console.log(b);
console.log(c);
```

Output:

```text
10
20
30
```

---

## 20. Destructuring in Function Parameters

You can destructure an array directly in a function parameter.

```javascript
function printNumbers([first, second]) {
    console.log(first);
    console.log(second);
}

printNumbers([10, 20]);
```

Output:

```text
10
20
```

---

## 21. Practical Example

Suppose a hotel table has:

```javascript
const table = ["T-01", 4, "available"];
```

You can destructure it:

```javascript
const [tableNumber, capacity, status] = table;

console.log(tableNumber);
console.log(capacity);
console.log(status);
```

Output:

```text
T-01
4
available
```

---

## 22. Array Destructuring vs Indexing

### Traditional indexing

```javascript
const user = ["Ram", 22, "Nepal"];

const name = user[0];
const age = user[1];
const country = user[2];
```

### Destructuring

```javascript
const [name, age, country] = user;
```

Destructuring is often cleaner when you need several values.

---

## 23. Common Mistakes

### Mistake 1: Wrong order

```javascript
const numbers = [10, 20];

const [b, a] = numbers;

console.log(a);
console.log(b);
```

Output:

```text
20
10
```

Destructuring follows **array position**, not variable names.

---

### Mistake 2: Forgetting commas when skipping

Correct:

```javascript
const [first, , third] = numbers;
```

Incorrect:

```javascript
const [first, third] = numbers;
```

The second version assigns index `1` to `third`.

---

### Mistake 3: Rest in the wrong position

Incorrect:

```javascript
const [...rest, last] = numbers;
```

Correct:

```javascript
const [first, ...rest] = numbers;
```

---

## 24. Quick Comparison

| Feature          | Example           |
| ---------------- | ----------------- |
| First value      | `[first]`         |
| Multiple values  | `[a, b, c]`       |
| Skip value       | `[a, , c]`        |
| Default value    | `[a = 10]`        |
| Remaining values | `[a, ...rest]`    |
| Nested array     | `[a, [b, c]]`     |
| Swap values      | `[a, b] = [b, a]` |

---

## 25. Quick Revision

```javascript
const numbers = [10, 20, 30, 40];

const [first, second, ...rest] = numbers;

console.log(first);  // 10
console.log(second); // 20
console.log(rest);   // [30, 40]
```

Remember:

```text
Array
  ↓
[position-based extraction]
  ↓
Variables
```

---

## 26. Cheat Sheet

### Basic

```javascript
const [a, b] = [10, 20];
```

### Skip

```javascript
const [a, , c] = [10, 20, 30];
```

### Default

```javascript
const [a = 10] = [];
```

### Rest

```javascript
const [first, ...rest] = numbers;
```

### Nested

```javascript
const [a, [b, c]] = [1, [2, 3]];
```

### Swap

```javascript
[a, b] = [b, a];
```

### Function return

```javascript
const [name, age] = getUser();
```

---

## 27. Key Takeaways

* Array destructuring extracts values from arrays.
* Values are assigned based on their position.
* You can skip values using commas.
* You can provide default values.
* `...rest` collects remaining values.
* The rest element must be last.
* Nested arrays can be destructured.
* Destructuring makes variable swapping simple.
* Functions that return arrays can be destructured.
* React commonly uses array destructuring with hooks such as `useState()`.

---
