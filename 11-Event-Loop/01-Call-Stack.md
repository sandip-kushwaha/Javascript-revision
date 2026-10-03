# JavaScript Call Stack

## What is the Call Stack?

The **Call Stack** is a mechanism used by the JavaScript engine to keep track of function execution.

JavaScript uses the call stack to know:

* which function is currently running
* which function called another function
* where execution should return after a function finishes

JavaScript executes synchronous code using the call stack.

---

# 1. Simple Example

```js
function greet() {
  console.log("Hello");
}

greet();
```

Execution:

```text
Global Code
    ↓
greet()
    ↓
console.log()
```

After `greet()` finishes, it is removed from the stack.

---

# 2. Stack Works with LIFO

The call stack follows:

**LIFO = Last In, First Out**

Example:

```text
Function A
Function B
Function C
```

If `C` was added last, it finishes first.

```text
Push A
   ↓
Push B
   ↓
Push C
   ↓
Pop C
   ↓
Pop B
   ↓
Pop A
```

This is similar to a stack of plates.

---

# 3. Push and Pop

When a function starts executing, it is added to the stack.

This is called **push**.

When the function finishes, it is removed.

This is called **pop**.

```text
Function called
      ↓
   Push Stack
      ↓
 Function runs
      ↓
   Pop Stack
      ↓
Continue execution
```

---

# 4. Example with Multiple Functions

```js
function first() {
  console.log("First");
}

function second() {
  console.log("Second");
}

first();
second();
```

Execution:

```text
Global
  ↓
first()
  ↓
console.log()
  ↓
first() finishes
  ↓
second()
  ↓
console.log()
  ↓
second() finishes
```

---

# 5. Nested Function Calls

Consider:

```js
function first() {
  second();
}

function second() {
  third();
}

function third() {
  console.log("Hello");
}

first();
```

The stack changes like this:

### Step 1

```text
Global
```

### Step 2

`first()` is called:

```text
first()
Global
```

### Step 3

Inside `first()`, `second()` is called:

```text
second()
first()
Global
```

### Step 4

Inside `second()`, `third()` is called:

```text
third()
second()
first()
Global
```

### Step 5

`third()` finishes:

```text
second()
first()
Global
```

### Step 6

`second()` finishes:

```text
first()
Global
```

### Step 7

`first()` finishes:

```text
Global
```

---

# 6. Stack Frame

Every function execution creates an execution context that is tracked by the JavaScript engine.

For a simple mental model, think of each function call as a **stack frame**.

Example:

```js
function add(a, b) {
  return a + b;
}

const result = add(10, 20);
```

When `add()` runs, its execution information is placed on the call stack.

```text
┌──────────────────┐
│ add(10, 20)      │
├──────────────────┤
│ Global Execution │
└──────────────────┘
```

After `add()` returns:

```text
┌──────────────────┐
│ Global Execution │
└──────────────────┘
```

---

# 7. Return from a Function

Example:

```js
function calculate() {
  return 10 + 20;
}

const result = calculate();

console.log(result);
```

Execution:

```text
calculate()
    ↓
10 + 20
    ↓
return 30
    ↓
calculate() removed
    ↓
result = 30
```

The returned value is given back to the calling code.

---

# 8. Function Calls Are Synchronous

Consider:

```js
console.log("A");

function show() {
  console.log("B");
}

show();

console.log("C");
```

Output:

```text
A
B
C
```

JavaScript completes the current synchronous operation before moving to the next one.

---

# 9. Call Stack and `console.log()`

Example:

```js
function greet() {
  console.log("Hello");
}

greet();
```

Conceptually:

```text
Global
  ↓
greet()
  ↓
console.log()
  ↓
console.log() finishes
  ↓
greet() finishes
  ↓
Global continues
```

The stack manages the execution order.

---

# 10. Call Stack with Return Values

```js
function multiply(a, b) {
  return a * b;
}

function calculate() {
  return multiply(5, 4);
}

const result = calculate();
```

Stack:

```text
multiply(5, 4)
calculate()
Global
```

Then:

```text
multiply() returns 20
        ↓
calculate() returns 20
        ↓
result = 20
```

---

# 11. Call Stack and Errors

Errors can also involve the call stack.

Example:

```js
function first() {
  second();
}

function second() {
  throw new Error("Something went wrong");
}

first();
```

The error occurs inside `second()`.

The stack can show the path:

```text
second()
called by first()
called by global code
```

This information is commonly visible in an error's stack trace.

---

# 12. Stack Trace

Example:

```js
function first() {
  second();
}

function second() {
  throw new Error("Database failed");
}

first();
```

A stack trace may conceptually look like:

```text
Error: Database failed
    at second (...)
    at first (...)
    at ...
```

The stack trace helps developers understand where an error originated and how execution reached that point.

---

# 13. Call Stack and Recursion

A function that calls itself creates additional stack frames.

Example:

```js
function count(number) {
  if (number === 0) {
    return;
  }

  console.log(number);

  count(number - 1);
}

count(3);
```

Stack grows:

```text
count(3)
count(2)
count(1)
count(0)
```

Then the calls return:

```text
count(0) returns
count(1) returns
count(2) returns
count(3) returns
```

---

# 14. Stack Overflow

If too many function calls are placed on the call stack, the stack can become full.

This is called a **stack overflow**.

Example:

```js
function forever() {
  forever();
}

forever();
```

There is no stopping condition.

