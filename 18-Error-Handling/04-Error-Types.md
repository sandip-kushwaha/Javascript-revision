# JavaScript Error Types

JavaScript provides several built-in error types.

Understanding these errors helps you:

* Debug applications
* Identify the cause of failures
* Handle errors correctly
* Write better validation
* Build reliable backend APIs

Common JavaScript errors include:

```text
Error
TypeError
ReferenceError
SyntaxError
RangeError
URIError
EvalError
AggregateError
```

---

# 1. Error

`Error` is the general-purpose error type.

```javascript
throw new Error("Something went wrong");
```

Handle it:

```javascript
try {
    throw new Error("Something went wrong");
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

Output:

```text
Error
Something went wrong
```

Use `Error` when no more specific built-in error type is appropriate.

---

# 2. Error Properties

An Error object commonly provides:

```javascript
const error = new Error("Something failed");

console.log(error.name);
console.log(error.message);
console.log(error.stack);
```

Important properties:

| Property  | Purpose                        |
| --------- | ------------------------------ |
| `name`    | Error type                     |
| `message` | Error description              |
| `stack`   | Debugging stack trace          |
| `cause`   | Underlying error when provided |

Example:

```javascript
const error = new Error("Database failed");

console.log(error.name);
// Error

console.log(error.message);
// Database failed
```

---

# 3. TypeError

A `TypeError` occurs when an operation is performed on a value of an inappropriate type.

Example:

```javascript
const user = null;

console.log(user.name);
```

This produces a `TypeError`.

Handle it:

```javascript
try {
    const user = null;

    console.log(user.name);
} catch (error) {
    console.log(error.name);
}
```

Output:

```text
TypeError
```

---

# 4. Common TypeError Examples

## Calling a non-function

```javascript
const value = 10;

value();
```

The value is a number, not a function.

---

## Accessing a property from null

```javascript
const user = null;

user.name;
```

---

## Accessing a property from undefined

```javascript
let user;

