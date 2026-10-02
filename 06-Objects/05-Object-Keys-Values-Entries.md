# JavaScript Object Keys, Values, and Entries

JavaScript provides useful methods for getting information from an object's properties.

The three main methods are:

```javascript
Object.keys()
Object.values()
Object.entries()
```

They are useful when working with:

* Objects
* API responses
* Database data
* Forms
* Loops
* React
* Node.js
* Dynamic data

---

# 1. Example Object

Consider this object:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};
```

It contains:

```text
Properties:
name
age
city
```

The corresponding values are:

```text
Sandip
22
Birgunj
```

---

# 2. `Object.keys()`

`Object.keys()` returns an array containing the object's **own enumerable property names**.

### Syntax

```javascript
Object.keys(object);
```

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const keys = Object.keys(user);

console.log(keys);
```

Output:

```text
["name", "age", "city"]
```

---

# 3. Understanding `Object.keys()`

Given:

```javascript
const user = {
  name: "Sandip",
  age: 22
};
```

This:

```javascript
Object.keys(user);
```

returns:

```javascript
["name", "age"]
```

It returns the **property names**, not their values.

---

# 4. `Object.keys()` Returns an Array

The result of `Object.keys()` is a normal array.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const keys = Object.keys(user);

console.log(Array.isArray(keys));
```

Output:

```text
true
```

Therefore, you can use array methods on the result:

```javascript
Object.keys(user).forEach((key) => {
  console.log(key);
});
```

Output:

```text
name
age
```

---

# 5. Looping Through Object Keys

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const keys = Object.keys(user);

keys.forEach((key) => {
  console.log(key);
});
```

Output:

```text
name
age
city
```

---

# 6. Getting Values Using Keys

You can combine `Object.keys()` with bracket notation.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

Object.keys(user).forEach((key) => {
  console.log(user[key]);
});
```

Output:

```text
Sandip
22
Birgunj
```

Here:

```javascript
user[key]
```

gets the value associated with the current key.

---

# 7. `Object.values()`

`Object.values()` returns an array containing the object's **own enumerable property values**.

### Syntax

```javascript
Object.values(object);
```

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const values = Object.values(user);

console.log(values);
```

Output:

```text
["Sandip", 22, "Birgunj"]
```

---

# 8. Understanding `Object.values()`

Given:

```javascript
const product = {
  name: "Laptop",
  price: 80000,
  available: true
};
```

This:

```javascript
Object.values(product);
```

returns:

```javascript
["Laptop", 80000, true]
```

It returns the **values**, not the property names.

---

# 9. Looping Through Values

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

Object.values(user).forEach((value) => {
  console.log(value);
});
```

Output:

```text
Sandip
22
Birgunj
```

---

# 10. `Object.entries()`

`Object.entries()` returns an array containing the object's property-value pairs.

### Syntax

```javascript
Object.entries(object);
```

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const entries = Object.entries(user);

console.log(entries);
```

Output:

```javascript
[
  ["name", "Sandip"],
  ["age", 22],
  ["city", "Birgunj"]
]
```

Each entry is an array containing:

```text
[key, value]
```

---

# 11. Understanding `Object.entries()`

Given:

```javascript
const user = {
  name: "Sandip",
  age: 22
};
```

The result is:

```javascript
[
  ["name", "Sandip"],
  ["age", 22]
]
```

Think of it as:

```text
[
  [key, value],
  [key, value]
]
```

---

# 12. Looping Through Entries

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

