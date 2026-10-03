# JavaScript throw

The `throw` statement is used to **manually create and raise an error**.

Instead of waiting for JavaScript to generate an error automatically, you can use `throw` when your application detects an invalid condition.

Basic syntax:

```javascript
throw new Error("Something went wrong");
```

---

# 1. Basic throw

```javascript
throw new Error("Something went wrong");
```

When JavaScript reaches this statement, execution stops at that point and the error is propagated to the nearest suitable error handler.

---

# 2. throw with try...catch

`throw` is commonly used together with `try...catch`.

```javascript
try {
    throw new Error("Something went wrong");
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Something went wrong
```

Flow:

```text
throw
  ↓
Error created
  ↓
catch receives error
  ↓
Error handled
```

---

# 3. Why Use throw?

Use `throw` when your application detects an invalid condition.

Common situations:

```text
Invalid user input
Missing required data
Unauthorized access
Invalid configuration
Business rule violation
Invalid API response
Resource not found
```

Example:

```javascript
function createUser(name) {
    if (!name) {
        throw new Error("Name is required");
    }

    return {
        name
    };
}
```

---

# 4. Throwing an Error

The recommended approach is to throw an `Error` object.

```javascript
throw new Error("Invalid username");
```

Then handle it:

```javascript
try {
    throw new Error("Invalid username");
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

Output:

```text
Error
Invalid username
```

---

# 5. Throwing Different Error Types

JavaScript provides built-in error classes.

Examples:

```text
Error
TypeError
ReferenceError
RangeError
SyntaxError
URIError
```

You can throw them manually.

```javascript
throw new TypeError("Expected a number");
```

Example:

```javascript
try {
    throw new TypeError("Age must be a number");
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

---

# 6. TypeError

Use `TypeError` when a value has an inappropriate type.

```javascript
function calculateAge(age) {
    if (typeof age !== "number") {
        throw new TypeError(
            "Age must be a number"
        );
    }

    return age;
}
```

Example:

```javascript
try {
    calculateAge("22");
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Age must be a number
```

---

# 7. RangeError

Use `RangeError` when a value is outside an allowed range.

```javascript
function setAge(age) {
    if (age < 0 || age > 120) {
        throw new RangeError(
            "Age must be between 0 and 120"
        );
    }

    return age;
}
```

Example:

```javascript
try {
    setAge(150);
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

Output:

```text
RangeError
Age must be between 0 and 120
```

---

# 8. Custom Validation with throw

```javascript
function registerUser(username, password) {
    if (!username) {
        throw new Error(
            "Username is required"
        );
    }

    if (!password) {
        throw new Error(
            "Password is required"
        );
    }

    return {
        username,
        password
    };
}
```

Usage:

```javascript
try {
    const user = registerUser(
        "Sandip",
        ""
    );

    console.log(user);
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Password is required
```

---

# 9. throw Stops the Current Flow

Consider:

```javascript
function test() {
    console.log("Before");

    throw new Error("Failed");

    console.log("After");
}

try {
    test();
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Before
Failed
```

This code does not execute:

```javascript
console.log("After");
```

because `throw` immediately interrupts the current execution path.

---

# 10. throw Inside a Condition

```javascript
function withdraw(balance, amount) {
    if (amount <= 0) {
        throw new Error(
            "Amount must be greater than zero"
        );
    }

    if (amount > balance) {
        throw new Error(
            "Insufficient balance"
        );
    }

    return balance - amount;
}
```

Usage:

```javascript
try {
    const balance = withdraw(1000, 1500);

    console.log(balance);
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Insufficient balance
```

---

# 11. Multiple throw Conditions

A function can contain multiple validation conditions.

```javascript
function createProduct(name, price) {
    if (!name) {
        throw new Error(
            "Product name is required"
        );
    }

    if (price <= 0) {
        throw new Error(
            "Price must be greater than zero"
        );
    }

    return {
        name,
        price
    };
}
```

Only the first failing condition reached during execution throws an error.

---

# 12. throw in Authentication

Backend applications commonly validate authentication data.

```javascript
function requireUser(user) {
    if (!user) {
        throw new Error(
            "Authentication required"
        );
    }

    return user;
}
```

Usage:

```javascript
try {
    const user = requireUser(null);

    console.log(user);
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Authentication required
```

In a real Express application, authentication errors are usually passed to centralized middleware rather than handled directly in every controller.

---

# 13. throw in Authorization

Authentication and authorization are different.

Example:

```javascript
function requireAdmin(user) {
    if (user.role !== "admin") {
        throw new Error(
            "Admin access required"
        );
    }
}
```

This can enforce an application-level rule before continuing.

For HTTP APIs, the final response might use an appropriate status such as `403 Forbidden`.

---

# 14. throw with JSON Parsing

```javascript
function parseUser(data) {
    try {
        return JSON.parse(data);
    } catch (error) {
        throw new Error(
            "User data contains invalid JSON"
        );
    }
}
```

Usage:

```javascript
try {
    const user = parseUser(
        '{"name":"Sandip"}'
    );

    console.log(user);
} catch (error) {
    console.log(error.message);
}
```

---

# 15. Rethrowing an Error

Sometimes a lower-level function should not completely handle an error.

It can rethrow it.

```javascript
function parseData(data) {
    try {
        return JSON.parse(data);
    } catch (error) {
        console.error(
            "Parsing failed:",
            error.message
        );

        throw error;
    }
}
```

The original error continues to the caller.

---

# 16. Rethrowing with More Context

Instead of rethrowing the exact error, you can create a new error.

```javascript
function loadUser(data) {
    try {
        return JSON.parse(data);
    } catch (error) {
        throw new Error(
            `Failed to load user data: ${error.message}`
        );
    }
}
```

This adds useful application context.

---

# 17. Preserve the Original Error

When wrapping an error, modern JavaScript allows you to specify the original error as the `cause`.

```javascript
try {
    JSON.parse("invalid");
} catch (error) {
    throw new Error(
        "Could not process user data",
        {
            cause: error
        }
    );
}
```

The original error can then be accessed through:

```javascript
try {
    // operation
} catch (error) {
    console.log(error.cause);
}
```

This is useful when building layered applications.

---

# 18. throw and return Are Different

`return` sends a value back to the caller.

```javascript
function getValue() {
    return 100;
}
```

`throw` signals an error condition.

```javascript
function getValue() {
    throw new Error("Value unavailable");
}
```

Comparison:

| `return`                            | `throw`                  |
| ----------------------------------- | ------------------------ |
| Returns a value                     | Raises an error          |
| Normal execution                    | Exceptional execution    |
| Caller receives result              | Caller must handle error |
| Does not indicate failure by itself | Indicates failure        |

---

# 19. throw vs console.error

These are not the same.

`console.error()` only logs information:

```javascript
console.error("Something went wrong");
```

`throw` actually raises an error:

```javascript
throw new Error(
    "Something went wrong"
);
```

Example:

```javascript
function test() {
    console.error("Failed");

    console.log("Still running");
}
```

Output:

```text
Failed
Still running
```

But:

```javascript
function test() {
    throw new Error("Failed");

    console.log("Still running");
}
```

The second statement is not reached.

---

# 20. throw and Validation

Validation functions often use `throw`.

```javascript
function validateUser(user) {
    if (!user) {
        throw new Error(
            "User is required"
        );
    }

    if (!user.email) {
        throw new Error(
            "Email is required"
        );
    }

    if (!user.password) {
        throw new Error(
            "Password is required"
        );
    }

    return true;
}
```

Usage:

```javascript
try {
    validateUser({
        email: "sandip@example.com",
        password: "123456"
    });

    console.log("Valid user");
} catch (error) {
    console.log(error.message);
}
```

---

# 21. Throwing from a Function

A function can throw an error to its caller.

```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error(
            "Cannot divide by zero"
        );
    }

    return a / b;
}
```

The caller decides how to handle it:

```javascript
try {
    const result = divide(10, 0);

    console.log(result);
} catch (error) {
    console.log(error.message);
}
```

This creates a useful separation:

```text
Function
   ↓
Detects problem
   ↓
throw
   ↓
Caller
   ↓
Handles problem
```

---

# 22. throw Across Function Calls

Errors can travel through multiple function calls until a suitable `catch` handles them.

```javascript
function third() {
    throw new Error("Something failed");
}

function second() {
    third();
}

function first() {
    second();
}

try {
    first();
} catch (error) {
    console.log(error.message);
}
```

Output:

```text
Something failed
```

Flow:

```text
first()
  ↓
second()
  ↓
third()
  ↓
throw
  ↓
catch
```

---

# 23. Custom Error Class

For larger applications, you can create custom error classes.

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);

        this.name = "ValidationError";
    }
}
```

Use it:

```javascript
throw new ValidationError(
    "Email is required"
);
```

Handle it:

```javascript
try {
    throw new ValidationError(
        "Email is required"
    );
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

Output:

```text
ValidationError
Email is required
```

---

# 24. Custom HTTP Error

A backend application may use an error class containing an HTTP status.

```javascript
class ApiError extends Error {
    constructor(
        statusCode,
        message
    ) {
        super(message);

        this.name = "ApiError";
        this.statusCode = statusCode;
    }
}
```

Example:

```javascript
throw new ApiError(
    404,
    "User not found"
);
```

Then centralized Express error handling can use:

```javascript
app.use((error, req, res, next) => {
    const statusCode =
        error.statusCode || 500;

    res.status(statusCode).json({
        message: error.message
    });
});
```

This pattern is common in Node.js and Express applications.

---

# 25. Don't Throw Strings

Technically, JavaScript allows:

```javascript
throw "Something went wrong";
```

But this is not recommended.

Prefer:

```javascript
throw new Error(
    "Something went wrong"
);
```

Why?

An `Error` object provides useful properties such as:

```text
name
message
stack
cause
```

when applicable.

---

# 26. Don't Throw Random Values

Avoid:

```javascript
throw 500;
```

or:

```javascript
throw {
    message: "Failed"
};
```

Prefer:

```javascript
throw new Error("Failed");
```

or an appropriate custom error class.

---

# 27. Throwing a TypeError

```javascript
function setUsername(username) {
    if (typeof username !== "string") {
        throw new TypeError(
            "Username must be a string"
        );
    }

    return username;
}
```

Usage:

```javascript
try {
    setUsername(123);
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

---

# 28. Throwing a RangeError

```javascript
function setQuantity(quantity) {
    if (quantity < 1 || quantity > 10) {
        throw new RangeError(
            "Quantity must be between 1 and 10"
        );
    }

    return quantity;
}
```

Usage:

```javascript
try {
    setQuantity(20);
} catch (error) {
    console.log(error.message);
}
```

---

# 29. throw in a Hotel Application

For a hotel management system:

```javascript
function validateTableCapacity(capacity) {
    if (
        capacity < 1 ||
        capacity > 10
    ) {
        throw new RangeError(
            "Table capacity must be between 1 and 10"
        );
    }

    return capacity;
}
```

Controller:

```javascript
try {
    const capacity =
        validateTableCapacity(
            req.body.capacity
        );

    console.log(capacity);
} catch (error) {
    console.error(error);

    res.status(400).json({
        message: error.message
    });
}
```

This keeps validation logic separate from the controller.

---

# 30. throw in a Service Layer

A cleaner backend architecture can use:

```text
Controller
    ↓
Service
    ↓
Database
```

The service can throw:

```javascript
async function getUserById(id) {
    const user = await User.findById(id);

    if (!user) {
        throw new Error(
            "User not found"
        );
    }

    return user;
}
```

The controller can handle the error:

```javascript
try {
    const user = await getUserById(
        req.params.id
    );

    res.json(user);
} catch (error) {
    res.status(404).json({
        message: error.message
    });
}
```

In a larger Express application, this can instead be passed to centralized error middleware.

---

# 31. throw and async Functions

An error thrown inside an `async` function causes the function's returned Promise to reject.

```javascript
async function getUser() {
    throw new Error(
        "User not found"
    );
}
```

Handle it with:

```javascript
try {
    await getUser();
} catch (error) {
    console.log(error.message);
}
```

Or:

```javascript
getUser()
    .catch((error) => {
        console.log(error.message);
    });
```

---

# 32. throw and API Validation

Example:

```javascript
function validateOrder(order) {
    if (!order.tableId) {
        throw new Error(
            "Table ID is required"
        );
    }

    if (!order.items?.length) {
        throw new Error(
            "Order must contain items"
        );
    }

    return true;
}
```

Usage:

```javascript
try {
    validateOrder(req.body);

    console.log("Order is valid");
} catch (error) {
    console.log(error.message);
}
```

---

# 33. Error Propagation

When an error is thrown, JavaScript searches for an appropriate error handler.

```text
Function A
    ↓
Function B
    ↓
Function C
    ↓
throw
    ↓
Does C have catch?
    ↓ No
Does B have catch?
    ↓ No
Does A have catch?
    ↓ Yes
Handle error
```

This is called **error propagation**.

---

# 34. Throwing After Validation

A useful pattern is:

```javascript
function createOrder(order) {
    if (!order.tableId) {
        throw new Error(
            "Table is required"
        );
    }

    if (!order.items?.length) {
        throw new Error(
            "Order items are required"
        );
    }

    return {
        ...order,
        status: "pending"
    };
}
```

The function either:

```text
returns valid data
```

or:

```text
throws an error
```

---

# 35. Best Practices

### Use Error objects

Prefer:

```javascript
throw new Error("Failed");
```

instead of:

```javascript
throw "Failed";
```

### Use specific error classes when useful

```javascript
TypeError
RangeError
ValidationError
ApiError
```

### Add useful context

```javascript
throw new Error(
    "Failed to create user"
);
```

### Let higher layers handle errors when appropriate

A service does not always need to send an HTTP response.

Keep responsibilities separate:

```text
Service
    → detects / throws error

Controller
    → handles application response

Error Middleware
    → centralizes unexpected errors
```

### Do not expose sensitive information

Avoid sending:

```text
Passwords
Database credentials
JWT secrets
Internal stack traces
Private configuration
```

to clients in production.

---

# 36. throw Cheat Sheet

```javascript
// Basic error
throw new Error("Something went wrong");

// Type error
throw new TypeError("Invalid type");

// Range error
throw new RangeError("Value out of range");

// Custom error
throw new ValidationError("Invalid data");

// With cause
throw new Error(
    "Operation failed",
    {
        cause: originalError
    }
);
```

---

# 37. throw vs try...catch

They have different responsibilities.

| Feature   | Purpose                |
| --------- | ---------------------- |
| `throw`   | Create/raise an error  |
| `try`     | Run code that may fail |
| `catch`   | Handle an error        |
| `finally` | Perform cleanup        |
| `Error`   | Represent an error     |

Typical flow:

```text
try
 ↓
operation
 ↓
problem?
 ↓
throw
 ↓
catch
 ↓
handle
```

---

# 38. Key Takeaways

* `throw` manually raises an error.
* `throw new Error()` is the normal approach.
* `throw` immediately interrupts the current execution path.
* Errors can propagate through multiple function calls.
* A caller can catch an error thrown by another function.
* `TypeError` is useful for invalid value types.
* `RangeError` is useful for values outside an allowed range.
* Custom error classes are useful in larger applications.
* `Error` objects provide useful debugging information.
* Avoid throwing strings or arbitrary values.
* `throw` and `console.error()` are different.
* `return` produces a normal result; `throw` signals failure.
* Errors inside `async` functions reject their returned Promise.
* Backend services can throw errors while controllers or centralized middleware handle responses.
* Do not expose sensitive internal error information to clients in production.
