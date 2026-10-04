# Garbage Collection in JavaScript

**Garbage Collection (GC)** is the automatic process JavaScript engines use to reclaim memory that is no longer reachable by the program.

JavaScript developers normally do not manually free memory.

The basic idea is:

```text
Create Data
    ↓
Use Data
    ↓
Data Becomes Unreachable
    ↓
Garbage Collector
    ↓
Memory Can Be Reclaimed
```

---

# 1. What Is Garbage Collection?

When JavaScript creates an object:

```javascript
const user = {
    name: "Sandip"
};
```

the runtime allocates memory for that object.

If the object is no longer reachable:

```javascript
let user = {
    name: "Sandip"
};

user = null;
```

the object may eventually become eligible for garbage collection.

---

# 2. Reachability

Garbage collection is primarily concerned with **reachability**.

An object is reachable when the program can still access it through references.

Example:

```javascript
const user = {
    name: "Sandip"
};

console.log(user.name);
```

The object is reachable through:

```text
user
 ↓
object
```

---

# 3. Unreachable Objects

Consider:

```javascript
let user = {
    name: "Sandip"
};

user = null;
```

The reference to the object has been removed.

Conceptually:

```text
Before:

user → Object


After:

user → null

Object → unreachable
```

If nothing else references the object, it becomes eligible for garbage collection.

---

# 4. Garbage Collection Is Automatic

You normally do not write:

```javascript
free(user);
```

or:

```javascript
deleteMemory(user);
```

JavaScript manages memory automatically.

Your responsibility is to avoid unnecessarily keeping objects reachable.

---

# 5. Root References

Garbage collectors begin from special **roots**.

Conceptually, roots can include:

```text
Global objects
Active execution contexts
Live references
Other runtime-managed roots
```

The collector follows references from these roots to determine what remains reachable.

---

# 6. Reachability Example

```javascript
const user = {
    name: "Sandip",
    address: {
        city: "Birgunj"
    }
};
```

Conceptually:

```text
Root
 ↓
user
 ↓
User Object
 ↓
Address Object
```

Both objects are reachable.

---

# 7. Removing a Reference

```javascript
let user = {
    name: "Sandip",
    address: {
        city: "Birgunj"
    }
};

user = null;
```

If no other references exist:

```text
user
 ↓
null

User Object
    ↓
unreachable

Address Object
    ↓
unreachable
```

Both objects can eventually be reclaimed.

---

# 8. Shared References

Consider:

```javascript
let user = {
    name: "Sandip"
};

let admin = user;

user = null;
```

The object is still reachable:

```text
admin
 ↓
User Object
```

Therefore, changing `user` to `null` does not make the object unreachable.

---

# 9. Removing All References

```javascript
let user = {
    name: "Sandip"
};

let admin = user;

user = null;
admin = null;
```

Now, assuming there are no other references:

```text
User Object
     ↓
unreachable
```

The object becomes eligible for garbage collection.

---

# 10. Mark-and-Sweep

A common conceptual garbage-collection algorithm is **mark-and-sweep**.

It has two major ideas:

```text
Mark
 ↓
Identify reachable objects

Sweep
 ↓
Reclaim unreachable objects
```

---

# 11. Mark Phase

Suppose memory contains:

```text
Root
 ↓
A
 ↓
B

C
 ↓
D
```

The collector starts from the root.

Reachable:

```text
Root
 ↓
A
 ↓
B
```

Objects `C` and `D` are not reachable from that root.

---

# 12. Sweep Phase

The collector can reclaim unreachable objects:

```text
Reachable:
A
B

Unreachable:
C
D
```

Conceptually:

```text
Mark
 ↓
A, B are reachable
 ↓
Sweep
 ↓
C, D can be reclaimed
```

Modern engines use more sophisticated strategies, but this is a useful mental model.

---

# 13. Cyclic References

Older memory-management approaches can have problems with cycles.

Consider:

```javascript
const a = {};
const b = {};

a.other = b;
b.other = a;
```

There is a cycle:

```text
a
 ↓
b
 ↓
a
```