Object.entries(user).forEach(([key, value]) => {
  console.log(key, value);
});
```

Output:

```text
name Sandip
age 22
city Birgunj
```

Here we are using **array destructuring**:

```javascript
[key, value]
```

---

# 13. `Object.keys()` vs `Object.values()` vs `Object.entries()`

Consider:

```javascript
const user = {
  name: "Sandip",
  age: 22
};
```

### `Object.keys()`

```javascript
Object.keys(user);
```

Result:

```javascript
["name", "age"]
```

### `Object.values()`

```javascript
Object.values(user);
```

Result:

```javascript
["Sandip", 22]
```

### `Object.entries()`

```javascript
Object.entries(user);
```

Result:

```javascript
[
  ["name", "Sandip"],
  ["age", 22]
]
```

---

# 14. Quick Comparison

| Method             | Returns              |
| ------------------ | -------------------- |
| `Object.keys()`    | Property names       |
| `Object.values()`  | Property values      |
| `Object.entries()` | `[key, value]` pairs |

Easy way to remember:

```text
keys    → names
values  → values
entries → both
```

---

# 15. Using `Object.keys()` to Count Properties

Because `Object.keys()` returns an array, you can use `.length`.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

console.log(Object.keys(user).length);
```

Output:

```text
3
```

This tells you there are three own enumerable properties.

---

# 16. Checking if an Object Is Empty

You can use:

```javascript
Object.keys(object).length === 0
```

Example:

```javascript
const user = {};

if (Object.keys(user).length === 0) {
  console.log("Object is empty");
}
```

Output:

```text
Object is empty
```

---

# 17. Checking if an Object Has Properties

```javascript
const user = {
  name: "Sandip"
};

if (Object.keys(user).length > 0) {
  console.log("Object has properties");
}
```

Output:

```text
Object has properties
```

---

# 18. Finding a Specific Key

You can use `.includes()` with `Object.keys()`.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

console.log(
  Object.keys(user).includes("name")
);
```

Output:

```text
true
```

For a missing key:

```javascript
console.log(
  Object.keys(user).includes("email")
);
```

Output:

```text
false
```

For a direct own-property check, however, this is usually simpler:

```javascript
Object.hasOwn(user, "name");
```

---

# 19. Finding a Specific Value

You can use `.includes()` with `Object.values()`.

```javascript
const user = {
  name: "Sandip",
  city: "Birgunj"
};

console.log(
  Object.values(user).includes("Sandip")
);
```

Output:

```text
true
```

Another example:

```javascript
console.log(
  Object.values(user).includes("Kathmandu")
);
```

Output:

```text
false
```

---

# 20. Searching Entries

`Object.entries()` can be useful when you need both the key and value.

```javascript
const user = {
  name: "Sandip",
  role: "admin"
};

const result = Object.entries(user).find(
  ([key, value]) => key === "role"
);

console.log(result);
```

Output:

```text
["role", "admin"]
```

---

# 21. Converting an Object to Entries

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const entries = Object.entries(user);

console.log(entries);
```

Result:

```javascript
[
  ["name", "Sandip"],
  ["age", 22]
]
```

This can be useful when you want to use array methods such as:

```javascript
map()
filter()
find()
reduce()
forEach()
```

---

# 22. Filtering Object Properties

You can use `Object.entries()` with `filter()`.

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const filtered = Object.entries(user)
  .filter(([key]) => key !== "age");

console.log(filtered);
```

Result:

```javascript
[
  ["name", "Sandip"],
  ["city", "Birgunj"]
]
```

---

# 23. Converting Entries Back Into an Object

Use:

```javascript
Object.fromEntries()
```

Example:

```javascript
const entries = [
  ["name", "Sandip"],
  ["age", 22]
];

const user = Object.fromEntries(entries);

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

# 24. `Object.entries()` + `Object.fromEntries()`

These methods can work together.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const entries = Object.entries(user);

const newUser = Object.fromEntries(entries);

console.log(newUser);
```

The result has the same properties.

---

# 25. Transforming Object Values

Suppose you want to increase all product prices by 10%.

```javascript
const products = {
  laptop: 80000,
  phone: 30000,
  mouse: 1500
};

const updatedProducts = Object.fromEntries(
  Object.entries(products).map(([name, price]) => [
    name,
    price * 1.1
  ])
);

console.log(updatedProducts);
```

Result:

```javascript
{
  laptop: 88000,
  phone: 33000,
  mouse: 1650
}
```

This is a powerful pattern:

```text
Object
   ↓
