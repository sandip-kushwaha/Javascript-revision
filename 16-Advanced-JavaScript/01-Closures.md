# JavaScript Closures

A **closure** happens when a function remembers and can access variables from its outer scope, even after the outer function has finished executing.

Closures are an important JavaScript concept used in:

* Private state
* Counters
* Callbacks
* Event handlers
* Timers
* Factory functions
* React hooks
* Data encapsulation

---

# 1. What is a Closure?

Consider:

```javascript
function outer() {
    const message = "Hello";

    function inner() {
        console.log(message);
    }

    inner();
}

outer();
```

The `inner()` function can access:

```text
message
```

from the outer function.

This relationship between the function and its surrounding variables is called a **closure**.

---

# 2. Basic Closure Example

```javascript
function outer() {
    const name = "Sandip";

    return function inner() {
        console.log(name);
    };
}

const greet = outer();

greet();
```

Output:

```text
Sandip
```

Notice:

```javascript
outer();
```

has already finished.

But `greet()` can still access:

```javascript
name
```

That is the key idea behind closures.

---

# 3. How Closure Works

Conceptually:

```text
outer()
   │
   ├── name = "Sandip"
   │
   └── returns inner()
              │
              └── remembers name
```

After:

```javascript
const greet = outer();
```

the returned function keeps access to the variables it needs from its outer lexical environment.

---

# 4. Closure with a Counter

One of the most common closure examples is a counter.

```javascript
function createCounter() {
    let count = 0;

    return function () {
        count++;

        return count;
    };
}

const counter = createCounter();

console.log(counter());
console.log(counter());
console.log(counter());
```

Output:

```text
1
2
3
```

The variable:

```javascript
count
```

is not directly accessible from outside.

But the returned function can access and modify it.

---

# 5. Private State

Closures can create private state.

```javascript
function createBankAccount(initialBalance) {
    let balance = initialBalance;

    return {
        deposit(amount) {
            balance += amount;
        },

        getBalance() {
            return balance;
        }
    };
}

const account = createBankAccount(1000);

account.deposit(500);

console.log(account.getBalance());
```

Output:

```text
1500
```

But this does not work:

```javascript
console.log(account.balance);
```

because `balance` is not a property of the returned object.

The state is protected by the closure.

---

# 6. Multiple Closures

Each call to the outer function creates a separate closure.

```javascript
function createCounter() {
    let count = 0;

    return function () {
        count++;

        return count;
    };
}

const counter1 = createCounter();
const counter2 = createCounter();

console.log(counter1());
console.log(counter1());

console.log(counter2());
console.log(counter2());
```

Output:

```text
1
2
1
2
```

Why?

Each call creates its own:

```text
count
```

variable.

Conceptually:

```text
counter1
   └── count = 2

counter2
   └── count = 2
```

They do not share the same variable.

---

# 7. Closure and Scope

Closures are closely related to lexical scope.

```javascript
const globalValue = "Global";

function outer() {
    const outerValue = "Outer";

    function inner() {
        const innerValue = "Inner";

        console.log(globalValue);
        console.log(outerValue);
        console.log(innerValue);
    }

    inner();
}

outer();
```

The inner function can access variables from:

```text
Inner scope
     ↓
Outer scope
     ↓
Global scope
```

JavaScript searches through these lexical environments when resolving variables.

---

# 8. Closure After the Outer Function Returns

This is the most important part.

```javascript
function createMessage() {
    const message = "Hello JavaScript";

    return function () {
        console.log(message);
    };
}

const showMessage = createMessage();

showMessage();
```

Execution:

```text
createMessage()
       ↓
creates message
       ↓
returns function
       ↓
createMessage() finishes
       ↓
showMessage() is called
       ↓
function still accesses message
```

The closure keeps the required lexical environment reachable.

---

# 9. Closure with Parameters

The outer function's parameters can also be captured.

```javascript
function multiplyBy(multiplier) {
    return function (number) {
        return number * multiplier;
    };
}

const double = multiplyBy(2);
const triple = multiplyBy(3);

console.log(double(5));
console.log(triple(5));
```

Output:

```text
10
15
```

Here:

```text
double → remembers multiplier = 2
triple → remembers multiplier = 3
```

This pattern is also related to **function factories** and **currying**.

---

# 10. Function Factory

A function factory creates functions with customized behavior.

