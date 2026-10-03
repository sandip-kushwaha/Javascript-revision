# JavaScript Set

`Set` is a built-in JavaScript data structure used to store **unique values**.

Unlike an array, a `Set` does not keep duplicate values.

---

# 1. What is Set?

A `Set` is a collection where each value can appear only once.

```js
const numbers = new Set();

numbers.add(10);
numbers.add(20);
numbers.add(10);

console.log(numbers);
```

Result:

```text
Set(2) { 10, 20 }
```

The second `10` is ignored because it already exists.

---

# 2. Creating a Set

Create an empty Set:

```js
const users = new Set();

console.log(users);
```

Create a Set with initial values:

```js
const numbers = new Set([
  10,
  20,
  30,
]);
```

Duplicates are automatically removed:

```js
const numbers = new Set([
  10,
  20,
  20,
  30,
  30,
]);

console.log(numbers);
```

Result:

```text
Set(3) { 10, 20, 30 }
```

---

# 3. add()

Use `add()` to add a value.

```js
const languages = new Set();

languages.add("JavaScript");
languages.add("Python");
languages.add("Java");

console.log(languages);
```

You can chain `add()` calls:

```js
const languages = new Set();

languages
  .add("JavaScript")
  .add("Python")
  .add("Java");
```

---

# 4. Adding Duplicate Values

Adding an existing value does not create another entry.

```js
const numbers = new Set();

numbers.add(10);
numbers.add(10);
numbers.add(10);

console.log(numbers.size);
// 1
```

This makes `Set` useful when uniqueness matters.

---

# 5. has()

`has()` checks whether a value exists.

```js
const languages = new Set([
  "JavaScript",
  "Python",
  "Java",
]);

console.log(
  languages.has("JavaScript")
);
// true

console.log(
  languages.has("C++")
);
// false
```

---

# 6. delete()

`delete()` removes a value.

```js
const languages = new Set([
  "JavaScript",
  "Python",
  "Java",
]);

languages.delete("Java");

console.log(languages);
```

`delete()` returns a boolean:

```text
true  → value was removed
false → value did not exist
```

Example:

```js
const removed = languages.delete("Python");

console.log(removed);
// true
```

---

# 7. clear()

`clear()` removes all values.

```js
const numbers = new Set([
  10,
  20,
  30,
]);

numbers.clear();

console.log(numbers.size);
// 0
```

---

# 8. size

Use `size` to get the number of unique values.

```js
const numbers = new Set([
  10,
  20,
  20,
  30,
]);

console.log(numbers.size);
// 3
```

Remember:

```text
Array → length

Set → size

Map → size
```

---

# 9. Iterating a Set

You can use `for...of`:

```js
const languages = new Set([
  "JavaScript",
  "Python",
  "Java",
]);

for (const language of languages) {
  console.log(language);
}
```

Output:

```text
JavaScript
Python
Java
```

A Set preserves insertion order during iteration.

---

# 10. values()

`values()` returns an iterator over the values.

```js
const numbers = new Set([
  10,
  20,
  30,
]);

for (const number of numbers.values()) {
  console.log(number);
}
```

Output:

```text
10
20
30
```

---

# 11. keys()

Set does not have separate keys and values like a Map.

However, `keys()` exists for compatibility and returns the same values as `values()`.

```js
const numbers = new Set([
  10,
  20,
  30,
]);

for (const value of numbers.keys()) {
  console.log(value);
}
```

Output:

```text
10
20
30
```

For a Set:

```js
set.keys() === set.values()
```

is not necessarily the correct comparison because each call returns a different iterator object, but both iterate the same values.

---

# 12. entries()

`entries()` returns pairs where the value appears twice.

```js
const numbers = new Set([
  10,
  20,
  30,
]);

for (const [key, value] of numbers.entries()) {
  console.log(key, value);
}
```

Output:

```text
10 10
20 20
30 30
```

This behavior exists mainly to make Set compatible with APIs that work with key-value collections.

---

# 13. forEach()

Set provides `forEach()`.

```js
const languages = new Set([
  "JavaScript",
  "Python",
  "Java",
]);

languages.forEach((language) => {
  console.log(language);
});
```

Output:

```text
JavaScript
Python
Java
```

The callback receives the value twice when using the full callback signature:

```js
set.forEach((value, valueAgain, set) => {
  console.log(value);
});
```

This matches the `Map` callback shape.

---

# 14. Removing Duplicates from an Array

One of the most common uses of `Set` is removing duplicates.

