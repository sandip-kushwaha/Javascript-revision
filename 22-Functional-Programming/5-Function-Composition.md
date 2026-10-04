# Function Composition in JavaScript

**Function composition** means combining multiple functions so that the output of one function becomes the input of another function.

The main idea is:

```text
Function A
    ↓
Function B
    ↓
Function C
    ↓
Final Result
```

Function composition is an important concept in functional programming.

---

# 1. Simple Example

Suppose we have two functions:

```javascript
function double(number) {
    return number * 2;
}

function addTen(number) {
    return number + 10;
}
```

We can use them separately:

```javascript
const result1 = double(5);
const result2 = addTen(result1);

console.log(result2);
```

Output:

```text
20
```

The flow is:

```text
5
 ↓
double()
 ↓
10
 ↓
addTen()
 ↓
20
```

---

# 2. Compose Functions Manually

We can write the same operation directly:

```javascript
const result = addTen(double(5));

console.log(result);
```

Output:

```text
20
```

The inner function runs first:

```text
double(5)
    ↓
10

addTen(10)
    ↓
20
```

---

# 3. Why Function Composition?

Without composition:

```javascript
const step1 = double(5);
const step2 = addTen(step1);
const step3 = String(step2);

console.log(step3);
```

With composition:

```javascript
const result = String(addTen(double(5)));

console.log(result);
```

Composition allows multiple operations to work together.

---

# 4. Basic Composition Function

We can create a reusable `compose()` function.

```javascript
function compose(first, second) {
    return function(value) {
        return second(first(value));
    };
}
```

Use it:

```javascript
function double(number) {
    return number * 2;
}

function addTen(number) {
    return number + 10;
}

const doubleThenAddTen = compose(
    double,
    addTen
);

console.log(doubleThenAddTen(5));
```

Output:

```text
20
```

The execution is:

```text
5
 ↓
double()
 ↓
10
 ↓
addTen()
 ↓
20
```

---

# 5. Compose Multiple Functions

We can create a composition function that accepts multiple functions.

```javascript
function compose(...functions) {
    return function(value) {
        return functions.reduceRight(
            (result, fn) => fn(result),
            value
        );
    };
}
```

Example functions:

```javascript
function double(number) {
    return number * 2;
}

function addTen(number) {
    return number + 10;
}

function square(number) {
    return number * number;
}
```

Compose them:

```javascript
const processNumber = compose(
    double,
    addTen,
    square
);
```

Run:

```javascript
console.log(processNumber(5));
```

Execution:

```text
5
 ↓
double
 ↓
10
 ↓
addTen
 ↓
20
 ↓
square
 ↓
400
```

Output:

```text
400
```

---

# 6. `compose()` Execution Order

With:

```javascript
const process = compose(
    double,
    addTen,
    square
);
```

The functions execute from **right to left**:

```text
square
   ↑
addTen
   ↑
double
```

Conceptually:

```javascript
square(
    addTen(
        double(5)
    )
);
```

---

# 7. Compose vs Pipe

Two common patterns are:

```text
compose()
pipe()
```

The main difference is execution direction.

### Compose

```text
Right → Left
```

### Pipe

```text
Left → Right
```

---

# 8. Basic `pipe()`

```javascript
function pipe(...functions) {
    return function(value) {
        return functions.reduce(
            (result, fn) => fn(result),
            value
        );
    };
}
```

Functions:

```javascript
function double(number) {
    return number * 2;
}

function addTen(number) {
    return number + 10;
}

function square(number) {
    return number * number;
}
```

Create a pipeline:

```javascript
const processNumber = pipe(
    double,
    addTen,
    square
);
```

Run:

```javascript
console.log(processNumber(5));
```

Execution:

```text
5
 ↓
double
 ↓
10
 ↓
addTen
 ↓
20
 ↓
square
 ↓
400
```

---

# 9. Compose vs Pipe

| Feature        | `compose()`          | `pipe()`          |
| -------------- | -------------------- | ----------------- |
| Direction      | Right → Left         | Left → Right      |
| First function | Runs later           | Runs first        |
| Style          | Nested               | Sequential        |
| Common idea    | Function composition | Function pipeline |

Conceptually:

```javascript
compose(a, b, c);
```

means:

```text
c → b → a
```

while:

```javascript
pipe(a, b, c);
```

means:

```text
a → b → c
```

---

# 10. Real Example — User Data

Suppose:

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

Create functions:

```javascript
function getName(user) {
    return user.name;
}

function uppercase(value) {
    return value.toUpperCase();
}

function addGreeting(value) {
    return `Hello ${value}`;
}
```

Use them:

```javascript
const result = pipe(
    getName,
    uppercase,
    addGreeting
);

console.log(result(user));
```

Output:

```text
Hello SANDIP
```