```javascript
function createGreeting(greeting) {
    return function (name) {
        return `${greeting}, ${name}!`;
    };
}

const sayHello = createGreeting("Hello");
const sayWelcome = createGreeting("Welcome");

console.log(sayHello("Sandip"));
console.log(sayWelcome("Sandip"));
```

Output:

```text
Hello, Sandip!
Welcome, Sandip!
```

The returned functions remember the `greeting` value.

---

# 11. Closure with `setTimeout()`

Closures are frequently used with timers.

```javascript
function delayedMessage(message) {
    setTimeout(() => {
        console.log(message);
    }, 1000);
}

delayedMessage("Hello");
```

The callback remembers:

```javascript
message
```

from the outer function.

After the delay, the callback can still access it.

---

# 12. Closure with Event Handlers

Closures are useful when attaching event handlers.

```javascript
function setupButton(button, message) {
    button.addEventListener("click", () => {
        console.log(message);
    });
}
```

The event handler remembers:

```javascript
message
```

from `setupButton()`.

Example:

```javascript
setupButton(
    document.querySelector("#save"),
    "Data saved!"
);
```

When the button is clicked, the callback can still access the message.

---

# 13. Closure with Loops

Closures are especially important when working with loops.

Using `let`:

```javascript
for (let i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 1000);
}
```

Output:

```text
0
1
2
```

`let` creates block-scoped bindings for the loop.

---

# 14. Why `var` Behaves Differently

Consider:

```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 1000);
}
```

Output:

```text
3
3
3
```

The callbacks refer to the same function-scoped `i`.

By the time the callbacks run, the loop has completed and:

```text
i = 3
```

---

# 15. Closure with `let` vs `var`

### `let`

```text
Iteration 1 → i = 0
Iteration 2 → i = 1
Iteration 3 → i = 2
```

Each iteration gets the appropriate block-scoped binding.

### `var`

```text
One shared function-scoped i
        ↓
loop finishes
        ↓
i = 3
        ↓
callbacks read 3
```

This is one reason `let` is preferred for modern loop code.

---

# 16. Closure and Data Privacy

Closures can hide implementation details.

```javascript
function createUser() {
    let password = "secret123";

    return {
        checkPassword(value) {
            return value === password;
        }
    };
}

const user = createUser();

console.log(user.checkPassword("secret123"));
```

Output:

```text
true
```

The password is not directly exposed as:

```javascript
user.password
```

The returned method has controlled access to it.

> Closure-based privacy is a programming technique, not a replacement for secure password storage. Real passwords should never be stored in plaintext.

---

# 17. Closure with Modules

Closures can help expose only selected functionality.

```javascript
const counter = (() => {
    let count = 0;

    return {
        increment() {
            count++;
        },

        getValue() {
            return count;
        }
    };
})();
```

Use:

```javascript
counter.increment();

console.log(counter.getValue());
```

The internal `count` remains hidden from direct access.

---

# 18. Closure and React

Closures are very common in React because functions can capture values from the render in which they were created.

Example:

```jsx
function UserGreeting({ name }) {
    const handleClick = () => {
        console.log(`Hello ${name}`);
    };

    return (
        <button onClick={handleClick}>
            Greet
        </button>
    );
}
```

The `handleClick` function can access:

```javascript
name
```

from its surrounding scope.

---

# 19. Closure in React State

Closures become particularly important with asynchronous code.

For example:

```jsx
function Counter() {
    const [count, setCount] = useState(0);

    const handleClick = () => {
        setTimeout(() => {
            console.log(count);
        }, 1000);
    };

    return (
        <button onClick={handleClick}>
            Show Count
        </button>
    );
}
```

The callback captures the `count` value from the render where the callback was created.

This is why understanding closures is important when working with:

* `useState`
* `useEffect`
* event handlers
* timers
* asynchronous operations

---

# 20. Closure and `useEffect`

Example:

```jsx
useEffect(() => {
    const timer = setTimeout(() => {
        console.log(count);
    }, 1000);

    return () => {
        clearTimeout(timer);
    };
}, [count]);
```

The effect callback uses the `count` value available to that particular render.

The dependency array:

```javascript
[count]
```

allows React to run the effect again when `count` changes.

---

# 21. Closure with Array Methods

Callbacks passed to array methods can access variables from their surrounding scope.

