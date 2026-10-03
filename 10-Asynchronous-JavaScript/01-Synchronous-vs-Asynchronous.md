# JavaScript Synchronous vs Asynchronous

## What is Synchronous JavaScript?

**Synchronous** code runs one operation at a time, in order.

The next operation waits for the current operation to finish.

```text id="q5k8t2"
Task 1
  ↓
Task 2
  ↓
Task 3
  ↓
Task 4
```

Example:

```js
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

Each statement runs before the next statement starts.

---

# 1. Synchronous Execution

Consider:

```js
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

The function finishes before JavaScript continues to the next statement.

---

# 2. Synchronous Code Blocks Execution

A long-running synchronous operation can block later code.

```js
console.log("Start");

for (let i = 0; i < 1000000000; i++) {
  // Large computation
}

console.log("End");
```

JavaScript must finish the loop before reaching:

```js
console.log("End");
```

So:

```text
Start
   ↓
Long operation
   ↓
End
```

This is called **blocking**.

---

# 3. What is Asynchronous JavaScript?

**Asynchronous** code allows an operation to start without making the rest of the program wait for it to finish.

For example:

```js
console.log("Start");

setTimeout(() => {
  console.log("Async operation");
}, 2000);

console.log("End");
```

Output:

```text
Start
End
Async operation
```

The timer starts, but JavaScript continues executing the next statement.

---

# 4. Synchronous vs Asynchronous

| Synchronous                    | Asynchronous                               |
| ------------------------------ | ------------------------------------------ |
| Runs in order                  | Can complete later                         |
| Next operation waits           | Next operation can continue                |
| Can block execution            | Helps avoid waiting on external operations |
| Easier to follow               | Requires handling completion               |
| Common for normal calculations | Common for network, timers, file I/O       |

---

# 5. Real-World Example

Imagine ordering food at a restaurant.

### Synchronous approach

```text
Order food
    ↓
Wait beside kitchen
    ↓
Food prepared
    ↓
Receive food
    ↓
Continue other work
```

You cannot do anything else while waiting.

### Asynchronous approach

```text
Place order
    ↓
Continue other work
    ↓
Kitchen prepares food
    ↓
Notification when ready
```

This is similar to asynchronous programming.

---

# 6. `setTimeout()` Example

`setTimeout()` is a common way to demonstrate asynchronous behavior.

```js
console.log("Start");

setTimeout(() => {
  console.log("Timer finished");
}, 1000);

console.log("End");
```

Output:

```text
Start
End
Timer finished
```

Even though the timer appears between the two `console.log()` statements, its callback runs later.

---

# 7. The Delay Is Not a Guaranteed Execution Time

Consider:

```js
setTimeout(() => {
  console.log("Done");
}, 1000);
```

The `1000` means the callback will not run **before approximately 1000 ms**.

It does not mean:

```text
Exactly after 1000 ms
```

The callback must wait until JavaScript can process it.

For example:

```text
Timer completes
     ↓
Callback becomes ready
     ↓
Waiting for execution
     ↓
Event loop schedules callback
     ↓
Callback runs
```

---

# 8. Asynchronous Does Not Mean Parallel

This is an important distinction.

Asynchronous code does not automatically mean that JavaScript is executing multiple JavaScript statements simultaneously on different CPU cores.

In browsers and Node.js, asynchronous operations are coordinated with the runtime and event loop.

```text
JavaScript execution
        ↓
     Event Loop
        ↓
Runtime / Web APIs / Node APIs
        ↓
Callback becomes ready
        ↓
JavaScript executes callback
```

---

# 9. Example with Multiple Timers

```js
console.log("Start");

setTimeout(() => {
  console.log("Timer 1");
}, 2000);

setTimeout(() => {
  console.log("Timer 2");
}, 1000);

console.log("End");
```

Output:

```text
Start
End
Timer 2
Timer 1
```

The shorter timer becomes ready first.

---

# 10. Synchronous Function

A normal function call is synchronous.

```js
function calculateTotal(price, quantity) {
  return price * quantity;
}

console.log("Start");

const total = calculateTotal(500, 3);

console.log(total);
console.log("End");
```

Output:

```text
Start
1500
End
```

The result is available immediately after the function returns.

---

# 11. Asynchronous Function

An asynchronous operation may produce its result later.

```js
console.log("Start");

setTimeout(() => {
  const total = 500 * 3;
  console.log(total);
}, 1000);

console.log("End");
```

Output:

```text
Start
End
1500
```

The result is available later.

