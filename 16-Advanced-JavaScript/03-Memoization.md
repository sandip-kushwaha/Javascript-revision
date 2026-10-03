# JavaScript Memoization

**Memoization** is an optimization technique where a function stores previously calculated results and reuses them when the same input appears again.

Instead of calculating the same result repeatedly:

```text
Input
  ↓
Check cache
  ↓
Already calculated?
  ├── Yes → Return saved result
  └── No  → Calculate → Store → Return
```

Memoization is useful when:

* A function is expensive to calculate.
* The same inputs occur repeatedly.
* The function is deterministic.
* Performance needs improvement.

---

# 1. Basic Example

Without memoization:

```javascript
function square(number) {
    console.log("Calculating...");

    return number * number;
}

console.log(square(5));
console.log(square(5));
console.log(square(5));
```

The calculation happens every time.

With memoization:

```javascript
function memoizedSquare() {
    const cache = new Map();

    return function (number) {
        if (cache.has(number)) {
            return cache.get(number);
        }

        console.log("Calculating...");

        const result = number * number;

        cache.set(number, result);

        return result;
    };
}

const square = memoizedSquare();

console.log(square(5));
console.log(square(5));
console.log(square(5));
```

The first call calculates the result.

Later calls can use the cached value.

---

# 2. How Memoization Works

Consider:

```javascript
const square = memoizedSquare();

square(5);
```

First call:

```text
5
 ↓
Cache?
 ↓
No
 ↓
Calculate 25
 ↓
Store 5 → 25
 ↓
Return 25
```

Second call:

```text
5
 ↓
Cache?
 ↓
Yes
 ↓
Return 25
```

The expensive calculation does not need to run again.

---

# 3. Cache

A cache stores previously calculated values.

Example:

```javascript
const cache = new Map();

cache.set(5, 25);

console.log(cache.get(5));
```

Output:

```text
25
```

Memoization uses a cache to connect:

```text
Input → Result
```

---

# 4. Simple Memoization Function

```javascript
function memoize(fn) {
    const cache = new Map();

    return function (value) {
        if (cache.has(value)) {
            return cache.get(value);
        }

        const result = fn(value);

        cache.set(value, result);

        return result;
    };
}
```

Use it:

```javascript
function square(number) {
    console.log("Calculating...");

    return number * number;
}

const memoizedSquare = memoize(square);

console.log(memoizedSquare(10));
console.log(memoizedSquare(10));
```

Output:

```text
Calculating...
100
100
```

The calculation happens only once for `10`.

---

# 5. Memoization with Multiple Arguments

Suppose:

```javascript
function add(a, b) {
    return a + b;
}
```

A cache needs to identify both:

```text
a
b
```

One simple approach is to create a key.

```javascript
function memoizeAdd(fn) {
    const cache = new Map();

    return function (a, b) {
        const key = `${a}:${b}`;

        if (cache.has(key)) {
            return cache.get(key);
        }

        const result = fn(a, b);

        cache.set(key, result);

        return result;
    };
}
```

Use:

```javascript
const add = memoizeAdd((a, b) => {
    console.log("Calculating...");
    return a + b;
});

console.log(add(10, 20));
console.log(add(10, 20));
```

Output:

```text
Calculating...
30
30
```

---

# 6. Generic Memoization

A more flexible implementation can serialize arguments into a cache key.

```javascript
function memoize(fn) {
    const cache = new Map();

    return function (...args) {
        const key = JSON.stringify(args);

        if (cache.has(key)) {
            return cache.get(key);
        }

        const result = fn(...args);

        cache.set(key, result);

        return result;
    };
}
```

Example:

```javascript
function multiply(a, b) {
    console.log("Calculating...");

    return a * b;
}

const memoizedMultiply = memoize(multiply);

console.log(memoizedMultiply(5, 10));
console.log(memoizedMultiply(5, 10));
```

Output:

```text
Calculating...
50
50
```

---

# 7. Memoization and Pure Functions

Memoization works best with **pure functions**.

A pure function:

* Produces the same output for the same input.
* Does not depend on changing external state.
* Does not produce unexpected side effects.

Example:

```javascript
function square(number) {
    return number * number;
}
```

For:

```javascript
square(5);
```

the result is always:

```text
25
```

