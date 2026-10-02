# JavaScript Higher-Order Functions

A **Higher-Order Function (HOF)** is a function that does at least one of these:

1. Takes another function as an argument.
2. Returns another function as its result.

Higher-order functions are an important part of **functional programming** in JavaScript.

---

## 1. What is a Higher-Order Function?

A function is called a **higher-order function** when it works with other functions.

```javascript
function greet(name) {
    return `Hello, ${name}`;
}

function processUser(callback) {
    return callback("Sandip");
}

console.log(processUser(greet));
```

Output:

```text
Hello, Sandip
```

Here:

* `greet` is a normal function.
* `processUser` is a higher-order function.
* `greet` is passed to `processUser` as a callback.

---

# 2. Why Are Higher-Order Functions Important?

Higher-order functions help us:

* Reuse code
* Avoid repetition
* Write cleaner code
* Work with arrays easily
* Create flexible functions
* Implement functional programming
* Build reusable utilities
* Handle callbacks
* Work with asynchronous operations

They are used heavily in:

* JavaScript
* React
* Node.js
* Express.js
* Array methods
* Event handling
* Middleware

---

# 3. Functions Are First-Class Citizens

JavaScript treats functions as **first-class values**.

This means functions can be:

* Stored in variables
* Passed as arguments
* Returned from functions
* Stored inside arrays
* Stored inside objects

Example:

```javascript
function greet() {
    console.log("Hello!");
}
```

Store a function in a variable:

```javascript
const message = greet;

message();
```

Output:

```text
Hello!
```

---

# 4. Passing a Function as an Argument

A function can receive another function.

```javascript
function sayHello() {
    console.log("Hello!");
}

function execute(callback) {
    callback();
}

execute(sayHello);
```

Output:

```text
Hello!
```

Here:

```javascript
execute(sayHello);
```

passes the function itself.

Do not write:

```javascript
execute(sayHello());
```

because that calls `sayHello` immediately.

---

# 5. Function Reference vs Function Call

This is very important.

### Function reference

```javascript
execute(sayHello);
```

You are passing the function.

### Function call

```javascript
execute(sayHello());
```

You are executing the function first.

Example:

```javascript
function greet() {
    return "Hello";
}

function printMessage(callback) {
    console.log(callback());
}

printMessage(greet);
```

Output:

```text
Hello
```

---

# 6. Simple Higher-Order Function

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

function add(x, y) {
    return x + y;
}

console.log(calculate(10, 20, add));
```

Output:

```text
30
```

Here:

```javascript
calculate()
```

is a higher-order function because it accepts another function.

---

# 7. Using Arrow Functions

Higher-order functions are often written using arrow functions.

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

console.log(calculate(10, 5, (a, b) => a + b));
```

Output:

```text
15
```

Another example:

```javascript
console.log(calculate(10, 5, (a, b) => a * b));
```

Output:

```text
50
```

---

# 8. Returning a Function

A higher-order function can also **return another function**.

```javascript
function createGreeting() {
    return function () {
        console.log("Hello!");
    };
}

const greet = createGreeting();

greet();
```

Output:

```text
Hello!
```

Here:

```javascript
createGreeting()
```

returns a function.

---

# 9. Returning a Function with Parameters

```javascript
function multiplier(number) {
    return function (value) {
        return number * value;
    };
}

const double = multiplier(2);

console.log(double(5));
```

Output:

```text
10
```

Another example:

```javascript
const triple = multiplier(3);

console.log(triple(5));
```

Output:

```text
15
```

---

# 10. Higher-Order Functions and Closures

Higher-order functions often work together with **closures**.

```javascript
function multiplier(number) {
    return function (value) {
        return number * value;
    };
}

const double = multiplier(2);

console.log(double(10));
```

The returned function remembers:

```text
number = 2
```

even after `multiplier()` has finished.

This behavior is provided by a **closure**.

Closures are covered in the Advanced JavaScript section.

---

# 11. Array Higher-Order Functions

JavaScript provides many built-in higher-order functions for arrays.

Common examples:

```text
forEach()
map()
filter()
find()
findIndex()
some()
every()
reduce()
sort()
```

These methods accept functions as arguments.

---

