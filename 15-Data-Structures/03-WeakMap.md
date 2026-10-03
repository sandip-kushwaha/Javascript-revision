# JavaScript WeakMap

`WeakMap` is a JavaScript collection used to store **key-value pairs where the keys must be objects or non-registered symbols**.

The main difference from `Map` is that `WeakMap` does not prevent its object keys from being garbage-collected when there are no other strong references to those keys.

---

# 1. What is WeakMap?

A `WeakMap` stores data like:

```text
object key → value
```

Example:

```js
const user = {
  name: "Sandip",
};

const metadata = new WeakMap();

metadata.set(user, {
  role: "admin",
});

console.log(metadata.get(user));
```

Result:

```js
{
  role: "admin"
}
```

---

# 2. Creating a WeakMap

Create an empty WeakMap:

```js
const weakMap = new WeakMap();

console.log(weakMap);
```

You can also initialize it with entries:

```js
const user = {
  name: "Sandip",
};

const weakMap = new WeakMap([
  [
    user,
    {
      role: "admin",
    },
  ],
]);
```

Each entry contains:

```text
[key, value]
```

The key must be an allowed object-like key.

---

# 3. WeakMap Keys

A WeakMap is designed primarily for object keys.

```js
const weakMap = new WeakMap();

const user = {
  id: 1,
};

weakMap.set(user, "Admin");

console.log(
  weakMap.get(user)
);
// Admin
```

Arrays can also be keys:

```js
const list = [];

weakMap.set(list, "My list");

console.log(
  weakMap.get(list)
);
// My list
```

Functions can also be keys:

```js
const calculate = () => {
  return 10;
};

weakMap.set(calculate, "Calculator");

console.log(
  weakMap.get(calculate)
);
// Calculator
```

---

# 4. Primitive Keys Are Not Allowed

A WeakMap does not accept ordinary primitive values as keys.

For example:

```js
const weakMap = new WeakMap();

weakMap.set("name", "Sandip");
```

This throws a `TypeError`.

The same applies to values such as:

```text
number
string
boolean
null
undefined
bigint
```

Use an object as the key:

```js
const key = {
  name: "user",
};

weakMap.set(key, "Sandip");
```

---

# 5. set()

`set()` adds or updates a key-value pair.

```js
const weakMap = new WeakMap();

const user = {
  id: 1,
};

weakMap.set(user, "Admin");
```

Calling `set()` with the same key updates the value:

```js
weakMap.set(user, "Super Admin");

console.log(
  weakMap.get(user)
);
// Super Admin
```

`set()` returns the WeakMap itself, so chaining is possible:

```js
const user = {};

const permissions = new WeakMap();

permissions
  .set(user, "admin");
```

---

# 6. get()

`get()` returns the value associated with an object key.

```js
const user = {
  id: 1,
};

const roles = new WeakMap();

roles.set(user, "admin");

console.log(
  roles.get(user)
);
// admin
```

If the key does not exist:

```js
console.log(
  roles.get({})
);
// undefined
```

This happens because the newly created object is a different reference.

---

# 7. has()

`has()` checks whether a key exists.

```js
const user = {
  id: 1,
};

const roles = new WeakMap();

roles.set(user, "admin");

console.log(
  roles.has(user)
);
// true
```

Unknown object:

```js
console.log(
  roles.has({})
);
// false
```

---

# 8. delete()

`delete()` removes the entry associated with an object key.

```js
const user = {
  id: 1,
};

const roles = new WeakMap();

roles.set(user, "admin");

roles.delete(user);

console.log(
  roles.has(user)
);
// false
```

Return value:

```text
true  → entry existed and was removed
false → entry did not exist
```

---

# 9. WeakMap Does Not Have clear()

Unlike `Map`, `WeakMap` does not provide:

```js
weakMap.clear();
```

This method does not exist.

If you need to remove an individual entry, use:

```js
weakMap.delete(key);
```

If you need to discard the entire collection, you can remove your reference to the WeakMap itself:

```js
let cache = new WeakMap();

cache = new WeakMap();
```

---

# 10. WeakMap Does Not Have size

A WeakMap does not provide:

```js
weakMap.size;
```

There is no reliable built-in way to ask:

```text
How many entries are currently inside this WeakMap?
```

This is intentional.

Because object keys can disappear through garbage collection, exposing a live entry count would conflict with the weak nature of the collection.

---

# 11. WeakMap Is Not Iterable

You cannot do:

```js
for (const item of weakMap) {
  console.log(item);
}
```

