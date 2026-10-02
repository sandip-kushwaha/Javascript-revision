# JavaScript Callbacks

A **callback function** is a function that is passed as an argument to another function and is called later by that function.

Callbacks are one of the most important concepts in JavaScript because they are used in:

* Array methods
* Event handling
* Timers
* Asynchronous programming
* Promises
* API requests
* Node.js
* React

---

# 1. What Is a Callback?

A callback is simply a function passed to another function.

```javascript
function greet() {
    console.log("Hello Sandip");
}

function execute(callback) {
    callback();
}

execute(greet);
```

Output:

```text
Hello Sandip
```

Here:

```text
greet       → callback function
execute     → function receiving the callback
callback()  → calls the function
```

---

# 2. Basic Callback Syntax

```javascript
function mainFunction(callback) {
    callback();
}

function callbackFunction() {
    console.log("Callback executed");
}

mainFunction(callbackFunction);
```

Flow:

```text
callbackFunction
       ↓
passed to mainFunction
       ↓
mainFunction calls callback()
       ↓
Callback executed
```

---

# 3. Passing a Function

When passing a function as a callback, don't call it immediately.

Correct:

```javascript
execute(greet);
```

Incorrect:

```javascript
execute(greet());
```

Why?

```javascript
execute(greet);
```

means:

> Give the `greet` function to `execute`.

While:

```javascript
execute(greet());
```

means:

> Execute `greet` first and pass its return value to `execute`.

---

# 4. Callback with Parameters

A callback can receive data.

```javascript
function processUser(name, callback) {
    callback(name);
}

function showUser(name) {
    console.log(`User: ${name}`);
}

processUser("Sandip", showUser);
```

Output:

```text
User: Sandip
```

Flow:

```text
"Sandip"
    ↓
processUser()
    ↓
callback(name)
    ↓
showUser("Sandip")
```

---

# 5. Callback Using an Arrow Function

Callbacks are often written as arrow functions.

```javascript
function processUser(name, callback) {
    callback(name);
}

processUser("Sandip", (name) => {
    console.log(`Hello ${name}`);
});
```

Output:

```text
Hello Sandip
```

Short version:

```javascript
processUser("Sandip", name => {
    console.log(`Hello ${name}`);
});
```

---

# 6. Anonymous Callback

A callback does not always need a separate function name.

```javascript
function execute(callback) {
    callback();
}

execute(function () {
    console.log("Hello");
});
```

Using an arrow function:

```javascript
execute(() => {
    console.log("Hello");
});
```

This is called an **anonymous function** because it has no function name.

---

# 7. Callback with Multiple Parameters

```javascript
function calculate(a, b, callback) {
    const result = a + b;

    callback(result);
}

function displayResult(result) {
    console.log(`Result: ${result}`);
}

calculate(10, 20, displayResult);
```

Output:

```text
Result: 30
```

---

# 8. Callback Can Return a Value

A callback can return a value.

```javascript
function calculate(a, b, callback) {
    return callback(a, b);
}

function add(x, y) {
    return x + y;
}

const result = calculate(10, 20, add);

console.log(result);
```

Output:

```text
30
```

Here:

```text
calculate()
     ↓
add(10, 20)
     ↓
30
     ↓
return 30
```

---

# 9. Callback with Different Operations

The same function can perform different operations depending on the callback.

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

function add(a, b) {
    return a + b;
}

function multiply(a, b) {
    return a * b;
}

console.log(calculate(10, 20, add));
console.log(calculate(10, 20, multiply));
```

Output:

```text
30
200
```

The main function doesn't need to know how the calculation works.

It delegates the operation to the callback.

---

# 10. Callback with Arrow Functions

The previous example can be shorter:

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

console.log(
    calculate(10, 20, (a, b) => a + b)
);

console.log(
    calculate(10, 20, (a, b) => a * b)
);
```

Output:

```text
30
200
```

---

# 11. Callbacks in `forEach()`

One of the most common uses of callbacks is array methods.

```javascript
const numbers = [10, 20, 30];

numbers.forEach(function (number) {
    console.log(number);
});
```

Output:

```text
10
20
30
```

The function passed to `forEach()` is a callback.

---

# 12. `forEach()` with Arrow Function

```javascript
const numbers = [10, 20, 30];

numbers.forEach(number => {
    console.log(number);
});
```

Short form:

```javascript
numbers.forEach(number => console.log(number));
```

---

# 13. Callback Parameters in `forEach()`