# 12. forEach()

`forEach()` executes a callback for every array element.

```javascript
const numbers = [1, 2, 3, 4];

numbers.forEach(function (number) {
    console.log(number);
});
```

Output:

```text
1
2
3
4
```

Arrow function:

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

---

# 13. map()

`map()` creates a new array by transforming every element.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

The callback:

```javascript
number => number * 2
```

is passed to `map()`.

Therefore `map()` is a higher-order function.

---

# 14. filter()

`filter()` creates a new array containing elements that satisfy a condition.

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

---

# 15. find()

`find()` returns the first element that satisfies a condition.

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.find(number => number > 20);

console.log(result);
```

Output:

```text
30
```

---

# 16. findIndex()

`findIndex()` returns the index of the first matching element.

```javascript
const numbers = [10, 20, 30, 40];

const index = numbers.findIndex(number => number > 20);

console.log(index);
```

Output:

```text
2
```

---

# 17. some()

`some()` checks whether **at least one** element satisfies a condition.

```javascript
const numbers = [1, 3, 5, 8];

const hasEven = numbers.some(number => number % 2 === 0);

console.log(hasEven);
```

Output:

```text
true
```

---

# 18. every()

`every()` checks whether **all** elements satisfy a condition.

```javascript
const numbers = [2, 4, 6, 8];

const allEven = numbers.every(number => number % 2 === 0);

console.log(allEven);
```

Output:

```text
true
```

---

# 19. reduce()

`reduce()` processes an array and produces a single result.

```javascript
const numbers = [1, 2, 3, 4];

const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);

console.log(total);
```

Output:

```text
10
```

The callback is passed to `reduce()`.

---

# 20. sort()

`sort()` can also receive a comparison function.

```javascript
const numbers = [40, 10, 30, 20];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output:

```text
[10, 20, 30, 40]
```

The comparison function controls how the values are sorted.

---

# 21. Custom Higher-Order Function

We can create our own higher-order functions.

```javascript
function processNumbers(numbers, callback) {
    const result = [];

    for (const number of numbers) {
        result.push(callback(number));
    }

    return result;
}

const numbers = [1, 2, 3, 4];

const doubled = processNumbers(
    numbers,
    number => number * 2
);

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

---

# 22. Reusable Calculation Function

Instead of creating separate functions for every calculation:

```javascript
function add(a, b) {
    return a + b;
}

function multiply(a, b) {
    return a * b;
}
```

We can create a reusable higher-order function:

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}
```

Now:

```javascript
console.log(calculate(10, 5, add));
console.log(calculate(10, 5, multiply));
```

Output:

```text
15
50
```

This reduces repeated code.

---

# 23. Practical Example: Hotel Orders

Suppose a hotel has orders:

```javascript
const orders = [
    { item: "Pizza", price: 500 },
    { item: "Burger", price: 300 },
    { item: "Momo", price: 250 }
];
```

Calculate total price:

```javascript
const total = orders.reduce((sum, order) => {
    return sum + order.price;
}, 0);

console.log(total);
```

Output:

```text
1050
```

---

# 24. Filter Hotel Orders

Find expensive orders:

```javascript
const expensiveOrders = orders.filter(order => {
    return order.price > 300;
});

console.log(expensiveOrders);
```

Result:

```text
[
    { item: "Pizza", price: 500 }
]
```

---

# 25. Extract Food Names

Using `map()`:

```javascript
const foodNames = orders.map(order => order.item);

console.log(foodNames);
```

Output:

```text
["Pizza", "Burger", "Momo"]
```

---

# 26. Practical Example: Users

```javascript
const users = [
    { name: "Sandip", age: 22 },
    { name: "Ram", age: 17 },
    { name: "Sita", age: 25 }
];
```

Find adults:

```javascript
const adults = users.filter(user => user.age >= 18);

console.log(adults);
```

Get names:

```javascript
const names = users.map(user => user.name);

console.log(names);
```

Find a specific user:

```javascript
const user = users.find(user => user.name === "Sandip");

console.log(user);
```

---

# 27. Higher-Order Function with Multiple Callbacks

A function can accept multiple callback functions.