Modern JavaScript garbage collectors can handle cycles because reachability is more important than simply counting references.

If the entire cycle becomes unreachable from the roots, it can be collected.

---

# 14. Unreachable Cycle

Example:

```javascript
let a = {};
let b = {};

a.other = b;
b.other = a;

a = null;
b = null;
```

The objects reference each other, but nothing else can reach them.

Conceptually:

```text
a → null
b → null

Object A ↔ Object B

No root → Object A
No root → Object B
```

Therefore, the cycle can eventually be reclaimed.

---

# 15. Function Scope

Consider:

```javascript
function createUser() {
    const user = {
        name: "Sandip"
    };

    console.log(user);
}

createUser();
```

After the function finishes, the local binding is no longer available from that execution context.

If the object is not referenced elsewhere, it can become eligible for collection.

---

# 16. Returned References

Now:

```javascript
function createUser() {
    const user = {
        name: "Sandip"
    };

    return user;
}

const user = createUser();
```

The object remains reachable:

```text
user
 ↓
Object
```

Therefore, it cannot be reclaimed while that reference remains reachable.

---

# 17. Closures and Garbage Collection

Closures can keep variables reachable.

Example:

```javascript
function createCounter() {
    let count = 0;

    return function() {
        count++;

        return count;
    };
}

const counter = createCounter();
```

The returned function uses:

```text
count
```

so the captured state needs to remain available while the closure is reachable.

---

# 18. When a Closure Can Be Collected

Consider:

```javascript
function createCounter() {
    let count = 0;

    return function() {
        return ++count;
    };
}

let counter = createCounter();

console.log(counter());

counter = null;
```

If there are no other references to the returned function, its closure and captured state can eventually become unreachable.

---

# 19. Event Listeners

Event listeners can keep functions and related objects reachable.

Example:

```javascript
const button = document.querySelector("#button");

function handleClick() {
    console.log("Clicked");
}

button.addEventListener(
    "click",
    handleClick
);
```

When the listener is no longer needed, remove it:

```javascript
button.removeEventListener(
    "click",
    handleClick
);
```

This is particularly important for dynamically created UI.

---

# 20. Timers

A running timer can keep its callback and referenced data alive.

Example:

```javascript
const user = {
    name: "Sandip"
};

const timer = setInterval(() => {
    console.log(user.name);
}, 1000);
```

Stop it when it is no longer required:

```javascript
clearInterval(timer);
```

---

# 21. `setTimeout()`

A scheduled timeout can retain references until it executes or is cancelled.

```javascript
const user = {
    name: "Sandip"
};

const timer = setTimeout(() => {
    console.log(user.name);
}, 5000);
```

It can be cancelled:

```javascript
clearTimeout(timer);
```

when appropriate.

---

# 22. React Cleanup

React components often create resources such as:

```text
Timers
Event listeners
Subscriptions
WebSocket connections
```

These resources may require cleanup.

Example:

```jsx
useEffect(() => {
    const timer = setInterval(() => {
        console.log("Running");
    }, 1000);

    return () => {
        clearInterval(timer);
    };
}, []);
```

The returned function performs cleanup.

---

# 23. Node.js and Long-Running Processes

Node.js servers may run continuously.

A small retention problem can become significant when repeated thousands or millions of times.

Potential sources include:

```text
Caches
Timers
Event listeners
Database results
WebSocket connections
Request objects
Large arrays
```

Long-running processes should carefully manage these resources.

---

# 24. Memory Leak vs Garbage Collection

A memory leak happens when data that is no longer logically needed remains reachable.

Example:

```javascript
const cache = [];

function saveData(data) {
    cache.push(data);
}
```

If this happens continuously:

```text
saveData()
    ↓
cache grows
    ↓
references remain
    ↓
objects remain reachable
    ↓
memory usage increases
```

The garbage collector cannot reclaim objects that are still reachable.

---

# 25. Garbage Collection Cannot Fix Every Memory Problem

Suppose:

```javascript
const cache = new Map();

cache.set("user1", largeObject);
```

If the cache continues to reference `largeObject`, garbage collection cannot reclaim it.

You must remove the reference:

```javascript
cache.delete("user1");
```

The key idea is:

```text
Garbage Collector
    ↓
Can reclaim unreachable memory

Garbage Collector
    ↓
Cannot reclaim reachable data
```

---

# 26. WeakMap and Garbage Collection

`WeakMap` allows object keys to be held weakly.

Example:

```javascript
const metadata = new WeakMap();

let user = {
    name: "Sandip"
};

metadata.set(user, {
    role: "developer"
});
```

If:

```javascript
user = null;
```

and no other references exist, the `WeakMap` does not by itself keep the user object alive.

This makes `WeakMap` useful for certain metadata and association patterns.

---

# 27. WeakSet

`WeakSet` also holds objects weakly.

```javascript
const processed = new WeakSet();

let user = {
    name: "Sandip"
};

processed.add(user);
```

Later:

```javascript
user = null;
```

If no other references exist, the `WeakSet` does not by itself keep the object alive.

---

# 28. Why Weak Collections Exist

Normal collections:

```javascript
Map
Set
```

hold strong references to their stored objects.

Weak collections:

```javascript
WeakMap
WeakSet
```

are designed for cases where object lifetime should not be extended merely because the object is present in the collection.

---

# 29. Garbage Collection Is Not Predictable

You should not assume:

```text
Object becomes unreachable
        ↓
Memory is immediately freed
```

Instead:

```text
Object becomes unreachable
        ↓
Eligible for garbage collection
        ↓
Runtime decides when/how to reclaim memory
```

The exact timing depends on the JavaScript engine and current runtime conditions.

---

# 30. Generational Garbage Collection

Modern JavaScript engines commonly use generational strategies.

The general idea is:

```text
Young objects
    ↓
Often short-lived

Old objects
    ↓
Survive longer
```

The runtime can use different collection strategies for different groups of objects.

The exact implementation differs between JavaScript engines.

---

# 31. Why Generational GC Helps

Many applications create temporary objects.

For example:

```javascript
function createMessage(name) {
    return {
        message: `Hello ${name}`
    };
}
```

Some objects may exist only briefly.

A generational strategy can focus collection work where short-lived objects are commonly found.

---

# 32. Garbage Collection and Performance

Garbage collection requires runtime work.

If an application continuously creates large amounts of temporary data:

```text
Create many objects
       ↓
Objects become unreachable
       ↓
Garbage collection work
       ↓
More allocations
       ↓
More collection work
```

This can affect performance.

---

# 33. Avoid Unnecessary Object Creation

Instead of repeatedly creating unnecessary data:

```javascript
function processUser(user) {
    return {
        ...user,
        timestamp: Date.now()
    };
}
```

consider whether a new object is actually required for the operation.

Do not avoid all object creation—just avoid unnecessary allocations in performance-sensitive code.

---

# 34. Large Temporary Arrays

Example:

```javascript
const result = hugeArray
    .map(transform)
    .filter(condition)
    .map(format);
```

This can create intermediate arrays.

For normal application code, this is often perfectly acceptable.

For extremely large datasets or performance-critical paths, consider whether processing can be made more memory-efficient.

---

# 35. Streaming

For large data, streams can reduce the amount of data held at once.

Node.js example:

```javascript
import fs from "node:fs";

const stream = fs.createReadStream(
    "large-file.txt"
);

stream.on("data", (chunk) => {
    console.log(chunk);
});
```

Instead of loading the entire file into memory, the application receives chunks.

---

# 36. Garbage Collection in Browser Applications

Browsers use garbage collection to manage JavaScript memory.

Common sources of unnecessary retention include:

```text
Detached DOM nodes
Event listeners
Timers
Closures
Large caches
Global references
```

Developer tools can help investigate these cases.

---

# 37. Heap Snapshots

A heap snapshot provides information about objects currently retained in memory.

A typical debugging process:

```text
Take Snapshot 1
      ↓
Perform application action
      ↓
Take Snapshot 2
      ↓
Compare
      ↓
Find unexpected retained objects
```

This can help identify memory leaks.

---

# 38. Retained Objects

When debugging memory, one important question is:

```text
Why is this object still reachable?
```

You may inspect:

```text
References
Retainers
Object paths
Event listeners
Closures
Caches
```

The goal is to find what is keeping the object alive.

---

# 39. Memory Debugging Strategy

A practical process:

```text
1. Observe memory growth
        ↓
2. Reproduce the behavior
        ↓
3. Take heap snapshots
        ↓
4. Compare snapshots
        ↓
5. Find retained objects
        ↓
6. Identify the reference
        ↓
7. Remove unnecessary retention
        ↓
8. Test again
```

---

# 40. Common Garbage Collection Mistakes

### Mistake 1: Assuming `null` immediately frees memory

```javascript
user = null;
```

This only removes that particular reference.

Other references may still exist.

---

### Mistake 2: Assuming GC runs immediately

Unreachable objects become eligible for collection, but reclamation timing is runtime-controlled.

---

### Mistake 3: Keeping unlimited caches

```javascript
cache.set(id, data);
```

without a cleanup strategy can cause memory growth.

---

### Mistake 4: Forgetting timers

```javascript
setInterval(...);
```

without eventually calling:

```javascript
clearInterval(...);
```

can keep resources alive unnecessarily.

---

### Mistake 5: Forgetting event listeners

Long-lived listeners can retain callbacks and related state.

---

# 41. Garbage Collection Flow

```text
Create Object
     ↓
Object Is Reachable
     ↓
Application Uses Object
     ↓
References Change
     ↓
Object May Become Unreachable
     ↓
Garbage Collector Detects It
     ↓
Memory Can Be Reclaimed
```

---

# 42. Memory Leak Flow

```text
Create Object
     ↓
Application Uses Object
     ↓
Object No Longer Needed
     ↓
Unexpected Reference Remains
     ↓
Object Stays Reachable
     ↓
Garbage Collector Keeps It
     ↓
Memory Usage Continues Growing
```

---

# 43. Garbage Collection vs Memory Management

These concepts are related but not identical.

### Memory Management

The broader process of:

```text
Allocating memory
Using memory
Managing references
Releasing resources
Optimizing memory usage
```

### Garbage Collection

The automatic mechanism that reclaims memory occupied by unreachable objects.

```text
Memory Management
        ↓
   Garbage Collection
        ↓
One part of memory management
```

---

# 44. Quick Comparison

| Concept            | Meaning                                     |
| ------------------ | ------------------------------------------- |
| Reachable          | Object can still be accessed                |
| Unreachable        | No active path from relevant roots          |
| Garbage Collection | Automatic reclamation of unreachable memory |
| Memory Leak        | Unneeded memory remains reachable           |
| Mark               | Identify reachable objects                  |
| Sweep              | Reclaim unreachable objects                 |
| WeakMap            | Weak object-key association                 |
| WeakSet            | Weak object collection                      |
| Heap Snapshot      | Memory debugging tool                       |

---

# 45. Good Practices

```text
Clean up event listeners
Clear unused timers
Limit caches
Avoid unnecessary global references
Clean up React effects
Close resources when appropriate
Process large data efficiently
Use streams for large files
Monitor long-running Node.js applications
Use memory profiling tools when necessary
```

---

# 46. Key Takeaways

* Garbage collection automatically reclaims memory from unreachable objects.
* JavaScript developers normally do not manually free memory.
* Reachability is central to garbage collection.
* Removing one reference does not necessarily make an object unreachable.
* Objects can remain alive through shared references, closures, timers, listeners, and caches.
* Cyclic references can still be collected when the entire cycle is unreachable.
* Mark-and-sweep is a useful conceptual model.
* Modern JavaScript engines use more advanced and optimized garbage-collection strategies.
* Generational collection separates objects based on their lifetime.
* Garbage collection does not remove objects that are still reachable.
* `WeakMap` and `WeakSet` can be useful when object lifetime should not be extended by a collection.
* Garbage collection timing is controlled by the runtime and should not be assumed to be immediate.
* Memory leaks usually require removing unnecessary references or resources.
* Heap snapshots and memory profiling tools are useful for diagnosing memory problems.