This makes it a good candidate for memoization.

---

# 8. Why Pure Functions Matter

Consider:

```javascript
let taxRate = 0.13;

function calculateTax(price) {
    return price * taxRate;
}
```

The result depends on external state:

```javascript
taxRate
```

If the tax rate changes:

```javascript
taxRate = 0.15;
```

then:

```javascript
calculateTax(1000);
```

returns a different result.

Caching the previous result without considering the changing tax rate could produce incorrect behavior.

A better design is:

```javascript
function calculateTax(price, taxRate) {
    return price * taxRate;
}
```

Now all important inputs are explicit.

---

# 9. Memoization with Recursion

Memoization is especially useful for recursive algorithms.

Consider Fibonacci:

```javascript
function fibonacci(n) {
    if (n <= 1) {
        return n;
    }

    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

This performs repeated calculations.

For example:

```text
fib(5)
 ├── fib(4)
 │    ├── fib(3)
 │    └── fib(2)
 └── fib(3)
      ├── fib(2)
      └── fib(1)
```

Some values are calculated multiple times.

Memoization can avoid this repeated work.

---

# 10. Memoized Fibonacci

```javascript
function fibonacci() {
    const cache = new Map();

    function calculate(n) {
        if (n <= 1) {
            return n;
        }

        if (cache.has(n)) {
            return cache.get(n);
        }

        const result =
            calculate(n - 1) +
            calculate(n - 2);

        cache.set(n, result);

        return result;
    }

    return calculate;
}

const fib = fibonacci();

console.log(fib(10));
```

Output:

```text
55
```

The cache stores previously calculated Fibonacci values.

---

# 11. Memoization with `Map`

`Map` is commonly useful for memoization.

```javascript
const cache = new Map();

function square(number) {
    if (cache.has(number)) {
        return cache.get(number);
    }

    const result = number * number;

    cache.set(number, result);

    return result;
}
```

Important methods:

```javascript
cache.has(key);
cache.get(key);
cache.set(key, value);
```

---

# 12. Memoization with `WeakMap`

For object-based keys, `WeakMap` can sometimes be useful.

```javascript
const cache = new WeakMap();

function processUser(user) {
    if (cache.has(user)) {
        return cache.get(user);
    }

    const result = {
        id: user.id,
        name: user.name
    };

    cache.set(user, result);

    return result;
}
```

`WeakMap` is useful when the cache should not keep an object key alive solely because it is stored in the cache.

---

# 13. Object Identity Matters

Consider:

```javascript
const user1 = {
    id: 1
};

const user2 = {
    id: 1
};
```

These are different objects.

```javascript
user1 === user2;
```

returns:

```text
false
```

Therefore:

```javascript
const cache = new WeakMap();

cache.set(user1, "Result");

console.log(cache.has(user1));
console.log(cache.has(user2));
```

Output:

```text
true
false
```

The keys are compared by object identity.

---

# 14. Memoization and `JSON.stringify()`

A simple generic memoizer can use:

```javascript
JSON.stringify(args);
```

Example:

```javascript
function memoize(fn) {
    const cache = new Map();

    return function (...args) {
        const key = JSON.stringify(args);

        if (cache.has(key)) {
            return cache.get(key);
        }

        const result = fn(...args);

        cache.set(key, result);

        return result;
    };
}
```

This is convenient but not perfect.

Potential issues include:

* Object property ordering considerations.
* Unsupported JSON values.
* Circular references.
* Large serialization cost.
* Different objects representing the same logical data.
* Functions and special values not being represented as expected.

For complex applications, choose the cache-key strategy carefully.

---

# 15. Memoization with Objects

Consider:

```javascript
function getFullName(user) {
    return `${user.firstName} ${user.lastName}`;
}
```

You could use a `WeakMap`:

```javascript
function memoizeObject(fn) {
    const cache = new WeakMap();

    return function (object) {
        if (cache.has(object)) {
            return cache.get(object);
        }

        const result = fn(object);

        cache.set(object, result);

        return result;
    };
}
```

Usage:

```javascript
const getFullName = memoizeObject(
    (user) => `${user.firstName} ${user.lastName}`
);

const user = {
    firstName: "Sandip",
    lastName: "Kushwaha"
};

