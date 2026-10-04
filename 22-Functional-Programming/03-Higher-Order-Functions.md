# Higher-Order Functions in JavaScript

A **Higher-Order Function (HOF)** is a function that does at least one of these:

1. Accepts another function as an argument.
2. Returns another function.

JavaScript supports Higher-Order Functions because functions are first-class values.

---

# 1. Basic Example

A function can receive another function:

```javascript
function processUser(name, callback) {
    callback(name);
}

function greet(name) {
    console.log(`Hello ${name}`);
}

processUser("Sandip", greet);
```

Here:

```text
processUser()
    ↓
accepts greet()
    ↓
calls greet()
```

`processUser()` is a Higher-Order Function.

---

# 2. Function as an Argument

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}
```

Now we can provide different operations:

```javascript
const add = (a, b) => a + b;

const multiply = (a, b) => a * b;

console.log(calculate(10, 5, add));
// 15

console.log(calculate(10, 5, multiply));
// 50
```

The `calculate()` function does not need to know how the operation works.

It simply receives a function and executes it.

---

# 3. Inline Function

Instead of creating a separate function:

```javascript
console.log(
    calculate(10, 5, (a, b) => a - b)
);
```

Output:

```text
5
```

Another example:

```javascript
console.log(
    calculate(10, 5, (a, b) => a / b)
);
```

Output:

```text
2
```

---

# 4. Function Returning a Function

A Higher-Order Function can also return another function.

```javascript
function createGreeting(message) {
    return function(name) {
        return `${message}, ${name}!`;
    };
}
```

Create specialized functions:

```javascript
const sayHello = createGreeting("Hello");

console.log(sayHello("Sandip"));
```

Output:

```text
Hello, Sandip!
```

Another:

```javascript
const sayWelcome = createGreeting("Welcome");

console.log(sayWelcome("Sandip"));
```

Output:

```text
Welcome, Sandip!
```

---

# 5. Why Return Functions?

Returning functions allows us to create reusable behavior.

```javascript
function multiplyBy(number) {
    return function(value) {
        return value * number;
    };
}

const double = multiplyBy(2);
const triple = multiplyBy(3);

console.log(double(5));
// 10

console.log(triple(5));
// 15
```

The same logic can create different functions.

---

# 6. Higher-Order Function vs First-Class Function

These concepts are related but different.

## First-Class Functions

Functions can be:

```text
stored in variables
passed as arguments
stored in objects
stored in arrays
returned from functions
```

Example:

```javascript
const greet = () => {
    console.log("Hello");
};
```

---

## Higher-Order Function

A function that accepts or returns another function.

```javascript
function execute(callback) {
    callback();
}
```

So:

```text
First-Class Function
    ↓
Functions can be treated as values

Higher-Order Function
    ↓
A function works with other functions
```

---

# 7. Built-in Higher-Order Functions

JavaScript arrays provide many Higher-Order Functions.

Common examples:

```text
map()
filter()
reduce()
find()
some()
every()
forEach()
sort()
```

They receive callback functions.

---

# 8. map()

`map()` transforms every element and returns a new array.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((number) => {
    return number * 2;
});

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

The callback:

```javascript
(number) => number * 2
```

is passed to `map()`.

---

# 9. filter()

`filter()` creates a new array containing elements that satisfy a condition.

```javascript
const numbers = [10, 15, 20, 25, 30];

const result = numbers.filter((number) => {
    return number >= 20;
});

console.log(result);
```

Output:

```text
[20, 25, 30]
```

---

# 10. reduce()

`reduce()` processes an array and produces a single result.

```javascript
const prices = [100, 200, 300];

const total = prices.reduce((sum, price) => {
    return sum + price;
}, 0);

console.log(total);
```

Output:

```text
600
```

The callback controls how the accumulated value changes.

---

# 11. some()

`some()` checks whether at least one element satisfies a condition.

```javascript
const ages = [15, 16, 22, 17];

const hasAdult = ages.some((age) => {
    return age >= 18;
});

