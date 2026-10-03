# JavaScript Heap

## What is the Heap?

The **Heap** is a memory area used by the JavaScript runtime to store dynamically allocated data.

Objects, arrays, functions, and other dynamically created values are stored and managed in memory.

A simplified JavaScript runtime can be viewed as:

```text
JavaScript Runtime
│
├── Call Stack
│   └── Function execution
│
└── Heap
    └── Dynamically allocated data
```

The exact implementation depends on the JavaScript engine, but this model is useful for understanding memory.

---

# 1. Call Stack vs Heap

The **Call Stack** mainly manages execution.

The **Heap** mainly manages dynamically allocated data.

```text
Call Stack
──────────────
Function calls
Execution
Return points


Heap
──────────────
Objects
Arrays
Functions
Other allocated data
```

---

# 2. Objects and the Heap

Consider:

```js
const user = {
  name: "Sandip",
  age: 22
};
```

A simplified model is:

```text
Call Stack
┌──────────────┐
│ user ────────┼──────────┐
└──────────────┘          │
                          ↓
                       Heap
                  ┌──────────────┐
                  │ name: Sandip │
                  │ age: 22      │
                  └──────────────┘
```

The variable can be thought of as holding a reference to an object managed in the heap.

---

# 3. Arrays and the Heap

Arrays are also dynamically allocated objects.

```js
const numbers = [10, 20, 30, 40];
```

Simplified:

```text
Call Stack
┌─────────────────┐
│ numbers ────────┼───────┐
└─────────────────┘       │
                          ↓
                       Heap
                  ┌─────────────┐
                  │ 10          │
                  │ 20          │
                  │ 30          │
                  │ 40          │
                  └─────────────┘
```

Again, this is a conceptual model rather than a literal description of every engine's memory layout.

---

# 4. Functions and Memory

Functions are also values that require memory.

```js
function greet() {
  console.log("Hello");
}
```

A simplified model:

```text
Heap
┌─────────────────────┐
│ greet function      │
│ function code/data  │
└─────────────────────┘
```

The JavaScript engine manages the memory associated with the function.

---

# 5. Primitive Values

JavaScript has primitive values such as:

```text
string
number
bigint
boolean
undefined
symbol
null
```

For learning purposes, it is useful to think of primitive values as directly represented in variables.

For example:

```js
let age = 22;
let name = "Sandip";
let active = true;
```

However, actual engine implementations are more complex and may optimize how values are represented and stored.

---

# 6. Reference Values

Objects, arrays, and functions are reference-type values.

Example:

```js
const user = {
  name: "Sandip"
};

const anotherUser = user;
```

Now both variables refer to the same object.

```text
user ───────────┐
               ↓
            Object
               ↑
               │
anotherUser ───┘
```

Changing the object through one reference affects what the other reference sees.

```js
anotherUser.name = "Alex";

console.log(user.name);
```

Output:

```text
Alex
```

---

# 7. Copying a Primitive

Primitive values behave differently.

```js
let a = 10;
let b = a;

b = 20;

console.log(a);
console.log(b);
```

Output:

```text
10
20
```

The value of `a` is not changed when `b` is reassigned.

---

# 8. Copying an Object

Consider:

```js
const user1 = {
  name: "Sandip"
};

const user2 = user1;

user2.name = "Alex";

console.log(user1.name);
```

Output:

```text
Alex
```

Both variables refer to the same object.

---

# 9. Creating a New Object

If you want a separate object:

```js
const user1 = {
  name: "Sandip"
};

const user2 = {
  ...user1
};

user2.name = "Alex";

console.log(user1.name);
console.log(user2.name);
```

Output:

```text
Sandip
Alex
```

The spread operator creates a new shallow object.

---

# 10. Memory Allocation

When JavaScript creates an object:

```js
const user = {
  name: "Sandip"
};
```

the runtime needs memory for that object.

Conceptually:

```text
Create object
     ↓
Allocate memory
     ↓
Store object data
     ↓
Keep reference
```

The JavaScript engine handles the details automatically.

---

# 11. Garbage Collection

JavaScript automatically manages unused memory using **Garbage Collection (GC)**.

For example:

```js
let user = {
  name: "Sandip"
};

user = null;
```

If nothing else references the original object, it may become eligible for garbage collection.

```text
Before:

user ─────→ Object


After:

user ─────→ null

Object
  ↑
  no useful reference
```

The object can eventually be removed from memory.

---

# 12. Reachability

Garbage collection is based largely on the idea of **reachability**.

If an object can still be reached through active references, it generally cannot be collected.

Example:

```js
const user = {
  name: "Sandip"
};
```

The object is reachable through `user`.

If:

```js
let user = {
  name: "Sandip"
};

user = null;
```

and there are no other references, the object may become unreachable.

---

# 13. Multiple References

Consider:

```js
let user1 = {
  name: "Sandip"
};

let user2 = user1;

user1 = null;
```