console.log(getFullName(user));
console.log(getFullName(user));
```

The same object reference can reuse the cached result.

---

# 16. Memoization vs Caching

These concepts are related.

### Caching

A general technique for storing data so it can be reused later.

Examples:

```text
Browser cache
API response cache
Database cache
Image cache
Memory cache
```

### Memoization

A specific optimization technique where function results are cached based on input.

```text
Function input
     ↓
Cache
     ↓
Previously calculated?
     ↓
Return stored result
```

So:

```text
Memoization is a type of caching.
```

---

# 17. Memoization vs Local Storage

Memoization normally stores data in memory:

```javascript
const cache = new Map();
```

The data is available while the JavaScript process/runtime keeps the cache.

`localStorage` stores string data in browser storage:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

They solve different problems.

| Memoization                  | localStorage                |
| ---------------------------- | --------------------------- |
| Function-result optimization | Persistent browser storage  |
| Usually memory-based         | Browser storage             |
| Fast repeated calculations   | Save data across page loads |
| Often temporary              | Can persist until removed   |
| Based on function inputs     | Based on keys               |

---

# 18. Memoization and React

React provides tools that can perform memoization-related optimizations.

One example is:

```javascript
useMemo()
```

Example:

```jsx
const filteredProducts = useMemo(() => {
    return products.filter(
        product => product.price > 500
    );
}, [products]);
```

The calculation can be reused until dependencies change.

Another React feature is:

```javascript
useCallback()
```

which memoizes a function reference based on dependencies.

Example:

```jsx
const handleClick = useCallback(() => {
    console.log("Clicked");
}, []);
```

These tools should be used when they solve an actual rendering or computation problem, not automatically everywhere.

---

# 19. `useMemo()` vs General Memoization

General JavaScript memoization:

```javascript
const memoizedFunction = memoize(expensiveFunction);
```

React:

```javascript
const result = useMemo(
    () => expensiveFunction(data),
    [data]
);
```

The concepts are related, but React's hooks operate within React's rendering model.

---

# 20. Memoization Example — Expensive Calculation

Imagine:

```javascript
function calculateReport(data) {
    console.log("Generating report...");

    // Expensive processing
    return data
        .filter(item => item.active)
        .reduce((total, item) => {
            return total + item.amount;
        }, 0);
}
```

If the same data and computation are repeatedly requested, memoization can avoid unnecessary recalculation.

Conceptually:

```text
Same input
    ↓
Cached result
    ↓
Reuse result
```

---

# 21. Memoization with a Search Function

Suppose searching a large dataset is expensive:

```javascript
function searchProducts(products, keyword) {
    return products.filter(product => {
        return product.name
            .toLowerCase()
            .includes(keyword.toLowerCase());
    });
}
```

A memoized version could reuse previous searches:

```javascript
const memoizedSearch = memoize(
    searchProducts
);
```

Then:

```javascript
memoizedSearch(products, "laptop");
```

can potentially reuse a cached result when the same inputs are requested again.

However, if `products` is recreated as a new array each time, a simple reference-based cache may not recognize it as the same input.

---

# 22. Important: Input Identity

Consider:

```javascript
const products = [
    { name: "Laptop" }
];
```

Calling:

```javascript
search(products);
```

again with the same array reference can be treated differently from:

```javascript
search([
    { name: "Laptop" }
]);
```

The second array is a different object.

```javascript
products === [
    { name: "Laptop" }
];
```

returns:

```text
false
```

Therefore, memoization strategy must consider whether equality should mean:

```text
Same reference
```

or:

```text
Same values
```

---

# 23. Cache Size

A cache can grow indefinitely if new inputs are continuously added.

Example:

```javascript
function memoize(fn) {
    const cache = new Map();

    return function (value) {
        if (cache.has(value)) {
            return cache.get(value);
        }

        const result = fn(value);

        cache.set(value, result);

        return result;
    };
}
```

If thousands or millions of unique values are passed, the cache can become large.

For long-running applications, consider:

* Cache limits
* Expiration
* Eviction
* LRU caches
* WeakMap for suitable object-key cases

---

# 24. LRU Cache Concept

**LRU = Least Recently Used**

An LRU cache removes entries that have not been used recently.

Conceptually:

```text
Cache
│
├── Most recently used
├── Recently used
├── ...
└── Least recently used → removed
```

This prevents unlimited cache growth.

JavaScript does not provide a built-in general-purpose LRU cache class, but it can be implemented or provided by libraries.

---

# 25. Memoization with Expiration

Sometimes cached results should only remain valid for a period.

Conceptually:

```javascript
const cache = new Map();