The stack continues growing:

```text
forever()
forever()
forever()
forever()
...
```

Eventually JavaScript throws an error such as:

```text
RangeError: Maximum call stack size exceeded
```

---

# 15. Avoiding Stack Overflow

Recursive functions should have a proper stopping condition.

Bad:

```js
function count(number) {
  console.log(number);

  count(number + 1);
}
```

Better:

```js
function count(number) {
  if (number > 5) {
    return;
  }

  console.log(number);

  count(number + 1);
}

count(1);
```

Now the recursion eventually stops.

---

# 16. Call Stack Is Not the Heap

The **call stack** and **heap** have different purposes.

### Call Stack

Tracks function execution.

```text
Function calls
Execution contexts
Return points
```

### Heap

Stores dynamically allocated objects and other data managed by the JavaScript runtime.

```text
Objects
Arrays
Functions
Other allocated data
```

Simplified:

```text
JavaScript Runtime
│
├── Call Stack
│   └── Function execution
│
└── Heap
    └── Objects and allocated data
```

---

# 17. Example: Stack and Heap

```js
const user = {
  name: "Sandip",
  age: 22
};

function greet() {
  console.log(user.name);
}

greet();
```

A simplified mental model:

```text
Call Stack
┌─────────────────┐
│ greet()         │
├─────────────────┤
│ Global          │
└─────────────────┘

Heap
┌─────────────────┐
│ user object     │
│ name: "Sandip"  │
│ age: 22         │
└─────────────────┘
```

The exact internal memory implementation depends on the JavaScript engine, but this model is useful for understanding execution.

---

# 18. Synchronous Code and the Call Stack

Consider:

```js
console.log("Start");

function processData() {
  console.log("Processing");
}

processData();

console.log("End");
```

Execution order:

```text
"Start"
   ↓
processData()
   ↓
"Processing"
   ↓
"End"
```

The current synchronous code runs through the call stack.

---

# 19. Long-Running Code Blocks the Stack

Consider:

```js
function heavyTask() {
  for (let i = 0; i < 1000000000; i++) {
    // heavy work
  }
}

heavyTask();

console.log("Done");
```

While `heavyTask()` is executing, the main JavaScript execution cannot continue to the next synchronous statement.

```text
heavyTask()
    │
    │ running
    │
    ↓
console.log("Done")
```

This is why CPU-heavy JavaScript can make a webpage feel unresponsive.

---

# 20. Call Stack and Asynchronous JavaScript

Consider:

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

Even though the timer uses `0` milliseconds, its callback does not execute immediately on the call stack.

A simplified flow is:

```text
Call Stack
    ↓
setTimeout()
    ↓
Timer handled by runtime
    ↓
Call Stack continues
    ↓
"End"
    ↓
Callback becomes eligible
    ↓
Event Loop
    ↓
Call Stack
    ↓
"Timer"
```

The **Event Loop** coordinates when asynchronous callbacks can return to the call stack.

---

# 21. Call Stack and Promises

Example:

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

The Promise callback is not executed in the middle of the current synchronous stack.

It is handled later through the microtask mechanism.

---

# 22. Call Stack and `async/await`

Example:

```js
async function loadData() {
  const result = await getData();

  console.log(result);
}
```

When execution reaches `await`, the async function can pause while waiting for the Promise.

Other JavaScript work can continue.

Conceptually:

```text
loadData()
    ↓
await Promise
    ↓
async function pauses
    ↓
other work can execute
    ↓
Promise settles
    ↓
async function continues
```

The call stack does not remain occupied waiting synchronously for the Promise.

---

# 23. Empty Call Stack

For asynchronous callbacks to execute, the call stack needs to be available.

Simplified:

```text
Current synchronous work
        ↓
Call Stack becomes empty
        ↓
Event Loop checks queues
        ↓
Eligible callback selected
        ↓
Callback pushed onto Call Stack
        ↓
Callback executes
```

This relationship becomes important when learning the Event Loop.

---

# 24. Call Stack Visualization

A useful simplified model:

```text
             JavaScript Runtime
                    │
                    ↓
              ┌───────────┐
              │ Call Stack│
              └─────┬─────┘
                    │
              Function calls
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
      Synchronous          Return
       execution           values
```

For asynchronous operations:

```text
                 JavaScript Runtime
                        │
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
   Call Stack         Web APIs       Queues
        │               │               │
        │               │               │
        └───────────────┴───────┬───────┘
                                ↓
                           Event Loop
```

The detailed interaction between these parts will be covered in the next Event Loop topics.

---

# 25. Key Takeaways

* The **Call Stack** tracks function execution.
* It follows **LIFO — Last In, First Out**.
* Function calls are pushed onto the stack.
* Completed functions are popped from the stack.
* Nested functions create multiple stack frames.
* Return values go back to the calling code.
* Recursive functions can grow the call stack.
* Missing recursion termination can cause stack overflow.
* Stack traces show useful information about error execution paths.
* The call stack is different from the heap.
* Long-running synchronous code can block JavaScript execution.
* Asynchronous callbacks do not execute immediately when scheduled.
* Promises and timers continue through the runtime's asynchronous mechanisms.
* The Event Loop helps move eligible asynchronous work back to the call stack.

## Simple Mental Model

```text
Function called
      ↓
Push onto Call Stack
      ↓
Function executes
      ↓
Function returns
      ↓
Pop from Call Stack
      ↓
Next work executes
```
