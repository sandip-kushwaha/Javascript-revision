# JavaScript Rest Parameters

Rest parameters allow a function to accept **any number of arguments** and collect them into a single array.

They are written using three dots:

```javascript
...parameter
```

Rest parameters are especially useful when you don't know in advance how many arguments a function will receive.

---

# 1. What Is a Rest Parameter?

Normally, a function has a fixed number of parameters:

```javascript
function add(a, b) {
    return a + b;
}

console.log(add(10, 20));
```

But what if we want to accept any number of numbers?

We can use a rest parameter:

```javascript
function add(...numbers) {
    console.log(numbers);
}

add(10, 20, 30, 40);
```

Output:

```text
[10, 20, 30, 40]
```

The rest parameter collects all remaining arguments into an **array**.

---

# 2. Basic Syntax

```javascript
function functionName(...parameters) {
    // code
}
```

Example:

```javascript
function showValues(...values) {
    console.log(values);
}

showValues(10, 20, 30);
```

Output:

```text
[10, 20, 30]
```

---

# 3. Why Use Rest Parameters?

Without rest parameters:

```javascript
function sum(a, b, c) {
    return a + b + c;
}
```

This function expects three values.

With rest parameters:

```javascript
function sum(...numbers) {
    return numbers.reduce(
        (total, number) => total + number,
        0
    );
}

console.log(sum(10, 20));
console.log(sum(10, 20, 30));
console.log(sum(10, 20, 30, 40, 50));
```

Output:

```text
30
60
100
```

The function can handle different numbers of arguments.

---

# 4. Rest Parameter Is an Array

A rest parameter creates a real array.

```javascript
function showItems(...items) {
    console.log(items);
    console.log(Array.isArray(items));
}

showItems("Momo", "Pizza", "Coffee");
```

Output:

```text
["Momo", "Pizza", "Coffee"]
true
```

Because `items` is an array, you can use array methods:

```javascript
function showItems(...items) {
    console.log(items.length);
    console.log(items[0]);
}

showItems("Momo", "Pizza", "Coffee");
```

Output:

```text
3
Momo
```

---

# 5. Rest Parameter Can Contain Zero Values

A rest parameter can be empty.

```javascript
function showItems(...items) {
    console.log(items);
}

showItems();
```

Output:

```text
[]
```

The rest parameter is still an array.

---

# 6. Rest Parameter with Normal Parameters

You can combine normal parameters with a rest parameter.

```javascript
function introduce(name, ...skills) {
    console.log(`Name: ${name}`);
    console.log("Skills:", skills);
}

introduce(
    "Sandip",
    "JavaScript",
    "React",
    "Node.js"
);
```

Output:

```text
Name: Sandip
Skills: ["JavaScript", "React", "Node.js"]
```

Here:

```text
name   → "Sandip"
skills → ["JavaScript", "React", "Node.js"]
```

---

# 7. Rest Parameter Must Be Last

This is very important.

Correct:

```javascript
function example(name, age, ...others) {
    console.log(name);
    console.log(age);
    console.log(others);
}
```

Incorrect:

```javascript
function example(...others, name) {
}
```

This produces a syntax error.

The rest parameter must always be the **last parameter**.

---

# 8. Multiple Normal Parameters

You can have multiple normal parameters before the rest parameter.

```javascript
function order(customer, table, ...items) {
    console.log(customer);
    console.log(table);
    console.log(items);
}

order(
    "Sandip",
    "T-03",
    "Momo",
    "Pizza",
    "Coffee"
);
```

Output:

```text
Sandip
T-03
["Momo", "Pizza", "Coffee"]
```

---

# 9. Rest Parameter with Numbers

A common use case is calculating a sum.

```javascript
function sum(...numbers) {
    let total = 0;

    for (const number of numbers) {
        total += number;
    }

    return total;
}

console.log(sum(10, 20, 30));
```

Output:

```text
60
```

---

# 10. Rest Parameter with `reduce()`

The same example can be written using `reduce()`.

```javascript
function sum(...numbers) {
    return numbers.reduce(
        (total, number) => total + number,
        0
    );
}

console.log(sum(10, 20, 30, 40));
```

Output:

```text
100
```

