# JavaScript Task Queue

## What is the Task Queue?

The **Task Queue** is a queue where certain asynchronous callbacks wait until the JavaScript runtime can execute them.

It is also commonly called the **Macrotask Queue**.

Examples of tasks that can enter the task queue include callbacks from:

* `setTimeout()`
* `setInterval()`
* DOM events
* some I/O operations
* other browser or runtime tasks

The Event Loop helps move eligible tasks to the Call Stack.

---

# 1. Basic Flow

A simplified JavaScript runtime looks like this:

```text
Call Stack
    ↓
JavaScript executes
    ↓
Async operation
    ↓
Task Queue
    ↓
Event Loop
    ↓
Call Stack
```

The task does not execute directly from the queue.

The Event Loop coordinates when it can be moved to the Call Stack.

---

# 2. Simple `setTimeout()` Example

```js
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

Why?

The synchronous code runs first.

```text
console.log("Start")
       ↓
setTimeout()
       ↓
console.log("End")
       ↓
callback becomes eligible
       ↓
Event Loop
       ↓
Task Queue
       ↓
Call Stack
       ↓
console.log("Timer")
```

---

# 3. `setTimeout(..., 0)` Does Not Mean Immediate

Consider:

```js
setTimeout(() => {
  console.log("Hello");
}, 0);
```

`0` means there is no requested delay beyond the minimum timer threshold.

It does **not** mean:

```text
Run immediately
```

Instead, the callback becomes eligible after the timer condition is satisfied and can run when the runtime gets an opportunity to process it.

---

# 4. Synchronous Code Runs First

Example:

```js
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

The current synchronous execution must finish before the timer callback can run.

---

# 5. Task Queue Example

Consider:

```js
setTimeout(() => {
  console.log("Task");
}, 0);
```

Simplified process:

```text
1. setTimeout() is called
2. Timer is registered
3. JavaScript continues
4. Timer becomes ready
5. Callback becomes eligible for the task queue
6. Event Loop waits for the Call Stack to be available
7. Callback is moved to the Call Stack
8. Callback executes
```

---

# 6. Queue Means FIFO

A queue generally follows:

**FIFO = First In, First Out**

Example:

```text
Task A
Task B
Task C
```

Normally:

```text
Task A
   ↓
Task B
   ↓
Task C
```

The first eligible task is processed before later tasks.

However, the browser/runtime has multiple types of queues and scheduling rules, so the overall event-loop behavior is more complex than one simple queue.

---

# 7. Multiple Timers

Example:

```js
setTimeout(() => {
  console.log("A");
}, 0);

setTimeout(() => {
  console.log("B");
}, 0);

setTimeout(() => {
  console.log("C");
}, 0);
```

A typical execution order is:

```text
A
B
C
```

The timers are registered in that order and their callbacks become eligible accordingly.

---

# 8. Timer Delays Are Minimum Delays

Consider:

```js
setTimeout(() => {
  console.log("Done");
}, 1000);
```

This does not guarantee that `Done` executes exactly after one second.

It means the callback cannot become eligible before the requested delay has elapsed.

If the Call Stack is busy:

```text
Timer ready
   ↓
Call Stack still busy
   ↓
Wait
   ↓
Call Stack becomes available
   ↓
Callback executes
```

---

# 9. Blocking the Call Stack

Example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timer");
}, 0);

for (let i = 0; i < 1000000000; i++) {
  // heavy synchronous work
}

console.log("End");
```

The timer callback cannot execute while the long synchronous loop is occupying the JavaScript thread.

The output remains:

```text
Start
End
Timer
```

The timer does not interrupt the running JavaScript code.

---

# 10. Task Queue and the Event Loop

The Event Loop continuously coordinates between queues and the Call Stack.

Simplified:

```text
                 JavaScript Runtime
                        │
                        ↓
                  ┌───────────┐
                  │ Call Stack│
                  └─────┬─────┘
                        ↑
                        │
                   Event Loop
                        ↑
                        │
                  Task Queue
```

When appropriate, a task can be moved from the queue to the Call Stack.

---

# 11. DOM Events

Browser events can also result in callbacks being scheduled.

Example:

```js
button.addEventListener("click", () => {
  console.log("Button clicked");
});
```

When the user clicks the button, the browser handles the event and eventually schedules the callback for JavaScript execution.

Simplified:

```text
User clicks button
       ↓
