# JavaScript Spread and Rest Operators

The `...` syntax is used for two related but different purposes:

* **Spread** → expands values
* **Rest** → collects values

```javascript
// Spread
const newArray = [...oldArray];

// Rest
function example(...values) {
  // values is an array
}
```

The same `...` syntax has different meanings depending on where it is used.

---

# 1. Spread Operator

The **spread operator** expands an iterable or object into individual elements/properties.

It is commonly used with:

* Arrays
* Objects
* Function arguments
* Copying data
* Combining data

---

# 2. Spread With Arrays

```javascript
const frontend = ["HTML", "CSS", "JavaScript"];

const skills = [
  ...frontend,
  "React",
  "Node.js"
];

console.log(skills);
```

Result:

```text
["HTML", "CSS", "JavaScript", "React", "Node.js"]
```

Without spread:

```javascript
const skills = [
  frontend,
  "React"
];
```

This creates a nested array.

---

# 3. Copying an Array

```javascript
const original = ["React", "Node.js", "MongoDB"];

const copy = [...original];
```

Now `copy` is a new array.

```javascript
console.log(copy);
```

```text
["React", "Node.js", "MongoDB"]
```

This is a **shallow copy**.

---

# 4. Why Spread Is Useful for Copying

Consider:

```javascript
const items = ["A", "B"];

const copy = items;

copy.push("C");

console.log(items);
```

Output:

```text
["A", "B", "C"]
```

Both variables refer to the same array.

Using spread:

```javascript
const items = ["A", "B"];

const copy = [...items];

copy.push("C");

console.log(items);
console.log(copy);
```

Output:

```text
["A", "B"]
["A", "B", "C"]
```

---

# 5. Combining Arrays

```javascript
const backend = ["Node.js", "Express"];
const database = ["MongoDB", "PostgreSQL"];

const technologies = [
  ...backend,
  ...database
];

console.log(technologies);
```

Result:

```text
[
  "Node.js",
  "Express",
  "MongoDB",
  "PostgreSQL"
]
```

---

# 6. Adding Items While Copying

```javascript
const pages = ["Home", "About"];

const updatedPages = [
  "Dashboard",
  ...pages,
  "Contact"
];
```

Result:

```text
[
  "Dashboard",
  "Home",
  "About",
  "Contact"
]
```

The position of `...pages` determines where its elements are inserted.

---

# 7. Spread With Function Arguments

Suppose a function expects separate arguments:

```javascript
function calculateTotal(a, b, c) {
  return a + b + c;
}
```

You have an array:

```javascript
const prices = [100, 200, 300];
```

Spread can pass the values individually:

```javascript
const total = calculateTotal(...prices);

console.log(total);
```

Output:

```text
600
```

Without spread, the entire array would be passed as one argument.

---

# 8. Spread With `Math.max()`

```javascript
const scores = [72, 91, 84, 96, 78];

const highest = Math.max(...scores);

console.log(highest);
```

Output:

```text
96
```

`Math.max()` expects separate numbers, so spread expands the array.

---

# 9. Spread With Strings

Strings are iterable.

```javascript
const language = "JavaScript";

const letters = [...language];

console.log(letters);
```

Result:

```text
["J", "a", "v", "a", "S", "c", "r", "i", "p", "t"]
```

---

# 10. Spread With Objects

Object spread copies properties into another object.

```javascript
const user = {
  name: "Sandip",
  role: "developer"
};

const profile = {
  ...user,
  active: true
};

console.log(profile);
```

Result:

```text
{
  name: "Sandip",
  role: "developer",
  active: true
}
```

---

# 11. Updating an Object With Spread

This is very common in React and JavaScript applications.

```javascript
const user = {
  name: "Sandip",
  role: "developer",
  active: true
};

const updatedUser = {
  ...user,
  role: "admin"
};
```

The original object remains unchanged.

```javascript
console.log(user.role);
console.log(updatedUser.role);
```

Output:

```text
developer
admin
```

---

# 12. Property Overwriting

When multiple objects contain the same property, the later value wins.

```javascript
const defaults = {
  theme: "light",
  language: "en"
};

const settings = {
  ...defaults,
  theme: "dark"
};
```

Result:

```javascript
{
  theme: "dark",
  language: "en"
}
```

The order matters.

---

