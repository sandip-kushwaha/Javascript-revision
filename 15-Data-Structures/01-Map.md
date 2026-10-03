# JavaScript Map

`Map` is a built-in JavaScript data structure used to store **key-value pairs**.

Unlike a normal object, a `Map` can use **almost any value as a key**, including objects, arrays, functions, numbers, strings, and other values.

---

## 1. What is Map?

A `Map` stores data like:

```text
key → value
```

Example:

```js
const users = new Map();

users.set(1, "Sandip");
users.set(2, "Ram");

console.log(users);
```

Conceptually:

```text
1 → "Sandip"
2 → "Ram"
```

---

# 2. Creating a Map

Create an empty Map:

```js
const map = new Map();

console.log(map);
```

You can also create a Map with initial entries:

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
  [3, "Hari"],
]);

console.log(users);
```

Each entry must have:

```text
[key, value]
```

---

# 3. set()

`set()` adds a key-value pair.

```js
const users = new Map();

users.set(1, "Sandip");
users.set(2, "Ram");
```

You can chain `set()` calls:

```js
const users = new Map();

users
  .set(1, "Sandip")
  .set(2, "Ram")
  .set(3, "Hari");
```

---

# 4. get()

`get()` retrieves the value associated with a key.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

console.log(users.get(1));
// Sandip

console.log(users.get(2));
// Ram
```

If the key doesn't exist:

```js
console.log(users.get(10));
// undefined
```

---

# 5. has()

`has()` checks whether a key exists.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

console.log(users.has(1));
// true

console.log(users.has(10));
// false
```

This is useful when you need to check before accessing or updating data.

---

# 6. delete()

`delete()` removes an entry.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

users.delete(2);

console.log(users.has(2));
// false
```

`delete()` returns:

```text
true  → entry was removed
false → key did not exist
```

Example:

```js
const removed = users.delete(1);

console.log(removed);
// true
```

---

# 7. clear()

`clear()` removes all entries.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

users.clear();

console.log(users.size);
// 0
```

---

# 8. size

`size` returns the number of entries.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
  [3, "Hari"],
]);

console.log(users.size);
// 3
```

Unlike an array:

```js
array.length
```

A Map uses:

```js
map.size
```

---

# 9. Updating a Value

Calling `set()` with an existing key updates its value.

```js
const users = new Map([
  [1, "Sandip"],
]);

users.set(1, "Sandip Prasad");

console.log(users.get(1));
// Sandip Prasad
```

There will still be only one entry for key `1`.

```js
console.log(users.size);
// 1
```

---

# 10. Map Keys Can Be Different Types

A Map can use different types as keys.

```js
const data = new Map();

data.set("name", "Sandip");
data.set(1, "User One");
data.set(true, "Active");
```

Retrieve them using the same key:

```js
console.log(data.get("name"));
// Sandip

console.log(data.get(1));
// User One

console.log(data.get(true));
// Active
```

---

# 11. Objects as Map Keys

One important feature of `Map` is that objects can be keys.

```js
const user = {
  id: 1,
};

const permissions = new Map();

permissions.set(user, "admin");

console.log(permissions.get(user));
// admin
```

The object itself is the key.

---

# 12. Object Keys Use Reference Identity

Two objects with identical contents are still different keys.

```js
const map = new Map();

const user1 = {
  id: 1,
};

const user2 = {
  id: 1,
};

map.set(user1, "Admin");

console.log(map.get(user1));
// Admin

console.log(map.get(user2));
// undefined
```

Why?

Because:

```js
user1 !== user2
```

They are different object references.

---

# 13. NaN as a Map Key

`Map` can use `NaN` as a key.

```js
const map = new Map();

map.set(NaN, "Not a Number");

console.log(map.get(NaN));
// Not a Number
```

A Map treats `NaN` as the same key when checking for another `NaN`.

```js
console.log(map.has(NaN));
// true
```

---

# 14. Iterating a Map

You can use `for...of` to iterate over entries.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
  [3, "Hari"],
]);