Flow:

```text
user object
    ↓
getName()
    ↓
"Sandip"
    ↓
uppercase()
    ↓
"SANDIP"
    ↓
addGreeting()
    ↓
"Hello SANDIP"
```

---

# 11. Data Transformation Pipeline

Function composition is useful when transforming data step by step.

```javascript
function trimText(text) {
    return text.trim();
}

function lowercase(text) {
    return text.toLowerCase();
}

function removeSpaces(text) {
    return text.replaceAll(" ", "-");
}
```

Create a pipeline:

```javascript
const formatText = pipe(
    trimText,
    lowercase,
    removeSpaces
);
```

Use it:

```javascript
console.log(
    formatText("  Hello JavaScript World  ")
);
```

Output:

```text
hello-javascript-world
```

---

# 12. API Data Transformation

Suppose an API returns:

```javascript
const user = {
    firstName: "Sandip",
    lastName: "Kushwaha"
};
```

Create small functions:

```javascript
function getFullName(user) {
    return `${user.firstName} ${user.lastName}`;
}

function uppercase(name) {
    return name.toUpperCase();
}

function createLabel(name) {
    return `USER: ${name}`;
}
```

Create a pipeline:

```javascript
const formatUser = pipe(
    getFullName,
    uppercase,
    createLabel
);
```

Use:

```javascript
console.log(formatUser(user));
```

Output:

```text
USER: SANDIP KUSHWAHA
```

---

# 13. Order Processing Example

Suppose an application receives an order:

```javascript
const order = {
    price: 1000,
    quantity: 2
};
```

Create individual functions:

```javascript
function calculateSubtotal(order) {
    return order.price * order.quantity;
}

function addTax(amount) {
    return amount * 1.13;
}

function roundAmount(amount) {
    return Math.round(amount);
}
```

Create a pipeline:

```javascript
const calculateTotal = pipe(
    calculateSubtotal,
    addTax,
    roundAmount
);
```

Run:

```javascript
console.log(calculateTotal(order));
```

Flow:

```text
Order
 ↓
calculateSubtotal()
 ↓
2000
 ↓
addTax()
 ↓
2260
 ↓
roundAmount()
 ↓
2260
```

---

# 14. Function Composition with Arrays

Composition works well with array transformations.

Example:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
```

Create functions:

```javascript
function getEvenNumbers(numbers) {
    return numbers.filter(
        (number) => number % 2 === 0
    );
}

function doubleNumbers(numbers) {
    return numbers.map(
        (number) => number * 2
    );
}
```

Compose them:

```javascript
const processNumbers = pipe(
    getEvenNumbers,
    doubleNumbers
);
```

Run:

```javascript
console.log(
    processNumbers(numbers)
);
```

Output:

```text
[4, 8, 12]
```

---

# 15. Composition with `reduce()`

A common implementation of `pipe()` uses `reduce()`:

```javascript
function pipe(...functions) {
    return (value) => {
        return functions.reduce(
            (result, fn) => fn(result),
            value
        );
    };
}
```

Suppose:

```javascript
const process = pipe(
    double,
    addTen,
    square
);
```

`reduce()` passes the result of one function to the next:

```text
initial value
     ↓
double
     ↓
result
     ↓
addTen
     ↓
result
     ↓
square
```

---

# 16. Composition and Small Functions

Composition works best when functions do one clear task.

Good:

```javascript
function trimText(text) {
    return text.trim();
}

function lowercase(text) {
    return text.toLowerCase();
}

function createSlug(text) {
    return text.replaceAll(" ", "-");
}
```

Then:

```javascript
const createSlugFromTitle = pipe(
    trimText,
    lowercase,
    createSlug
);
```

Each function has one responsibility.

---

# 17. Composition vs Large Function

Without composition:

```javascript
function createSlug(title) {
    const trimmed = title.trim();
    const lowercase = trimmed.toLowerCase();
    const slug = lowercase.replaceAll(" ", "-");

    return slug;
}
```

With reusable functions:

```javascript
const createSlug = pipe(
    trimText,
    lowercase,
    createSlugFromText
);
```

The second approach makes each transformation independently reusable.

---

# 18. Composition in React

Composition can be useful when preparing data before rendering.

```javascript
function getActiveUsers(users) {
    return users.filter(
        (user) => user.isActive
    );
}

function getUserNames(users) {
    return users.map(
        (user) => user.name
    );
}

const prepareUsers = pipe(
    getActiveUsers,
    getUserNames
);
```

Then:

```javascript
const names = prepareUsers(users);
```

React can render:

```jsx
{names.map((name) => (
    <p key={name}>
        {name}
    </p>
))}
```

---

# 19. Composition in Node.js

Node.js applications can use pipelines for data transformation.

For example:

```javascript
function validateUser(user) {
    if (!user.email) {
        throw new Error("Email is required");
    }

    return user;
}