console.log(hasAdult);
```

Output:

```text
true
```

---

# 12. every()

`every()` checks whether all elements satisfy a condition.

```javascript
const ages = [20, 25, 30];

const allAdults = ages.every((age) => {
    return age >= 18;
});

console.log(allAdults);
```

Output:

```text
true
```

---

# 13. find()

`find()` returns the first element that satisfies a condition.

```javascript
const users = [
    { id: 1, name: "Ram" },
    { id: 2, name: "Sandip" },
    { id: 3, name: "Hari" }
];

const user = users.find((user) => {
    return user.id === 2;
});

console.log(user);
```

Result:

```javascript
{
    id: 2,
    name: "Sandip"
}
```

---

# 14. forEach()

`forEach()` executes a callback for each element.

```javascript
const names = [
    "Sandip",
    "Ram",
    "Hari"
];

names.forEach((name) => {
    console.log(name);
});
```

Output:

```text
Sandip
Ram
Hari
```

Unlike `map()`, `forEach()` is mainly used for side effects rather than creating a transformed array.

---

# 15. Custom Higher-Order Function

You can create your own Higher-Order Functions.

```javascript
function executeOperation(a, b, operation) {
    return operation(a, b);
}
```

Use it:

```javascript
const add = (a, b) => a + b;

const result = executeOperation(
    20,
    10,
    add
);

console.log(result);
```

Output:

```text
30
```

---

# 16. Reusable Tax Calculator

A Higher-Order Function can create different tax calculators.

```javascript
function createTaxCalculator(rate) {
    return function(price) {
        return price + price * rate;
    };
}
```

Create calculators:

```javascript
const tax10 = createTaxCalculator(0.10);
const tax15 = createTaxCalculator(0.15);
```

Use them:

```javascript
console.log(tax10(1000));
// 1100

console.log(tax15(1000));
// 1150
```

---

# 17. Reusable Role Check

This pattern is useful in backend applications.

```javascript
function allowRole(role) {
    return function(user) {
        return user.role === role;
    };
}
```

Create a checker:

```javascript
const isAdmin = allowRole("admin");
```

Use it:

```javascript
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

This kind of pattern can be useful when building authentication and authorization logic.

---

# 18. Multiple Allowed Roles

We can create a reusable role checker:

```javascript
function allowRoles(...allowedRoles) {
    return function(user) {
        return allowedRoles.includes(user.role);
    };
}
```

Create a checker:

```javascript
const canManageOrders =
    allowRoles("admin", "waiter");
```

Use it:

```javascript
const user = {
    role: "waiter"
};

console.log(canManageOrders(user));
```

Output:

```text
true
```

---

# 19. Reusable Filtering

Suppose we have products:

```javascript
const products = [
    { name: "Laptop", price: 800 },
    { name: "Mouse", price: 20 },
    { name: "Keyboard", price: 50 }
];
```

Create a reusable filter:

```javascript
function filterProducts(products, condition) {
    return products.filter(condition);
}
```

Use it:

```javascript
const expensiveProducts = filterProducts(
    products,
    (product) => product.price > 100
);

console.log(expensiveProducts);
```

The filtering logic is supplied from outside.

---

# 20. Logging Wrapper

Higher-Order Functions can wrap existing functions.

```javascript
function withLogging(fn) {
    return function(...args) {
        console.log("Function called");

        const result = fn(...args);

        console.log("Function finished");

        return result;
    };
}
```

Create a wrapped function:

```javascript
const add = (a, b) => a + b;

const loggedAdd = withLogging(add);

console.log(loggedAdd(10, 20));
```

Output:

```text
Function called
Function finished
30
```

---

# 21. Adding Validation

A Higher-Order Function can also add validation.

```javascript
function withValidation(fn) {
    return function(value) {
        if (value === null || value === undefined) {
            throw new Error("Value is required");
        }

        return fn(value);
    };
}
```

Create a function:

```javascript
const getLength = withValidation(
    (value) => value.length
);
```

Use it:

```javascript
console.log(getLength("JavaScript"));
```

Output:

```text
10
```

---