```javascript
const minimumPrice = 500;

const products = [
    { name: "Laptop", price: 800 },
    { name: "Mouse", price: 300 },
    { name: "Keyboard", price: 600 }
];

const result = products.filter((product) => {
    return product.price >= minimumPrice;
});

console.log(result);
```

The callback closes over:

```javascript
minimumPrice
```

---

# 22. Closure with `map()`

```javascript
const taxRate = 0.13;

const prices = [100, 200, 300];

const pricesWithTax = prices.map((price) => {
    return price + price * taxRate;
});

console.log(pricesWithTax);
```

The callback remembers:

```javascript
taxRate
```

from the surrounding scope.

---

# 23. Closure and Memory

Closures keep references to variables that are still needed by the closure.

Example:

```javascript
function createHandler() {
    const data = {
        name: "Sandip"
    };

    return function () {
        console.log(data.name);
    };
}

const handler = createHandler();
```

As long as `handler` remains reachable, the closure may keep the required data reachable as well.

When the closure and its captured data are no longer reachable, the garbage collector can eventually reclaim eligible memory.

---

# 24. Closures and Memory Leaks

Closures do not automatically cause memory leaks.

A problem can occur when a long-lived object unnecessarily keeps a closure reachable.

For example:

```javascript
const handlers = [];

function createHandler() {
    const largeData = new Array(1000000).fill("data");

    return () => {
        console.log(largeData.length);
    };
}

handlers.push(createHandler());
```

As long as the handler remains in:

```javascript
handlers
```

the captured data may remain reachable.

Good practice:

* Remove unused event listeners.
* Clear unnecessary timers.
* Avoid storing unnecessary closures.
* Release references when objects are no longer needed.

---

# 25. Closure vs Global Variable

Without a closure:

```javascript
let count = 0;

function increment() {
    count++;
}
```

The variable is globally accessible from its scope.

With a closure:

```javascript
function createCounter() {
    let count = 0;

    return () => {
        count++;
        return count;
    };
}

const increment = createCounter();
```

The `count` variable is private to the closure.

---

# 26. Closure vs Class Private Field

Modern JavaScript also provides private class fields.

Closure:

```javascript
function createCounter() {
    let count = 0;

    return {
        increment() {
            count++;
        },

        getCount() {
            return count;
        }
    };
}
```

Private class field:

```javascript
class Counter {
    #count = 0;

    increment() {
        this.#count++;
    }

    getCount() {
        return this.#count;
    }
}
```

Both can encapsulate internal state, but they use different programming styles.

---

# 27. Closure and Factory Pattern

Closures can create configurable objects or functions.

```javascript
function createLogger(prefix) {
    return {
        log(message) {
            console.log(`[${prefix}] ${message}`);
        }
    };
}

const apiLogger = createLogger("API");
const dbLogger = createLogger("DB");

apiLogger.log("Request received");
dbLogger.log("Database connected");
```

Output:

```text
[API] Request received
[DB] Database connected
```

Each logger remembers its own prefix.

---

# 28. Closure Chain

Closures can exist across multiple levels of scope.

```javascript
function levelOne() {
    const a = 10;

    function levelTwo() {
        const b = 20;

        return function levelThree() {
            return a + b;
        };
    }

    return levelTwo();
}

const result = levelOne();

console.log(result());
```

Output:

```text
30
```

`levelThree()` can access:

```text
b → levelTwo scope
a → levelOne scope
```

---

# 29. Lexical Scope vs Closure

These concepts are related but not identical.

### Lexical Scope

Determines where variables can be accessed based on where code is written.

```javascript
function outer() {
    const value = 10;

    function inner() {
        console.log(value);
    }
}
```

### Closure

The function retains access to the surrounding lexical environment when it is used outside that original execution context.

```javascript
function outer() {
    const value = 10;

    return function inner() {
        console.log(value);
    };
}

const fn = outer();

fn();
```

Simple distinction:

```text
Lexical scope
    → determines variable visibility

Closure
    → allows a function to retain access
      to its surrounding lexical environment
```

---

# 30. Closure Execution Model

Consider:

```javascript
function outer() {
    let count = 0;

    return function inner() {
        count++;

        return count;
    };
}

const counter = outer();
```

Conceptually:

```text
counter
   │
   ▼
inner function
   │
   ▼
captured lexical environment
   │
   └── count = 0
```