```js
const numbers = [
  10,
  20,
  20,
  30,
  30,
  40,
];

const uniqueNumbers = [
  ...new Set(numbers),
];

console.log(uniqueNumbers);
```

Result:

```js
[10, 20, 30, 40]
```

This pattern is very useful:

```js
const unique = [...new Set(array)];
```

---

# 15. Unique Strings

```js
const skills = [
  "JavaScript",
  "React",
  "JavaScript",
  "Node.js",
  "React",
];

const uniqueSkills = [
  ...new Set(skills),
];

console.log(uniqueSkills);
```

Result:

```js
[
  "JavaScript",
  "React",
  "Node.js"
]
```

---

# 16. Set with Different Data Types

A Set can contain different types of values.

```js
const data = new Set();

data.add("Sandip");
data.add(22);
data.add(true);
data.add(null);

console.log(data);
```

Set values can include:

```text
String
Number
Boolean
Object
Array
Function
Symbol
BigInt
null
undefined
```

---

# 17. Objects in a Set

Objects can be stored in a Set.

```js
const user1 = {
  id: 1,
};

const user2 = {
  id: 2,
};

const users = new Set();

users.add(user1);
users.add(user2);

console.log(users.size);
// 2
```

---

# 18. Object Reference Identity

Two objects with the same properties are still different objects.

```js
const user1 = {
  id: 1,
};

const user2 = {
  id: 1,
};

const users = new Set();

users.add(user1);
users.add(user2);

console.log(users.size);
// 2
```

Because:

```js
user1 !== user2
```

They have different object references.

---

# 19. Same Object Reference

If the same object reference is added multiple times, only one entry exists.

```js
const user = {
  id: 1,
};

const users = new Set();

users.add(user);
users.add(user);
users.add(user);

console.log(users.size);
// 1
```

---

# 20. NaN in Set

A Set can contain `NaN`.

```js
const values = new Set();

values.add(NaN);
values.add(NaN);

console.log(values.size);
// 1
```

The Set treats `NaN` as the same value when checking uniqueness.

---

# 21. Practical Example: Unique User IDs

Suppose an application receives duplicate user IDs:

```js
const userIds = [
  101,
  102,
  101,
  103,
  102,
  104,
];
```

Create a unique collection:

```js
const uniqueUserIds = [
  ...new Set(userIds),
];

console.log(uniqueUserIds);
```

Result:

```js
[
  101,
  102,
  103,
  104
]
```

---

# 22. Practical Example: Unique Tags

```js
const tags = [
  "javascript",
  "react",
  "node",
  "javascript",
  "react",
];

const uniqueTags = new Set(tags);

console.log(uniqueTags);
```

Convert back to an array when needed:

```js
const tagList = [...uniqueTags];
```

---

# 23. Practical Example: Tracking Selected IDs

A Set is useful when an application needs to track selected items.

```js
const selectedProducts = new Set();

selectedProducts.add("P100");
selectedProducts.add("P101");

console.log(
  selectedProducts.has("P100")
);
// true
```

Remove a selected item:

```js
selectedProducts.delete("P100");
```

This avoids manually checking for duplicates.

---

# 24. Practical Example: Visited Pages

```js
const visitedPages = new Set();

visitedPages.add("/home");
visitedPages.add("/products");
visitedPages.add("/home");

console.log(visitedPages);
```

The `/home` page appears only once.

---

# 25. Converting Set to Array

Spread syntax:

```js
const numbers = new Set([
  10,
  20,
  30,
]);

const array = [...numbers];

console.log(array);
```

Using `Array.from()`:

```js
const array = Array.from(numbers);
```

Both produce an array.

---

# 26. Converting Array to Set

```js
const numbers = [
  10,
  20,
  20,
  30,
];

const uniqueNumbers = new Set(numbers);

console.log(uniqueNumbers);
```

This is useful when you want to temporarily enforce uniqueness.

---

# 27. Set Operations

JavaScript now provides built-in Set methods for common mathematical set operations in modern runtimes.

Consider:

```js
const frontend = new Set([
  "HTML",
  "CSS",
  "JavaScript",
  "React",
]);

const backend = new Set([
  "JavaScript",
  "Node.js",
  "MongoDB",
]);
```

---

## Union

Union contains values from both Sets.

```js
const allSkills =
  frontend.union(backend);

console.log(allSkills);
```

Conceptually:

```text
HTML
CSS
JavaScript
React
Node.js
MongoDB
```

---

## Intersection