# 22. Higher-Order Functions in React

Higher-Order Functions are common in React and JavaScript code.

For example:

```jsx
const activeUsers = users.filter(
    (user) => user.isActive
);
```

Or:

```jsx
const userNames = users.map(
    (user) => user.name
);
```

The callback controls what happens to each item.

---

# 23. Higher-Order Functions in Node.js

Node.js applications frequently use functions as callbacks.

Example:

```javascript
app.get("/users", (req, res) => {
    res.json({
        message: "Users fetched"
    });
});
```

The function:

```javascript
(req, res) => {}
```

is supplied to:

```javascript
app.get()
```

The framework later calls that function when the route is requested.

---

# 24. Function Pipeline

Higher-Order Functions can be chained together.

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter((number) => number % 2 === 0)
    .map((number) => number * 10);

console.log(result);
```

Output:

```text
[20, 40, 60]
```

Here:

```text
filter()
    ↓
select even numbers
    ↓
map()
    ↓
multiply by 10
```

---

# 25. Practical Order Example

Suppose a hotel system contains orders:

```javascript
const orders = [
    {
        id: 1,
        status: "pending",
        total: 500
    },
    {
        id: 2,
        status: "completed",
        total: 1000
    },
    {
        id: 3,
        status: "pending",
        total: 750
    }
];
```

Find pending orders:

```javascript
const pendingOrders = orders.filter(
    (order) => order.status === "pending"
);
```

Get their totals:

```javascript
const pendingTotals = pendingOrders.map(
    (order) => order.total
);
```

Calculate the total:

```javascript
const total = pendingTotals.reduce(
    (sum, amount) => sum + amount,
    0
);

console.log(total);
```

Output:

```text
1250
```

This demonstrates how Higher-Order Functions can be combined to process application data.

---

# 26. Advantages

Higher-Order Functions help with:

* Code reuse
* Flexible behavior
* Cleaner data processing
* Less duplicated logic
* Functional programming
* Reusable utilities
* Middleware-style patterns
* React development
* Node.js development

---

# 27. Common Structure

A Higher-Order Function that accepts a function:

```javascript
function higherOrder(callback) {
    return callback();
}
```

A Higher-Order Function that returns a function:

```javascript
function higherOrder() {
    return function() {
        console.log("Hello");
    };
}
```

A function can also do both:

```javascript
function higherOrder(callback) {
    return function(value) {
        return callback(value);
    };
}
```

---

# 28. Important Difference

```text
Normal Function
    ↓
Performs a specific operation

First-Class Function
    ↓
Function can be treated like a value

Higher-Order Function
    ↓
Accepts or returns another function
```

Example:

```javascript
const double = (number) => number * 2;
```

`double` is a normal function and can be treated as a first-class value.

```javascript
function process(number, operation) {
    return operation(number);
}
```

`process` is a Higher-Order Function because it receives a function.

---

# 29. Quick Reference

```text
Higher-Order Function
        │
        ├── Accepts a function
        │
        └── Returns a function
```

Common built-in examples:

```javascript
map()
filter()
reduce()
find()
some()
every()
forEach()
sort()
```

Custom example:

```javascript
function execute(callback) {
    return callback();
}
```

Returning a function:

```javascript
function createFunction() {
    return function() {
        console.log("Hello");
    };
}
```

---

# 30. Key Takeaways

* A Higher-Order Function works with other functions.
* It can accept a function as an argument.
* It can return a function.
* `map()`, `filter()`, and `reduce()` are common examples.
* Higher-Order Functions make code more reusable.
* They are heavily used in React and Node.js.
* Functions returned by HOFs can preserve configuration.
* HOFs are useful for reusable authorization, validation, logging, filtering, and calculation logic.
* First-class functions describe how functions can be treated as values.
* Higher-Order Functions describe functions that accept or return other functions.

---

# Simple Mental Model

```text
Function
   ↓
Can be used as a value
   ↓
Can be passed to another function
   ↓
Can be returned from another function
   ↓
Higher-Order Functions
   ↓
Reusable and flexible code
```