# 13. Object Spread Order

```javascript
const first = {
  status: "pending"
};

const second = {
  status: "completed"
};

const result = {
  ...first,
  ...second
};
```

Result:

```javascript
{
  status: "completed"
}
```

If the order is reversed:

```javascript
const result = {
  ...second,
  ...first
};
```

Result:

```javascript
{
  status: "pending"
}
```

The last copied property overwrites earlier properties.

---

# 14. Adding Properties

```javascript
const product = {
  name: "Laptop",
  price: 85000
};

const productWithStock = {
  ...product,
  stock: 12
};
```

This creates a new object with the additional property.

---

# 15. Removing a Property With Object Rest

Spread and rest can work together.

```javascript
const user = {
  name: "Sandip",
  email: "sandip@example.com",
  password: "secret123"
};

const {
  password,
  ...safeUser
} = user;

console.log(safeUser);
```

Result:

```javascript
{
  name: "Sandip",
  email: "sandip@example.com"
}
```

Here:

* `password` is extracted
* `...safeUser` collects the remaining properties

This pattern is useful when creating a public version of an object.

---

# 16. Rest Parameter

The **rest parameter** collects multiple function arguments into an array.

```javascript
function sum(...numbers) {
  let total = 0;

  for (const number of numbers) {
    total += number;
  }

  return total;
}
```

Now:

```javascript
console.log(sum(10, 20));
console.log(sum(10, 20, 30, 40));
```

Output:

```text
30
100
```

---

# 17. Rest Parameter Is an Array

Inside the function:

```javascript
function showValues(...values) {
  console.log(values);
}
```

Calling:

```javascript
showValues("React", "Node.js", "MongoDB");
```

Produces:

```text
["React", "Node.js", "MongoDB"]
```

You can therefore use array methods:

```javascript
function countValues(...values) {
  return values.length;
}
```

---

# 18. Normal Parameters Before Rest

You can combine normal parameters with a rest parameter.

```javascript
function orderInfo(table, ...items) {
  console.log(table);
  console.log(items);
}

orderInfo("T-05", "Momo", "Chowmein", "Coffee");
```

Result:

```text
T-05
["Momo", "Chowmein", "Coffee"]
```

The first argument goes to `table`.

The remaining arguments go into `items`.

---

# 19. Rest Parameter Must Be Last

Correct:

```javascript
function example(first, second, ...others) {
  console.log(first);
  console.log(second);
  console.log(others);
}
```

Incorrect:

```javascript
function example(...others, last) {
}
```

Only one rest parameter is allowed, and it must be the final parameter.

---

# 20. Rest in Array Destructuring

Rest can collect remaining array elements.

```javascript
const [first, ...others] = [
  "HTML",
  "CSS",
  "JavaScript",
  "React"
];

console.log(first);
console.log(others);
```

Result:

```text
HTML
["CSS", "JavaScript", "React"]
```

---

# 21. Rest in Object Destructuring

```javascript
const account = {
  username: "sandip",
  email: "sandip@example.com",
  role: "admin"
};

const {
  username,
  ...details
} = account;

console.log(username);
console.log(details);
```

Result:

```text
sandip
{
  email: "sandip@example.com",
  role: "admin"
}
```

---

# 22. Spread vs Rest

The easiest way to remember the difference:

| Feature    | Spread                       | Rest                |
| ---------- | ---------------------------- | ------------------- |
| Purpose    | Expands                      | Collects            |
| Direction  | One → many                   | Many → one          |
| Common use | Copy/combine data            | Function parameters |
| Result     | Individual values/properties | Array/object        |
| Syntax     | `...value`                   | `...values`         |

Example of **spread**:

```javascript
const numbers = [1, 2, 3];

console.log(Math.max(...numbers));
```

Example of **rest**:

```javascript
function max(...numbers) {
  return Math.max(...numbers);
}
```

The first `...numbers` collects arguments.

The second `...numbers` expands the array.

---

# 23. Spread and Rest in the Same Code

```javascript
function getTotal(...prices) {
  return Math.max(...prices);
}

console.log(getTotal(20, 50, 30));
```

Here:

```text
getTotal(20, 50, 30)
        ↓
...prices collects
        ↓
[20, 50, 30]
        ↓
...prices expands
        ↓
Math.max(20, 50, 30)
```

