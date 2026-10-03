# JavaScript WeakSet

`WeakSet` is a JavaScript collection used to store **objects without keeping those objects strongly reachable just because they are members of the collection**.

It is similar to `Set`, but it is designed specifically for object membership and weak references.

---

# 1. What is WeakSet?

A `WeakSet` stores unique objects.

```js
const weakSet = new WeakSet();

const user = {
  name: "Sandip",
};

weakSet.add(user);

console.log(weakSet.has(user));
// true
```

Unlike a normal `Set`, a `WeakSet` does not keep its object members alive by itself.

---

# 2. Creating a WeakSet

Create an empty WeakSet:

```js
const weakSet = new WeakSet();

console.log(weakSet);
```

You can also initialize it with objects:

```js
const user1 = {
  name: "Sandip",
};

const user2 = {
  name: "Ram",
};

const users = new WeakSet([
  user1,
  user2,
]);
```

---

# 3. WeakSet Stores Objects

The main rule is:

```text
WeakSet → objects
```

Example:

```js
const users = new WeakSet();

const user = {
  id: 1,
};

users.add(user);
```

You can also add arrays:

```js
const list = [];

users.add(list);
```

Functions can also be stored:

```js
const task = () => {
  console.log("Task");
};

users.add(task);
```

---

# 4. Primitive Values Are Not Allowed

A WeakSet cannot contain ordinary primitive values.

For example:

```js
const values = new WeakSet();

values.add("JavaScript");
```

This throws a `TypeError`.

Primitive values include:

```text
String
Number
Boolean
BigInt
Symbol
null
undefined
```

Use objects instead:

```js
const value = {
  name: "JavaScript",
};

values.add(value);
```

---

# 5. add()

`add()` adds an object to the WeakSet.

```js
const users = new WeakSet();

const user = {
  name: "Sandip",
};

users.add(user);
```

`add()` returns the WeakSet, so chaining is possible:

```js
const users = new WeakSet();

users
  .add(user1)
  .add(user2);
```

---

# 6. Duplicate Objects

Adding the same object multiple times does not create duplicates.

```js
const user = {
  id: 1,
};

const users = new WeakSet();

users.add(user);
users.add(user);
users.add(user);
```

There is still only one membership entry for that object.

However, remember that WeakSet does not provide `size`, so you cannot check the number directly.

---

# 7. Object Identity

WeakSet uses object identity.

```js
const user1 = {
  id: 1,
};

const user2 = {
  id: 1,
};

const users = new WeakSet();

users.add(user1);

console.log(users.has(user1));
// true

console.log(users.has(user2));
// false
```

Why?

```js
user1 !== user2;
```

They are two different object references.

---

# 8. Same Object Reference

If the same reference is used, membership is preserved.

```js
const user = {
  id: 1,
};

const users = new WeakSet();

users.add(user);

console.log(users.has(user));
// true
```

If another variable points to the same object:

```js
const sameUser = user;

console.log(users.has(sameUser));
// true
```

Both variables refer to the same object.

---

# 9. has()

`has()` checks whether an object belongs to the WeakSet.

```js
const users = new WeakSet();

const user = {
  id: 1,
};

users.add(user);

console.log(users.has(user));
// true
```

For an object that is not stored:

```js
const anotherUser = {
  id: 2,
};

console.log(users.has(anotherUser));
// false
```

---

# 10. delete()

`delete()` removes an object from the WeakSet.

```js
const users = new WeakSet();

const user = {
  id: 1,
};

users.add(user);

users.delete(user);

console.log(users.has(user));
// false
```

Return values:

```text
true  → object was removed
false → object was not present
```

---

# 11. WeakSet Does Not Have clear()

Unlike `Set`, WeakSet does not provide:

```js
weakSet.clear();
```

This method does not exist.

Remove an individual object with:

```js
weakSet.delete(object);
```

If you no longer need the entire collection, you can discard your reference to it:

```js
let users = new WeakSet();

users = new WeakSet();
```

---

# 12. WeakSet Does Not Have size

A WeakSet does not provide:

```js
weakSet.size;
```

You cannot ask it:

```text
How many objects are currently inside?
```

This is intentional because members can become eligible for garbage collection when no strong references remain.

---

