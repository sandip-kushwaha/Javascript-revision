# JavaScript Spread Operator

The **spread operator** is written using three dots:

```javascript
...
```

It is used to **expand or spread values** from an array, object, or other iterable into another place.

Examples:

```javascript
const numbers = [1, 2, 3];

const newNumbers = [...numbers];

console.log(newNumbers);
```

Output:

```text
[1, 2, 3]
```

---

# 1. What Does Spread Mean?

Spread means **take the values inside something and expand them**.

For example:

```javascript
const numbers = [1, 2, 3];

console.log(...numbers);
```

This is similar to:

```javascript
console.log(1, 2, 3);
```

The array values are spread out.

---

# 2. Spread With Arrays

The spread operator is commonly used to copy an array.

```javascript
const fruits = ["Apple", "Mango", "Banana"];

const newFruits = [...fruits];

console.log(newFruits);
```

Output:

```text
["Apple", "Mango", "Banana"]
```

---

# 3. Copying an Array

Without spread:

```javascript
const numbers = [1, 2, 3];

const copy = numbers;
```

Both variables refer to the same array.

```javascript
copy.push(4);

console.log(numbers);
```

Output:

```text
[1, 2, 3, 4]
```

Using spread:

```javascript
const numbers = [1, 2, 3];

const copy = [...numbers];

copy.push(4);

console.log(numbers);
console.log(copy);
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

Spread creates a **shallow copy**.

---

# 4. Combining Arrays

Spread makes it easy to combine arrays.

```javascript
const frontend = ["HTML", "CSS", "JavaScript"];
const backend = ["Node.js", "Express"];

const skills = [
  ...frontend,
  ...backend
];

console.log(skills);
```

Output:

```text
["HTML", "CSS", "JavaScript", "Node.js", "Express"]
```

---

# 5. Adding Values to an Array

You can add values while spreading an existing array.

```javascript
const numbers = [2, 3, 4];

const newNumbers = [
  1,
  ...numbers,
  5
];

console.log(newNumbers);
```

Output:

```text
[1, 2, 3, 4, 5]
```

---

# 6. Adding Values at the Beginning

```javascript
const fruits = ["Mango", "Banana"];

const newFruits = [
  "Apple",
  ...fruits
];

console.log(newFruits);
```

Output:

```text
["Apple", "Mango", "Banana"]
```

---

# 7. Adding Values at the End

```javascript
const fruits = ["Apple", "Mango"];

const newFruits = [
  ...fruits,
  "Banana"
];

console.log(newFruits);
```

Output:

```text
["Apple", "Mango", "Banana"]
```

---

# 8. Spread With Function Arguments

Spread can expand an array into individual function arguments.

```javascript
const numbers = [10, 20, 30];

function add(a, b, c) {
  return a + b + c;
}

console.log(add(...numbers));
```

Output:

```text
60
```

This:

```javascript
add(...numbers);
```

is similar to:

```javascript
add(10, 20, 30);
```

---

# 9. Spread With `Math.max()`

```javascript
const numbers = [10, 50, 20, 80, 30];

const maximum = Math.max(...numbers);

console.log(maximum);
```

Output:

```text
80
```

Without spread, `Math.max()` does not receive the array elements as separate arguments.

---

# 10. Spread With `Math.min()`

```javascript
const numbers = [10, 50, 20, 80, 30];

const minimum = Math.min(...numbers);

console.log(minimum);
```

Output:

```text
10
```

---

# 11. Spread With Strings

Strings are iterable, so they can be spread into individual characters.

```javascript
const name = "Sandip";

const characters = [...name];

console.log(characters);
```

Output:

```text
["S", "a", "n", "d", "i", "p"]
```

---

# 12. Spread With a String Into an Array

```javascript
const word = "Hello";

const letters = [...word];

console.log(letters);
```

Result:

```text
["H", "e", "l", "l", "o"]
```

---

# 13. Spread With Objects

Spread can also be used with objects.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const copy = {
  ...user
};

console.log(copy);
```

Output:

```javascript
{
  name: "Sandip",
  age: 22
}
```

This creates a shallow copy of the object.

---

# 14. Combining Objects

You can combine multiple objects using spread.

```javascript
const userInfo = {
  name: "Sandip",
  age: 22
};

const address = {
  city: "Birgunj",
  country: "Nepal"
};

const user = {
  ...userInfo,
  ...address
};

console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22,
  city: "Birgunj",
  country: "Nepal"
}
```

---

# 15. Adding Properties to an Object

You can add properties while spreading.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const updatedUser = {
  ...user,
  city: "Birgunj"
};

console.log(updatedUser);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22,
  city: "Birgunj"
}
```

The original object is not changed.

---

# 16. Updating an Object Property

A common use of spread is creating a new object with an updated property.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const updatedUser = {
  ...user,
  age: 23
};

console.log(updatedUser);
```

Result:

```javascript
{
  name: "Sandip",
  age: 23,
  city: "Birgunj"
}
```

The original object remains:

```javascript
console.log(user.age);
```

Output:

```text
22
```

---

# 17. Property Overwriting

When spreading objects, later properties can overwrite earlier properties.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const updatedUser = {
  ...user,
  age: 23
};

console.log(updatedUser);
```

The later:

```javascript
age: 23
```

overwrites:

```javascript
age: 22
```

---

# 18. Order Matters

Consider:

```javascript
const user = {
  age: 23,
  ...{
    age: 22
  }
};

console.log(user.age);
```

Output:

```text
22
```

The later value wins.

Compare:

```javascript
const user = {
  ...{
    age: 22
  },
  age: 23
};

console.log(user.age);
```

Output:

```text
23
```

So remember:

> **For duplicate object properties, the later value overwrites the earlier value.**

---

# 19. Merging Objects With the Same Property

```javascript
const defaultSettings = {
  theme: "light",
  language: "en"
};

const userSettings = {
  theme: "dark"
};

const settings = {
  ...defaultSettings,
  ...userSettings
};

console.log(settings);
```

Result:

```javascript
{
  theme: "dark",
  language: "en"
}
```

The user's `theme` overrides the default theme.

---

# 20. Spread and `null` / `undefined`

Object spread safely ignores `null` and `undefined` values in modern JavaScript.

```javascript
const user = {
  name: "Sandip",
  ...null,
  ...undefined
};

console.log(user);
```

Result:

```javascript
{
  name: "Sandip"
}
```

However, you should still avoid unnecessary spread of nullish values because clear code is easier to understand.

---

# 21. Spread With Arrays of Objects

Suppose:

```javascript
const users = [
  { name: "Sandip" },
  { name: "Ram" }
];
```

You can create a new array:

```javascript
const newUsers = [
  ...users
];
```

But this is only a **shallow copy**.

The objects inside are still shared.

---

# 22. Shallow Copy Example

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const copy = {
  ...user
};

copy.address.city = "Kathmandu";

console.log(user.address.city);
```

Output:

```text
Kathmandu
```

Why?

Because spread only copied the top-level object.

The nested `address` object is still the same reference.

---

# 23. Spread Does Not Deep Copy

This:

```javascript
const copy = {
  ...user
};
```

creates a **shallow copy**, not a deep copy.

Think:

```text
Original Object
      │
      └── address ──┐
                    │
Copy Object         │
      │             │
      └── address ──┘
```

Both objects reference the same nested `address`.

Deep copying is a separate topic.

---

# 24. Hotel Management Example

Suppose you have:

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "available"
};
```

Update the status without changing the original:

```javascript
const occupiedTable = {
  ...table,
  status: "occupied"
};

console.log(occupiedTable);
```

Result:

```javascript
{
  tableNumber: "T-03",
  capacity: 6,
  status: "occupied"
}
```

The original remains:

```javascript
console.log(table.status);
```

Output:

```text
available
```

---

# 25. Food Example

```javascript
const food = {
  name: "Chicken Momo",
  price: 180,
  isAvailable: true
};
```

Update the price:

```javascript
const updatedFood = {
  ...food,
  price: 200
};