cache.set(key, {
    value: result,
    expiresAt: Date.now() + 60000
});
```

Before returning the cached result:

```javascript
const cached = cache.get(key);

if (
    cached &&
    cached.expiresAt > Date.now()
) {
    return cached.value;
}
```

This is useful when results become stale.

---

# 26. Memoization and API Requests

Memoization can sometimes be used for API requests, but API caching has additional concerns.

For example:

```javascript
const cache = new Map();

async function getUser(id) {
    if (cache.has(id)) {
        return cache.get(id);
    }

    const response = await fetch(
        `/api/users/${id}`
    );

    const data = await response.json();

    cache.set(id, data);

    return data;
}
```

Now repeated requests for the same ID can reuse the cached result.

However, real applications must consider:

* Stale data
* Cache expiration
* Authentication
* Errors
* Mutations
* Concurrent requests
* Memory usage

---

# 27. Cache Errors Carefully

Suppose:

```javascript
async function getUser(id) {
    const response = await fetch(
        `/api/users/${id}`
    );

    if (!response.ok) {
        throw new Error("Failed to fetch user");
    }

    return response.json();
}
```

Do not blindly cache failed requests as successful data.

A cache strategy should clearly distinguish:

```text
Successful result
Failed request
Expired result
Missing result
```

---

# 28. Memoizing Promises

For asynchronous operations, you can cache the Promise itself.

```javascript
const cache = new Map();

function getUser(id) {
    if (cache.has(id)) {
        return cache.get(id);
    }

    const promise = fetch(`/api/users/${id}`)
        .then(response => {
            if (!response.ok) {
                throw new Error("Request failed");
            }

            return response.json();
        });

    cache.set(id, promise);

    return promise;
}
```

Now simultaneous calls can share the same in-flight Promise.

---

# 29. Handling Failed Promise Cache Entries

A rejected Promise should not necessarily remain cached forever.

For example:

```javascript
const cache = new Map();

function getUser(id) {
    if (cache.has(id)) {
        return cache.get(id);
    }

    const promise = fetch(`/api/users/${id}`)
        .then(response => {
            if (!response.ok) {
                throw new Error("Request failed");
            }

            return response.json();
        })
        .catch(error => {
            cache.delete(id);
            throw error;
        });

    cache.set(id, promise);

    return promise;
}
```

If the request fails:

```text
cache entry
     ↓
removed
     ↓
future request can try again
```

---

# 30. Memoization and Side Effects

Memoization should be used carefully with functions that have side effects.

Avoid blindly memoizing:

```javascript
function sendEmail(user) {
    // sends an actual email
}
```

If the result is cached, calling:

```javascript
sendEmail(user);
```

again may not perform the expected side effect.

Memoization is most suitable for computations where reusing the previous result is safe.

---

# 31. Good Memoization Candidates

Good candidates often include:

```text
Expensive mathematical calculations
Recursive algorithms
Large data transformations
Repeated filtering
Repeated parsing
Derived calculations
Pure functions
```

Examples:

```javascript
calculateStatistics(data);

calculateTotals(items);

fibonacci(n);

expensiveTransformation(data);
```

---

# 32. Poor Memoization Candidates

Be careful with:

```text
Random values
Current time
Functions with important side effects
Rapidly changing data
Functions with unique inputs every time
Very cheap calculations
```

For example:

```javascript
Math.random();
```

should not normally be memoized because each call is expected to produce a new random value.

Similarly:

```javascript
Date.now();
```

depends on the current time.

---

# 33. Memoization Has a Cost

Memoization is not always faster.

There is overhead for:

```text
Cache lookup
Cache storage
Cache key generation
Memory usage
Cache maintenance
```

For a very cheap function:

```javascript
function add(a, b) {
    return a + b;
}
```

memoization could actually make the code slower or unnecessarily complex.

---

# 34. Memoization Trade-Off

Without memoization:

```text
More computation
Less memory
```

With memoization:

```text
Less repeated computation
More memory
Cache management required
```

So memoization trades:

```text
Memory
   ↕