# 13. WeakSet Is Not Iterable

You cannot use:

```js
for (const user of weakSet) {
  console.log(user);
}
```

WeakSet does not provide:

```js
weakSet.keys();
weakSet.values();
weakSet.entries();
weakSet.forEach();
```

Its main operations are:

```text
add()
has()
delete()
```

---

# 14. Why WeakSet Is Not Iterable

Consider:

```js
let user = {
  name: "Sandip",
};

const users = new WeakSet();

users.add(user);
```

Now:

```js
user = null;
```

If no other strong reference to the object exists, the object can become eligible for garbage collection.

Because membership can disappear as a result of garbage collection, WeakSet cannot provide predictable iteration over all members.

The JavaScript engine decides when garbage collection occurs.

---

# 15. WeakSet and Garbage Collection

This is the key difference from `Set`.

With a normal Set:

```js
let user = {
  name: "Sandip",
};

const users = new Set();

users.add(user);

user = null;
```

The Set still strongly references the object.

With a WeakSet:

```js
let user = {
  name: "Sandip",
};

const users = new WeakSet();

users.add(user);

user = null;
```

If there are no other strong references, the object can become eligible for garbage collection.

WeakSet itself does not keep the object alive.

---

# 16. WeakSet Does Not Trigger Garbage Collection

WeakSet does not manually remove objects from memory.

It only avoids creating a strong reference from the collection to its members.

The JavaScript engine controls garbage collection.

So this:

```text
WeakSet
   ↓
does not force GC
```

Instead:

```text
No strong references
        ↓
Object becomes eligible for GC
        ↓
Engine may eventually collect it
```

---

# 17. Practical Example: Tracking Processed Objects

A WeakSet can be useful when you want to remember whether an object has already been processed.

```js
const processed = new WeakSet();

function processUser(user) {
  if (processed.has(user)) {
    console.log("Already processed");
    return;
  }

  console.log("Processing:", user.name);

  processed.add(user);
}
```

Usage:

```js
const user = {
  name: "Sandip",
};

processUser(user);
processUser(user);
```

Output:

```text
Processing: Sandip
Already processed
```

---

# 18. Practical Example: Prevent Duplicate Processing

Suppose an application receives the same object reference multiple times.

```js
const visited = new WeakSet();

function visit(page) {
  if (visited.has(page)) {
    return;
  }

  visited.add(page);

  console.log("Visiting page");
}
```

Example:

```js
const page = {
  url: "/dashboard",
};

visit(page);
visit(page);
```

The second call can detect that the object was already processed.

---

# 19. Practical Example: DOM Elements

WeakSet can be useful for tracking DOM elements that have already been initialized.

```js
const initialized = new WeakSet();

function initialize(button) {
  if (initialized.has(button)) {
    return;
  }

  initialized.add(button);

  button.addEventListener("click", () => {
    console.log("Clicked");
  });
}
```

Now:

```js
const button = document.querySelector("#save");

initialize(button);
initialize(button);
```

The listener setup can be performed only once for that object.

---

# 20. Practical Example: Tracking Objects

```js
const activeObjects = new WeakSet();

function activate(object) {
  activeObjects.add(object);
}

function isActive(object) {
  return activeObjects.has(object);
}

const user = {
  id: 101,
};

activate(user);

console.log(isActive(user));
// true
```

The WeakSet stores membership rather than additional data.

If you need associated data such as:

```text
user → role
user → login count
user → settings
```

a `WeakMap` is more appropriate.

---

# 21. WeakSet vs Set

| Feature                | Set    | WeakSet |
| ---------------------- | ------ | ------- |
| Stores                 | Values | Objects |
| Primitive values       | Yes    | No      |
| Duplicate members      | No     | No      |
| `add()`                | Yes    | Yes     |
| `has()`                | Yes    | Yes     |
| `delete()`             | Yes    | Yes     |
| `clear()`              | Yes    | No      |
| `size`                 | Yes    | No      |
| Iteration              | Yes    | No      |
| `keys()`               | Yes    | No      |
| `values()`             | Yes    | No      |
| `entries()`            | Yes    | No      |
| `forEach()`            | Yes    | No      |
| Weak object references | No     | Yes     |

---

# 22. WeakSet vs WeakMap