Object.entries()
   ↓
Array
   ↓
map/filter
   ↓
Object.fromEntries()
   ↓
Object
```

---

# 26. Filtering Object Properties

You can remove properties based on their values.

```javascript
const scores = {
  math: 80,
  science: 65,
  english: 90
};

const passedSubjects = Object.fromEntries(
  Object.entries(scores)
    .filter(([subject, score]) => score >= 70)
);

console.log(passedSubjects);
```

Result:

```javascript
{
  math: 80,
  english: 90
}
```

---

# 27. Hotel Table Example

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "occupied",
  location: "indoor"
};
```

### Get keys

```javascript
console.log(Object.keys(table));
```

Output:

```text
["tableNumber", "capacity", "status", "location"]
```

### Get values

```javascript
console.log(Object.values(table));
```

Output:

```text
["T-03", 6, "occupied", "indoor"]
```

### Get entries

```javascript
console.log(Object.entries(table));
```

Output:

```javascript
[
  ["tableNumber", "T-03"],
  ["capacity", 6],
  ["status", "occupied"],
  ["location", "indoor"]
]
```

---

# 28. Food Example

```javascript
const food = {
  name: "Chicken Momo",
  price: 180,
  isVeg: false,
  isAvailable: true
};
```

Get keys:

```javascript
Object.keys(food);
```

Result:

```javascript
["name", "price", "isVeg", "isAvailable"]
```

Get values:

```javascript
Object.values(food);
```

Result:

```javascript
["Chicken Momo", 180, false, true]
```

Get entries:

```javascript
Object.entries(food);
```

Result:

```javascript
[
  ["name", "Chicken Momo"],
  ["price", 180],
  ["isVeg", false],
  ["isAvailable", true]
]
```

---

# 29. Order Example

```javascript
const order = {
  orderNumber: "ORD-001",
  status: "pending",
  totalAmount: 850
};

Object.entries(order).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

Output:

```text
orderNumber: ORD-001
status: pending
totalAmount: 850
```

This pattern is useful for displaying dynamic object data.

---

# 30. React Example

Suppose you have:

```javascript
const user = {
  name: "Sandip",
  email: "sandip@example.com",
  role: "admin"
};
```

You can display its properties dynamically:

```jsx
{Object.entries(user).map(([key, value]) => (
  <p key={key}>
    {key}: {String(value)}
  </p>
))}
```

`Object.entries()` converts the object into an array that React can iterate over using `map()`.

---

# 31. API Response Example

Suppose an API returns:

```javascript
const response = {
  username: "sandip",
  email: "sandip@example.com",
  role: "admin"
};
```

You can inspect the fields:

```javascript
console.log(Object.keys(response));
```

You can inspect the values:

```javascript
console.log(Object.values(response));
```

Or process both:

```javascript
Object.entries(response).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

---

# 32. `Object.keys()` Only Gets Own Enumerable Properties

Consider:

```javascript
const user = {
  name: "Sandip"
};
```

Then:

```javascript
Object.keys(user);
```

returns:

```javascript
["name"]
```

It does not include properties inherited through the prototype chain.

This is why `Object.keys()` is useful when you want the object's own enumerable properties.

---

# 33. Enumerable Properties

In simple terms, an **enumerable property** is a property that is included in common property iteration operations.

Normal object properties created like this:

```javascript
const user = {
  name: "Sandip"
};
```

are enumerable.

Therefore:

```javascript
Object.keys(user);
```

includes:

```text
name
```

Property descriptors can control whether a property is enumerable, but that is a more advanced topic.

---

# 34. Object With No Properties

```javascript
const user = {};

console.log(Object.keys(user));
console.log(Object.values(user));
console.log(Object.entries(user));
```

Output:

```javascript
[]
[]
[]
```

All three return empty arrays.

---

# 35. Nested Objects