user.name;
```

These operations can produce:

```text
TypeError
```

---

# 5. Preventing Some TypeErrors

Optional chaining can safely access potentially missing properties.

Instead of:

```javascript
console.log(user.address.city);
```

use:

```javascript
console.log(
    user?.address?.city
);
```

This does not mean every TypeError should be hidden. Use optional chaining when missing values are expected and acceptable.

---

# 6. ReferenceError

A `ReferenceError` occurs when JavaScript cannot find a variable or identifier being referenced.

Example:

```javascript
console.log(username);
```

If `username` has not been declared, JavaScript throws:

```text
ReferenceError
```

---

# 7. ReferenceError Example

```javascript
try {
    console.log(username);
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

Possible output:

```text
ReferenceError
username is not defined
```

The exact message can vary between JavaScript engines.

---

# 8. ReferenceError and Scope

A variable may exist but be inaccessible because of scope.

```javascript
function test() {
    const message = "Hello";
}

console.log(message);
```

The `message` variable exists only inside the function.

The outside access can produce a `ReferenceError`.

---

# 9. SyntaxError

A `SyntaxError` occurs when JavaScript code does not follow valid syntax.

Example:

```javascript
const = 10;
```

This is invalid JavaScript syntax.

Another example:

```javascript
if (true {
    console.log("Hello");
}
```

The missing `)` creates invalid syntax.

---

# 10. SyntaxError and Parsing

Syntax errors normally happen while JavaScript is being parsed.

Because the code must be parsed before normal execution begins, this generally cannot be handled by putting the invalid source code directly inside the same `try...catch`.

For example, this is not valid:

```javascript
try {
    const = 10;
} catch (error) {
    console.log(error);
}
```

The JavaScript parser cannot successfully parse the program.

---

# 11. Runtime SyntaxError

Syntax errors can also occur when code is dynamically parsed.

For example:

```javascript
try {
    JSON.parse("{invalid}");
} catch (error) {
    console.log(error.name);
}
```

`JSON.parse()` throws a `SyntaxError` for invalid JSON.

Output:

```text
SyntaxError
```

---

# 12. RangeError

A `RangeError` occurs when a value is outside an allowed range.

Example:

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

Usage:

```javascript
try {
    setAge(150);
} catch (error) {
    console.log(error.name);
}
```

Output:

```text
RangeError
```

---

# 13. Another RangeError Example

JavaScript can produce a `RangeError` when certain operations exceed allowed limits.

For example, invalid array length:

```javascript
new Array(-1);
```

This produces a `RangeError`.

---

# 14. URIError

A `URIError` is related to invalid URI encoding or decoding operations.

Example:

```javascript
decodeURIComponent("%");
```

This can throw:

```text
URIError
```

Handle it:

```javascript
try {
    decodeURIComponent("%");
} catch (error) {
    console.log(error.name);
}
```

Output:

```text
URIError
```

---

# 15. URI Encoding

Common URI functions include:

```javascript
encodeURI()
decodeURI()

encodeURIComponent()
decodeURIComponent()
```

Example:

```javascript
const value =
    encodeURIComponent(
        "hello world"
    );

console.log(value);
```

Output:

```text
hello%20world
```

Invalid encoded data can result in a `URIError` during decoding.

---

# 16. EvalError

`EvalError` exists in the JavaScript specification but modern JavaScript engines generally do not use it for normal `eval()` failures.

Example:

```javascript
console.log(EvalError);
```

You may encounter the constructor, but typical application errors from `eval()` are generally `Error`, `SyntaxError`, or another relevant error type.

In normal application development, you usually do not need to create or handle `EvalError`.

---

# 17. AggregateError

`AggregateError` represents multiple errors together.

It is especially useful when several asynchronous operations can fail independently.

Example:

```javascript
const error = new AggregateError(
    [
        new Error("Database failed"),
        new Error("API failed")
    ],
    "Multiple operations failed"
);
```

Inspect it:

```javascript
console.log(error.name);
console.log(error.message);
console.log(error.errors);
```

Output:

```text
AggregateError
Multiple operations failed
```

---

# 18. Promise.any() and AggregateError

A common example is `Promise.any()`.

```javascript
Promise.any([
    Promise.reject(
        new Error("API 1 failed")
    ),
    Promise.reject(
        new Error("API 2 failed")
    )
])
.catch((error) => {
    console.log(error.name);
    console.log(error.errors);
});
```

If every Promise rejects, `Promise.any()` rejects with an `AggregateError`.

The individual errors are available through:

```javascript
error.errors
```

---

# 19. Error Inheritance

JavaScript error classes have an inheritance relationship.

Conceptually:

```text
Object
   ↓
Error
   ├── TypeError
   ├── ReferenceError
   ├── SyntaxError
   ├── RangeError
   ├── URIError
   ├── EvalError
   └── AggregateError
```

This means specialized errors are also Errors.

For example:

```javascript
const error =
    new TypeError("Invalid value");

console.log(
    error instanceof TypeError
);
```

Output:

```text
true
```

And:

```javascript
console.log(
    error instanceof Error
);
```

Output:

```text
true
```

---

# 20. `instanceof` with Error Types

You can identify specific error types:

```javascript
try {
    JSON.parse("invalid");
} catch (error) {
    if (error instanceof SyntaxError) {
        console.log("Invalid JSON");
    }
}
```

Another example:

```javascript
try {
    const user = null;

    console.log(user.name);
} catch (error) {
    if (error instanceof TypeError) {
        console.log(
            "Invalid property access"
        );
    }
}
```

---

# 21. Checking Multiple Error Types

```javascript
try {
    someOperation();
} catch (error) {
    if (error instanceof TypeError) {
        console.log("Type problem");
    } else if (
        error instanceof RangeError
    ) {
        console.log("Range problem");
    } else if (
        error instanceof ReferenceError
    ) {
        console.log("Reference problem");
    } else {
        console.log("Unknown error");
    }
}
```

This can be useful when different errors require different handling.

---

# 22. Error Type Comparison

| Error            | Common Meaning                                         |
| ---------------- | ------------------------------------------------------ |
| `Error`          | General error                                          |
| `TypeError`      | Invalid value type or operation                        |
| `ReferenceError` | Invalid or unavailable identifier                      |
| `SyntaxError`    | Invalid JavaScript syntax or dynamically parsed syntax |
| `RangeError`     | Value outside an allowed range                         |
| `URIError`       | Invalid URI encoding/decoding                          |
| `EvalError`      | Legacy/rare error type related to `eval`               |
| `AggregateError` | Multiple errors combined                               |

---

# 23. Error Types in Form Validation

Consider:

```javascript
function setQuantity(quantity) {
    if (
        typeof quantity !== "number"
    ) {
        throw new TypeError(
            "Quantity must be a number"
        );
    }

    if (
        quantity < 1 ||
        quantity > 10
    ) {
        throw new RangeError(
            "Quantity must be between 1 and 10"
        );
    }

    return quantity;
}
```

Here:

```text
Wrong type
    ↓
TypeError

Wrong range
    ↓
RangeError
```

This makes the error more descriptive.

---

# 24. Error Types in API Development

A backend API may use custom errors together with built-in errors.

For example:

```text
ValidationError
AuthenticationError
AuthorizationError
NotFoundError
ConflictError
DatabaseError
```

These application-specific errors can extend:

```javascript
Error
```

Example:

```javascript
class NotFoundError extends Error {
    constructor(message) {
        super(message);

        this.name = "NotFoundError";
        this.statusCode = 404;
    }
}
```

This combines JavaScript's error system with application-specific behavior.

---

# 25. Error Types and HTTP Status Codes

JavaScript error types and HTTP status codes are different concepts.

For example:

```text
TypeError
```

is a JavaScript error type.

While:

```text
400
404
500
```

are HTTP status codes.

An application may map an application error to an HTTP response.

Example:

```javascript
class NotFoundError extends Error {
    constructor(message) {
        super(message);

        this.statusCode = 404;
    }
}
```

The custom property connects application logic to the HTTP response layer.

---

# 26. Operational vs Programming Errors

In backend applications, it is useful to distinguish expected application failures from unexpected programming failures.

### Operational examples

```text
User not found
Invalid input
Unauthorized request
Duplicate email
Database temporarily unavailable
```

### Programming errors

```text
Undefined variable
Incorrect function call
Unexpected null access
Logic bug
Invalid application state
```

The exact classification depends on the application's architecture.

Custom errors can help make this distinction clearer.

---

# 27. Error Cause

Modern JavaScript allows one error to reference another error as its cause.

```javascript
try {
    JSON.parse("invalid");
} catch (originalError) {
    throw new Error(
        "Could not load configuration",
        {
            cause: originalError
        }
    );
}
```

The new error contains:

```javascript
error.cause
```

which points to the original error.

This is useful when errors pass through multiple application layers.

---

# 28. Logging Error Types

During development:

```javascript
try {
    JSON.parse("invalid");
} catch (error) {
    console.error({
        name: error.name,
        message: error.message,
        stack: error.stack
    });
}
```

This gives useful debugging information without needing to print unrelated application data.

---

# 29. Never Assume Every Error Has the Same Type

Avoid code such as:

```javascript
catch (error) {
    console.log(
        error.statusCode
    );
}
```

Not every JavaScript `Error` has a `statusCode`.

A safer approach is:

```javascript
catch (error) {
    const statusCode =
        error.statusCode || 500;

    console.log(statusCode);
}
```

Or use a known custom error hierarchy.

---

# 30. Error Type Flow

A typical application can work like this:

```text
Operation
    ↓
Error occurs
    ↓
Identify error type
    ↓
Handle expected error
    ↓
Log unexpected error
    ↓
Return appropriate response
```

For an API:

```text
Request
   ↓
Controller
   ↓
Service
   ↓
Database
   ↓
Error
   ↓
Central Error Middleware
   ↓
HTTP Response
```

---

# 31. Practical Backend Example

```javascript
class NotFoundError extends Error {
    constructor(message) {
        super(message);

        this.name = "NotFoundError";
        this.statusCode = 404;
    }
}

async function getUser(id) {
    const user = await User.findById(id);

    if (!user) {
        throw new NotFoundError(
            "User not found"
        );
    }

    return user;
}
```

Controller:

```javascript
const getUserController =
    async (req, res, next) => {
        try {
            const user =
                await getUser(req.params.id);

            res.json(user);
        } catch (error) {
            next(error);
        }
    };
```

Error middleware:

```javascript
const errorHandler =
    (error, req, res, next) => {
        const statusCode =
            error.statusCode || 500;

        res.status(statusCode).json({
            success: false,
            message: error.message
        });
    };
```

This creates a clean separation between:

```text
Business logic
Error creation
HTTP response
```

---

# 32. Common Mistakes

## Mistake 1 — Treating every error as TypeError

Not every failure is a `TypeError`.

Use the appropriate error type when the distinction matters.

---

## Mistake 2 — Confusing ReferenceError and TypeError

Example:

```javascript
console.log(user);
```

If `user` was never declared:

```text
ReferenceError
```

But:

```javascript
const user = null;

console.log(user.name);
```

produces:

```text
TypeError
```

---

## Mistake 3 — Confusing SyntaxError with Runtime Errors

Invalid JavaScript syntax is generally detected during parsing.

Runtime errors happen while valid JavaScript is executing.

---

## Mistake 4 — Assuming `fetch()` errors are always HTTP errors

A network failure can reject `fetch()`, while a normal HTTP response such as `404` does not automatically cause a rejected Promise.

Check:

```javascript
response.ok
```

when appropriate.

---

# 33. Quick Error Type Guide

```text
Error
│
├── TypeError
│   └── Wrong type / invalid operation
│
├── ReferenceError
│   └── Identifier cannot be found
│
├── SyntaxError
│   └── Invalid syntax / dynamically parsed syntax
│
├── RangeError
│   └── Value outside valid range
│
├── URIError
│   └── Invalid URI encoding/decoding
│
├── EvalError
│   └── Legacy / rarely used
│
└── AggregateError
    └── Multiple errors
```

---

# 34. Quick Cheat Sheet

```javascript
// General
throw new Error("Something failed");

// Type
throw new TypeError("Invalid type");

// Reference
// Usually produced when an identifier cannot be found.

// Syntax
// Usually produced when JavaScript syntax is invalid.

// Range
throw new RangeError("Value out of range");

// URI
decodeURIComponent("%");

// Multiple errors
new AggregateError(
    [
        new Error("Failed 1"),
        new Error("Failed 2")
    ],
    "Multiple operations failed"
);
```

---

# 35. Key Takeaways

* JavaScript has several built-in error types.
* `Error` is the general-purpose error type.
* `TypeError` usually indicates an inappropriate type or operation.
* `ReferenceError` indicates that an identifier cannot be resolved.
* `SyntaxError` indicates invalid JavaScript syntax or dynamically parsed syntax.
* `RangeError` indicates a value outside an allowed range.
* `URIError` is related to invalid URI encoding or decoding.
* `EvalError` exists but is rarely relevant in modern application development.
* `AggregateError` represents multiple errors together.
* Specialized errors inherit from `Error`.
* `instanceof` can be used to identify error types.
* Custom application errors can extend `Error` or a base custom error class.
* JavaScript error types and HTTP status codes are different concepts.
* `cause` can preserve the original error when wrapping another error.
* Error classification helps large applications handle failures consistently.
