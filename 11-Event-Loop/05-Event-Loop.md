# JavaScript Event Loop

The **Event Loop** is the mechanism that allows JavaScript to handle asynchronous operations while JavaScript itself runs code on a single main thread.

It coordinates:

* Call Stack
* Heap
* Host APIs
* Task Queue
* Microtask Queue
* JavaScript execution

---

## 1. Why Do We Need the Event Loop?

JavaScript executes synchronous code one statement at a time.

For example:

```javascript
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

But JavaScript applications also need to handle things such as:

* Timers
* Network requests
* User clicks
* File operations
* Promises
* `fetch()`
* `async/await`

JavaScript should not remain blocked while waiting for these operations.

The Event Loop helps coordinate this work.

---

## 2. Main Components

A simplified JavaScript runtime can be viewed as:

```text
              JavaScript Runtime
                     │
        ┌────────────┴────────────┐
        │                         │
   Call Stack                   Heap
        │
        │
        ▼
   Host Environment
   ├── Timers
   ├── Network
   ├── DOM Events
   └── Other APIs
        │
        ├──────────────► Task Queue
        │
        └──────────────► Microtask Queue
                              │
                              ▼
                         Event Loop
                              │
                              ▼
                         Call Stack
```

This is a simplified model. Browsers and Node.js have additional implementation details.

---

# 3. Call Stack

The **Call Stack** keeps track of currently executing JavaScript functions.

Example:

```javascript
function first() {
    second();
}

function second() {
    console.log("Hello");
}

first();
```

Execution:

```text
first()
   ↓
second()
   ↓
console.log()
```

When a function finishes, it is removed from the stack.

The stack follows **LIFO**:

> Last In, First Out

---

# 4. Heap

The **Heap** is an area of memory used for dynamically allocated data such as objects, arrays, and functions.

Example:

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

The object requires memory managed by the JavaScript runtime.

The heap is also involved with garbage collection.

> The heap is a simplified conceptual model; JavaScript engines manage memory internally in more complex ways.

---

# 5. Host Environment

JavaScript itself does not provide every asynchronous capability.

The environment running JavaScript provides additional functionality.

### Browser

A browser provides features such as:

* Timers
* DOM events
* Network requests
* `fetch()`
* Storage APIs

### Node.js

Node.js provides features such as:

* File system operations
* Timers
* Network operations
* Streams
* Event handling

These are provided by the host environment rather than being ordinary JavaScript language syntax.

---

# 6. Task Queue

The **Task Queue** contains callbacks that are ready to be executed as tasks.

Examples can include callbacks from:

```javascript
setTimeout()
```

and browser events such as:

```javascript
click
input
```

Example:

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("End");
```

Output:

```text
Start
End
Timer
```

Even with `0` milliseconds, the timer callback does not execute immediately.

It becomes eligible to run after the required delay and after the current JavaScript work has finished.

---

# 7. Microtask Queue

The **Microtask Queue** contains microtasks such as:

* Promise reactions
* `queueMicrotask()`
* Continuations of `async/await`

Example:

```javascript
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

The synchronous code finishes first.

Then the microtask is processed.

---

# 8. Event Loop

The **Event Loop** coordinates when queued work can be executed.

A simplified model is:

```text
1. Run synchronous JavaScript
          ↓
2. Call Stack becomes empty
          ↓
3. Process available microtasks
          ↓
4. Run an eligible task
          ↓
5. Process microtasks again
          ↓
6. Continue
```

The exact scheduling details depend on the host environment.

---

# 9. Event Loop Example

Consider:

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

Promise.resolve().then(() => {
    console.log("C");
});

console.log("D");
```

Output:

```text
A
D
C
B
```

### Step 1

Synchronous code starts:

```javascript
console.log("A");
```

Output:

```text
A
```

### Step 2

The timer is registered with the host environment:

```javascript
setTimeout(() => {
    console.log("B");
}, 0);
```

### Step 3

The Promise callback is scheduled as a microtask:

```javascript
Promise.resolve().then(() => {
    console.log("C");
});
```

### Step 4

Synchronous execution continues:

```javascript
console.log("D");
```

Output:

```text
A
D
```

### Step 5

The current synchronous work is complete.

The microtask runs:

```text
C
```