Browser handles event
       ↓
Callback becomes eligible
       ↓
Event Loop
       ↓
Call Stack
       ↓
Callback executes
```

---

# 12. Multiple User Events

Suppose several events occur:

```text
Click
Click
Input
Click
```

Their associated callbacks may need to wait for JavaScript execution time.

If the Call Stack is busy:

```text
Call Stack
    │
    │ busy
    ↓
Event callbacks waiting
```

Once JavaScript becomes available, eligible callbacks can be processed according to the runtime's scheduling rules.

---

# 13. `setInterval()`

`setInterval()` can repeatedly schedule callbacks.

Example:

```js
const timer = setInterval(() => {
  console.log("Running");
}, 1000);
```

To stop it:

```js
clearInterval(timer);
```

Conceptually:

```text
Timer
  ↓
Callback
  ↓
Timer
  ↓
Callback
  ↓
Timer
  ↓
Callback
```

The callback still cannot interrupt currently running synchronous JavaScript.

---

# 14. `setTimeout()` vs `setInterval()`

### `setTimeout()`

Runs a callback once:

```js
setTimeout(() => {
  console.log("Once");
}, 1000);
```

### `setInterval()`

Schedules repeated callbacks:

```js
setInterval(() => {
  console.log("Repeated");
}, 1000);
```

Both are asynchronous scheduling mechanisms.

---

# 15. Task Queue Does Not Execute Tasks Itself

The queue is only a waiting area.

It does not execute JavaScript.

```text
Task Queue
──────────────
Callback A
Callback B
Callback C
```

The Event Loop coordinates moving an eligible callback to the Call Stack.

```text
Task Queue
    ↓
Event Loop
    ↓
Call Stack
    ↓
Execute callback
```

---

# 16. Task Queue vs Call Stack

### Call Stack

Contains currently executing JavaScript.

```text
functionA()
functionB()
```

### Task Queue

Contains callbacks waiting to execute.

```text
timerCallback()
clickCallback()
otherCallback()
```

Simplified:

```text
Call Stack             Task Queue
────────────           ─────────────
Running code           Waiting callbacks
     │                       │
     └──────── Event Loop ───┘
```

---

# 17. Task Queue vs Microtask Queue

JavaScript also has a **Microtask Queue**.

For example:

```js
Promise.resolve().then(() => {
  console.log("Microtask");
});

setTimeout(() => {
  console.log("Task");
}, 0);
```

Typical output:

```text
Microtask
Task
```

After the current synchronous code finishes, microtasks are generally processed before the next task.

This distinction is important for understanding Promise execution.

---

# 18. Example: Task vs Microtask

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

Execution:

```text
Synchronous code
       ↓
Start
       ↓
End
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

# 19. Why Microtasks Matter

Promise callbacks use the microtask mechanism.

Example:

```js
Promise.resolve().then(() => {
  console.log("Promise callback");
});
```

The callback does not normally go into the same task queue as a timer.

It goes to the **Microtask Queue**.

This gives microtasks higher priority in the usual event-loop processing model.

---

# 20. Task Queue Example with Promise

```js
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

Why?

```text
1. A → synchronous
2. D → synchronous
3. C → microtask
4. B → task
```

---

# 21. Tasks Are Not Always Timers

A common misunderstanding is:

> "The Task Queue only contains timers."

That is not correct.

Depending on the environment, tasks can be associated with:

```text
Timers
User interaction events
Network-related callbacks
I/O
Other runtime scheduling mechanisms
```

The exact scheduling behavior depends on the browser or JavaScript runtime.

---

# 22. Browser Task Processing

In a browser, the runtime may process work such as:

```text
JavaScript
Timers
User events
Network activity
Rendering-related work
Microtasks
```

The browser has additional scheduling responsibilities beyond simply executing JavaScript.

---

# 23. Node.js Task Processing

Node.js also has its own event-loop phases and queues.

Examples include work related to:

```text
Timers
I/O callbacks
Poll
Check
Close callbacks
```

Node.js also has Promise microtasks and its own scheduling mechanisms.

The exact Node.js event-loop phases are more advanced and can be studied separately.

---

# 24. Task Queue and API Requests

Consider:

```js
fetch("/api/users")
  .then((response) => response.json())
  .then((users) => {
    console.log(users);
  });