Intersection contains values present in both Sets.

```js
const common =
  frontend.intersection(backend);

console.log(common);
```

Result:

```text
JavaScript
```

---

## Difference

Difference contains values in the first Set that are not in the second.

```js
const onlyFrontend =
  frontend.difference(backend);
```

Result:

```text
HTML
CSS
React
```

---

## Symmetric Difference

Symmetric difference contains values that appear in exactly one of the two Sets.

```js
const different =
  frontend.symmetricDifference(backend);
```

Conceptually:

```text
HTML
CSS
React
Node.js
MongoDB
```

---

# 28. Set Relationship Methods

Modern Set APIs also provide methods for checking relationships.

## isSubsetOf()

```js
const basic = new Set([
  "HTML",
  "CSS",
]);

const web = new Set([
  "HTML",
  "CSS",
  "JavaScript",
]);

console.log(
  basic.isSubsetOf(web)
);
// true
```

---

## isSupersetOf()

```js
console.log(
  web.isSupersetOf(basic)
);
// true
```

---

## isDisjointFrom()

Checks whether two Sets have no values in common.

```js
const a = new Set([1, 2]);

const b = new Set([3, 4]);

console.log(
  a.isDisjointFrom(b)
);
// true
```

These Set methods are available in modern JavaScript environments.

---

# 29. Set vs Array

| Feature          | Set                              | Array              |
| ---------------- | -------------------------------- | ------------------ |
| Duplicate values | Not allowed                      | Allowed            |
| Order            | Insertion order during iteration | Ordered            |
| Access by index  | No                               | Yes                |
| `length`         | No                               | Yes                |
| `size`           | Yes                              | No                 |
| `has()`          | Yes                              | No                 |
| `delete()`       | Yes                              | No                 |
| `push()`         | No                               | Yes                |
| Main purpose     | Unique values                    | Ordered collection |

Example:

```js
const numbers = [
  10,
  20,
  20,
];
```

Duplicates remain.

With Set:

```js
const numbers = new Set([
  10,
  20,
  20,
]);
```

Duplicates are removed.

---

# 30. Set vs Map

`Set` stores values:

```text
value
```

`Map` stores:

```text
key → value
```

Example Set:

```js
const ids = new Set([
  101,
  102,
  103,
]);
```

Example Map:

```js
const users = new Map([
  [101, "Sandip"],
  [102, "Ram"],
]);
```

Use Set when uniqueness is the main requirement.

Use Map when you need a relationship between keys and values.

---

# 31. Set vs Object

An Object usually represents a record:

```js
const user = {
  name: "Sandip",
  age: 22,
};
```

A Set represents a collection of unique values:

```js
const roles = new Set([
  "admin",
  "waiter",
  "kitchen",
]);
```

They solve different problems.

---

# 32. Important Set Methods

```text
new Set()
```

Creates a Set.

```js
set.add(value)
```

Adds a value.

```js
set.has(value)
```

Checks whether a value exists.

```js
set.delete(value)
```

Removes a value.

```js
set.clear()
```

Removes all values.

```js
set.size
```

Returns the number of unique values.

```js
set.values()
```

Returns values.

```js
set.keys()
```

Returns the same values for Set iteration.

```js
set.entries()
```

Returns `[value, value]` pairs.

```js
set.forEach()
```

Iterates over values.

---

# 33. Quick Cheat Sheet

```js
// Create
const set = new Set();

// Add
set.add("JavaScript");

// Check
set.has("JavaScript");

// Delete
set.delete("JavaScript");

// Clear
set.clear();

// Size
set.size;

// Iterate
for (const value of set) {
  console.log(value);
}
```

Remove duplicates:

```js
const unique = [...new Set(array)];
```

---

# 34. Common Use Cases

Set is commonly useful for:

```text
Unique IDs
Unique usernames
Selected items
Visited pages
Tags
Permissions
Categories
Deduplication
Membership checking
Set operations
```

---

# 35. Key Points

```text
Set
 ↓
Collection of unique values

add()
 ↓
Add value

has()
 ↓
Check value

delete()
 ↓
Remove value

clear()
 ↓
Remove everything

size
 ↓
Number of unique values
```

### Remember

```text
Array
→ ordered collection
→ duplicates allowed
→ index access

Set
→ unique collection
→ duplicates ignored
→ no index access

Map
→ key-value collection
→ arbitrary key types
```

The next data structure is **WeakMap**, which is useful when you want object-keyed data that can participate in garbage collection.
