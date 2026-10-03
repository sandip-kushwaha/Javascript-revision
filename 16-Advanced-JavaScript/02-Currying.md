# JavaScript Currying

**Currying** is a technique where a function that normally accepts multiple arguments is converted into a sequence of functions, each accepting one argument at a time.

Instead of:

```javascript
function add(a, b, c) {
    return a + b + c;
}

add(10, 20, 30);
```

A curried version looks like:

```javascript
function add(a) {
    return function (b) {
        return function (c) {
            return a + b + c;
        };
    };
}

add(10)(20)(30);
```

Output:

```text
60
```

---

# 1. What is Currying?

Currying transforms:

```text
f(a, b, c)
```

into:

```text
f(a)(b)(c)
```

Each function receives one argument and returns another function until all required values are provided.

Conceptually:

```text
add(10)
   ↓
function waiting for b
   ↓
add(10)(20)
   ↓
function waiting for c
   ↓
add(10)(20)(30)
   ↓
60
```

---

# 2. Normal Function

A normal function can receive multiple arguments:

```javascript
function multiply(a, b, c) {
    return a * b * c;
}

console.log(multiply(2, 3, 4));
```

Output:

```text
24
```

---

# 3. Curried Function

The same function can be written using currying:

```javascript
function multiply(a) {
    return function (b) {
        return function (c) {
            return a * b * c;
        };
    };
}

console.log(multiply(2)(3)(4));
```

Output:

```text
24
```

---

# 4. Arrow Function Syntax

Currying is often written with arrow functions.

```javascript
const multiply = (a) => (b) => (c) => {
    return a * b * c;
};

console.log(multiply(2)(3)(4));
```

Output:

```text
24
```

A shorter version:

```javascript
const multiply = a => b => c => a * b * c;
```

---

# 5. How Currying Works

Consider:

```javascript
const add = a => b => c => a + b + c;
```

Calling:

```javascript
add(10);
```

returns a function.

Then:

```javascript
add(10)(20);
```

returns another function.

Finally:

```javascript
add(10)(20)(30);
```

returns:

```text
60
```

The functions remember previous arguments through **closures**.

---

# 6. Currying and Closures

Currying and closures are closely related.

```javascript
const add = (a) => {
    return (b) => {
        return (c) => {
            return a + b + c;
        };
    };
};
```

The inner functions can access:

```text
a
b
```

from their outer scopes.

This works because of JavaScript closures.

Conceptually:

```text
add(10)
   ↓
closure remembers a = 10
   ↓
(20)
   ↓
closure remembers b = 20
   ↓
(30)
   ↓
result
```

---

# 7. Partial Application vs Currying

These concepts are related but not exactly the same.

### Currying

Converts a multi-argument function into chained single-argument functions.

```javascript
const add = a => b => c => a + b + c;

add(10)(20)(30);
```

### Partial Application

Creates a new function with some arguments already fixed.

```javascript
function multiply(a, b) {
    return a * b;
}

const double = (b) => multiply(2, b);

console.log(double(5));
```

Output:

```text
10
```

Here:

```text
a = 2
```

has already been fixed.

---

# 8. Simple Partial Application

```javascript
function calculateTax(rate, price) {
    return price * rate;
}

const tax13 = (price) => {
    return calculateTax(0.13, price);
};

console.log(tax13(1000));
```

Output:

```text
130
```

The tax rate is fixed once.

---

# 9. Practical Example — Tax Calculator

Currying can make configurable functions.

```javascript
const calculateTax = (rate) => (price) => {
    return price * rate;
};

const calculateVAT = calculateTax(0.13);

console.log(calculateVAT(1000));
console.log(calculateVAT(2000));
```

Output:

```text
130
260
```

Instead of repeatedly providing:

```text
0.13
```

we configure the function once.

---

# 10. Practical Example — Discount Calculator

```javascript
const calculateDiscount = (discountRate) => (price) => {
    return price - price * discountRate;
};

const tenPercentOff = calculateDiscount(0.10);
const twentyPercentOff = calculateDiscount(0.20);

console.log(tenPercentOff(1000));
console.log(twentyPercentOff(1000));
```