console.log(updatedFood);
```

Result:

```javascript
{
  name: "Chicken Momo",
  price: 200,
  isAvailable: true
}
```

---

# 26. Order Example

```javascript
const order = {
  orderNumber: "ORD-001",
  status: "pending",
  totalAmount: 850
};
```

Update status:

```javascript
const confirmedOrder = {
  ...order,
  status: "confirmed"
};

console.log(confirmedOrder);
```

Result:

```javascript
{
  orderNumber: "ORD-001",
  status: "confirmed",
  totalAmount: 850
}
```

---

# 27. React State Example

Spread is very common in React when updating objects.

Suppose state contains:

```javascript
const user = {
  name: "Sandip",
  age: 22
};
```

Instead of changing the object directly:

```javascript
user.age = 23;
```

you can create a new object:

```javascript
const updatedUser = {
  ...user,
  age: 23
};
```

In React, a similar pattern is:

```javascript
setUser({
  ...user,
  age: 23
});
```

This creates a new object reference.

---

# 28. React Array State Example

Suppose:

```javascript
const [items, setItems] = useState([
  "Laptop",
  "Mouse"
]);
```

To add an item:

```javascript
setItems([
  ...items,
  "Keyboard"
]);
```

Result:

```text
["Laptop", "Mouse", "Keyboard"]
```

This is a common immutable update pattern in React.

---

# 29. Removing an Array Item With Spread

Suppose:

```javascript
const items = [
  "Laptop",
  "Mouse",
  "Keyboard"
];
```

You can use `filter()`:

```javascript
const updatedItems = items.filter(
  (item) => item !== "Mouse"
);
```

Result:

```text
["Laptop", "Keyboard"]
```

Spread can then be used when constructing larger arrays, but `filter()` is generally the direct tool for removing based on a condition.

---

# 30. Spread vs Rest

Both use:

```javascript
...
```

But they do different things.

### Spread

**Expands** values.

```javascript
const numbers = [1, 2, 3];

console.log(...numbers);
```

### Rest

**Collects** values.

```javascript
function sum(...numbers) {
  console.log(numbers);
}
```

So:

```text
Spread → expands
Rest   → collects
```

---

# 31. Spread in Function Calls

```javascript
const numbers = [10, 20, 30];

function show(a, b, c) {
  console.log(a);
  console.log(b);
  console.log(c);
}

show(...numbers);
```

Equivalent to:

```javascript
show(10, 20, 30);
```

---

# 32. Spread in Array Literals

```javascript
const first = [1, 2];
const second = [3, 4];

const combined = [
  ...first,
  ...second
];

console.log(combined);
```

Result:

```text
[1, 2, 3, 4]
```

---

# 33. Spread in Object Literals

```javascript
const first = {
  name: "Sandip"
};

const second = {
  age: 22
};

const user = {
  ...first,
  ...second
};

console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22
}
```

---

# 34. Spread With `Set`

A `Set` is iterable, so you can convert it into an array.

```javascript
const numbers = new Set([1, 2, 3]);

const array = [...numbers];

console.log(array);
```

Output:

```text
[1, 2, 3]
```

---

# 35. Spread With `Map`

A `Map` is also iterable.

```javascript
const map = new Map([
  ["name", "Sandip"],
  ["age", 22]
]);

const entries = [...map];

console.log(entries);
```

Result:

```javascript
[
  ["name", "Sandip"],
  ["age", 22]
]
```

---

# 36. Converting a Set to an Array

A common use:

```javascript
const numbers = new Set([1, 2, 2, 3, 3]);

const uniqueNumbers = [...numbers];

console.log(uniqueNumbers);
```

Output:

```text
[1, 2, 3]
```

---

# 37. Spread and Strings

You can convert a string into an array of characters:

```javascript
const text = "JavaScript";

const characters = [...text];