```javascript
function processData(data, onSuccess, onError) {
    if (data) {
        onSuccess(data);
    } else {
        onError("No data found");
    }
}
```

Usage:

```javascript
processData(
    "User Data",
    data => console.log("Success:", data),
    error => console.log("Error:", error)
);
```

Output:

```text
Success: User Data
```

---

# 28. Higher-Order Function with Conditions

```javascript
function checkNumber(number, onEven, onOdd) {
    if (number % 2 === 0) {
        onEven(number);
    } else {
        onOdd(number);
    }
}
```

Usage:

```javascript
checkNumber(
    10,
    number => console.log(`${number} is even`),
    number => console.log(`${number} is odd`)
);
```

Output:

```text
10 is even
```

---

# 29. Function Returning Another Function

Example:

```javascript
function createLogger(prefix) {
    return function (message) {
        console.log(`${prefix}: ${message}`);
    };
}

const info = createLogger("INFO");
const error = createLogger("ERROR");

info("Server started");
error("Something went wrong");
```

Output:

```text
INFO: Server started
ERROR: Something went wrong
```

This is useful for creating reusable behavior.

---

# 30. Higher-Order Function for Authorization

A simplified example:

```javascript
function requireRole(role) {
    return function (user) {
        return user.role === role;
    };
}
```

Usage:

```javascript
const isAdmin = requireRole("admin");

const user = {
    name: "Sandip",
    role: "admin"
};

console.log(isAdmin(user));
```

Output:

```text
true
```

This pattern is commonly useful in authentication and authorization systems.

---

# 31. Higher-Order Functions in React

Higher-order functions are commonly used in React applications.

For example:

```javascript
const users = [
    { name: "Sandip", active: true },
    { name: "Ram", active: false }
];

const activeUsers = users.filter(user => user.active);
```

Rendering data:

```javascript
users.map(user => (
    <div key={user.name}>
        {user.name}
    </div>
));
```

Here:

```javascript
map()
```

receives a callback function.

---

# 32. Higher-Order Functions in Node.js

Node.js APIs commonly use functions as callbacks.

Example:

```javascript
setTimeout(() => {
    console.log("Task completed");
}, 1000);
```

The arrow function is passed to:

```javascript
setTimeout()
```

Another example:

```javascript
app.get("/users", (req, res) => {
    res.json({
        message: "Users"
    });
});
```

The callback function handles the request.

---

# 33. Higher-Order Functions and Middleware

Express middleware follows the same general idea of passing functions around.

```javascript
function logger(req, res, next) {
    console.log(req.method, req.url);
    next();
}
```

Then:

```javascript
app.use(logger);
```

A function is supplied to another API.

Middleware is an important practical example of function composition and callback-based design.

---

# 34. HOF vs Callback

These concepts are related but different.

### Callback

A **callback** is a function passed to another function to be called later or during an operation.

```javascript
function greet(name, callback) {
    callback(name);
}
```

### Higher-Order Function

A **higher-order function** is a function that accepts a function and/or returns a function.

```javascript
function greet(name, callback) {
    callback(name);
}
```

In this example:

* `callback` is the callback function.
* `greet()` is a higher-order function.

---

# 35. HOF vs Normal Function

Normal function:

```javascript
function add(a, b) {
    return a + b;
}
```

It receives normal values.

Higher-order function:

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}
```

It receives a function.

---

# 36. HOF Can Return Functions

A function does not have to accept a function to be higher-order.

This is also a higher-order function:

```javascript
function createMultiplier(number) {
    return function (value) {
        return number * value;
    };
}
```

Because it returns a function.

---

# 37. HOF Can Both Accept and Return Functions

```javascript
function createProcessor(callback) {
    return function (value) {
        return callback(value);
    };
}
```

Usage:

```javascript
const double = createProcessor(number => number * 2);