The object is still reachable through `user2`.

```text
user1 ───→ null

user2 ─────────→ Object
```

Therefore, the object is still in use.

---

# 14. Object Becomes Unreachable

```js
let user1 = {
  name: "Sandip"
};

let user2 = user1;

user1 = null;
user2 = null;
```

Now there are no references from the application to the object.

```text
user1 ───→ null
user2 ───→ null

Object
  ↓
Unreachable
```

The object can become eligible for garbage collection.

---

# 15. Garbage Collection Is Automatic

You normally do not manually free JavaScript objects.

For example, there is no normal JavaScript equivalent of manually calling:

```text
free(object)
```

The runtime manages memory automatically.

The garbage collector determines which objects are no longer reachable and can reclaim their memory.

---

# 16. Garbage Collection Does Not Mean Immediate Deletion

When an object becomes unreachable:

```js
let data = {
  value: 100
};

data = null;
```

it does **not** mean the object is necessarily removed from memory at that exact moment.

It becomes eligible for garbage collection.

The JavaScript engine decides when garbage collection should occur.

---

# 17. Memory Leaks

A **memory leak** happens when memory that is no longer logically needed remains reachable.

Example:

```js
const cache = [];

function storeData(data) {
  cache.push(data);
}
```

If `cache` keeps growing indefinitely, old data remains reachable.

```text
cache
  ↓
data
data
data
data
data
...
```

The garbage collector cannot remove those objects while they remain reachable from `cache`.

---

# 18. Common Causes of Memory Leaks

Common causes include:

```text
Unnecessary global variables
Long-lived caches
Forgotten event listeners
Timers that are never cleared
Closures retaining unnecessary data
Detached DOM elements
Large objects kept in application state
```

---

# 19. Global Variables

Example:

```js
window.largeData = {
  // large object
};
```

If the application does not need the data anymore but the global reference remains, the object can remain reachable.

Prefer keeping variables scoped to where they are actually needed.

---

# 20. Event Listener Example

Consider:

```js
const button = document.querySelector("#button");

function handleClick() {
  console.log("Clicked");
}

button.addEventListener("click", handleClick);
```

When the listener is no longer needed, remove it when appropriate:

```js
button.removeEventListener("click", handleClick);
```

This is particularly important in long-lived applications and components that mount and unmount repeatedly.

---

# 21. Timers and Memory

A timer can keep references alive while it remains active.

Example:

```js
const timer = setInterval(() => {
  console.log("Running");
}, 1000);
```

If the timer is no longer required:

```js
clearInterval(timer);
```

This helps prevent unnecessary work and retained references.

---

# 22. Closures and Memory

Closures can retain references to variables from their outer scope.

Example:

```js
function createCounter() {
  let count = 0;

  return function () {
    count++;

    return count;
  };
}

const counter = createCounter();
```

The returned function still needs access to `count`.

Therefore, the relevant data remains reachable through the closure.

```text
counter
   ↓
Function
   ↓
Closure environment
   ↓
count
```

This is normal behavior.

A memory problem occurs when unnecessarily large data is retained for too long.

---

# 23. Large Data in Closures

Example:

```js
function createHandler() {
  const largeData = new Array(1000000).fill("data");

  return function () {
    console.log(largeData.length);
  };
}

const handler = createHandler();
```

As long as `handler` remains reachable and needs the closure, the referenced data may also remain reachable.

The important principle is:

> References keep objects reachable.

---

# 24. WeakMap

A `WeakMap` can be useful for certain memory-sensitive associations.

Example:

```js
const metadata = new WeakMap();

const user = {};

metadata.set(user, {
  role: "admin"
});
```

If the `user` object becomes unreachable elsewhere, its WeakMap entry does not prevent garbage collection.

This is one reason `WeakMap` is useful for object-associated metadata.

---

# 25. WeakSet

`WeakSet` also stores object references without preventing those objects from becoming garbage-collectable.

```js
const visited = new WeakSet();

const user = {};

visited.add(user);
```

If `user` becomes unreachable elsewhere, the WeakSet does not keep it alive.

---

# 26. Heap and Performance

Large amounts of allocated data can increase memory usage.

Example:

```js
const users = [];

for (let i = 0; i < 1000000; i++) {
  users.push({
    id: i,
    name: `User ${i}`
  });
}
```

The application now keeps a large amount of data reachable through `users`.

Memory usage can increase significantly.

---

# 27. Releasing References

If data is no longer needed, remove unnecessary references.

```js
let largeData = createLargeData();

// use largeData

largeData = null;
```

This can make the object eligible for garbage collection if no other references exist.

Whether this is necessary depends on the application's scope and lifetime.

---

# 28. Heap and Browser Applications

In a browser, a web application may continuously create:

```text
DOM elements
JavaScript objects
Arrays
Event handlers
Timers
API response data
Caches
Application state
```