---

# 11. Finding the Maximum Number

Rest parameters work well with `Math.max()`.

```javascript
function findMaximum(...numbers) {
    return Math.max(...numbers);
}

console.log(findMaximum(10, 50, 30, 80, 20));
```

Output:

```text
80
```

Notice that there are two different uses of `...`:

```javascript
function findMaximum(...numbers)
```

Here it is a **rest parameter**.

```javascript
Math.max(...numbers)
```

Here it is the **spread syntax**.

They look similar but perform different operations.

---

# 12. Rest vs Spread

This distinction is very important.

### Rest

Rest **collects** values.

```javascript
function show(...values) {
    console.log(values);
}
```

Arguments:

```text
10, 20, 30
```

Become:

```text
[10, 20, 30]
```

### Spread

Spread **expands** values.

```javascript
const numbers = [10, 20, 30];

console.log(Math.max(...numbers));
```

The array is expanded into:

```text
10, 20, 30
```

Simple rule:

```text
Rest   → collect
Spread → expand
```

---

# 13. Rest Parameters with Strings

```javascript
function joinWords(...words) {
    return words.join(" ");
}

console.log(
    joinWords("JavaScript", "is", "awesome")
);
```

Output:

```text
JavaScript is awesome
```

---

# 14. Rest Parameters with Arrays

```javascript
function getFirstItem(...items) {
    return items[0];
}

console.log(
    getFirstItem("Apple", "Banana", "Orange")
);
```

Output:

```text
Apple
```

You can use any array method:

```javascript
function countItems(...items) {
    return items.length;
}

console.log(
    countItems("A", "B", "C", "D")
);
```

Output:

```text
4
```

---

# 15. Rest Parameters with Objects

You can pass objects as arguments too.

```javascript
function showUsers(...users) {
    console.log(users);
}

showUsers(
    { name: "Sandip" },
    { name: "Ram" },
    { name: "Shyam" }
);
```

Output:

```javascript
[
    { name: "Sandip" },
    { name: "Ram" },
    { name: "Shyam" }
]
```

---

# 16. Rest Parameters with Functions

Functions can also be collected.

```javascript
function executeAll(...functions) {
    for (const fn of functions) {
        fn();
    }
}

function first() {
    console.log("First");
}

function second() {
    console.log("Second");
}

executeAll(first, second);
```

Output:

```text
First
Second
```

This pattern is useful when working with callbacks.

---

# 17. Rest Parameters and Arrow Functions

Rest parameters work very well with arrow functions.

```javascript
const sum = (...numbers) => {
    return numbers.reduce(
        (total, number) => total + number,
        0
    );
};

console.log(sum(10, 20, 30));
```

Output:

```text
60
```

Short version:

```javascript
const sum = (...numbers) =>
    numbers.reduce(
        (total, number) => total + number,
        0
    );
```

---

# 18. Rest Parameters vs `arguments`

Before rest parameters, developers often used the `arguments` object.

### `arguments`

```javascript
function sum() {
    let total = 0;

    for (const number of arguments) {
        total += number;
    }

    return total;
}
```

### Rest parameter

```javascript
function sum(...numbers) {
    let total = 0;

    for (const number of numbers) {
        total += number;
    }

    return total;
}
```

The rest parameter is generally easier to understand.

---

# 19. Important Difference: `arguments` Is Not an Array

In a traditional function:

```javascript
function show() {
    console.log(arguments);
}
```

`arguments` is an **array-like object**, not a real array.

Rest parameters create a real array:

```javascript
function show(...values) {
    console.log(Array.isArray(values));
}
```

Output:

```text
true
```

This means you can directly use:

```javascript
values.map(...)
values.filter(...)
values.reduce(...)
values.forEach(...)
```

---

# 20. Rest Parameters Have No `arguments` Problem in Arrow Functions

Arrow functions don't have their own `arguments`.

Instead of:

```javascript
const sum = () => {
    // arguments is not the arrow function's own object
};
```

Use:

```javascript
const sum = (...numbers) => {
    return numbers.reduce(
        (total, number) => total + number,
        0
    );
};
```

---

# 21. Rest Parameters with Default Parameters

Rest parameters can be combined with default parameters.