for (const [id, name] of users) {
  console.log(id, name);
}
```

Output:

```text
1 Sandip
2 Ram
3 Hari
```

Map iteration follows **insertion order**.

---

# 15. keys()

`keys()` returns an iterator containing the keys.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

for (const id of users.keys()) {
  console.log(id);
}
```

Output:

```text
1
2
```

---

# 16. values()

`values()` returns an iterator containing the values.

```js
for (const name of users.values()) {
  console.log(name);
}
```

Output:

```text
Sandip
Ram
```

---

# 17. entries()

`entries()` returns key-value pairs.

```js
for (const [id, name] of users.entries()) {
  console.log(id, name);
}
```

This is equivalent to:

```js
for (const [id, name] of users) {
  console.log(id, name);
}
```

because Map's default iterator is its entries.

---

# 18. forEach()

A Map also provides `forEach()`.

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

users.forEach((name, id) => {
  console.log(id, name);
});
```

Notice the callback order:

```text
value, key
```

not:

```text
key, value
```

---

# 19. Practical Example: Users by ID

A Map can be useful when you frequently need to find data by an identifier.

```js
const users = new Map([
  [101, {
    name: "Sandip",
    role: "admin",
  }],
  [102, {
    name: "Ram",
    role: "user",
  }],
]);

const user = users.get(101);

console.log(user);
```

Result:

```js
{
  name: "Sandip",
  role: "admin"
}
```

---

# 20. Practical Example: Product Lookup

```js
const products = new Map([
  ["P100", {
    name: "Laptop",
    price: 80000,
  }],
  ["P101", {
    name: "Mouse",
    price: 1200,
  }],
]);

const product = products.get("P101");

console.log(product.name);
// Mouse
```

This creates a convenient lookup structure.

---

# 21. Practical Example: Counting Values

A Map can be used to count occurrences.

```js
const items = [
  "apple",
  "banana",
  "apple",
  "orange",
  "banana",
  "apple",
];

const count = new Map();

for (const item of items) {
  count.set(
    item,
    (count.get(item) ?? 0) + 1
  );
}

console.log(count);
```

Conceptually:

```text
apple  → 3
banana → 2
orange → 1
```

---

# 22. Practical Example: Cache

Map can be used for simple in-memory caching.

```js
const cache = new Map();

function getUser(id) {
  if (cache.has(id)) {
    return cache.get(id);
  }

  const user = {
    id,
    name: `User ${id}`,
  };

  cache.set(id, user);

  return user;
}

console.log(getUser(1));
console.log(getUser(1));
```

The second lookup can reuse the cached value.

---

# 23. Map vs Object

Both can store key-value data, but they have different characteristics.

| Feature      | Map                    | Object                       |
| ------------ | ---------------------- | ---------------------------- |
| Key types    | Any value              | String or Symbol             |
| Size         | `map.size`             | Manual calculation           |
| Key order    | Insertion order        | Property ordering rules      |
| Iteration    | Built-in               | Usually `Object.keys()` etc. |
| `clear()`    | Yes                    | No direct equivalent         |
| Object keys  | Supported by reference | Converted to property keys   |
| Intended use | Key-value collection   | Records/entities             |

Example Object:

```js
const user = {
  name: "Sandip",
  age: 22,
};
```

Example Map:

```js
const users = new Map();

users.set(1, "Sandip");
users.set(2, "Ram");
```

Use the structure that best represents the data.

---

# 24. Converting Object to Map

`Object.entries()` can be passed to the `Map` constructor.

```js
const user = {
  name: "Sandip",
  age: 22,
};

const userMap = new Map(
  Object.entries(user)
);

console.log(userMap);
```

Conceptually:

```text
name → Sandip
age  → 22
```

---

# 25. Converting Map to Array

Use the spread operator:

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);

const entries = [...users];

console.log(entries);
```

Result:

```js
[
  [1, "Sandip"],
  [2, "Ram"]
]
```

You can also use:

```js
const entries = Array.from(users);
```

---

# 26. Converting Map to Object

If the Map keys are suitable as JavaScript object property keys:

```js
const users = new Map([
  ["name", "Sandip"],
  ["role", "admin"],
]);

const userObject = Object.fromEntries(users);

console.log(userObject);
```