---

# 24. Shallow Copy

Spread creates a **shallow copy**, not a deep copy.

For example:

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
```

The top-level object is different:

```javascript
console.log(copy === user);
```

Output:

```text
false
```

But the nested object is still shared:

```javascript
console.log(copy.address === user.address);
```

Output:

```text
true
```

---

# 25. Updating a Nested Object

If you want to update a nested property without modifying the original object:

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj",
    country: "Nepal"
  }
};

const updatedUser = {
  ...user,
  address: {
    ...user.address,
    city: "Kathmandu"
  }
};
```

Now:

```javascript
console.log(user.address.city);
console.log(updatedUser.address.city);
```

Output:

```text
Birgunj
Kathmandu
```

This pattern is common when updating nested React state.

---

# 26. Spread With React State

For an object state:

```jsx
setUser({
  ...user,
  name: "Sandip"
});
```

This creates a new object while keeping the other properties.

For an array state:

```jsx
setItems([
  ...items,
  newItem
]);
```

This creates a new array containing the previous items plus `newItem`.

---

# 27. Practical API Example

Suppose an API returns:

```javascript
const response = {
  id: 101,
  name: "Sandip",
  email: "sandip@example.com",
  role: "admin"
};
```

You can create a modified object:

```javascript
const displayUser = {
  ...response,
  displayName: response.name
};
```

Or exclude sensitive information:

```javascript
const {
  role,
  ...publicUser
} = response;
```

---

# 28. Practical Order Example

Suppose an order contains:

```javascript
const order = {
  table: "T-05",
  items: ["Momo", "Coffee"],
  status: "pending"
};
```

Create an updated order:

```javascript
const confirmedOrder = {
  ...order,
  status: "confirmed"
};
```

The original remains:

```javascript
console.log(order.status);
```

```text
pending
```

The new object contains:

```javascript
console.log(confirmedOrder.status);
```

```text
confirmed
```

---

# 29. Spread Does Not Deep Clone

This:

```javascript
const copy = {
  ...original
};
```

does **not** recursively copy every nested object.

For supported data types, `structuredClone()` can create a deep clone:

```javascript
const copy = structuredClone(original);
```

However, cloning strategy should depend on the data being handled.

---

# 30. Common Mistakes

### Mistake 1: Thinking spread and rest are different syntax

Both use:

```javascript
...
```

Their meaning depends on context.

---

### Mistake 2: Thinking spread creates a deep copy

```javascript
const copy = {
  ...original
};
```

This is only a shallow copy.

---

### Mistake 3: Putting rest in the wrong position

Invalid:

```javascript
function example(...values, last) {
}
```

Rest must be last.

---

### Mistake 4: Confusing array and object spread

Array:

```javascript
const result = [...array];
```

Object:

```javascript
const result = {...object};
```

They operate on different data structures.

---

### Mistake 5: Expecting spread to mutate the original

```javascript
const updated = {
  ...user,
  role: "admin"
};
```

This creates a new object. It does not directly change `user`.

---

# 31. Quick Reference

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
const result = [...items, newItem];
```

### Copy object

```javascript
const copy = {...object};
```

### Update object

```javascript
const updated = {
  ...object,
  property: newValue
};
```

### Collect function arguments

```javascript
function example(...args) {}
```

### Collect remaining array values

```javascript
const [first, ...rest] = array;
```

### Collect remaining object properties

```javascript
const {name, ...rest} = user;
```

### Expand function arguments

```javascript
functionName(...array);
```

---

# 32. Key Takeaways

* `...` can mean **spread** or **rest**.
* Spread expands values.
* Rest collects values.
* Spread is useful for copying and combining arrays.
* Spread is useful for copying and updating objects.
* Rest parameters collect function arguments into an array.
* Rest can also be used in destructuring.
* Rest must always be last.
* Object spread is useful for immutable updates.
* Array and object spread create shallow copies.
* Nested objects remain shared in a shallow copy.
* Spread and rest are heavily used in React, Node.js, APIs, and modern JavaScript.

## Remember

```text
SPREAD → EXPAND
REST   → COLLECT
```

Example:

```javascript
const values = [10, 20, 30];

console.log(Math.max(...values));
```

```javascript
function sum(...values) {
  return values.reduce((total, value) => total + value, 0);
}
```

---