`forEach()` can provide:

1. Current value
2. Index
3. Entire array

Example:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits.forEach((fruit, index, array) => {
    console.log(fruit);
    console.log(index);
    console.log(array);
});
```

The callback receives:

```text
fruit → current element
index → current index
array → original array
```

---

# 14. Callbacks in `map()`

`map()` also receives a callback.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => {
    return number * 2;
});

console.log(doubled);
```

Output:

```text
[2, 4, 6]
```

Here:

```javascript
number => number * 2
```

is the callback.

---

# 15. Callbacks in `filter()`

```javascript
const numbers = [1, 2, 3, 4, 5];

const evenNumbers = numbers.filter(number => {
    return number % 2 === 0;
});

console.log(evenNumbers);
```

Output:

```text
[2, 4]
```

The callback determines whether each element should remain in the result.

---

# 16. Callbacks in `find()`

```javascript
const users = [
    { name: "Sandip", age: 22 },
    { name: "Ram", age: 25 }
];

const user = users.find(user => {
    return user.name === "Ram";
});

console.log(user);
```

Result:

```javascript
{
    name: "Ram",
    age: 25
}
```

---

# 17. Callbacks in `reduce()`

```javascript
const numbers = [10, 20, 30];

const total = numbers.reduce(
    (sum, number) => {
        return sum + number;
    },
    0
);

console.log(total);
```

Output:

```text
60
```

The callback is executed for each element.

---

# 18. Callback with `setTimeout()`

Callbacks are also used with timers.

```javascript
setTimeout(() => {
    console.log("Hello after 2 seconds");
}, 2000);
```

The arrow function is a callback.

The browser or Node.js executes it after the timer finishes.

---

# 19. Synchronous Callback

A callback can execute immediately.

```javascript
function execute(callback) {
    console.log("Before callback");

    callback();

    console.log("After callback");
}

execute(() => {
    console.log("Inside callback");
});
```

Output:

```text
Before callback
Inside callback
After callback
```

The callback is executed synchronously.

---

# 20. Asynchronous Callback

A callback can also execute later.

```javascript
console.log("Start");

setTimeout(() => {
    console.log("Callback executed");
}, 1000);

console.log("End");
```

Output:

```text
Start
End
Callback executed
```

The timer callback executes later.

This is an example of asynchronous JavaScript.

---

# 21. Callback in Event Handling

Browser events commonly use callbacks.

```javascript
const button = document.querySelector("#button");

button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

The function:

```javascript
() => {
    console.log("Button clicked");
}
```

is a callback.

The browser calls it when the button is clicked.

---

# 22. Callback with Event Object

Event callbacks can receive an event object.

```javascript
button.addEventListener("click", (event) => {
    console.log(event);
});
```

The browser passes the event object to the callback.

You can use:

```javascript
button.addEventListener("click", event => {
    console.log(event.target);
});
```

---

# 23. Callback with Node.js

Callbacks are heavily used in Node.js APIs.

For example, file operations can use callbacks.

```javascript
const fs = require("fs");

fs.readFile("data.txt", "utf8", (error, data) => {
    if (error) {
        console.error(error);
        return;
    }

    console.log(data);
});
```

The function:

```javascript
(error, data) => {
    // ...
}
```

is a callback.

---

# 24. Error-First Callback Pattern

Node.js traditionally uses an **error-first callback** pattern.

```javascript
function callback(error, data) {
    if (error) {
        // handle error
        return;
    }

    // use data
}
```

Example:

```javascript
fs.readFile(
    "data.txt",
    "utf8",
    (error, data) => {
        if (error) {
            console.error(error);
            return;
        }

        console.log(data);
    }
);
```

The common convention is:

```text
callback(error, result)
```

If an error occurs, the error contains information about the failure.

---

# 25. Callback Hell

When many asynchronous callbacks are nested inside each other, the code can become difficult to read.

Example:

```javascript
getUser(userId, (user) => {
    getOrders(user.id, (orders) => {
        getPayment(orders[0].id, (payment) => {
            getReceipt(payment.id, (receipt) => {
                console.log(receipt);
            });
        });
    });
});
```

This style is commonly called **callback hell**.

It can produce deeply nested code.

---

# 26. Why Callback Hell Is a Problem

Deep callback nesting can make code:

* Harder to read
* Harder to maintain
* Harder to debug
* Difficult to handle errors
* Difficult to modify

Modern JavaScript often uses **Promises** and **async/await** to handle complex asynchronous operations more clearly.

---

# 27. Callbacks and Promises

Callback style:

```javascript
getUser(id, user => {
    getOrders(user.id, orders => {
        console.log(orders);
    });
});
```

Promise style:

```javascript
getUser(id)
    .then(user => getOrders(user.id))
    .then(orders => {
        console.log(orders);
    });