Output:

```text
900
800
```

This is useful when the same configuration is reused.

---

# 11. Practical Example — Greeting

```javascript
const createGreeting = (greeting) => (name) => {
    return `${greeting}, ${name}!`;
};

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

The first function configures the greeting.

The second function supplies the name.

---

# 12. Practical Example — Logger

```javascript
const createLogger = (level) => (message) => {
    console.log(`[${level}] ${message}`);
};

const info = createLogger("INFO");
const error = createLogger("ERROR");

info("Server started");
error("Database connection failed");
```

Output:

```text
[INFO] Server started
[ERROR] Database connection failed
```

---

# 13. Practical Example — API URL

Currying can also be used for API configuration.

```javascript
const createApiUrl = (baseURL) => (endpoint) => {
    return `${baseURL}${endpoint}`;
};

const apiUrl = createApiUrl(
    "https://example.com/api"
);

console.log(apiUrl("/users"));
console.log(apiUrl("/products"));
```

Output:

```text
https://example.com/api/users
https://example.com/api/products
```

The base URL is configured once.

---

# 14. Currying with Three Arguments

Normal function:

```javascript
function calculate(a, b, c) {
    return a + b * c;
}
```

Curried version:

```javascript
const calculate = (a) => (b) => (c) => {
    return a + b * c;
};
```

Usage:

```javascript
calculate(10)(20)(2);
```

Output:

```text
50
```

Because:

```text
10 + 20 × 2
= 50
```

---

# 15. Currying with Four Arguments

Currying is not limited to three arguments.

```javascript
const calculate = (a) => (b) => (c) => (d) => {
    return a + b + c + d;
};

console.log(
    calculate(10)(20)(30)(40)
);
```

Output:

```text
100
```

---

# 16. Generic Curry Function

Instead of manually writing:

```javascript
(a) => (b) => (c) => ...
```

we can create a reusable `curry()` helper.

```javascript
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn(...args);
        }

        return (...nextArgs) => {
            return curried(...args, ...nextArgs);
        };
    };
}
```

Now:

```javascript
function add(a, b, c) {
    return a + b + c;
}

const curriedAdd = curry(add);
```

You can use:

```javascript
curriedAdd(10)(20)(30);
```

Output:

```text
60
```

---

# 17. Generic Curry with Different Call Styles

A good curry helper can support multiple argument groups.

```javascript
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn(...args);
        }

        return (...nextArgs) => {
            return curried(...args, ...nextArgs);
        };
    };
}
```

Example:

```javascript
function add(a, b, c) {
    return a + b + c;
}

const sum = curry(add);
```

Different calls:

```javascript
sum(1)(2)(3);

sum(1, 2)(3);

sum(1)(2, 3);

sum(1, 2, 3);
```

All produce:

```text
6
```

This is useful when building reusable functional utilities.

---

# 18. Currying with Array Methods

Curried functions can be passed to array methods.

```javascript
const greaterThan = (minimum) => (value) => {
    return value > minimum;
};

const greaterThan100 = greaterThan(100);

const prices = [50, 120, 200, 80];

const result = prices.filter(greaterThan100);

console.log(result);
```

Output:

```text
[120, 200]
```

This makes the condition reusable.

---

# 19. Currying with `map()`

```javascript
const multiplyBy = (factor) => (value) => {
    return value * factor;
};

const double = multiplyBy(2);

const numbers = [1, 2, 3, 4];

const result = numbers.map(double);

console.log(result);
```

Output:

```text
[2, 4, 6, 8]
```

The function:

```javascript
double
```

can be reused anywhere a transformation function is required.

---

# 20. Currying with `filter()`

```javascript
const isGreaterThan = (limit) => (value) => {
    return value > limit;
};

const isGreaterThan50 = isGreaterThan(50);

const numbers = [20, 60, 80, 30];

const result = numbers.filter(
    isGreaterThan50
);