function normalizeUser(user) {
    return {
        ...user,
        email: user.email.toLowerCase()
    };
}

function prepareUser(user) {
    return {
        ...user,
        name: user.name.trim()
    };
}
```

Create a pipeline:

```javascript
const processUser = pipe(
    validateUser,
    normalizeUser,
    prepareUser
);
```

Use:

```javascript
const result = processUser({
    name: " Sandip ",
    email: "SANDIP@example.com"
});
```

Result:

```javascript
{
    name: "Sandip",
    email: "sandip@example.com"
}
```

---

# 20. Composition and Immutability

Function composition works especially well with immutable transformations.

Example:

```javascript
function addUser(users, user) {
    return [
        ...users,
        user
    ];
}

function activateUsers(users) {
    return users.map((user) => ({
        ...user,
        isActive: true
    }));
}
```

These functions return new values instead of modifying existing data.

They can be combined into a pipeline when their input and output types match.

---

# 21. Composition Requirements

For simple composition, the functions should have compatible inputs and outputs.

For example:

```text
Function A
    input → number
    output → number

Function B
    input → number
    output → number
```

They can easily be connected:

```text
A(number)
   ↓
number
   ↓
B(number)
```

But this would not work directly:

```text
Function A
    output → object

Function B
    input → number
```

because the values do not match.

---

# 22. Composition Pattern

A common functional programming pattern is:

```text
Input
  ↓
Function 1
  ↓
Function 2
  ↓
Function 3
  ↓
Output
```

Example:

```javascript
const process = pipe(
    validate,
    normalize,
    transform,
    format
);
```

This creates a clear data flow.

---

# 23. Practical Example — Product Price

```javascript
const product = {
    price: 1000
};
```

Functions:

```javascript
function addTax(product) {
    return {
        ...product,
        price: product.price * 1.13
    };
}

function addDiscount(product) {
    return {
        ...product,
        price: product.price * 0.90
    };
}

function roundPrice(product) {
    return {
        ...product,
        price: Math.round(product.price)
    };
}
```

Pipeline:

```javascript
const calculatePrice = pipe(
    addTax,
    addDiscount,
    roundPrice
);
```

Run:

```javascript
console.log(
    calculatePrice(product)
);
```

The original product remains unchanged.

---

# 24. Benefits of Function Composition

Function composition provides:

* Small reusable functions
* Clear data flow
* Less duplicated logic
* Easier testing
* Easier maintenance
* Reusable transformations
* Better separation of responsibilities
* Cleaner functional programming patterns

---

# 25. When to Use It

Function composition is useful for:

```text
Data transformation
API response processing
Form data normalization
Validation pipelines
Formatting
Price calculations
Authentication processing
Data filtering
React data preparation
Node.js backend utilities
```

---

# 26. When Not to Overuse It

Composition is useful, but not every function needs a pipeline.

For simple logic:

```javascript
const result = number * 2 + 10;
```

is perfectly readable.

Do not create a complicated composition system when a simple function is easier to understand.

Prefer readability.

---

# 27. Quick Reference

### Compose

```javascript
function compose(...functions) {
    return (value) => {
        return functions.reduceRight(
            (result, fn) => fn(result),
            value
        );
    };
}
```

Execution:

```text
Right → Left
```

---

### Pipe

```javascript
function pipe(...functions) {
    return (value) => {
        return functions.reduce(
            (result, fn) => fn(result),
            value
        );
    };
}
```

Execution:

```text
Left → Right
```

---

# 28. Simple Comparison

```text
compose()
    ↓
Right → Left

pipe()
    ↓
Left → Right
```

Example:

```javascript
const result = compose(
    functionA,
    functionB,
    functionC
);
```

Conceptually:

```text
functionC
    ↓
functionB
    ↓
functionA
```

While:

```javascript
const result = pipe(
    functionA,
    functionB,
    functionC
);
```

means:

```text
functionA
    ↓
functionB
    ↓
functionC
```

---

# 29. Key Takeaways

* Function composition combines multiple functions into a single workflow.
* The output of one function becomes the input of another.
* `compose()` commonly works from right to left.
* `pipe()` commonly works from left to right.
* Small functions are easier to compose.
* Composition is useful for data transformation and processing pipelines.
* `reduce()` can be used to implement a pipeline.
* Composition works well with immutable transformations.
* React and Node.js applications can benefit from clear function pipelines.
* Do not overuse composition when straightforward code is easier to read.

---

# Simple Mental Model

```text
Input
  ↓
Function A
  ↓
Output A
  ↓
Function B
  ↓
Output B
  ↓
Function C
  ↓
Final Output
```

That is the core idea behind **function composition**.