```

Async/await style:

```javascript
async function loadOrders(id) {
    const user = await getUser(id);
    const orders = await getOrders(user.id);

    console.log(orders);
}
```

The underlying idea is still:

```text
Do something
    ↓
Wait for result
    ↓
Do something with result
```

---

# 28. Callback Function vs Function Call

These two are different:

### Passing a callback

```javascript
execute(greet);
```

### Calling the function immediately

```javascript
execute(greet());
```

Remember:

```text
greet
   ↓
function reference

greet()
   ↓
function execution
```

---

# 29. Callback Reference

You can store a function in a variable.

```javascript
function greet() {
    console.log("Hello");
}

const callback = greet;

callback();
```

Output:

```text
Hello
```

Then pass it:

```javascript
function execute(callback) {
    callback();
}

execute(callback);
```

---

# 30. Callback Can Be Stored in an Object

Functions are values in JavaScript.

```javascript
const actions = {
    greet: () => {
        console.log("Hello");
    },

    goodbye: () => {
        console.log("Goodbye");
    }
};

function execute(action) {
    action();
}

execute(actions.greet);
```

Output:

```text
Hello
```

---

# 31. Practical Example — Hotel Order Processing

Suppose a hotel system processes an order and then performs another operation.

```javascript
function processOrder(order, callback) {
    console.log(`Processing order: ${order.id}`);

    callback(order);
}

function confirmOrder(order) {
    console.log(`Order ${order.id} confirmed`);
}

const order = {
    id: "ORD-101",
    table: "T-03"
};

processOrder(order, confirmOrder);
```

Output:

```text
Processing order: ORD-101
Order ORD-101 confirmed
```

---

# 32. Practical Example — Order Status

```javascript
function updateOrderStatus(order, callback) {
    order.status = "ready";

    callback(order);
}

updateOrderStatus(
    { id: "ORD-101", status: "preparing" },
    order => {
        console.log(order);
    }
);
```

Result:

```javascript
{
    id: "ORD-101",
    status: "ready"
}
```

---

# 33. Practical Example — User Validation

```javascript
function validateUser(user, callback) {
    const isValid =
        user.name &&
        user.email;

    callback(isValid);
}

validateUser(
    {
        name: "Sandip",
        email: "sandip@example.com"
    },
    isValid => {
        console.log(
            isValid ? "Valid user" : "Invalid user"
        );
    }
);
```

Output:

```text
Valid user
```

---

# 34. Practical Example — Custom Filter Function

You can build your own function that accepts a callback.

```javascript
function filterNumbers(numbers, condition) {
    const result = [];

    for (const number of numbers) {
        if (condition(number)) {
            result.push(number);
        }
    }

    return result;
}

const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = filterNumbers(
    numbers,
    number => number % 2 === 0
);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

This is similar to how JavaScript's built-in `filter()` works.

---

# 35. Practical Example — Custom Map Function

```javascript
function transformNumbers(numbers, transform) {
    const result = [];

    for (const number of numbers) {
        result.push(transform(number));
    }

    return result;
}

const numbers = [1, 2, 3];

const doubled = transformNumbers(
    numbers,
    number => number * 2
);

console.log(doubled);
```

Output:

```text
[2, 4, 6]
```

The callback defines how each value should be transformed.

---

# 36. Callback with Multiple Callbacks

A function can receive multiple callbacks.

```javascript
function process(
    successCallback,
    errorCallback
) {
    const success = true;

    if (success) {
        successCallback();
    } else {
        errorCallback();
    }
}

process(
    () => {
        console.log("Success");
    },
    () => {
        console.log("Error");
    }
);
```

Output:

```text
Success
```

This pattern was common in older asynchronous JavaScript code.

Promises provide another way to represent success and failure.

---

# 37. Callback Execution Order

Consider:

```javascript
function execute(callback) {
    console.log("A");

    callback();

    console.log("C");
}

execute(() => {
    console.log("B");
});
```

Output:

```text
A
B
C
```

The callback executes wherever the main function calls it.

---

# 38. Callback Doesn't Always Mean Asynchronous

This is important.

A callback can be synchronous:

```javascript
[1, 2, 3].forEach(number => {
    console.log(number);
});
```

It can also be asynchronous:

```javascript
setTimeout(() => {
    console.log("Later");
}, 1000);
```

Therefore:

```text
Callback ≠ automatically asynchronous
```

A callback simply means:

> A function passed to another function to be invoked by it.

---

# 39. Callback vs Regular Function

A function itself is not inherently a callback.

For example:

```javascript
function greet() {
    console.log("Hello");
}
```

At this point, `greet` is simply a function.

When passed to another function:

```javascript
execute(greet);
```

it is being used as a **callback**.

So "callback" describes the **role of the function**, not a special type of function.

---

# 40. Common Mistakes

### Mistake 1: Calling the callback too early

Wrong:

```javascript
execute(greet());
```

Correct:

```javascript
execute(greet);
```

---

### Mistake 2: Forgetting to call the callback

```javascript
function execute(callback) {
    console.log("Running...");
}
```

The callback is received but never executed.

If you want to execute it:

```javascript
function execute(callback) {
    console.log("Running...");
    callback();
}
```

---

### Mistake 3: Assuming every callback is asynchronous

```javascript
[1, 2, 3].forEach(number => {
    console.log(number);
});
```

This callback executes synchronously.

---

### Mistake 4: Creating unnecessary nested callbacks

Deep nesting:

```javascript
first(() => {
    second(() => {
        third(() => {
            fourth(() => {
                // ...
            });
        });
    });
});
```

For complex asynchronous flows, Promises and `async/await` are usually easier to maintain.

---

### Mistake 5: Not handling errors in callback-based APIs

For Node.js error-first callbacks:

```javascript
fs.readFile(
    "data.txt",
    "utf8",
    (error, data) => {
        if (error) {
            console.error(error);
            return;
        }

        console.log(data);
    }
);
```

Always check the error when the API follows this convention.

---

# 41. Best Practices

### 1. Use descriptive callback names

Instead of:

```javascript
function process(x, cb) {
}
```

Prefer:

```javascript
function processUser(user, onComplete) {
}
```

### 2. Keep callbacks small

```javascript
numbers.map(number => number * 2);
```

is easier to understand than a huge callback containing unrelated logic.

### 3. Avoid unnecessary nesting

Use Promises or `async/await` for complex asynchronous flows.

### 4. Handle errors

Especially with callback-based Node.js APIs.

### 5. Don't accidentally invoke the callback while passing it

Use:

```javascript
execute(greet);
```

not:

```javascript
execute(greet());
```

### 6. Remember that callbacks can be synchronous or asynchronous

Don't assume timing based only on the fact that a callback is being used.

---

# 42. Callback Flow

A simple callback flow looks like this:

```text
Main Function
      ↓
Receives Callback
      ↓
Does Some Work
      ↓
Calls Callback
      ↓
Callback Executes
```

Example:

```javascript
function process(data, callback) {
    const result = data * 2;

    callback(result);
}

process(10, result => {
    console.log(result);
});
```

Flow:

```text
10
 ↓
process()
 ↓
10 × 2
 ↓
20
 ↓
callback(20)
 ↓
console.log(20)
```

---

# 43. Quick Revision

```text
Callback
   ↓
Function passed to another function
   ↓
Called by the receiving function
```

Basic example:

```javascript
function execute(callback) {
    callback();
}

execute(() => {
    console.log("Hello");
});
```

### Callback with data

```javascript
function process(value, callback) {
    callback(value * 2);
}

process(10, result => {
    console.log(result);
});
```

### Array callback

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(
    number => number * 2
);
```

### Asynchronous callback

```javascript
setTimeout(() => {
    console.log("Later");
}, 1000);
```

### Important

```text
Callback ≠ necessarily asynchronous
```

---

# Key Takeaways

* A callback is a function passed to another function.
* The receiving function decides when to execute the callback.
* Callbacks can receive parameters.
* Callbacks can return values.
* Array methods such as `forEach()`, `map()`, `filter()`, `find()`, and `reduce()` use callbacks.
* Event listeners use callbacks.
* Timers use callbacks.
* Node.js APIs traditionally use callbacks extensively.
* Callbacks can be synchronous or asynchronous.
* Passing `greet` and calling `greet()` are different.
* Complex nested callbacks can lead to callback hell.
* Promises and `async/await` provide cleaner approaches for many asynchronous workflows.
* A callback is not a special type of function; it is a function being used in a particular role.

---