This does not work.

WeakMap does not provide:

```js
weakMap.keys();
weakMap.values();
weakMap.entries();
```

It also does not provide `forEach()`.

The main operations are:

```text
set()
get()
has()
delete()
```

---

# 12. Why Can't WeakMap Be Iterated?

Suppose an object is used as a WeakMap key:

```js
let user = {
  name: "Sandip",
};

const metadata = new WeakMap();

metadata.set(user, {
  loginCount: 5,
});
```

Later:

```js
user = null;
```

If no other strong reference exists, the object may become eligible for garbage collection.

The JavaScript engine decides when garbage collection occurs.

Because the entry can disappear automatically, a WeakMap cannot provide normal predictable iteration over all keys.

---

# 13. WeakMap and Garbage Collection

This is the most important concept.

Consider:

```js
let user = {
  name: "Sandip",
};

const metadata = new WeakMap();

metadata.set(user, {
  role: "admin",
});
```

There are two references to the object:

```text
user
 ↓
{ name: "Sandip" }

WeakMap
 ↓
object key
```

Now:

```js
user = null;
```

If there are no other strong references to the object, it can become eligible for garbage collection.

The WeakMap does not keep the object alive merely because it is a key.

---

# 14. WeakMap Does Not Force Garbage Collection

This is important:

```text
WeakMap
    ↓
does not force garbage collection
```

Garbage collection is controlled by the JavaScript engine.

You cannot use WeakMap to manually trigger garbage collection.

WeakMap only avoids creating a strong reference from the collection to its object keys.

---

# 15. Map vs WeakMap

| Feature                | Map       | WeakMap                            |
| ---------------------- | --------- | ---------------------------------- |
| Key types              | Any value | Objects and non-registered symbols |
| `get()`                | Yes       | Yes                                |
| `set()`                | Yes       | Yes                                |
| `has()`                | Yes       | Yes                                |
| `delete()`             | Yes       | Yes                                |
| `clear()`              | Yes       | No                                 |
| `size`                 | Yes       | No                                 |
| Iteration              | Yes       | No                                 |
| `keys()`               | Yes       | No                                 |
| `values()`             | Yes       | No                                 |
| `entries()`            | Yes       | No                                 |
| `forEach()`            | Yes       | No                                 |
| Weak object references | No        | Yes                                |

---

# 16. Practical Example: Private Metadata

WeakMap can store metadata associated with objects without adding that metadata directly to the objects.

```js
const metadata = new WeakMap();

function createUser(name) {
  const user = {
    name,
  };

  metadata.set(user, {
    loginCount: 0,
    lastLogin: null,
  });

  return user;
}

const user = createUser("Sandip");

console.log(
  metadata.get(user)
);
```

The metadata is stored separately from the user object.

---

# 17. Updating Private Metadata

```js
const metadata = new WeakMap();

function createUser(name) {
  const user = {
    name,
  };

  metadata.set(user, {
    loginCount: 0,
  });

  return user;
}

function login(user) {
  const data = metadata.get(user);

  data.loginCount++;
}

const user = createUser("Sandip");

login(user);
login(user);

console.log(
  metadata.get(user).loginCount
);
// 2
```

The metadata is associated with the object without becoming a normal property of that object.

---

# 18. Practical Example: DOM Element Metadata

WeakMap can associate information with DOM elements.

```js
const elementData = new WeakMap();

const button = document.querySelector("#save");

elementData.set(button, {
  clicks: 0,
  action: "save",
});
```

Later:

```js
const data = elementData.get(button);

data.clicks++;

console.log(data.clicks);
```

If the DOM element becomes unreachable and is garbage-collected, the WeakMap does not keep it alive just because it was used as a key.

---

# 19. Practical Example: DOM Element State

```js
const state = new WeakMap();

function initialize(element) {
  state.set(element, {
    active: false,
  });
}

function activate(element) {
  const data = state.get(element);

  if (data) {
    data.active = true;
  }
}
```

This can be useful when managing state associated with objects without modifying those objects directly.

---

# 20. Practical Example: Caching Objects

WeakMap can be useful for object-based caches.

```js
const cache = new WeakMap();

function processUser(user) {
  if (cache.has(user)) {
    return cache.get(user);
  }

  const result = {
    displayName: user.name.toUpperCase(),
  };

  cache.set(user, result);

  return result;
}
```

Usage:

```js
const user = {
  name: "Sandip",
};

console.log(
  processUser(user)
);

console.log(
  processUser(user)
);
```

The same object reference can retrieve the cached result.