If unnecessary references remain, memory usage can grow over time.

---

# 29. Heap and Node.js

Node.js applications also allocate memory for:

```text
Request objects
Response data
Database results
Caches
Buffers
Application objects
Sessions
Event listeners
```

Long-running backend applications should pay attention to unnecessary memory retention.

---

# 30. Heap and Buffers

Node.js commonly handles binary data using `Buffer`.

Example:

```js
const buffer = Buffer.from("Hello");
```

Buffers use memory managed by the Node.js runtime and underlying environment.

Large buffers should be handled carefully, especially when processing files or network data.

---

# 31. Memory Usage in Node.js

Node.js provides memory information:

```js
const memory = process.memoryUsage();

console.log(memory);
```

You may see information such as:

```text
rss
heapTotal
heapUsed
external
arrayBuffers
```

For example:

```js
console.log(process.memoryUsage().heapUsed);
```

This can help when investigating memory behavior.

---

# 32. Heap Growth

A simplified example of continuously growing memory:

```js
const cache = [];

setInterval(() => {
  cache.push({
    timestamp: Date.now()
  });
}, 100);
```

The `cache` array continues holding objects.

Therefore:

```text
cache
 ↓
Object
Object
Object
Object
Object
...
```

If nothing removes old entries, memory usage can continue growing.

---

# 33. Better Cache Management

Instead of keeping everything forever:

```js
const cache = [];
```

an application can implement limits or expiration.

Conceptually:

```text
Add data
   ↓
Cache
   ↓
Check age/size
   ↓
Remove old data
```

This prevents unnecessary memory retention.

---

# 34. Heap and Garbage Collector

A simplified memory lifecycle:

```text
Create object
      ↓
Allocate memory
      ↓
Object is reachable
      ↓
Application uses object
      ↓
References removed
      ↓
Object becomes unreachable
      ↓
Garbage Collector
      ↓
Memory can be reclaimed
```

---

# 35. JavaScript Does Not Give Direct Garbage Collection Control

Normal JavaScript code does not directly decide:

```text
"Run garbage collection now."
```

The JavaScript engine controls garbage collection.

Some runtime environments may provide diagnostic or special GC controls, but normal application code should not depend on manually triggering GC.

---

# 36. Memory Optimization

Useful practices include:

### Avoid unnecessary global data

```js
// Keep data local when possible
function processUser() {
  const user = getUser();
}
```

### Remove unnecessary listeners

```js
element.removeEventListener("click", handler);
```

### Clear timers

```js
clearInterval(timer);
clearTimeout(timeout);
```

### Limit caches

```text
Maximum size
Expiration time
LRU-style eviction
```

### Avoid retaining unnecessary large objects

```text
Keep only the data the application actually needs.
```

---

# 37. Stack + Heap

The call stack and heap work together.

Example:

```js
const user = {
  name: "Sandip"
};

function greet() {
  console.log(user.name);
}

greet();
```

Simplified:

```text
             JavaScript Runtime
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
   Call Stack                  Heap
┌──────────────┐        ┌────────────────┐
│ greet()      │───────→│ user object    │
├──────────────┤        │ name: Sandip   │
│ Global       │        └────────────────┘
└──────────────┘
```

The stack handles execution while the heap contains dynamically allocated data.

---

# 38. Important Concept

Do not think of the heap as simply:

> "Where all variables are stored."

That is an oversimplification.

The JavaScript engine decides how values are represented and optimized internally.

A better mental model is:

> **The heap is an area used by the runtime for dynamically allocated data whose lifetime is managed by the engine.**

---

# 39. Key Takeaways

* The **Heap** is used for dynamically allocated memory.
* Objects, arrays, and functions require dynamically managed memory.
* The Call Stack and Heap have different responsibilities.
* Objects can be shared through references.
* Multiple variables can reference the same object.
* Garbage collection automatically reclaims memory that is no longer reachable.
* An unreachable object is eligible for garbage collection.
* Garbage collection does not necessarily happen immediately.
* Memory leaks occur when unnecessary data remains reachable.
* Global variables, caches, timers, listeners, and closures can retain memory.
* `clearTimeout()` and `clearInterval()` can release unnecessary timer work.
* Event listeners should be removed when they are no longer needed.
* `WeakMap` and `WeakSet` do not prevent their object keys/values from being garbage-collected.
* Node.js provides `process.memoryUsage()` for memory information.
* Good memory management is mostly about controlling unnecessary references and data lifetime.

## Simple Mental Model

```text
          JavaScript Runtime
                 │
       ┌─────────┴─────────┐
       ↓                   ↓
  Call Stack              Heap
       │                   │
       ↓                   ↓
Function calls       Objects / Arrays
Execution            Dynamic data
       │                   │
       └─────────┬─────────┘
                 ↓
          Garbage Collector
                 ↓
       Reclaim unreachable data
```
