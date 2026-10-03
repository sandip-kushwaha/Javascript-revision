# JavaScript Nullish Coalescing Operator

The **nullish coalescing operator (`??`)** provides a fallback value when the left side is:

* `null`
* `undefined`

Syntax:

```javascript
const result = value ?? fallback;
```

If `value` is `null` or `undefined`, `fallback` is used.

Otherwise, the original value is returned.

---

# 1. Basic Example

```javascript
const username = null;

const name = username ?? "Guest";

console.log(name);
```

Output:

```text
Guest
```

Because `username` is `null`.

---

# 2. With `undefined`

```javascript
let username;

const name = username ?? "Guest";

console.log(name);
```

Output:

```text
Guest
```

An uninitialized variable has the value `undefined`.

---

# 3. When the Value Exists

```javascript
const username = "Sandip";

const name = username ?? "Guest";

console.log(name);
```

Output:

```text
Sandip
```

The fallback is not used.

---

# 4. Important: `??` Only Checks Nullish Values

`??` only considers these two values missing:

```text
null
undefined
```

It does **not** treat these as missing:

```text
0
false
""
NaN
```

Example:

```javascript
const count = 0;

const result = count ?? 10;

console.log(result);
```

Output:

```text
0
```

The value `0` is preserved.

---

# 5. `false` Is Preserved

```javascript
const isActive = false;

const result = isActive ?? true;

console.log(result);
```

Output:

```text
false
```

This is useful when `false` is a meaningful value.

---

# 6. Empty String Is Preserved

```javascript
const username = "";

const result = username ?? "Guest";

console.log(result);
```

Output:

```text
""
```

An empty string is not `null` or `undefined`, so the fallback is not used.

---

# 7. `NaN` Is Preserved

```javascript
const value = NaN;

const result = value ?? 100;

console.log(result);
```

Output:

```text
NaN
```

`NaN` is not nullish.

---

# 8. The Main Difference From `||`

The logical OR operator:

```javascript
||
```

uses the right side when the left side is **falsy**.

The nullish coalescing operator:

```javascript
??
```

uses the right side only when the left side is `null` or `undefined`.

This difference is very important.

---

# 9. `0` Example

Using `||`:

```javascript
const quantity = 0;

const result = quantity || 10;

console.log(result);
```

Output:

```text
10
```

Because `0` is falsy.

Using `??`:

```javascript
const result = quantity ?? 10;

console.log(result);
```

Output:

```text
0
```

Because `0` is a valid non-nullish value.

---

# 10. `false` Example

Using `||`:

```javascript
const enabled = false;

const result = enabled || true;

console.log(result);
```

Output:

```text
true
```

This may be incorrect if `false` is a meaningful value.

Using `??`:

```javascript
const result = enabled ?? true;

console.log(result);
```

Output:

```text
false
```

---

# 11. Empty String Example

Using `||`:

```javascript
const name = "";

const result = name || "Guest";

console.log(result);
```

Output:

```text
Guest
```

Using `??`:

```javascript
const result = name ?? "Guest";

console.log(result);
```

Output:

```text
""
```

---

# 12. Comparison Table

| Value | `value || "Default"` | `value ?? "Default"` |
|---|---|---|
| `null` | `"Default"` | `"Default"` |
| `undefined` | `"Default"` | `"Default"` |
| `0` | `"Default"` | `0` |
| `false` | `"Default"` | `false` |
| `""` | `"Default"` | `""` |
| `NaN` | `"Default"` | `NaN` |
| `"Hello"` | `"Hello"` | `"Hello"` |

This is the key difference to remember.

---

# 13. Why `??` Is Useful

Suppose `0` is a valid price:

```javascript
const price = 0;
```

Using:

```javascript
const displayPrice = price || 100;
```

would incorrectly produce:

```text
100
```

Using:

```javascript
const displayPrice = price ?? 100;
```

produces:

```text
0
```

This preserves the actual value.

---

# 14. API Data Example

Suppose an API returns:

```javascript
const user = {
  name: "Sandip",
  age: 0
};
```

You can safely provide a fallback:

```javascript
const age = user.age ?? 18;

console.log(age);
```

Output:

```text
0
```

The API intentionally returned `0`, so it should not be replaced.

---

# 15. Optional Chaining + `??`

These operators are commonly used together.

```javascript
const user = {};

const city =
  user?.profile?.address?.city ?? "Unknown";

console.log(city);
```

Output:

```text
Unknown
```

The process is:

```text
user
 ↓
profile
 ↓
address
 ↓
city
 ↓
if null/undefined
 ↓
"Unknown"
```

---

# 16. React Example

Suppose a component receives:

```jsx
function Product({ product }) {
  const stock = product?.stock ?? 0;

  return <p>Stock: {stock}</p>;
}
```

If:

```javascript
product.stock = 0;
```

the displayed value is:

```text
Stock: 0
```

It will not incorrectly replace `0` with another default.

---

# 17. Configuration Example

Suppose:

```javascript
const config = {
  timeout: 0
};
```

If `0` is a meaningful configuration value:

```javascript
const timeout =
  config.timeout ?? 5000;
```

Result:

```text
0
```

Using `||` would incorrectly replace it:

```javascript
const timeout =
  config.timeout || 5000;
```

Result:

```text
5000
```

---

# 18. Function Parameters

You can use `??` inside a function:

```javascript
function getLimit(limit) {
  return limit ?? 10;
}

console.log(getLimit());
console.log(getLimit(0));
console.log(getLimit(20));
```

Output:

```text
10
0
20
```

---