### Step 6

The timer callback becomes a task that can run:

```text
B
```

Final output:

```text
A
D
C
B
```

---

# 10. `setTimeout(0)` Is Not Immediate

This is an important concept.

```javascript
setTimeout(() => {
    console.log("Hello");
}, 0);
```

`0` does **not** mean:

> Execute immediately.

It means the callback can become eligible after approximately the specified delay.

The callback still has to wait for:

1. Current synchronous code to finish.
2. Appropriate microtasks to be processed.
3. The host environment to schedule the task.

Therefore:

```javascript
setTimeout(callback, 0);
```

does not guarantee immediate execution.

---

# 11. Promise vs Timer

Consider:

```javascript
setTimeout(() => {
    console.log("Timer");
}, 0);

Promise.resolve().then(() => {
    console.log("Promise");
});
```

Usually:

```text
Promise
Timer
```

Why?

The Promise callback is a microtask, while the timer callback is a task.

In the usual event-loop processing model, microtasks are processed before the next task.

---

# 12. `queueMicrotask()`

JavaScript also provides:

```javascript
queueMicrotask();
```

Example:

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

The callback runs after the current synchronous execution completes.

---

# 13. Multiple Microtasks

Microtasks can schedule additional microtasks.

```javascript
console.log("A");

Promise.resolve().then(() => {
    console.log("B");

    Promise.resolve().then(() => {
        console.log("C");
    });
});

console.log("D");
```

Output:

```text
A
D
B
C
```

The newly created microtask is processed as part of the microtask processing before moving to the next task.

---

# 14. Microtask Starvation

Because microtasks can schedule more microtasks, excessive microtask work can delay tasks.

Example:

```javascript
function run() {
    queueMicrotask(() => {
        console.log("Microtask");
        run();
    });
}

run();
```

This continuously schedules microtasks.

As a result, normal tasks may not get an opportunity to run.

This is called **microtask starvation**.

Avoid creating endless microtask chains.

---

# 15. `async/await` and the Event Loop

`async/await` is built on Promises.

Example:

```javascript
async function loadData() {
    console.log("Start");

    await Promise.resolve();

    console.log("After await");
}

loadData();

console.log("End");
```

Output:

```text
Start
End
After await
```

The code after `await` continues asynchronously.

Conceptually:

```text
loadData()
   ↓
Start
   ↓
await
   ↓
current function pauses
   ↓
synchronous code continues
   ↓
Promise continuation runs
   ↓
After await
```

`await` does not block the entire JavaScript runtime.

---

# 16. `fetch()` and the Event Loop

Consider:

```javascript
async function getUser() {
    const response = await fetch("/api/user");

    const user = await response.json();

    console.log(user);
}
```

The network operation is handled by the host environment.

JavaScript does not continuously execute code while waiting for the network response.

Once the Promise settles, the continuation can be scheduled for JavaScript execution.

Conceptually:

```text
JavaScript
    │
    ▼
fetch()
    │
    ▼
Host Environment
    │
    │ Network request
    ▼
Promise settles
    │
    ▼
Microtask / async continuation
    │
    ▼
Call Stack
```

---

# 17. DOM Events and the Event Loop

Suppose a user clicks a button:

```javascript
button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

The browser handles the event and eventually schedules the callback for JavaScript execution.

Conceptually:

```text
User clicks
    ↓
Browser handles event
    ↓
Callback becomes a task
    ↓
Event Loop
    ↓
Call Stack
    ↓
Callback executes
```

---

# 18. Rendering

Browsers also need to update the page visually.

For example:

```javascript
element.textContent = "Hello";
```

The browser may need to perform rendering work after JavaScript execution.

A simplified browser model is:

```text
JavaScript
    ↓
Microtasks
    ↓
Rendering opportunity
    ↓
Next task
```

The exact rendering schedule is controlled by the browser and is more complicated than this simplified diagram.

Do not assume that the browser performs a visual render after every JavaScript statement or after every task.

---

# 19. Event Loop and Blocking Code

Consider:

```javascript
console.log("Start");

for (let i = 0; i < 1000000000; i++) {
    // Heavy work
}