```javascript
function createUser(
    name = "Guest",
    role = "user",
    ...permissions
) {
    return {
        name,
        role,
        permissions
    };
}

console.log(
    createUser(
        "Sandip",
        "admin",
        "read",
        "write",
        "delete"
    )
);
```

Result:

```javascript
{
    name: "Sandip",
    role: "admin",
    permissions: [
        "read",
        "write",
        "delete"
    ]
}
```

---

# 22. Practical Example — Hotel Order

A hotel order can contain multiple food items.

```javascript
function createOrder(customerName, tableNumber, ...items) {
    return {
        customerName,
        tableNumber,
        items
    };
}

const order = createOrder(
    "Sandip",
    "T-03",
    "Momo",
    "Pizza",
    "Coffee"
);

console.log(order);
```

Result:

```javascript
{
    customerName: "Sandip",
    tableNumber: "T-03",
    items: [
        "Momo",
        "Pizza",
        "Coffee"
    ]
}
```

---

# 23. Practical Example — Calculate Order Total

Instead of passing an array:

```javascript
function calculateTotal(...prices) {
    return prices.reduce(
        (total, price) => total + price,
        0
    );
}

const total = calculateTotal(
    250,
    500,
    150
);

console.log(total);
```

Output:

```text
900
```

---

# 24. Practical Example — Create Permissions

```javascript
function createRole(roleName, ...permissions) {
    return {
        roleName,
        permissions
    };
}

const adminRole = createRole(
    "admin",
    "create",
    "read",
    "update",
    "delete"
);

console.log(adminRole);
```

Result:

```javascript
{
    roleName: "admin",
    permissions: [
        "create",
        "read",
        "update",
        "delete"
    ]
}
```

---

# 25. Practical Example — Logging

A custom logging function can use rest parameters.

```javascript
function log(...messages) {
    console.log(messages);
}

log(
    "Server started",
    "Port: 8000",
    "Environment: development"
);
```

Output:

```text
[
    "Server started",
    "Port: 8000",
    "Environment: development"
]
```

You could also process each message:

```javascript
function log(...messages) {
    for (const message of messages) {
        console.log(`[LOG] ${message}`);
    }
}

log("Server started", "Database connected");
```

Output:

```text
[LOG] Server started
[LOG] Database connected
```

---

# 26. Practical Example — Middleware-Like Function

A function can receive a main value and multiple handlers.

```javascript
function executeHandlers(request, ...handlers) {
    for (const handler of handlers) {
        handler(request);
    }
}

function authenticate(request) {
    console.log("Authenticating:", request);
}

function validate(request) {
    console.log("Validating:", request);
}

executeHandlers(
    "/users",
    authenticate,
    validate
);
```

Output:

```text
Authenticating: /users
Validating: /users
```

This demonstrates how rest parameters can help build flexible APIs.

---

# 27. Empty Rest Parameter

A rest parameter can receive no values.

```javascript
function show(...values) {
    console.log(values);
}

show();
```

Output:

```text
[]
```

The result is an empty array, not `undefined`.

---

# 28. Rest Parameter and Parameter Count

You can check how many values were collected.

```javascript
function count(...values) {
    return values.length;
}

console.log(count(10, 20, 30));
```

Output:

```text
3
```

---

# 29. Rest Parameter with `filter()`

```javascript
function getEvenNumbers(...numbers) {
    return numbers.filter(
        number => number % 2 === 0
    );
}

console.log(
    getEvenNumbers(1, 2, 3, 4, 5, 6)
);
```

Output:

```text
[2, 4, 6]
```

---

# 30. Rest Parameter with `map()`

```javascript
function doubleNumbers(...numbers) {
    return numbers.map(
        number => number * 2
    );
}

console.log(
    doubleNumbers(1, 2, 3)
);
```

Output:

```text
[2, 4, 6]
```

---

# 31. Rest Parameter with `forEach()`

```javascript
function printItems(...items) {
    items.forEach(item => {
        console.log(item);
    });
}

printItems(
    "JavaScript",
    "React",
    "Node.js"
);
```

Output:

```text
JavaScript
React
Node.js
```

---

# 32. Rest Parameter with Destructuring