# 19. Difference Between `??` and Default Parameters

Default parameters:

```javascript
function createUser(name = "Guest") {
  return name;
}
```

The default parameter is used when the argument is:

```text
undefined
```

For example:

```javascript
createUser();
```

returns:

```text
Guest
```

But:

```javascript
createUser(null);
```

returns:

```text
null
```

With `??`:

```javascript
function createUser(name) {
  return name ?? "Guest";
}
```

Now both:

```text
undefined
null
```

use the fallback.

---

# 20. `??` With Object Properties

```javascript
const settings = {
  language: "English"
};

const language =
  settings.language ?? "Nepali";

console.log(language);
```

Output:

```text
English
```

If the property is missing:

```javascript
const settings = {};

const language =
  settings.language ?? "Nepali";
```

Result:

```text
Nepali
```

---

# 21. `??` With Array Values

```javascript
const values = [0, null, undefined];

const first = values[0] ?? 100;
const second = values[1] ?? 100;
const third = values[2] ?? 100;

console.log(first);
console.log(second);
console.log(third);
```

Output:

```text
0
100
100
```

---

# 22. Chaining `??`

You can use multiple nullish fallbacks:

```javascript
const value =
  firstValue ??
  secondValue ??
  thirdValue ??
  "Default";
```

JavaScript uses the first value that is neither `null` nor `undefined`.

Example:

```javascript
const first = null;
const second = undefined;
const third = "Available";

const result =
  first ?? second ?? third ?? "Default";

console.log(result);
```

Output:

```text
Available
```

---

# 23. `??` Is Short-Circuiting

If the left side contains a valid value, the right side is not evaluated.

```javascript
const value = "Hello";

const result =
  value ?? someFunction();
```

Because `value` is not nullish, `someFunction()` does not need to run.

This can be useful when the fallback calculation is expensive or has side effects.

---

# 24. `??` Cannot Be Mixed Freely With `||` or `&&`

This is invalid without parentheses:

```javascript
const result = a || b ?? c;
```

JavaScript does not allow `??` to be directly mixed with `||` or `&&`.

Use parentheses:

```javascript
const result =
  (a || b) ?? c;
```

or:

```javascript
const result =
  a || (b ?? c);
```

The parentheses make the intended evaluation explicit.

---

# 25. `??` vs `||` in Real Applications

Use `||` when you intentionally want a fallback for **any falsy value**.

```javascript
const label = userInput || "Not provided";
```

Here, an empty string may reasonably mean "not provided."

Use `??` when only `null` and `undefined` should trigger the fallback.

```javascript
const count = response.count ?? 0;
```

Here, `0` should remain `0`.

---

# 26. Hotel Example

Suppose an order has an optional discount:

```javascript
const order = {
  total: 1000,
  discount: 0
};
```

Use:

```javascript
const discount =
  order.discount ?? 0;
```

Result:

```text
0
```

The discount is genuinely zero.

---

# 27. Food Example

Suppose a food item has an optional preparation time:

```javascript
const food = {
  name: "Momo",
  preparationTime: 0
};

const preparationTime =
  food.preparationTime ?? 10;
```

Result:

```text
0
```

The value is preserved because `0` is not nullish.

---

# 28. User Settings Example

```javascript
const settings = {
  notifications: false
};

const notifications =
  settings.notifications ?? true;
```

Result:

```text
false
```

This is important because `false` may represent an intentional user choice.

---

# 29. Common Mistakes

## Mistake 1: Thinking `??` checks all falsy values

It does not.

```javascript
0 ?? 10       // 0
false ?? true // false
"" ?? "Guest" // ""
```

Only `null` and `undefined` trigger the fallback.

---

## Mistake 2: Always replacing `||` with `??`

They have different purposes.

Use `||` when falsy values should trigger the fallback.

Use `??` when only missing values should trigger the fallback.

---

## Mistake 3: Forgetting parentheses

Avoid:

```javascript
a || b ?? c
```

Use explicit grouping:

```javascript
(a || b) ?? c
```

---

# 30. Quick Reference

### Basic

```javascript
const value = data ?? "Default";
```

### Optional chaining + fallback

```javascript
const name =
  user?.profile?.name ?? "Guest";
```

### Preserve `0`

```javascript
const count = value ?? 0;
```

### Preserve `false`

```javascript
const active = value ?? false;
```

### Multiple fallbacks

```javascript
const value =
  first ?? second ?? "Default";
```

---

# 31. `??` vs `?.` vs `||`

| Operator | Main Purpose                    |   |                           |
| -------- | ------------------------------- | - | ------------------------- |
| `?.`     | Safely access something         |   |                           |
| `??`     | Fallback for `null`/`undefined` |   |                           |
| `        |                                 | ` | Fallback for falsy values |

Example:

```javascript
const city =
  user?.address?.city ?? "Unknown";
```

Here:

```text
?. → safely access city
?? → use "Unknown" if city is null/undefined
```

---

# 32. Key Takeaways

* `??` is the **nullish coalescing operator**.
* It returns the right side only when the left side is `null` or `undefined`.
* `0`, `false`, `""`, and `NaN` are preserved.
* `??` is useful for API responses and configuration values.
* `??` works very well with optional chaining.
* `||` and `??` are not interchangeable.
* Default parameters handle `undefined`; `??` handles both `undefined` and `null`.
* Parentheses are required when mixing `??` with `||` or `&&`.

## Remember

```text
?. → safely access
?? → fallback for null/undefined
|| → fallback for falsy values
```

Example:

```javascript
const city =
  user?.profile?.city ?? "Unknown";
```

---
