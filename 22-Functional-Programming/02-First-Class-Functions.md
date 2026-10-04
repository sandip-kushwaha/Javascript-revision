# JavaScript — First-Class Functions

JavaScript treats functions as **first-class values**.

This means functions can be used like other values such as:

```text
numbers
strings
objects
arrays
```

A function can be:

* Stored in a variable
* Stored in an object
* Stored in an array
* Passed as an argument
* Returned from another function

This concept is fundamental to callbacks, higher-order functions, functional programming, and many JavaScript patterns.

---

# 1. Function Stored in a Variable

A function can be assigned to a variable.

```javascript
const greet = function () {
    console.log("Hello Sandip");
};

greet();
```

Output:

```text
Hello Sandip
```

The variable `greet` now contains a function value.

---

# 2. Arrow Functions

Arrow functions can also be stored in variables.

```javascript
const add = (a, b) => {
    return a + b;
};

console.log(add(10, 20));
```

Output:

```text
30
```

Short form:

```javascript
const add = (a, b) => a + b;
```

---

# 3. Functions Stored in Arrays

Functions can be elements of an array.

```javascript
const operations = [
    () => console.log("Add"),
    () => console.log("Update"),
    () => console.log("Delete")
];

operations[0]();
operations[1]();
operations[2]();
```

Output:

```text
Add
Update
Delete
```

This can be useful when a program needs to store a collection of actions.

---

# 4. Functions Stored in Objects

Functions can be stored as object properties.

```javascript
const user = {
    name: "Sandip",

    greet() {
        console.log(`Hello ${this.name}`);
    }
};

user.greet();
```

Here:

```text
name  → string value
greet → function value
```

---

# 5. Functions as Arguments

A function can be passed to another function.

```javascript
function greet(name) {
    console.log(`Hello ${name}`);
}

function processUser(callback) {
    callback("Sandip");
}

processUser(greet);
```

Output:

```text
Hello Sandip
```

The function `greet` is passed as a value.

---

# 6. Callback Example

A callback is simply a function supplied to another function for later execution.

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

const add = (a, b) => a + b;

const result =
    calculate(10, 20, add);

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
receives add()
    ↓
calls add(10, 20)
```

---

# 7. Passing Arrow Functions

The function does not need to be stored in a variable first.

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

const result =
    calculate(
        10,
        20,
        (a, b) => a * b
    );

console.log(result);
```

Output:

```text
200
```

---

# 8. Function as a Return Value

A function can return another function.

```javascript
function createGreeting() {
    return function () {
        console.log("Hello Sandip");
    };
}

const greet =
    createGreeting();

greet();
```

Output:

```text
Hello Sandip
```

The returned function is stored in `greet`.

---

# 9. Returning an Arrow Function

The same concept can be written more concisely.

```javascript
function createMultiplier(multiplier) {
    return number => number * multiplier;
}

const double =
    createMultiplier(2);

console.log(double(5));
```

Output:

```text
10
```

The returned function remembers the `multiplier` value.

This pattern is closely related to closures.

---

# 10. Functions Can Be Compared

Functions are values, so references can be compared.

```javascript
const greet = () => {
    console.log("Hello");
};

const anotherGreet = greet;

console.log(greet === anotherGreet);
```

Output:

```text
true
```

Both variables reference the same function.

But:

```javascript
const first = () => {};
const second = () => {};

console.log(first === second);
```

Output:

```text
false
```

They are two different function objects.

---

# 11. Function References

You can pass a function without calling it.

Correct:

```javascript
setTimeout(greet, 1000);
```

Here:

```text
greet
```

is a function reference.

Do not write:

```javascript
setTimeout(greet(), 1000);
```

because `greet()` executes immediately and its return value is passed to `setTimeout()`.

---

# 12. Built-in Methods Use Functions

Many JavaScript methods accept functions.

Example:

```javascript
const numbers = [1, 2, 3, 4];

const doubled =
    numbers.map(number => number * 2);

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

The function:

```javascript
number => number * 2
```

is passed to `map()`.

---

# 13. `filter()` Example

```javascript
const numbers = [
    10,
    15,
    20,
    25
];

const result =
    numbers.filter(
        number => number >= 20
    );

console.log(result);
```

Output:

```text
[20, 25]
```

The callback function determines which values should remain.

---

# 14. `reduce()` Example

```javascript
const prices = [
    100,
    200,
    300
];

const total =
    prices.reduce(
        (sum, price) => sum + price,
        0
    );

console.log(total);
```

Output:

```text
600
```

The reducer function is passed to `reduce()`.

---

# 15. Functions in Variables vs Function Declarations

Function declaration:

```javascript
function add(a, b) {
    return a + b;
}
```

Function expression:

```javascript
const add = function (a, b) {
    return a + b;
};
```

Arrow function:

```javascript
const add = (a, b) => a + b;
```

All create callable functions, but their syntax and behavior around hoisting and `this` differ.

---

# 16. Functions as Object Properties

```javascript
const calculator = {
    add(a, b) {
        return a + b;
    },

    subtract(a, b) {
        return a - b;
    },

    multiply(a, b) {
        return a * b;
    }
};

console.log(
    calculator.add(10, 5)
);

console.log(
    calculator.multiply(10, 5)
);
```

Output:

```text
15
50
```

---

# 17. Functions as Array Elements

You can create an action list.

```javascript
const actions = [
    () => console.log("Login"),
    () => console.log("Dashboard"),
    () => console.log("Logout")
];

for (const action of actions) {
    action();
}
```

Output:

```text
Login
Dashboard
Logout
```

---

# 18. Dynamic Function Selection

Functions can be selected based on data.

```javascript
const operations = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b
};

const operation = "multiply";

const result =
    operations[operation](10, 5);

console.log(result);
```

Output:

```text
50
```

This can be useful instead of writing many `if...else` blocks for simple operation selection.

---

# 19. Function Factories

A function can create specialized functions.

```javascript
function createMultiplier(multiplier) {
    return number => number * multiplier;
}

const double =
    createMultiplier(2);

const triple =
    createMultiplier(3);

console.log(double(10));
console.log(triple(10));
```

Output:

```text
20
30
```

The outer function creates different functions based on the supplied value.

---

# 20. Functions and Closures

Consider:

```javascript
function createCounter() {
    let count = 0;

    return function () {
        count++;

        return count;
    };
}

const counter =
    createCounter();

console.log(counter());
console.log(counter());
```

Output:

```text
1
2
```

The returned function remembers the `count` variable.

This works because the function forms a closure over its surrounding scope.

---

# 21. Functions Can Have Properties

Functions are objects in JavaScript and can have properties.

```javascript
function greet() {
    console.log("Hello");
}

greet.message = "Welcome";

console.log(greet.message);
```

Output:

```text
Welcome
```

This is possible because functions are objects with callable behavior.

---

# 22. Function Name Property

Functions have a `name` property.

```javascript
function greet() {
    console.log("Hello");
}

console.log(greet.name);
```

Output:

```text
greet
```

For a named function expression:

```javascript
const add = function addNumbers(a, b) {
    return a + b;
};

console.log(add.name);
```

Output:

```text
addNumbers
```

---

# 23. Function Length Property

The `length` property represents the number of parameters before the first parameter with a default value.

```javascript
function add(a, b, c) {
    return a + b + c;
}

console.log(add.length);
```

Output:

```text
3
```

Example with a default parameter:

```javascript
function greet(name, age = 22) {
    console.log(name, age);
}

console.log(greet.length);
```

Output:

```text
1
```

---

# 24. Functions as Data

Because functions are values, they can be handled like data.

```javascript
const greet = () => "Hello";

const functions = {
    greeting: greet
};

const selectedFunction =
    functions.greeting;