console.log(result);
```

Output:

```text
[60, 80]
```

---

# 21. Currying with Objects

Suppose we have products:

```javascript
const products = [
    {
        name: "Laptop",
        category: "electronics"
    },
    {
        name: "Shirt",
        category: "clothing"
    },
    {
        name: "Mouse",
        category: "electronics"
    }
];
```

Create a reusable category filter:

```javascript
const byCategory = (category) => (product) => {
    return product.category === category;
};

const electronics = byCategory("electronics");

const result = products.filter(electronics);

console.log(result);
```

This is useful for reusable filtering logic.

---

# 22. Currying and Configuration

Currying is useful when some values stay constant while another value changes.

Example:

```javascript
const formatPrice = (currency) => (price) => {
    return `${currency}${price.toFixed(2)}`;
};

const formatUSD = formatPrice("$");
const formatNPR = formatPrice("Rs. ");

console.log(formatUSD(100));
console.log(formatNPR(100));
```

Output:

```text
$100.00
Rs. 100.00
```

---

# 23. Currying in Functional Programming

Currying is common in functional programming because it makes functions easier to compose and reuse.

For example:

```javascript
const multiplyBy = (factor) => (value) => {
    return value * factor;
};

const double = multiplyBy(2);
const triple = multiplyBy(3);
```

Then:

```javascript
[1, 2, 3].map(double);
```

or:

```javascript
[1, 2, 3].map(triple);
```

The same function factory can create different reusable operations.

---

# 24. Currying vs Normal Functions

| Feature                | Normal Function  | Curried Function      |
| ---------------------- | ---------------- | --------------------- |
| Arguments              | Multiple at once | Usually one at a time |
| Syntax                 | `add(a, b)`      | `add(a)(b)`           |
| Reusability            | Normal           | Easy to specialize    |
| Configuration          | Usually repeated | Can be fixed early    |
| Closures               | Optional         | Commonly involved     |
| Functional programming | Useful           | Very common           |

---

# 25. Currying vs Partial Application

| Concept             | Meaning                                            |
| ------------------- | -------------------------------------------------- |
| Currying            | Converts arguments into a sequence of functions    |
| Partial application | Pre-fills some arguments                           |
| Closure             | Allows functions to remember surrounding variables |

Example currying:

```javascript
const add = a => b => a + b;

add(10)(20);
```

Example partial application:

```javascript
const add10 = (b) => add(10)(b);

add10(20);
```

Both can create reusable specialized functions.

---

# 26. Important Rules

When working with currying, remember:

### 1. Each stage usually receives one argument

```javascript
add(10)(20)(30);
```

### 2. Each stage returns another function until the final value is available

```javascript
const add = a => b => c => a + b + c;
```

### 3. Closures preserve previous values

```javascript
const add10 = add(10);
```

`add10` remembers:

```text
a = 10
```

### 4. Currying is optional

You do not need to curry every function.

A normal function may be clearer:

```javascript
add(10, 20);
```

instead of:

```javascript
add(10)(20);
```

---

# 27. When to Use Currying

Currying can be useful when:

* A function has reusable configuration.
* The same first argument is used repeatedly.
* You want specialized functions.
* You are working with functional programming.
* You want reusable predicates for `filter()`.
* You want reusable transformations for `map()`.
* You are composing functions.

Example:

```javascript
const isAbove = (limit) => (value) => {
    return value > limit;
};

const isAbove100 = isAbove(100);
```

---

# 28. When Not to Use Currying

Avoid unnecessary currying when it makes code harder to understand.

Instead of:

```javascript
const calculate = a => b => c => d => {
    return a + b + c + d;
};
```

a normal function may be easier:

```javascript
function calculate(a, b, c, d) {
    return a + b + c + d;
}
```

Use the style that makes the code easiest to read and maintain.

---

# 29. Currying with Default Parameters

Be careful when using a generic curry helper with default parameters.

Example:

```javascript
function greet(name, message = "Hello") {
    return `${message}, ${name}`;
}
```

Function metadata such as:

```javascript
greet.length
```

does not count parameters after the first parameter with a default value.

Therefore, generic currying based on `fn.length` can behave differently than expected.

For simple learning examples, use functions with required parameters:

```javascript
function add(a, b, c) {
    return a + b + c;
}
```

---

# 30. Currying with Rest Parameters

A generic curry helper may use:

```javascript
(...args)
```

to collect arguments.

Example:

```javascript
const collect = (...values) => {
    return values;
};

