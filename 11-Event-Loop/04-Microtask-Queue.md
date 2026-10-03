# JavaScript Microtask Queue

## What is the Microtask Queue?

The **Microtask Queue** is a queue used by JavaScript for scheduling certain callbacks that should run after the current synchronous code finishes.

Common sources of microtasks include:

* `Promise.then()`
* `Promise.catch()`
* `Promise.finally()`
* `queueMicrotask()`
* continuations after `await`

Microtasks are processed by the runtime before moving on to the next task in the usual event-loop model.

---

# 1. Basic Example

```js
console.log("Start");

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

Output:

```text
Start
End
Promise
```

Why?

```text
Synchronous code
      ↓
Start
      ↓
End
      ↓
Microtask Queue
      ↓
Promise callback
```

---

# 2. Promise Callbacks Use Microtasks

Consider:

```js
Promise.resolve().then(() => {
  console.log("Hello");
});
```

The callback passed to `.then()` is scheduled as a microtask.

Simplified:

```text
Promise resolved
      ↓
.then() callback
      ↓
Microtask Queue
      ↓
Event Loop
      ↓
Call Stack
      ↓
Callback executes
```

---

# 3. `queueMicrotask()`

JavaScript provides a direct way to schedule a microtask:

```js
queueMicrotask(() => {
  console.log("Microtask");
});
```

Example:

```js
console.log("A");

queueMicrotask(() => {
  console.log("B");
});

console.log("C");
```

Output:

```text
A
C
B
```

The microtask runs after the current synchronous code finishes.

---

# 4. Microtask vs Synchronous Code

Consider:

```js
console.log("1");

queueMicrotask(() => {
  console.log("2");
});

console.log("3");
```

Output:

```text
1
3
2
```

The microtask does not interrupt the currently executing synchronous code.

---

# 5. Microtask vs Task

Consider:

```js
setTimeout(() => {
  console.log("Task");
}, 0);

queueMicrotask(() => {
  console.log("Microtask");
});
```

Typical output:

```text
Microtask
Task
```

Simplified:

```text
Current code
    ↓
Microtask Queue
    ↓
Microtask executes
    ↓
Task Queue
    ↓
Task executes
```

---

# 6. Promise vs `setTimeout()`

Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

Output:

```text
Start
End
Promise
Timeout
```

Execution:

```text
1. Start
2. End
3. Promise callback
4. Timer callback
```

The Promise callback is a microtask, while the timer callback is a task.

---

# 7. Multiple Microtasks

Example:

```js
queueMicrotask(() => {
  console.log("A");
});

queueMicrotask(() => {
  console.log("B");
});

queueMicrotask(() => {
  console.log("C");
});
```

They are processed in queue order:

```text
A
B
C
```

Conceptually:

```text
Microtask Queue

A
B
C
```

---

# 8. Microtasks Created During a Microtask

A microtask can schedule another microtask.

```js
queueMicrotask(() => {
  console.log("A");

  queueMicrotask(() => {
    console.log("B");
  });
});

queueMicrotask(() => {
  console.log("C");
});
```

Output:

```text
A
C
B
```

The first queue initially contains:

```text
A
C
```

After `A` starts, it adds `B`.

The queue becomes:

```text
C
B
```

So `C` runs before `B`.

---

# 9. Promise Chains

Promise chains also create microtasks.

```js
Promise.resolve()
  .then(() => {
    console.log("A");
  })
  .then(() => {
    console.log("B");
  });
```

The callbacks are scheduled as the Promise chain progresses.

Output:

```text
A
B
```

Conceptually:

```text
Promise resolved
      ↓
First .then()
      ↓
Microtask
      ↓
Second .then()
      ↓
Another microtask
```

---

# 10. `.catch()` and Microtasks

Promise rejection handlers also use the microtask mechanism.

```js
Promise.reject(new Error("Failed"))
  .catch(() => {
    console.log("Handled");
  });
```

The `.catch()` callback runs asynchronously as a microtask.

---

# 11. `.finally()` and Microtasks

Example:

```js
Promise.resolve("Done")
  .finally(() => {
    console.log("Cleanup");
  });
