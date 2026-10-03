# JavaScript Execution Order

JavaScript execution order describes **the order in which JavaScript code is executed**.

Understanding execution order is especially important when working with:

* Synchronous code
* Functions
* Callbacks
* Promises
* `async/await`
* Timers
* Microtasks
* Tasks
* Event Loop

---

# 1. Basic Execution Order

JavaScript normally executes synchronous code from top to bottom.

```javascript
console.log("First");
console.log("Second");
console.log("Third");
```

Output:

```text
First
Second
Third
```

The order is:

```text
First
  ↓
Second
  ↓
Third
```

---

# 2. Function Calls

When JavaScript encounters a function call, it executes the function before continuing with the following statement.

```javascript
function greet() {
    console.log("Hello");
}

console.log("Start");

greet();

console.log("End");
```

Output:

```text
Start
Hello
End
```

Execution:

```text
console.log("Start")
        ↓
greet()
        ↓
console.log("Hello")
        ↓
console.log("End")
```

---

# 3. Nested Function Calls

Consider:

```javascript
function first() {
    console.log("First");

    second();

    console.log("After second");
}

function second() {
    console.log("Second");
}

first();
```

Output:

```text
First
Second
After second
```

The call stack works like:

```text
first()
  ↓
second()
  ↓
second() finishes
  ↓
first() continues
```

---

# 4. Synchronous Code Runs Before Asynchronous Code

Consider:

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

console.log("C");
```

Output:

```text
A
C
B
```

Even though the timer uses `0` milliseconds, the callback does not run before the synchronous code.

The order is:

```text
A
↓
C
↓
Timer callback
↓
B
```

---

# 5. Promise Callbacks

Promise callbacks are scheduled as microtasks.

```javascript
console.log("A");