---

# 12. Why Asynchronous Programming Is Needed

Many operations can take time:

* API requests
* database queries
* reading files
* writing files
* timers
* user interactions
* network requests
* uploading files
* downloading files

If all of these operations blocked JavaScript, applications could become unresponsive.

---

# 13. Network Request Example

Consider a website loading data from a server.

```js
console.log("Loading users...");

fetch("/api/users")
  .then((response) => response.json())
  .then((users) => {
    console.log(users);
  });

console.log("Page continues...");
```

The browser can continue running JavaScript while waiting for the network response.

Conceptually:

```text
Request sent
    ↓
JavaScript continues
    ↓
Server processes request
    ↓
Response arrives
    ↓
Callback / Promise continuation runs
```

---

# 14. Database Example in Node.js

In a Node.js backend:

```js
const users = await User.find();
```

The database operation may take time.

Instead of blocking the entire Node.js process while waiting, Node.js can handle other work while the asynchronous operation is in progress.

When the database operation finishes, execution continues after `await`.

---

# 15. Blocking vs Non-Blocking

### Blocking

A blocking operation prevents later code from continuing until the operation finishes.

```text
Operation
   ↓
WAIT
   ↓
Finish
   ↓
Continue
```

### Non-blocking

A non-blocking operation allows other work to continue.

```text
Start operation
      ↓
Continue other work
      ↓
Operation completes
      ↓
Handle result
```

---

# 16. JavaScript Is Synchronous by Default

JavaScript normally executes statements one at a time.

```js
console.log(1);
console.log(2);
console.log(3);
```

This is synchronous.

Asynchronous behavior comes from language features and runtime APIs such as:

```text
Timers
Promises
Fetch
DOM events
Node.js APIs
```

---

# 17. Asynchronous Programming Tools

JavaScript provides several ways to handle asynchronous operations.

### Callbacks

```js
setTimeout(() => {
  console.log("Done");
}, 1000);
```

### Promises

```js
fetch("/api/users")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

### Async/Await

```js
async function loadUsers() {
  const response = await fetch("/api/users");
  const data = await response.json();

  console.log(data);
}
```

These approaches are covered in more detail later.

---

# 18. Callback Example

A callback is a function that is executed later by some operation.

```js
function processOrder(callback) {
  setTimeout(() => {
    console.log("Order processed");
    callback();
  }, 1000);
}

processOrder(() => {
  console.log("Send confirmation");
});
```

Output:

```text
Order processed
Send confirmation
```

The callback runs after the asynchronous operation completes.

---

# 19. Promise Example

Promises represent a future result.

```js
const order = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Order completed");
  }, 1000);
});

order.then((message) => {
  console.log(message);
});
```

After the operation completes:

```text
Promise
   ↓
fulfilled
   ↓
.then()
```

---

# 20. Async/Await Example

`async` and `await` make asynchronous code easier to read.

```js
function createOrder() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Order created");
    }, 1000);
  });
}

async function process() {
  console.log("Starting");

  const result = await createOrder();

  console.log(result);
  console.log("Finished");
}

process();
```

Output:

```text
Starting
Order created
Finished
```

The function waits for the Promise at the `await` expression, while the JavaScript runtime can continue handling other work.

---

# 21. Synchronous Code Around `await`

Consider:

```js
async function example() {
  console.log("A");

  await Promise.resolve();

  console.log("B");
}

console.log("C");

example();

console.log("D");
```

Output:

```text
C
A
D
B
```

Why?

```text
C
 ↓
example()
 ↓
A
 ↓
await
 ↓
function pauses
 ↓
D
 ↓
Promise continuation
 ↓
B
```

This is related to the **microtask queue**, which is covered in the Event Loop section.

---

# 22. User Interface Example

Suppose a button sends a request:

```js
button.addEventListener("click", async () => {
  const response = await fetch("/api/orders");
  const orders = await response.json();

  console.log(orders);
});
```

The browser can continue handling other events while the network request is pending.

This is important for responsive web applications.

---

# 23. Asynchronous JavaScript in Node.js

Node.js heavily uses asynchronous APIs.

For example:

```js
import fs from "node:fs/promises";

async function readFile() {
  const data = await fs.readFile(
    "data.txt",
    "utf8"
  );

  console.log(data);
}