console.log(
    selectedFunction()
);
```

Output:

```text
Hello
```

---

# 25. Practical Example — Notification System

```javascript
function sendNotification(message, handler) {
    handler(message);
}

const emailNotification =
    message => {
        console.log(`Email: ${message}`);
    };

const smsNotification =
    message => {
        console.log(`SMS: ${message}`);
    };

sendNotification(
    "Order confirmed",
    emailNotification
);

sendNotification(
    "Order confirmed",
    smsNotification
);
```

Output:

```text
Email: Order confirmed
SMS: Order confirmed
```

The same function accepts different behaviors.

---

# 26. Practical Example — Hotel Order Status

```javascript
const statusHandlers = {
    pending: () =>
        console.log("Order is pending"),

    preparing: () =>
        console.log("Order is being prepared"),

    ready: () =>
        console.log("Order is ready"),

    completed: () =>
        console.log("Order completed")
};

const status = "ready";

statusHandlers[status]();
```

Output:

```text
Order is ready
```

Functions stored in an object can make simple status-based behavior easier to organize.

---

# 27. Practical Example — Validation

```javascript
const validators = {
    username: value =>
        /^[a-zA-Z0-9_]{4,15}$/.test(value),

    email: value =>
        /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value)
};

console.log(
    validators.username("sandip_22")
);

console.log(
    validators.email("sandip@example.com")
);
```

The object stores different validation functions.

---

# 28. First-Class Functions and Functional Programming

First-class functions make patterns such as these possible:

```text
Callbacks
Higher-order functions
Closures
Function factories
Function composition
Array transformations
Event handlers
Middleware
```

Example:

```javascript
const numbers = [1, 2, 3, 4];

const result =
    numbers
        .filter(number => number % 2 === 0)
        .map(number => number * 10);

console.log(result);
```

Output:

```text
[20, 40]
```

---

# 29. First-Class Functions in React

React uses functions heavily.

Components are commonly functions:

```jsx
function UserCard({ name }) {
    return <h2>{name}</h2>;
}
```

Event handlers are functions:

```jsx
function Button() {
    const handleClick = () => {
        console.log("Clicked");
    };

    return (
        <button onClick={handleClick}>
            Click
        </button>
    );
}
```

Array methods also receive functions:

```jsx
const users = [
    { id: 1, name: "Sandip" },
    { id: 2, name: "Ram" }
];

const names =
    users.map(user => user.name);
```

---

# 30. First-Class Functions in Node.js

Node.js also uses functions extensively.

Middleware example:

```javascript
const logger = (req, res, next) => {
    console.log(req.method, req.url);

    next();
};
```

Express receives the function as middleware.

```javascript
app.use(logger);
```

The function is passed as a value to `app.use()`.

---

# 31. First-Class Functions Summary

```text
Function
   │
   ├── Store in variable
   │
   ├── Store in array
   │
   ├── Store in object
   │
   ├── Pass as argument
   │
   ├── Return from function
   │
   └── Use like other values
```

---

# Quick Cheat Sheet

```javascript
// Store in variable
const greet = () => {
    console.log("Hello");
};

// Store in object
const user = {
    greet
};

// Store in array
const actions = [
    greet
];

// Pass as argument
function run(callback) {
    callback();
}

run(greet);

// Return from function
function createFunction() {
    return () => {
        console.log("Created");
    };
}

const fn = createFunction();

fn();
```

---

# Key Takeaways

* JavaScript functions are first-class values.
* Functions can be stored in variables.
* Functions can be stored in arrays and objects.
* Functions can be passed as arguments.
* Functions can be returned from other functions.
* Callbacks are possible because functions can be passed as values.
* Function factories can create specialized functions.
* Closures allow returned functions to remember surrounding variables.
* `map()`, `filter()`, and `reduce()` accept functions as arguments.
* React event handlers and components commonly use functions as values.
* Node.js and Express use functions extensively for middleware and callbacks.