```

The `finally` callback is part of Promise reaction processing and therefore uses the microtask mechanism.

---

# 12. `async/await` and Microtasks

Consider:

```js
async function test() {
  console.log("A");

  await Promise.resolve();

  console.log("B");
}

test();

console.log("C");
```

Output:

```text
A
C
B
```

Why?

Before `await`:

```text
A
```

The async function pauses at `await`.

The continuation:

```js
console.log("B");
```

is scheduled through Promise microtask processing.

Then:

```text
C
```

runs as part of the current synchronous code.

Finally:

```text
B
```

runs.

---

# 13. `await` Does Not Block the Entire Program

Consider:

```js
async function load() {
  console.log("Start");

  await Promise.resolve();

  console.log("After await");
}

load();

console.log("Other code");
```

Output:

```text
Start
Other code
After await
```

The `await` pauses the current async function, not the entire JavaScript runtime.

---

# 14. `queueMicrotask()` vs `setTimeout()`

### Microtask

```js
queueMicrotask(() => {
  console.log("Microtask");
});
```

### Task

```js
setTimeout(() => {
  console.log("Task");
}, 0);
```

Typical order:

```text
Microtask
Task
```

This difference is important when understanding asynchronous execution order.

---

# 15. Microtasks Run After Current Synchronous Code

Example:

```js
console.log("A");

queueMicrotask(() => {
  console.log("B");
});

console.log("C");

queueMicrotask(() => {
  console.log("D");
});

console.log("E");
```

Output:

```text
A
C
E
B
D
```

All current synchronous code executes first:

```text
A
C
E
```

Then microtasks:

```text
B
D
```

---

# 16. Microtask Queue Processing

A simplified model:

```text
Current JavaScript
       ↓
Call Stack
       ↓
Stack becomes empty
       ↓
Process Microtasks
       ↓
Microtask Queue empty
       ↓
Continue event-loop processing
       ↓
Next Task
```

The actual browser event loop also includes rendering and other scheduling details.

---

# 17. Microtask Queue Can Delay Tasks

Consider:

```js
queueMicrotask(() => {
  console.log("Microtask 1");
});

setTimeout(() => {
  console.log("Timer");
}, 0);
```

The microtask is processed before the timer task.

This means microtasks can delay tasks if many microtasks are continuously added.

---

# 18. Microtask Starvation

A program can keep creating microtasks:

```js
function loop() {
  queueMicrotask(loop);
}

loop();
```

Conceptually:

```text
Microtask
   ↓
Microtask
   ↓
Microtask
   ↓
Microtask
   ↓
...
```

If microtasks continuously keep getting added, normal task processing can be delayed.

This situation is sometimes described as **microtask starvation**.

Avoid creating uncontrolled microtask loops.

---

# 19. Promise Example

```js
console.log("Start");

Promise.resolve()
  .then(() => {
    console.log("First");
  })
  .then(() => {
    console.log("Second");
  });

setTimeout(() => {
  console.log("Timer");
}, 0);

console.log("End");
```

Output:

```text
Start
End
First
Second
Timer
```

Simplified:

```text
Synchronous
    ↓
Start
End
    ↓
Microtask
    ↓
First
    ↓
Microtask
    ↓
Second
    ↓
Task
    ↓
Timer
```

---

# 20. Microtask Queue and `fetch()`

Consider:

```js
fetch("/api/users")
  .then((response) => response.json())
  .then((users) => {
    console.log(users);
  });
```

The network operation itself is handled by the runtime/browser.

When the Promise settles, the `.then()` continuation is scheduled through Promise microtask processing.

Simplified:

```text
fetch()
  ↓
Network operation
  ↓
Promise settles
  ↓
Microtask Queue
  ↓
.then()
  ↓
Call Stack
```

---

# 21. Microtasks and Error Handling

Promise rejection handlers are also microtasks.

```js
Promise.reject(new Error("Failed"))
  .catch((error) => {
    console.log(error.message);
  });