```

The network operation does not simply block the JavaScript Call Stack while waiting.

The runtime handles the asynchronous operation, and when the Promise settles, its continuation is scheduled through the microtask mechanism.

Simplified:

```text
fetch()
  ↓
Network operation
  ↓
Promise settles
  ↓
Microtask
  ↓
Call Stack
  ↓
.then() callback
```

---

# 25. Task Queue and User Interface

Consider a webpage with:

```js
button.addEventListener("click", handleClick);
```

When the user clicks:

```text
User action
    ↓
Browser event handling
    ↓
Callback becomes eligible
    ↓
Task processing
    ↓
Call Stack
    ↓
handleClick()
```

If the Call Stack is blocked by heavy JavaScript, the event cannot be processed immediately.

---

# 26. Long Tasks

A **long task** is JavaScript work that occupies the main thread for a significant amount of time.

Example:

```js
for (let i = 0; i < 1000000000; i++) {
  // expensive operation
}
```

While this runs:

```text
Call Stack
     │
     │ blocked
     ↓
User events wait
Timers wait
Other callbacks wait
```

This can make the page feel slow or unresponsive.

---

# 27. Breaking Up Heavy Work

Instead of performing one huge synchronous operation, work can sometimes be divided into smaller pieces.

Conceptually:

```text
Large Task
    ↓
Small Task
    ↓
Small Task
    ↓
Small Task
```

This can give the runtime opportunities to process other work between chunks.

The exact technique depends on the application.

---

# 28. Queue Visualization

A simplified model:

```text
                 ┌───────────────┐
                 │  Call Stack   │
                 └───────▲───────┘
                         │
                    Event Loop
                         │
          ┌──────────────┴──────────────┐
          │                             │
          │                             │
   Microtask Queue                 Task Queue
          │                             │
    Promise callbacks            Timer callbacks
    async continuations          Event callbacks
```

Microtasks and tasks are different scheduling mechanisms.

---

# 29. Important Rule

A useful simplified rule is:

```text
Run current synchronous JavaScript
            ↓
Process available microtasks
            ↓
Continue with the event-loop/task cycle
```

The actual browser specification includes rendering and other scheduling details, so this should be treated as a learning model rather than a complete specification.

---

# 30. Common Mistakes

## Mistake 1: `setTimeout(0)` Means Immediate

```js
setTimeout(callback, 0);
```

It does not execute immediately.

---

## Mistake 2: The Task Queue Executes Code

The queue stores waiting callbacks.

The Call Stack executes JavaScript.

---

## Mistake 3: All Async Work Uses the Task Queue

Promises use the microtask mechanism.

---

## Mistake 4: Timer Guarantees Exact Execution Time

```js
setTimeout(callback, 1000);
```

This does not guarantee execution exactly at 1000 ms.

---

## Mistake 5: Async Means Parallel

Asynchronous scheduling does not automatically mean JavaScript code is executing in parallel.

---

# 31. Practical Example

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

Output:

```text
1
4
3
2
```

Simplified execution:

```text
                 Start
                   │
                   ↓
            Synchronous code
               1 → 4
                   │
                   ↓
             Microtask Queue
                   │
                   ↓
                   3
                   │
                   ↓
               Task Queue
                   │
                   ↓
                   2
```

---

# 32. Key Takeaways

* The **Task Queue** stores certain callbacks waiting for execution.
* It is also commonly called the **Macrotask Queue**.
* `setTimeout()` callbacks can enter task processing.
* DOM event callbacks can also be scheduled as tasks.
* `setTimeout(..., 0)` does not mean immediate execution.
* Timer delays are minimum delays, not exact execution times.
* The Call Stack must be available before queued JavaScript can execute.
* Long synchronous code can delay queued callbacks.
* The Task Queue is different from the Microtask Queue.
* Promise callbacks use the Microtask Queue.
* Microtasks are generally processed before the next task.
* The Event Loop coordinates queues and the Call Stack.
* Async operations do not automatically mean parallel execution.
* Browser and Node.js runtimes have additional scheduling details.

## Simple Mental Model

```text
Synchronous JavaScript
        ↓
    Call Stack
        ↓
Current code finishes
        ↓
Microtasks
        ↓
Event Loop
        ↓
Eligible Task
        ↓
    Call Stack
        ↓
Task executes
```