console.log("End");
```

While the loop is executing, the JavaScript thread is busy.

Other JavaScript callbacks cannot execute on that same thread until the blocking work finishes.

Therefore, asynchronous APIs do not automatically make CPU-heavy JavaScript non-blocking.

---

# 20. Asynchronous Does Not Mean Parallel

Consider:

```javascript
setTimeout(() => {
    console.log("Done");
}, 1000);
```

The timer allows the runtime to handle other work while waiting.

But this does not mean the JavaScript callback itself is running simultaneously with another JavaScript callback on the same main thread.

For CPU-intensive work, environments such as browsers and Node.js can use other mechanisms such as:

* Web Workers
* Worker Threads
* Other processes

when parallel computation is needed.

---

# 21. A Practical Execution Model

A useful mental model is:

```text
              Synchronous Code
                     │
                     ▼
                Call Stack
                     │
              Stack becomes empty
                     │
                     ▼
              Microtask Queue
                     │
                     ▼
              Eligible Task
                     │
                     ▼
                Call Stack
                     │
                     ▼
              Continue...
```

Remember that actual browser and Node.js scheduling has additional rules.

---

# 22. Complete Example

```javascript
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

### Why?

Synchronous:

```text
1
5
```

Microtasks:

```text
3
4
```

Task:

```text
2
```

Therefore:

```text
1
5
3
4
2
```

---

# 23. Event Loop in Node.js

Node.js also uses an event loop, but its architecture is different from the browser.

Node.js handles asynchronous operations using its runtime and underlying system facilities.

Examples include:

* Timers
* File system operations
* Network operations
* I/O
* Event handling

Node.js also has event-loop phases and additional scheduling behavior.

For basic JavaScript learning, remember:

```text
JavaScript Code
      ↓
Node.js Runtime
      ↓
Asynchronous Operations
      ↓
Queues / Event Loop
      ↓
JavaScript Call Stack
```

The detailed Node.js event-loop phases can be studied separately when working deeply with Node.js.

---

# 24. Common Mistakes

### Mistake 1: Thinking `setTimeout(0)` runs immediately

```javascript
setTimeout(() => {
    console.log("Hello");
}, 0);
```

It does not execute immediately.

---

### Mistake 2: Thinking asynchronous means parallel

Asynchronous programming allows work to be coordinated without blocking the current flow.

It does not automatically mean multiple JavaScript callbacks execute simultaneously.

---

### Mistake 3: Thinking `await` blocks everything

```javascript
await fetch("/api/users");
```

`await` pauses the current async function's continuation.

It does not freeze the entire JavaScript runtime.

---

### Mistake 4: Ignoring microtasks

Promise callbacks usually run before the next task.

```javascript
Promise.resolve().then(() => {
    console.log("Promise");
});
```

This is why Promise callbacks commonly appear before timer callbacks.

---

### Mistake 5: Assuming the Event Loop executes callbacks itself

The Event Loop coordinates when work can proceed.

The callback ultimately executes on the JavaScript execution stack.

---

# 25. Event Loop Summary

| Component        | Purpose                                |
| ---------------- | -------------------------------------- |
| Call Stack       | Executes JavaScript functions          |
| Heap             | Manages dynamically allocated memory   |
| Host Environment | Provides timers, network, events, etc. |
| Task Queue       | Holds eligible tasks                   |
| Microtask Queue  | Holds Promise and microtask callbacks  |
| Event Loop       | Coordinates execution of queued work   |

---

# 26. Key Rules to Remember

```text
Synchronous code runs first.
        ↓
Call Stack executes JavaScript.
        ↓
Async operations are handled by the host environment.
        ↓
Callbacks become queued work.
        ↓
Microtasks are generally processed before the next task.
        ↓
Tasks are processed when the runtime can execute them.
```

The most important idea is:

> **The Event Loop allows JavaScript to coordinate asynchronous work without blocking the current execution flow.**

---

## Related Topics

* [Call Stack](./01-Call-Stack.md)
* [Heap](./02-Heap.md)
* [Task Queue](./03-Task-Queue.md)
* [Microtask Queue](./04-Microtask-Queue.md)
* [Execution Order](./06-Execution-Order.md)
* [Promises](../10-Asynchronous-JavaScript/04-Promises.md)
* [`async/await`](../10-Asynchronous-JavaScript/06-async-await.md)