Result:

```js
{
  name: "Sandip",
  role: "admin"
}
```

Be careful with non-string keys because ordinary object properties are limited to strings and symbols.

---

# 27. JSON and Map

JSON does not have a native Map data type.

This does not preserve a Map directly:

```js
const map = new Map([
  ["name", "Sandip"],
]);

JSON.stringify(map);
```

A common approach is to convert the Map to an array first:

```js
const json = JSON.stringify(
  [...map]
);
```

Later:

```js
const map = new Map(
  JSON.parse(json)
);
```

This is useful when transmitting or storing Map data as JSON.

---

# 28. Map Chaining

Because `set()` returns the Map itself, calls can be chained.

```js
const settings = new Map();

settings
  .set("theme", "dark")
  .set("language", "en")
  .set("fontSize", 16);
```

Then:

```js
console.log(settings.get("theme"));
// dark
```

---

# 29. Important Map Methods

```text
new Map()
```

Creates a Map.

```js
map.set(key, value)
```

Adds or updates an entry.

```js
map.get(key)
```

Gets a value.

```js
map.has(key)
```

Checks whether a key exists.

```js
map.delete(key)
```

Removes one entry.

```js
map.clear()
```

Removes all entries.

```js
map.size
```

Returns the number of entries.

```js
map.keys()
```

Returns keys.

```js
map.values()
```

Returns values.

```js
map.entries()
```

Returns key-value pairs.

```js
map.forEach()
```

Runs a function for each entry.

---

# 30. Map Example with Functions as Keys

Functions can also be keys.

```js
const cache = new Map();

const calculate = (value) => {
  return value * 2;
};

cache.set(calculate, "cached function");

console.log(
  cache.get(calculate)
);
```

The function reference itself is the key.

---

# 31. When to Use Map

`Map` is useful when:

* You need arbitrary key types.
* You frequently add and remove key-value entries.
* You need a collection specifically designed for key-value pairs.
* You need reliable insertion-order iteration.
* You need a convenient `size`.
* You need object or function references as keys.
* You are building lookup tables or caches.

Common use cases:

```text
User lookup
Product lookup
Caching
Counting
Permissions
Configuration
Graph structures
In-memory indexes
```

---

# 32. Map vs Array

An array is generally suitable for ordered lists:

```js
const users = [
  "Sandip",
  "Ram",
  "Hari",
];
```

A Map is suitable for key-value relationships:

```js
const users = new Map([
  [101, "Sandip"],
  [102, "Ram"],
  [103, "Hari"],
]);
```

Use an array when the primary concept is:

```text
list of values
```

Use a Map when the primary concept is:

```text
key → value
```

---

# 33. Map vs Set

`Map` stores:

```text
key → value
```

`Set` stores:

```text
unique value
```

Example Map:

```js
const users = new Map([
  [1, "Sandip"],
  [2, "Ram"],
]);
```

Example Set:

```js
const ids = new Set([
  1,
  2,
  3,
]);
```

The next file covers `Set` in detail.

---

# 34. Quick Cheat Sheet

```js
// Create
const map = new Map();

// Add
map.set("name", "Sandip");

// Get
map.get("name");

// Check
map.has("name");

// Delete
map.delete("name");

// Clear
map.clear();

// Size
map.size;

// Keys
map.keys();

// Values
map.values();

// Entries
map.entries();

// Iterate
for (const [key, value] of map) {
  console.log(key, value);
}
```

---

# 35. Key Points

```text
Map
 ↓
Key-value collection

set()
 ↓
Add or update

get()
 ↓
Read value

has()
 ↓
Check key

delete()
 ↓
Remove entry

clear()
 ↓
Remove everything

size
 ↓
Number of entries

keys()
 ↓
Keys

values()
 ↓
Values

entries()
 ↓
Key-value pairs
```

### Remember

```text
Object → record/entity with properties

Map → collection of key-value entries

Array → ordered list

Set → collection of unique values
```

`Map` is especially useful when your data naturally represents **lookup relationships** rather than a simple object or list.