Promise.resolve().then(() => {
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

Why?

```text
Synchronous code
      ↓
A
      ↓
C
      ↓
Microtask
      ↓
B
```

---

# 6. Promise vs `setTimeout`

This is one of the most important execution-order examples.

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Timer");
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
Timer
```

### Execution

First, synchronous code:

```text
Start
End
```

Then the microtask:

```text
Promise
```

Then the timer task:

```text
Timer
```

So:

```text
Start
  ↓
End
  ↓
Promise
  ↓
Timer
```

---

# 7. Multiple Promise Callbacks

Consider:

```javascript
Promise.resolve().then(() => {
    console.log("A");
});

Promise.resolve().then(() => {
    console.log("B");
});

console.log("C");
```

Output:

```text
C
A
B
```

The current synchronous code finishes first.

Then microtasks are processed in their scheduled order.

```text
Synchronous
    ↓
C
    ↓
Microtask A
    ↓
Microtask B
```

---

# 8. `queueMicrotask()`

`queueMicrotask()` also schedules a microtask.

```javascript
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

The microtask waits until the current synchronous execution finishes.

---

# 9. Promise and `queueMicrotask()`

Both can create microtasks.

```javascript
console.log("Start");

Promise.resolve().then(() => {
    console.log("Promise");
});

queueMicrotask(() => {
    console.log("Microtask");
});

console.log("End");
```

Output:

```text
Start
End
Promise
Microtask
```

They are processed according to the order in which the microtasks were queued.

---

# 10. Microtask Scheduling Another Microtask

A microtask can create another microtask.

```javascript
Promise.resolve().then(() => {
    console.log("A");

    Promise.resolve().then(() => {
        console.log("B");
    });
});

Promise.resolve().then(() => {
    console.log("C");
});
```

Output:

```text
A
C
B
```

Why?

Initially:

```text
Microtask Queue:

A
C
```

`A` executes and schedules `B`:

```text
Microtask Queue:

C
B
```

So:

```text
A
C
B
```

---

# 11. Timer and Microtask Inside a Timer

Consider:

```javascript
setTimeout(() => {
    console.log("Timer");

    Promise.resolve().then(() => {
        console.log("Promise");
    });
}, 0);

setTimeout(() => {
    console.log("Second Timer");
}, 0);
```

A typical output is:

```text
Timer
Promise
Second Timer
```

The first timer runs.

Inside it, a Promise callback is scheduled.

The microtask is processed before moving to the next task.

Conceptually:

```text
Timer 1
   ↓
Promise microtask
   ↓
Timer 2
```

---

# 12. `async` Functions

An `async` function starts executing synchronously until it reaches an `await`.

```javascript
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

Execution:

```text
test()
  ↓
A
  ↓
await
  ↓
function continuation is scheduled
  ↓
C
  ↓
B
```

---

# 13. Code Before `await`

Code before `await` normally executes immediately when the async function is called.

```javascript
async function load() {
    console.log("Before");

    await Promise.resolve();

    console.log("After");
}

console.log("Start");

load();

console.log("End");
```

Output:

```text
Start
Before
End
After
```

---

# 14. Code After `await`

The code after `await` continues asynchronously.

```javascript
async function example() {
    console.log("1");

    await Promise.resolve();

    console.log("2");
}

example();

console.log("3");
```

Output:

```text
1
3
2
```

The continuation after `await` is associated with Promise-based microtask processing.

---

# 15. `fetch()` Execution Order

Consider:

```javascript
console.log("Start");

fetch("/api/users")
    .then(() => {
        console.log("Response");
    });

console.log("End");
```

The exact timing depends on the network and environment.

But:

```text
Start
End
```

will execute before the response callback can run because the current synchronous code finishes first.

A simplified model is:

```text
Start
   ↓
fetch()
   ↓
End
   ↓
network operation completes later
   ↓
Promise callback
   ↓
Response
```

---

# 16. Function + Promise + Timer

Consider:

```javascript
function run() {
    console.log("Function");

    Promise.resolve().then(() => {
        console.log("Promise");
    });
}

console.log("Start");

run();

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("End");
```

Output:

```text
Start
Function
End
Promise
Timer
```

The execution order is:

```text
Start
  ↓
Function
  ↓
End
  ↓
Promise
  ↓
Timer
```

---

# 17. A More Complete Example

```javascript
console.log("1");

setTimeout(() => {
    console.log("2");

    Promise.resolve().then(() => {
        console.log("3");
    });
}, 0);

Promise.resolve().then(() => {
    console.log("4");
});

console.log("5");
```

Output:

```text
1
5
4
2
3
```

### Step 1 — Synchronous

```text
1
5
```

### Step 2 — Microtask

```text
4
```

### Step 3 — Timer task

```text
2
```

### Step 4 — Microtask created by the timer

```text
3
```

Final:

```text
1
5
4
2
3
```

---

# 18. General Execution Rule

A useful simplified model is:

```text
1. Execute synchronous JavaScript
             ↓
2. Current stack finishes
             ↓
3. Process available microtasks
             ↓
4. Run an eligible task
             ↓
5. Process microtasks created during that task
             ↓
6. Continue with the event loop
```

This is a simplified model. Browser rendering and host-specific scheduling can add additional behavior.

---

# 19. Task vs Microtask

| Work                       | Typical Queue                                       |
| -------------------------- | --------------------------------------------------- |
| `Promise.then()`           | Microtask                                           |
| `Promise.catch()`          | Microtask                                           |
| `Promise.finally()`        | Microtask                                           |
| `queueMicrotask()`         | Microtask                                           |
| `async/await` continuation | Microtask                                           |
| `setTimeout()` callback    | Task                                                |
| `setInterval()` callback   | Task                                                |
| DOM event callback         | Task                                                |
| Network-related callback   | Host-dependent; Promise continuation is a microtask |

The exact classification of some host operations depends on the environment.

---

# 20. Important Rule: Current Code Finishes First

Consider:

```javascript
console.log("A");

Promise.resolve().then(() => {
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

The Promise callback cannot interrupt the currently executing synchronous statement sequence.

The current synchronous execution must reach a point where the stack is available before queued asynchronous work can execute.

---

# 21. Execution Order Mental Model

When you see asynchronous JavaScript, ask:

### Step 1

What code is synchronous?

```javascript
console.log("A");
```

### Step 2

What callbacks are being scheduled?

```javascript
setTimeout(...)
Promise.then(...)
queueMicrotask(...)
```

### Step 3

Which callbacks are microtasks?

```javascript
Promise.then(...)
queueMicrotask(...)
```

### Step 4

Which callbacks are tasks?

```javascript
setTimeout(...)
```

### Step 5

What new work is scheduled inside each callback?

This helps determine the final execution order.

---

# 22. Common Mistakes

### Mistake 1: `setTimeout(0)` runs first

Incorrect:

```text
Timer
Synchronous code
```

Usually:

```text
Synchronous code
Timer
```

---

### Mistake 2: Promise runs before synchronous code

Incorrect:

```javascript
Promise.resolve().then(() => {
    console.log("Promise");
});

console.log("Sync");
```

Output:

```text
Promise
Sync
```

Correct output:

```text
Sync
Promise
```

---

### Mistake 3: `await` blocks the entire application

`await` pauses the current async function's continuation.

It does not stop the entire JavaScript runtime.

---

### Mistake 4: All asynchronous operations use exactly the same queue

Different host operations have different scheduling behavior.

For basic reasoning, distinguish between:

```text
Microtasks
```

and

```text
Tasks
```

while remembering that browser and Node.js implementations have additional details.

---

# 23. Quick Reference

```text
Synchronous Code
      ↓
Call Stack
      ↓
Stack becomes available
      ↓
Microtasks
      ↓
Eligible Task
      ↓
Microtasks created by that task
      ↓
Next Task
```

---

# 24. Key Takeaways

* JavaScript executes synchronous code first.
* Function calls execute through the Call Stack.
* Promise callbacks are microtasks.
* `queueMicrotask()` creates a microtask.
* `async/await` uses Promise-based scheduling.
* `setTimeout()` callbacks are tasks.
* `setTimeout(0)` does not mean immediate execution.
* Microtasks are generally processed before the next task.
* A microtask can schedule another microtask.
* Excessive microtasks can delay tasks.
* `await` pauses the current async function, not the whole runtime.
* Exact scheduling details can differ between browsers and Node.js.

> **To understand JavaScript execution order, first separate synchronous code, microtasks, and tasks.**

---

## Related Topics

* [Call Stack](./01-Call-Stack.md)
* [Heap](./02-Heap.md)
* [Task Queue](./03-Task-Queue.md)
* [Microtask Queue](./04-Microtask-Queue.md)
* [Event Loop](./05-Event-Loop.md)
* [Promises](../10-Asynchronous-JavaScript/04-Promises.md)
* [`async/await`](../10-Asynchronous-JavaScript/06-async-await.md)