console.log(double(10));
```

Output:

```text
20
```

---

# 38. Common Mistakes

## Mistake 1: Calling the callback immediately

Wrong:

```javascript
process(greet());
```

Correct:

```javascript
process(greet);
```

---

## Mistake 2: Forgetting to call the callback

Wrong:

```javascript
function process(callback) {
    console.log(callback);
}
```

Correct:

```javascript
function process(callback) {
    callback();
}
```

---

## Mistake 3: Forgetting to return

Wrong:

```javascript
function createMultiplier(number) {
    function multiply(value) {
        return number * value;
    }
}
```

There is no returned function.

Correct:

```javascript
function createMultiplier(number) {
    return function multiply(value) {
        return number * value;
    };
}
```

---

## Mistake 4: Confusing `map()` and `forEach()`

`map()` returns a new array:

```javascript
const result = numbers.map(number => number * 2);
```

`forEach()` does not create a transformed array:

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

Use:

* `map()` → transform
* `forEach()` → perform an action

---

## Mistake 5: Using `map()` when no new array is needed

Avoid:

```javascript
numbers.map(number => {
    console.log(number);
});
```

If you only need to perform an action, use:

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

---

# 39. Best Practices

### 1. Keep callbacks simple

Good:

```javascript
const doubled = numbers.map(number => number * 2);
```

Avoid unnecessarily complicated callbacks.

---

### 2. Use descriptive function names

Good:

```javascript
const activeUsers = users.filter(user => user.isActive);
```

---

### 3. Use the correct array method

| Requirement            | Method        |
| ---------------------- | ------------- |
| Perform an action      | `forEach()`   |
| Transform values       | `map()`       |
| Select matching values | `filter()`    |
| Find one value         | `find()`      |
| Find index             | `findIndex()` |
| Check at least one     | `some()`      |
| Check all              | `every()`     |
| Produce one result     | `reduce()`    |

---

### 4. Avoid unnecessary nesting

If callbacks become deeply nested, consider:

* Named functions
* Promises
* `async/await`
* Smaller reusable functions

---

### 5. Prefer reusable functions

Instead of repeating:

```javascript
numbers.map(number => number * 2);
```

in many places, you can create reusable functionality when appropriate.

---

# 40. Functional Programming Connection

Higher-order functions are a major part of **functional programming**.

Functional programming commonly focuses on:

* Functions as values
* Pure functions
* Immutability
* Function composition
* Higher-order functions
* Avoiding unnecessary side effects

Example:

```javascript
const numbers = [1, 2, 3, 4, 5];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 2);

console.log(result);
```

Output:

```text
[4, 8]
```

Here:

```text
filter()
    ↓
map()
    ↓
result
```

This is an example of composing operations.

---

# 41. Function Composition

Higher-order functions can be used to combine functions.

```javascript
const double = number => number * 2;

const square = number => number * number;

const result = square(double(5));

console.log(result);
```

Output:

```text
100
```

Because:

```text
5
↓
double → 10
↓
square → 100
```

Function composition becomes especially useful in larger applications.

---

# 42. Real-World Uses

Higher-order functions are used in:

### Frontend

```javascript
map()
filter()
find()
some()
every()
```

### React

```javascript
map()
event handlers
callbacks
higher-order components
```

### Node.js

```javascript
callbacks
middleware
event handlers
```

### Express

```javascript
app.get()
app.post()
app.use()
middleware
```

### Backend

```javascript
authorization
validation
data transformation
logging
error handling
```

---

# 43. Quick Revision

```text
Higher-Order Function
        │
        ├── Accepts a function
        │
        └── Returns a function
```

Example:

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}
```

Calling it:

```javascript
calculate(10, 5, (a, b) => a + b);
```

Result:

```text
15
```

Returning a function:

```javascript
function multiplier(x) {
    return y => x * y;
}
```

Usage:

```javascript
const double = multiplier(2);

console.log(double(5));
```

Result:

```text
10
```

---

# 44. Key Takeaways

* A higher-order function works with other functions.
* It can accept a function as an argument.
* It can return a function.
* Functions are first-class values in JavaScript.
* Callbacks are commonly used with higher-order functions.
* `map()` transforms arrays.
* `filter()` selects elements.
* `find()` finds the first matching element.
* `some()` checks whether at least one element matches.
* `every()` checks whether all elements match.
* `reduce()` produces a single result.
* `forEach()` performs an action for each element.
* Higher-order functions improve code reuse.
* They are heavily used in React, Node.js, and Express.
* Higher-order functions are an important concept in functional programming.
* Closures and higher-order functions often work together.

---