Consider:

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj",
    country: "Nepal"
  }
};
```

`Object.keys()` only gets the top-level properties:

```javascript
console.log(Object.keys(user));
```

Output:

```text
["name", "address"]
```

It does not automatically get:

```text
city
country
```

You can separately inspect the nested object:

```javascript
console.log(Object.keys(user.address));
```

Output:

```text
["city", "country"]
```

---

# 36. Object Keys Are Strings or Symbols

JavaScript object property keys are generally:

* Strings
* Symbols

For example:

```javascript
const user = {
  name: "Sandip"
};
```

The key:

```text
name
```

is a string property key.

Symbol keys are more advanced and are not included by `Object.keys()`.

---

# 37. Number-Like Keys

Consider:

```javascript
const marks = {
  101: 80,
  102: 90
};
```

Now:

```javascript
console.log(Object.keys(marks));
```

Result:

```javascript
["101", "102"]
```

Number-like object keys are returned as strings.

---

# 38. Property Order

For ordinary object properties, JavaScript has defined ordering rules for property keys.

Example:

```javascript
const data = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

console.log(Object.keys(data));
```

Result follows the object's property order:

```javascript
["name", "age", "city"]
```

For integer-index-like keys, JavaScript applies special ordering rules.

For normal application objects, the important point is that `Object.keys()`, `Object.values()`, and `Object.entries()` use the same corresponding property ordering.

---

# 39. Common Mistakes

## Mistake 1: Expecting `Object.keys()` to return values

```javascript
Object.keys(user);
```

returns:

```javascript
["name", "age"]
```

Not:

```javascript
["Sandip", 22]
```

For values, use:

```javascript
Object.values(user);
```

---

## Mistake 2: Expecting `Object.values()` to return keys

Use:

```javascript
Object.keys(user);
```

for keys.

---

## Mistake 3: Forgetting that `Object.entries()` returns arrays

This:

```javascript
Object.entries(user);
```

returns:

```javascript
[
  ["name", "Sandip"],
  ["age", 22]
]
```

not an object.

---

## Mistake 4: Using `forEach()` directly on an object

This does not work:

```javascript
user.forEach(...);
```

Objects do not have `forEach()`.

Instead:

```javascript
Object.entries(user).forEach(([key, value]) => {
  console.log(key, value);
});
```

---

# 40. Cheat Sheet

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};
```

### Keys

```javascript
Object.keys(user);
```

Result:

```javascript
["name", "age", "city"]
```

### Values

```javascript
Object.values(user);
```

Result:

```javascript
["Sandip", 22, "Birgunj"]
```

### Entries

```javascript
Object.entries(user);
```

Result:

```javascript
[
  ["name", "Sandip"],
  ["age", 22],
  ["city", "Birgunj"]
]
```

### Convert entries back to object

```javascript
Object.fromEntries(
  Object.entries(user)
);
```

---

# 41. Quick Comparison

```text
Object
   │
   ├── Object.keys()
   │      ↓
   │   ["name", "age"]
   │
   ├── Object.values()
   │      ↓
   │   ["Sandip", 22]
   │
   └── Object.entries()
          ↓
      [["name", "Sandip"], ["age", 22]]
```

---

# 42. Key Takeaways

* `Object.keys()` returns an array of own enumerable property names.
* `Object.values()` returns an array of own enumerable property values.
* `Object.entries()` returns an array of `[key, value]` pairs.
* All three return arrays.
* You can use array methods such as `map()`, `filter()`, `find()`, and `forEach()` on their results.
* `Object.entries()` is especially useful when you need both keys and values.
* `Object.fromEntries()` converts `[key, value]` pairs back into an object.
* These methods are very useful when working with dynamic data and API responses.
* They only operate on the object's own enumerable string-keyed properties.

---

## Quick Example

```javascript
const user = {
  name: "Sandip",
  age: 22,
  role: "admin"
};

console.log(Object.keys(user));

console.log(Object.values(user));

Object.entries(user).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

Output:

```text
["name", "age", "role"]

["Sandip", 22, "admin"]

name: Sandip
age: 22
role: admin
```

---