Computation
```

---

# 35. Simple Memoization Pattern

The general pattern is:

```javascript
function memoize(fn) {
    const cache = new Map();

    return function (...args) {
        const key = JSON.stringify(args);

        if (cache.has(key)) {
            return cache.get(key);
        }

        const result = fn(...args);

        cache.set(key, result);

        return result;
    };
}
```

Usage:

```javascript
const expensiveFunction = memoize(
    function (number) {
        return number * number;
    }
);

expensiveFunction(10);
expensiveFunction(10);
```

The second call can reuse the first result.

---

# 36. Memoization Flow

```text
Function call
      ↓
Create cache key
      ↓
Check cache
      ↓
 ┌────┴────┐
 ↓         ↓
Found     Not found
 ↓         ↓
Return    Calculate
cached       ↓
result     Store result
              ↓
           Return result
```

---

# 37. Memoization vs Debouncing

These concepts solve different problems.

### Memoization

Avoids repeated calculations:

```text
Same input
   ↓
Reuse previous result
```

### Debouncing

Controls how frequently a function runs:

```text
Many rapid calls
   ↓
Wait
   ↓
Run once after activity stops
```

Example:

```text
Memoization
→ cache expensive calculation

Debouncing
→ search input API request
```

They can also be used together in some applications.

---

# 38. Memoization vs Throttling

### Memoization

```text
Optimize repeated calculations
```

### Throttling

```text
Limit execution frequency
```

Example:

```text
Memoization
→ reuse result for same input

Throttling
→ execute at most once within a time interval
```

---

# 39. Practical Example — Hotel Order Total

Suppose a hotel application repeatedly calculates an order total.

```javascript
function calculateOrderTotal(items) {
    return items.reduce((total, item) => {
        return total + item.price * item.quantity;
    }, 0);
}
```

A memoized version could cache calculations when the same input representation is reused.

However, because arrays and objects are mutable, the application must carefully decide how to detect whether the order data has actually changed.

In React, derived values are often handled with tools such as:

```javascript
useMemo()
```

when appropriate.

---

# 40. Practical Example — Dashboard Statistics

Suppose a dashboard repeatedly calculates:

```text
Total orders
Total revenue
Completed orders
Pending orders
Average order value
```

If the underlying data has not changed, recomputing all statistics on every render may be unnecessary.

A memoized calculation can reuse derived results.

Conceptually:

```text
Orders
  ↓
Expensive calculation
  ↓
Cached statistics
  ↓
Reuse while inputs remain valid
```

The cache must be invalidated or bypassed when relevant data changes.

---

# 41. Key Takeaways

* Memoization caches function results.
* The same input can reuse a previously calculated result.
* `Map` is commonly used for in-memory memoization.
* `WeakMap` can be useful for object-keyed caches.
* Memoization works best with predictable, pure functions.
* Recursive algorithms can benefit significantly from memoization.
* Cache keys are important when functions have multiple arguments.
* `JSON.stringify()` is convenient but has limitations.
* Memoization uses additional memory.
* Unlimited caches can cause memory problems.
* Cache expiration and eviction can control cache growth.
* API request caching requires freshness and error-handling strategies.
* Promises themselves can sometimes be cached for request deduplication.
* Memoization is different from debouncing and throttling.
* React provides `useMemo()` for memoizing calculated values within React's rendering model.
* Memoization should be used when the optimization is useful, not automatically everywhere.

---

# Quick Cheat Sheet

```text
Memoization
     ↓
Cache previous function results
     ↓
Same input?
     ↓
Yes → return cached result
No  → calculate → cache → return
```

Basic example:

```javascript
function memoize(fn) {
    const cache = new Map();

    return function (value) {
        if (cache.has(value)) {
            return cache.get(value);
        }

        const result = fn(value);

        cache.set(value, result);

        return result;
    };
}
```

Usage:

```javascript
const square = memoize(
    number => number * number
);

square(5); // calculates
square(5); // cached
square(5); // cached
```

Remember:

```text
Memoization → reuse results
Debouncing  → wait before running
Throttling  → limit execution frequency
Caching     → general storage/reuse technique
```

---