console.log(collect(10, 20, 30));
```

Output:

```text
[10, 20, 30]
```

Rest parameters and currying are separate concepts, but they are often used together when implementing generic curry utilities.

---

# 31. Practical Full Example — Product Price

Suppose an application needs to calculate a final product price after discount and tax.

```javascript
const applyDiscount = (discountRate) => (price) => {
    return price - price * discountRate;
};

const applyTax = (taxRate) => (price) => {
    return price + price * taxRate;
};

const discount10 = applyDiscount(0.10);
const tax13 = applyTax(0.13);

const discountedPrice = discount10(1000);
const finalPrice = tax13(discountedPrice);

console.log(finalPrice);
```

The functions can be reused for many products.

---

# 32. Practical Full Example — User Permission

```javascript
const hasRole = (requiredRole) => (user) => {
    return user.role === requiredRole;
};

const isAdmin = hasRole("admin");

const users = [
    {
        name: "Sandip",
        role: "admin"
    },
    {
        name: "Ram",
        role: "waiter"
    },
    {
        name: "Hari",
        role: "admin"
    }
];

const admins = users.filter(isAdmin);

console.log(admins);
```

The reusable function:

```javascript
isAdmin
```

can be used anywhere an admin filter is needed.

---

# 33. Currying and Composition

Currying can make functions easier to combine.

Example:

```javascript
const addTax = (rate) => (price) => {
    return price + price * rate;
};

const addDiscount = (rate) => (price) => {
    return price - price * rate;
};

const tax13 = addTax(0.13);
const discount10 = addDiscount(0.10);

const price = 1000;

const discounted = discount10(price);
const finalPrice = tax13(discounted);

console.log(finalPrice);
```

Each function performs one specific operation.

This style can make larger applications easier to organize when used appropriately.

---

# 34. Common Currying Pattern

```javascript
const functionName = (firstValue) => {
    return (secondValue) => {
        return (thirdValue) => {
            return result;
        };
    };
};
```

Arrow function shorthand:

```javascript
const functionName =
    firstValue =>
    secondValue =>
    thirdValue =>
    result;
```

Usage:

```javascript
functionName(value1)(value2)(value3);
```

---

# 35. Key Takeaways

* Currying transforms a multi-argument function into a sequence of functions.
* A curried function commonly uses the syntax:

  ```javascript
  fn(a)(b)(c)
  ```
* Each stage returns another function until the final result is produced.
* Closures allow curried functions to remember previous arguments.
* Currying is useful for creating specialized reusable functions.
* Partial application is related but different from currying.
* Curried functions work well with `map()`, `filter()`, and other higher-order functions.
* Currying is common in functional programming.
* Currying should not be used everywhere.
* Readability should come before clever syntax.
* Generic curry helpers commonly use `fn.length` to determine how many required parameters remain.
* Default parameters can make `fn.length` unsuitable for some generic curry implementations.

---

# Quick Cheat Sheet

```text
Normal:

add(a, b, c)


Curried:

add(a)(b)(c)
```

Example:

```javascript
const add = a => b => c => {
    return a + b + c;
};

console.log(add(10)(20)(30));
// 60
```

Specialized function:

```javascript
const add10 = add(10);
```

Then:

```javascript
add10(20)(30);
// 60
```

The main idea:

```text
Multiple arguments
       ↓
One argument at a time
       ↓
Reusable specialized functions
       ↓
Final result
```

---

# Next

Continue with:

```text
16-Advanced-JavaScript/
├── 01-Closures.md
├── 02-Currying.md
└── 03-Memoization.md
```