---

# 21. WeakMap and Object Identity

WeakMap uses object identity for keys.

```js
const weakMap = new WeakMap();

const user1 = {
  id: 1,
};

const user2 = {
  id: 1,
};

weakMap.set(user1, "Admin");

console.log(
  weakMap.get(user1)
);
// Admin

console.log(
  weakMap.get(user2)
);
// undefined
```

Because:

```js
user1 !== user2
```

Even though their contents look identical.

---

# 22. WeakMap with a Class

WeakMap can be used to store internal data for class instances.

```js
const privateData = new WeakMap();

class User {
  constructor(name) {
    privateData.set(this, {
      name,
      loginCount: 0,
    });
  }

  login() {
    const data = privateData.get(this);

    data.loginCount++;
  }

  getLoginCount() {
    return privateData.get(this).loginCount;
  }
}

const user = new User("Sandip");

user.login();
user.login();

console.log(
  user.getLoginCount()
);
// 2
```

The private data is not directly stored as a normal property on the instance.

---

# 23. WeakMap vs Private Fields

Modern JavaScript classes also support private fields:

```js
class User {
  #loginCount = 0;

  login() {
    this.#loginCount++;
  }
}
```

WeakMap and private fields can both be used for encapsulation, but they are different tools.

### Private fields

```js
class User {
  #name;

  constructor(name) {
    this.#name = name;
  }
}
```

Advantages:

* Native class syntax
* Easy to understand
* Truly private from normal external access
* Convenient for class-specific state

### WeakMap

```js
const privateData = new WeakMap();
```

Advantages:

* Works outside class syntax
* Can associate metadata with arbitrary objects
* Does not keep object keys alive by itself

For modern classes, private fields are often the simpler choice when class-private state is all you need.

---

# 24. WeakMap vs Map for Caching

Consider object-based caching.

With `Map`:

```js
const cache = new Map();

let user = {
  name: "Sandip",
};

cache.set(user, "result");

user = null;
```

The Map still has a strong reference to the original object through its key.

With `WeakMap`:

```js
const cache = new WeakMap();

let user = {
  name: "Sandip",
};

cache.set(user, "result");

user = null;
```

If no other strong reference exists, the object can become eligible for garbage collection.

The exact moment of garbage collection is determined by the JavaScript engine.

---

# 25. When to Use WeakMap

Use WeakMap when:

* Keys are objects.
* You need metadata associated with objects.
* You want object keys not to be kept alive by the collection.
* You do not need iteration.
* You do not need to know the collection size.
* You are building object-based caches.
* You need external private state for objects or class instances.

Common use cases:

```text
Object metadata
DOM element metadata
Object-based caching
Private class state
Framework internals
Resource association
```

---

# 26. When Not to Use WeakMap

Do not use WeakMap when:

* You need primitive keys.
* You need to iterate over entries.
* You need `size`.
* You need `clear()`.
* You need to retrieve all keys.
* You need predictable collection-wide inspection.

In these situations, `Map` or another data structure may be more appropriate.

---

# 27. Important WeakMap Methods

```text
new WeakMap()
```

Creates a WeakMap.

```js
weakMap.set(key, value)
```

Adds or updates an entry.

```js
weakMap.get(key)
```

Gets the value.

```js
weakMap.has(key)
```

Checks whether the key exists.

```js
weakMap.delete(key)
```

Removes an entry.

WeakMap does **not** provide:

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
const weakMap = new WeakMap();

// Object key
const user = {
  id: 1,
};

// Set
weakMap.set(user, "Admin");

// Get
weakMap.get(user);

// Check
weakMap.has(user);

// Delete
weakMap.delete(user);
```

---

# 29. Map vs WeakMap — Simple Memory Model

```text
Map
│
├── key → value
├── iterable
├── has size
├── supports clear()
└── keeps keys strongly reachable

WeakMap
│
├── object key → value
├── not iterable
├── no size
├── no clear()
└── does not keep object keys alive by itself
```

---

# 30. Key Points

```text
WeakMap
   ↓
Key-value collection

Key
   ↓
Object or non-registered Symbol

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

No size
   ↓
Cannot inspect entry count

No iteration
   ↓
No keys(), values(), entries()

Weak reference behavior
   ↓
Does not keep object keys alive by itself
```

### Remember

```text
Map
→ general-purpose key-value collection
→ any key type
→ iterable
→ has size

WeakMap
→ object-keyed metadata/cache
→ not iterable
→ no size
→ object keys can become garbage-collectable
```