Calling:

```javascript
counter();
```

updates the captured:

```text
count
```

to:

```text
1
```

Calling again:

```javascript
counter();
```

updates it to:

```text
2
```

---

# 31. Practical Example — Order ID Generator

Closures can maintain a private sequence.

```javascript
function createOrderIdGenerator() {
    let nextId = 1;

    return function () {
        return `ORD-${nextId++}`;
    };
}

const generateOrderId = createOrderIdGenerator();

console.log(generateOrderId());
console.log(generateOrderId());
console.log(generateOrderId());
```

Output:

```text
ORD-1
ORD-2
ORD-3
```

The counter remains private.

---

# 32. Practical Example — Permission Checker

```javascript
function createPermissionChecker(role) {
    return function (requiredRole) {
        return role === requiredRole;
    };
}

const isAdmin = createPermissionChecker("admin");

console.log(isAdmin("admin"));
console.log(isAdmin("waiter"));
```

Output:

```text
true
false
```

The returned function remembers the original role.

---

# 33. Practical Example — Configuration

```javascript
function createApiClient(baseURL) {
    return {
        get(endpoint) {
            return fetch(`${baseURL}${endpoint}`);
        }
    };
}

const api = createApiClient(
    "https://example.com/api"
);

api.get("/users");
```

The `get()` method remembers:

```javascript
baseURL
```

through a closure.

---

# 34. Important Characteristics of Closures

A closure:

* Is created when a function is defined in an outer lexical environment.
* Allows inner functions to access outer variables.
* Can retain access after the outer function returns.
* Can provide private state.
* Can create function factories.
* Is common in callbacks and event handlers.
* Is common in asynchronous JavaScript.
* Is heavily used by React code.
* Can keep captured data reachable while the closure remains reachable.

---

# 35. Common Closure Pattern

The general pattern is:

```javascript
function outer() {
    let privateValue = 0;

    return function inner() {
        privateValue++;

        return privateValue;
    };
}

const fn = outer();
```

Think:

```text
Outer function
      ↓
Private variable
      ↓
Returns inner function
      ↓
Inner function remembers variable
      ↓
Private state remains available
```

---

# 36. Closure vs Callback

These are not the same thing.

### Callback

A function passed to another function:

```javascript
setTimeout(() => {
    console.log("Done");
}, 1000);
```

### Closure

A function that retains access to variables from its surrounding lexical environment:

```javascript
function outer() {
    const message = "Hello";

    return () => {
        console.log(message);
    };
}
```

A callback **can also be a closure**, but not every callback must demonstrate meaningful captured state.

---

# 37. Closure vs Scope

```text
Scope
  ↓
Where a variable can be accessed

Closure
  ↓
Function retains access to
its surrounding lexical environment
```

Example:

```javascript
function outer() {
    const message = "Hello";

    return () => {
        console.log(message);
    };
}
```

Here:

```text
message
   ↓
outer scope
   ↓
captured by returned function
   ↓
closure
```

---

# 38. Key Takeaways

* A closure is created when a function retains access to its surrounding lexical environment.
* Closures allow inner functions to access outer variables.
* A closure can continue accessing variables after the outer function returns.
* Each call to an outer function can create an independent closure.
* Closures are useful for private state.
* Closures are commonly used with callbacks and timers.
* Event handlers frequently use closures.
* React code relies heavily on JavaScript closures.
* Function factories commonly use closures.
* Closures can help with encapsulation.
* Closures do not automatically cause memory leaks.
* Captured data can remain reachable as long as the closure remains reachable.
* `let` behaves differently from `var` in loop closure examples because of block scoping.
* Closures are based on lexical scope.

---

# Quick Cheat Sheet

```text
Closure
   ↓
Function + surrounding lexical environment

Common uses:
   ↓
Private state
Counters
Callbacks
Timers
Event handlers
Function factories
React
Encapsulation
```

Basic pattern:

```javascript
function outer() {
    let value = 0;

    return function () {
        value++;
        return value;
    };
}

const fn = outer();

fn(); // 1
fn(); // 2
fn(); // 3
```

The most important idea:

```text
The returned function remembers
the variables it needs from its outer scope.
```

---

# Next

Continue with:

```text
16-Advanced-JavaScript/
└── 02-Currying.md
```