console.log(characters);
```

Result:

```javascript
[
  "J",
  "a",
  "v",
  "a",
  "S",
  "c",
  "r",
  "i",
  "p",
  "t"
]
```

---

# 38. Spread and Function Arguments

Suppose:

```javascript
function calculateTotal(a, b, c) {
  return a + b + c;
}

const prices = [100, 200, 300];

console.log(
  calculateTotal(...prices)
);
```

Output:

```text
600
```

---

# 39. Common Mistakes

## Mistake 1: Thinking spread creates a deep copy

```javascript
const copy = {
  ...original
};
```

This creates a **shallow copy**.

Nested objects and arrays can still be shared.

---

## Mistake 2: Confusing spread and rest

Spread:

```javascript
const copy = [...numbers];
```

Rest:

```javascript
function test(...numbers) {}
```

Remember:

```text
Spread → expands
Rest → collects
```

---

## Mistake 3: Forgetting property overwrite order

```javascript
const user = {
  ...userData,
  role: "admin"
};
```

Here `role: "admin"` comes later and overwrites an existing `role`.

But:

```javascript
const user = {
  role: "admin",
  ...userData
};
```

allows `userData.role` to overwrite `"admin"` if `userData` contains a `role` property.

---

## Mistake 4: Mutating nested data accidentally

```javascript
const copy = {
  ...user
};

copy.address.city = "Kathmandu";
```

The nested `address` may still be shared with `user`.

Spread does not automatically deep clone nested objects.

---

# 40. Spread Operator Cheat Sheet

### Copy array

```javascript
const copy = [...array];
```

### Combine arrays

```javascript
const combined = [...a, ...b];
```

### Add array items

```javascript
const result = [0, ...numbers, 4];
```

### Copy object

```javascript
const copy = { ...object };
```

### Combine objects

```javascript
const combined = { ...a, ...b };
```

### Update object

```javascript
const updated = {
  ...user,
  age: 23
};
```

### Function arguments

```javascript
fn(...array);
```

### String to array

```javascript
const chars = [...text];
```

### Set to array

```javascript
const array = [...set];
```

---

# 41. Spread vs Assignment

Consider:

```javascript
const user = {
  name: "Sandip"
};
```

### Assignment

```javascript
const copy = user;
```

Both variables reference the same object.

### Spread

```javascript
const copy = {
  ...user
};
```

A new top-level object is created.

---

# 42. Visual Explanation

### Assignment

```text
user ────────┐
             ↓
        { name: "Sandip" }
             ↑
copy ────────┘
```

### Spread

```text
user ────────> { name: "Sandip" }

copy ────────> { name: "Sandip" }
```

The second case creates a new top-level object.

---

# 43. Important Rule

Remember this:

> **Spread creates a new shallow copy, not a deep copy.**

For example:

```javascript
const original = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const copy = {
  ...original
};
```

The top-level objects are different:

```javascript
original !== copy
```

But the nested address is shared:

```javascript
original.address === copy.address
```

---

# 44. Key Takeaways

* The spread operator uses `...`.
* Spread means **expand values**.
* It works with arrays, objects, and iterables.
* It can copy arrays.
* It can combine arrays.
* It can copy objects.
* It can combine objects.
* It can update objects without changing the original top-level object.
* Later object properties overwrite earlier properties with the same key.
* Spread is heavily used in React state updates.
* Spread creates a **shallow copy**.
* Spread does not deep-copy nested objects or arrays.
* Spread is different from rest syntax.
* Rest collects values; spread expands values.

---

## Quick Example

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const updatedUser = {
  ...user,
  age: 23,
  role: "admin"
};

console.log(updatedUser);
```

Output:

```javascript
{
  name: "Sandip",
  age: 23,
  city: "Birgunj",
  role: "admin"
}
```

Array example:

```javascript
const frontend = ["HTML", "CSS", "JavaScript"];
const backend = ["Node.js", "MongoDB"];

const skills = [
  ...frontend,
  ...backend
];

console.log(skills);
```

Output:

```text
["HTML", "CSS", "JavaScript", "Node.js", "MongoDB"]
```

---