readFile();
```

The file operation is asynchronous.

This allows Node.js applications to handle other work while waiting for I/O.

---

# 24. CPU-Heavy Work Is Different

Asynchronous APIs are especially useful for I/O operations.

But a large CPU-intensive JavaScript loop can still block the main JavaScript thread.

For example:

```js
for (let i = 0; i < 10_000_000_000; i++) {
  // Heavy computation
}
```

Simply wrapping this in:

```js
setTimeout(() => {
  // heavy computation
}, 0);
```

does not make the computation itself non-blocking once it starts executing.

For CPU-heavy work, techniques such as **Web Workers** in browsers or **Worker Threads** in Node.js may be appropriate.

---

# 25. `setTimeout(..., 0)` Is Still Asynchronous

Consider:

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

Even with `0` milliseconds, the callback does not execute immediately.

It is scheduled to run later.

---

# 26. A Simple Execution Model

A simplified view is:

```text
JavaScript Code
      │
      ↓
   Call Stack
      │
      ↓
Runtime APIs
      │
      ↓
Queues
      │
      ↓
 Event Loop
      │
      ↓
   Call Stack
```

For example:

```js
setTimeout(() => {
  console.log("Done");
}, 1000);
```

Conceptually:

```text
setTimeout()
    ↓
Timer handled by runtime
    ↓
Timer completes
    ↓
Callback waits in queue
    ↓
Event loop checks stack
    ↓
Callback enters stack
    ↓
"Done"
```

The exact queues involved depend on the type of asynchronous operation and runtime.

---

# 27. Synchronous vs Asynchronous Example

### Synchronous

```js
function taskOne() {
  console.log("Task 1");
}

function taskTwo() {
  console.log("Task 2");
}

taskOne();
taskTwo();
```

Output:

```text
Task 1
Task 2
```

### Asynchronous

```js
function taskOne() {
  setTimeout(() => {
    console.log("Task 1");
  }, 1000);
}

function taskTwo() {
  console.log("Task 2");
}

taskOne();
taskTwo();
```

Output:

```text
Task 2
Task 1
```

Because `taskOne()` schedules asynchronous work.

---

# 28. Important Difference

Do not think:

```text
Asynchronous = faster
```

That is not always true.

Asynchronous programming mainly means:

```text
Do not unnecessarily block while waiting
```

The actual operation can still take:

```text
100 ms
1 second
10 seconds
```

The benefit is that other work can continue while waiting.

---

# 29. Common Asynchronous Operations

### Browser

```text
fetch()
setTimeout()
setInterval()
DOM events
Web APIs
```

### Node.js

```text
File system
HTTP requests
Database operations
Timers
Streams
Network operations
```

---

# 30. Synchronous vs Asynchronous in a Web Application

Consider a food ordering application.

A customer clicks:

```text
Place Order
```

The frontend sends:

```text
POST /api/orders
```

The server may:

```text
1. Validate session
2. Validate food items
3. Save order to MongoDB
4. Return response
```

The database operation takes time.

An asynchronous flow allows the server to handle other requests while waiting for the database.

```text
Customer
   │
   ↓
POST /orders
   │
   ↓
Backend
   │
   ↓
MongoDB ──────────┐
   │              │
   │          Other requests
   │              │
   └──── Result ──┘
          ↓
       Response
```

This is one reason asynchronous programming is fundamental to Node.js backend development.

---

# 31. Key Takeaways

* **Synchronous** code runs one operation at a time and waits for each operation to finish.
* **Asynchronous** operations can complete later while other JavaScript work continues.
* Synchronous CPU-heavy code can block execution.
* Asynchronous does not automatically mean parallel execution.
* `setTimeout()` schedules a callback for later.
* A timeout delay is a minimum delay before the callback becomes eligible to run.
* Network, file, and database operations are common asynchronous operations.
* Callbacks, Promises, and `async/await` are common ways to handle asynchronous results.
* `await` pauses the async function's continuation, not the entire JavaScript runtime.
* `setTimeout(..., 0)` still runs later.
* The Event Loop coordinates when queued asynchronous work can run.
* CPU-heavy JavaScript can still block the main thread.
* Understanding asynchronous JavaScript is important for React and Node.js development.

## Simple Mental Model

```text
Synchronous

Task A
  ↓
Task B
  ↓
Task C
  ↓
Task D
```

```text
Asynchronous

Start Task A ──────────┐
                       │
Continue Task B        │
                       │
Continue Task C        │
                       │
Task A finishes ───────┘
         ↓
     Handle result
```

## Learning Flow

```text
Synchronous
     ↓
Asynchronous
     ↓
Callbacks
     ↓
Promises
     ↓
async / await
     ↓
Event Loop
```