Both use weak references to objects.

### WeakSet

Stores membership:

```text
object
```

Example:

```js
const processed = new WeakSet();

processed.add(user);
```

Question:

```text
Has this object been processed?
```

### WeakMap

Stores associated data:

```text
object → value
```

Example:

```js
const metadata = new WeakMap();

metadata.set(user, {
  role: "admin",
});
```

Question:

```text
What data is associated with this object?
```

---

# 23. WeakSet vs Map

A normal Map stores:

```text
key → value
```

Example:

```js
const users = new Map();

users.set(101, "Sandip");
```

A WeakSet stores:

```text
object membership
```

Example:

```js
const users = new WeakSet();

users.add(user);
```

Use Map when you need key-value relationships.

Use WeakSet when you only need to know whether an object belongs to a collection.

---

# 24. WeakSet vs Array

An Array:

```js
const users = [
  user1,
  user2,
];
```

supports:

* Index access
* Iteration
* Length
* Duplicate values

A WeakSet:

```js
const users = new WeakSet([
  user1,
  user2,
]);
```

supports:

* Object membership
* `has()`
* `add()`
* `delete()`
* Weak references

WeakSet does not provide index access or iteration.

---

# 25. When to Use WeakSet

Use WeakSet when:

* You only need object membership.
* You need to track whether an object was processed.
* You need to associate membership with DOM objects.
* You want object members to remain eligible for garbage collection.
* You do not need iteration.
* You do not need the collection size.

Common use cases:

```text
Processed objects
DOM element tracking
Initialization tracking
Visited objects
Object membership
Framework internals
```

---

# 26. When Not to Use WeakSet

Do not use WeakSet when:

* You need primitive values.
* You need to iterate over members.
* You need `size`.
* You need `clear()`.
* You need to retrieve all members.
* You need associated values.

Use:

```text
Set  → unique values + iteration
Map  → key-value data
WeakMap → object → metadata
WeakSet → object membership
```

---

# 27. Important WeakSet Methods

```text
new WeakSet()
```

Creates a WeakSet.

```js
weakSet.add(object);
```

Adds an object.

```js
weakSet.has(object);
```

Checks membership.

```js
weakSet.delete(object);
```

Removes an object.

WeakSet does not provide:

```text
size
clear()
keys()
values()
entries()
forEach()
```

---

# 28. Quick Cheat Sheet

```js
// Create
const processed = new WeakSet();

// Object
const user = {
  id: 1,
};

// Add
processed.add(user);

// Check
processed.has(user);

// Delete
processed.delete(user);
```

Practical pattern:

```js
const processed = new WeakSet();

function process(object) {
  if (processed.has(object)) {
    return;
  }

  processed.add(object);

  // Process object
}
```

---

# 29. Simple Memory Model

```text
Set
│
├── unique values
├── iterable
├── has size
└── strongly references members

WeakSet
│
├── object membership
├── not iterable
├── no size
├── no clear()
└── does not keep object members alive by itself
```

---

# 30. Map / Set / WeakMap / WeakSet

```text
                Key-Value      Unique Values
                Collection      Collection

Map             ✓
WeakMap         ✓
Set                             ✓
WeakSet                         ✓
```

More specifically:

```text
Map
→ key → value
→ any key type
→ iterable

Set
→ unique values
→ any value type
→ iterable

WeakMap
→ object → value
→ weak object keys
→ not iterable

WeakSet
→ object membership
→ weak object members
→ not iterable
```

---

# 31. Key Takeaways

* `WeakSet` stores unique objects.
* Primitive values cannot be members.
* Use `add()` to add an object.
* Use `has()` to check membership.
* Use `delete()` to remove an object.
* WeakSet has no `size`.
* WeakSet has no `clear()`.
* WeakSet cannot be iterated.
* WeakSet does not provide `keys()`, `values()`, `entries()`, or `forEach()`.
* Object identity determines membership.
* WeakSet does not keep its object members alive by itself.
* Garbage collection is controlled by the JavaScript engine.
* Use `WeakSet` for object membership.
* Use `WeakMap` when you need to associate data with an object.

### Remember

```text
Set
→ unique values

WeakSet
→ unique object membership

Map
→ key → value

WeakMap
→ object → value with weak keys
```