Rest syntax can also appear in destructuring.

This is related to rest syntax but is not a function rest parameter.

```javascript
const numbers = [10, 20, 30, 40];

const [first, ...remaining] = numbers;

console.log(first);
console.log(remaining);
```

Output:

```text
10
[20, 30, 40]
```

Here:

```text
first     → 10
remaining → [20, 30, 40]
```

---

# 33. Object Rest Syntax

Rest syntax can also be used with objects.

```javascript
const user = {
    name: "Sandip",
    age: 22,
    role: "admin"
};

const { name, ...details } = user;

console.log(name);
console.log(details);
```

Output:

```text
Sandip
{
    age: 22,
    role: "admin"
}
```

Again, this is **rest syntax in destructuring**, not a function rest parameter.

---

# 34. Rest Parameter vs Destructuring Rest

### Function rest parameter

```javascript
function show(...values) {
}
```

Collects function arguments.

### Array destructuring rest

```javascript
const [first, ...remaining] = numbers;
```

Collects remaining array elements.

### Object destructuring rest

```javascript
const { name, ...details } = user;
```

Collects remaining object properties.

The common idea is:

```text
... → collect the remaining values
```

---

# 35. Common Mistakes

### Mistake 1: Rest parameter in the middle

Incorrect:

```javascript
function test(...items, name) {
}
```

Correct:

```javascript
function test(name, ...items) {
}
```

---

### Mistake 2: Confusing Rest and Spread

Rest:

```javascript
function sum(...numbers) {
}
```

Spread:

```javascript
const numbers = [1, 2, 3];

sum(...numbers);
```

Remember:

```text
Rest   → collect
Spread → expand
```

---

### Mistake 3: Thinking Rest Creates an array-like object

It creates a real array:

```javascript
function test(...values) {
    console.log(Array.isArray(values));
}

test(1, 2, 3);
```

Output:

```text
true
```

---

### Mistake 4: Using `arguments` unnecessarily

Instead of:

```javascript
function sum() {
    return Array.from(arguments)
        .reduce((a, b) => a + b, 0);
}
```

Modern JavaScript can use:

```javascript
function sum(...numbers) {
    return numbers.reduce(
        (a, b) => a + b,
        0
    );
}
```

---

# 36. Best Practices

### 1. Use descriptive rest parameter names

Good:

```javascript
function calculateTotal(...prices) {
}
```

Less descriptive:

```javascript
function calculateTotal(...x) {
}
```

### 2. Use rest parameters when the number of arguments is variable

```javascript
function sum(...numbers) {
}
```

### 3. Keep the rest parameter last

```javascript
function createOrder(customer, ...items) {
}
```

### 4. Remember that the rest parameter is an array

You can use:

```javascript
items.length
items.map(...)
items.filter(...)
items.reduce(...)
```

### 5. Prefer rest parameters over manually handling `arguments`

They are clearer and work naturally with arrow functions.

---

# 37. Quick Revision

```text
Rest Parameter
       ↓
Uses ...
       ↓
Collects remaining arguments
       ↓
Creates a real Array
```

Example:

```javascript
function sum(...numbers) {
    return numbers.reduce(
        (total, number) => total + number,
        0
    );
}

sum(10, 20, 30);
```

Result:

```text
60
```

### With normal parameters

```javascript
function createOrder(
    customer,
    table,
    ...items
) {
}
```

### Important rule

```text
Rest parameter must be the last parameter.
```

### Rest vs Spread

```text
Rest   → collects values
Spread → expands values
```

---

# Key Takeaways

* Rest parameters use the `...` syntax.
* They collect remaining function arguments into an array.
* A rest parameter is a real JavaScript array.
* A function can have normal parameters before the rest parameter.
* The rest parameter must always be last.
* Rest parameters can receive zero or many values.
* They work with normal functions, function expressions, and arrow functions.
* Rest parameters are generally easier to use than the `arguments` object.
* Rest parameters can be used with array methods such as `map()`, `filter()`, `reduce()`, and `forEach()`.
* `...` in a function parameter is rest syntax.
* `...` when passing an array into a function is spread syntax.
* Rest syntax also appears in array and object destructuring.

---