```

The error handler does not execute in the middle of the current synchronous operation.

It runs during microtask processing.

---

# 22. Microtasks and DOM Updates

In browsers, microtasks can run before the browser proceeds to certain rendering steps.

For example:

```js
button.addEventListener("click", () => {
  element.textContent = "Updated";

  queueMicrotask(() => {
    console.log("Microtask");
  });
});
```

The exact rendering timing depends on the browser and event-loop scheduling, but microtasks are generally processed as part of the current event-loop turn before the browser moves on to subsequent phases such as rendering.

---

# 23. Task Queue vs Microtask Queue

| Feature                                  | Microtask Queue | Task Queue          |
| ---------------------------------------- | --------------- | ------------------- |
| Promise callbacks                        | Yes             | No                  |
| `queueMicrotask()`                       | Yes             | No                  |
| `async/await` continuation               | Yes             | No                  |
| `setTimeout()`                           | No              | Yes                 |
| DOM event callbacks                      | Generally task  | Yes                 |
| Priority in normal event-loop processing | Higher          | Lower               |
| Processed after current synchronous code | Yes             | Yes                 |
| Can delay tasks                          | Yes             | Not in the same way |

This table is a simplified learning model; browser and runtime specifications have additional scheduling details.

---

# 24. Example Combining Everything

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

queueMicrotask(() => {
  console.log("4");
});

console.log("5");
```

Output:

```text
1
5
3
4
2
```

Execution:

```text
Synchronous
────────────
1
5

Microtasks
──────────
3
4

Task
────
2
```

---

# 25. Important Rule for Promises

Consider:

```js
Promise.resolve().then(() => {
  console.log("A");
});

console.log("B");
```

Output:

```text
B
A
```

Even though the Promise is already resolved, its `.then()` callback runs asynchronously through the microtask mechanism.

---

# 26. Microtasks Are Not Parallel Threads

A microtask does not automatically create a new thread.

For example:

```js
queueMicrotask(() => {
  for (let i = 0; i < 1000000000; i++) {
    // heavy work
  }
});
```

The microtask itself still runs JavaScript on the relevant thread.

If it performs heavy synchronous work, it can block other work.

---

# 27. Practical Use of `queueMicrotask()`

You can use `queueMicrotask()` when you specifically need to schedule small work after the current synchronous operation.

Example:

```js
let ready = false;

function initialize() {
  ready = true;

  queueMicrotask(() => {
    console.log("Initialization finished");
  });
}
```

It is useful when you need microtask timing without creating a Promise solely for scheduling.

---

# 28. Common Mistakes

### Mistake 1: Promise callbacks execute immediately

```js
Promise.resolve().then(callback);
```

The callback is asynchronous.

---

### Mistake 2: `setTimeout(0)` executes before Promise callbacks

Normally:

```text
Promise callback
      ↓
Timer callback
```

---

### Mistake 3: `await` blocks JavaScript

`await` pauses the current async function, not the entire runtime.

---

### Mistake 4: Microtasks are parallel

They are still JavaScript callbacks executed by the runtime.

---

### Mistake 5: Microtasks cannot affect task timing

A large or continuously replenished microtask queue can delay tasks.

---

# 29. Simple Mental Model

```text
             Synchronous Code
                    ↓
               Call Stack
                    ↓
              Stack becomes
                 empty
                    ↓
             Microtask Queue
                    ↓
          Process microtasks
                    ↓
          Microtask Queue empty
                    ↓
               Event Loop
                    ↓
                Next Task
                    ↓
               Call Stack
```

---

# 30. Key Takeaways

* The **Microtask Queue** handles certain high-priority asynchronous callbacks.
* Promise callbacks use the microtask mechanism.
* `.then()`, `.catch()`, and `.finally()` use microtasks.
* `queueMicrotask()` directly schedules a microtask.
* `async/await` continuations use Promise-based microtask processing.
* Current synchronous code always completes before queued microtasks run.
* Microtasks are normally processed before the next task.
* `setTimeout()` callbacks are tasks, not microtasks.
* `setTimeout(..., 0)` does not execute before microtasks.
* Too many microtasks can delay tasks.
* Microtasks do not automatically create parallel execution.
* Heavy microtasks can still block JavaScript execution.

## Quick Example

```js
console.log("Start");

setTimeout(() => {
  console.log("Task");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask");
});

console.log("End");
```

Output:

```text
Start
End
Microtask
Task
```

