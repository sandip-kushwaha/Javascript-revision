# JavaScript Error Handling

## What is Error Handling?

**Error handling** is the process of detecting, handling, and responding to errors in a JavaScript application.

Errors can happen because of:

* invalid input
* missing data
* network failures
* API errors
* database failures
* incorrect code
* unavailable resources
* unexpected values

A good error-handling system prevents failures from becoming difficult-to-understand application problems.

---

# 1. Common Error Handling Tools

JavaScript provides several mechanisms:

```text
try...catch
throw
finally
Error
Custom Error Classes
Promise.catch()
async/await + try...catch
```

---

# 2. JavaScript Error Object

The basic error object is:

```js
const error = new Error("Something went wrong");
```

It contains useful information such as:

```js
console.log(error.name);
console.log(error.message);
console.log(error.stack);
```

Example:

```js
const error = new Error("Database connection failed");

console.log(error.name);
console.log(error.message);
```

Output:

```text
Error
Database connection failed
```

---

# 3. `throw`

Use `throw` to create an error intentionally.

```js
throw new Error("Invalid input");
```

Example:

```js
function withdraw(balance, amount) {
  if (amount > balance) {
    throw new Error("Insufficient balance");
  }

  return balance - amount;
}
```

Handle it:

```js
try {
  const result = withdraw(1000, 1500);

  console.log(result);
} catch (error) {
  console.error(error.message);
}
```

---

# 4. `throw` Can Throw Different Values

JavaScript technically allows throwing different values:

```js
throw "Something went wrong";
```

or:

```js
throw 404;
```

or:

```js
throw { message: "Failed" };
```

However, prefer throwing `Error` objects:

```js
throw new Error("Something went wrong");
```

This provides standard error information such as `name`, `message`, and `stack`.

---

# 5. Built-in Error Types

JavaScript provides several built-in error types.

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

# 6. `Error`

The general-purpose error:

```js
throw new Error("Something went wrong");
```

Use it when a more specific built-in type does not describe the problem.

---

# 7. `TypeError`

A `TypeError` occurs when a value is used in an inappropriate way.

Example:

```js
const user = null;

user.name;
```

This produces a `TypeError`.

Another example:

```js
const number = 10;

number.toUpperCase();
```

A number does not have a `toUpperCase()` method.

---

# 8. `ReferenceError`

A `ReferenceError` occurs when JavaScript cannot find the referenced variable or identifier.

```js
console.log(username);
```

If `username` was never declared, JavaScript throws a `ReferenceError`.

---

# 9. `SyntaxError`

A `SyntaxError` occurs when JavaScript code cannot be parsed correctly.

For example:

```js
const user = {
  name: "Sandip"
```

The object is incomplete.

Another common example:

```js
JSON.parse("{invalid}");
```

This throws a `SyntaxError`.

---

# 10. `RangeError`

A `RangeError` occurs when a value is outside an allowed range.

Example:

```js
const numbers = new Array(-1);
```

This causes a `RangeError`.

Another example:

```js
(10).toFixed(200);
```

The number of decimal places is outside the allowed range.

---

# 11. `URIError`

A `URIError` can occur when URI-related functions receive invalid input.

```js
decodeURIComponent("%");
```

This can throw a `URIError`.

---

# 12. `AggregateError`

`AggregateError` represents multiple errors.

It is commonly associated with:

```js
Promise.any()
```

Example:

```js
Promise.any([
  Promise.reject(new Error("Server 1 failed")),
  Promise.reject(new Error("Server 2 failed"))
])
.catch((error) => {
  console.log(error instanceof AggregateError);
  console.log(error.errors);
});
```

The `errors` property contains the individual errors.

---

# 13. Error Type Checking

You can check the error type using `instanceof`.

```js
try {
  JSON.parse("{invalid}");
} catch (error) {
  if (error instanceof SyntaxError) {
    console.log("Invalid JSON");
  }
}
```

Another example:

```js
try {
  null.toUpperCase();
} catch (error) {
  if (error instanceof TypeError) {
    console.log("Invalid value type");
  }
}
```

---

# 14. Handling Different Error Types

You can handle different errors separately:

```js
try {
  const data = JSON.parse(input);

  console.log(data.name.toUpperCase());
} catch (error) {
  if (error instanceof SyntaxError) {
    console.error("Invalid JSON");
  } else if (error instanceof TypeError) {
    console.error("Invalid data type");
  } else {
    console.error("Unknown error");
  }
}
```

This allows more specific responses.

---

# 15. Error Handling with `try...catch`

Basic structure:

```js
try {
  riskyOperation();
} catch (error) {
  handleError(error);
}
```

For asynchronous code:

```js
async function loadData() {
  try {
    const data = await getData();

    return data;
  } catch (error) {
    console.error(error);
  }
}
```

---

# 16. Error Handling with `finally`

```js
try {
  startOperation();
} catch (error) {
  handleError(error);
} finally {
  cleanup();
}
```

`finally` is useful when something must happen regardless of success or failure.

Examples:

* stop loading state
* close a resource
* release temporary state
* clean up listeners

---

# 17. Error Propagation

An error can move upward through function calls until something handles it.

Example:

```js
function database() {
  throw new Error("Database failed");
}

function service() {
  database();
}

function controller() {
  service();
}

try {
  controller();
} catch (error) {
  console.error(error.message);
}
```

Flow:

```text
controller()
    ↓
service()
    ↓
database()
    ↓
throw Error
    ↓
controller's caller
    ↓
catch
```

---

# 18. Rethrowing Errors

A function can catch an error, perform some local work, and rethrow it.

```js
function getUser() {
  try {
    return databaseQuery();
  } catch (error) {
    console.error("Database operation failed");

    throw error;
  }
}
```

The caller can then handle it:

```js
try {
  const user = getUser();
} catch (error) {
  console.error("Could not get user");
}
```

---

# 19. Adding Error Context

Instead of rethrowing the exact error:

```js
throw error;
```

you can add useful context:

```js
throw new Error(
  `Failed to load user: ${error.message}`
);
```

This can make logs easier to understand.

---

# 20. Preserve the Original Error

Modern JavaScript supports the `cause` option.

```js
try {
  await databaseQuery();
} catch (error) {
  throw new Error("Failed to load user", {
    cause: error
  });
}
```

Later:

```js
try {
  await getUser();
} catch (error) {
  console.log(error.message);
  console.log(error.cause);
}
```

This allows higher-level errors to keep the original error as context.

---

# 21. Custom Error Classes

Applications often need domain-specific errors.

Example:

```js
class ValidationError extends Error {
  constructor(message) {
    super(message);

    this.name = "ValidationError";
  }
}
```

Use it:

```js
throw new ValidationError("Email is required");
```

Handle it:

```js
try {
  throw new ValidationError("Email is required");
} catch (error) {
  console.log(error.name);
  console.log(error.message);
}
```

---

# 22. Custom Error for Not Found

```js
class NotFoundError extends Error {
  constructor(message = "Resource not found") {
    super(message);

    this.name = "NotFoundError";
  }
}
```

Use:

```js
throw new NotFoundError("User not found");
```

---

# 23. Custom Error for Authentication

```js
class AuthenticationError extends Error {
  constructor(message = "Authentication failed") {
    super(message);

    this.name = "AuthenticationError";
  }
}
```

Use:

```js
throw new AuthenticationError("Invalid credentials");
```

This makes the error type meaningful to the application.

---

# 24. Custom Error with Status Code

In a backend application, an error can contain an HTTP status code.

```js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);

    this.name = "AppError";
    this.statusCode = statusCode;
  }
}
```

Use:

```js
throw new AppError("User not found", 404);
```

Then:

```js
try {
  throw new AppError("User not found", 404);
} catch (error) {
  console.log(error.statusCode);
  console.log(error.message);
}
```

---

# 25. Express Error Handling

In Express, an application can use centralized error middleware.

Example:

```js
const errorHandler = (err, req, res, next) => {
  const statusCode = err.statusCode || 500;

  res.status(statusCode).json({
    success: false,
    message: err.message || "Internal Server Error"
  });
};
```

Register it after the routes:

```js
app.use(errorHandler);
```

---

# 26. Passing Errors to Express Middleware

A controller can pass an error to Express:

```js
const getUser = async (req, res, next) => {
  try {
    const user = await User.findById(req.params.id);

    if (!user) {
      throw new AppError("User not found", 404);
    }

    res.json({
      success: true,
      data: user
    });
  } catch (error) {
    next(error);
  }
};
```

Then the centralized error handler receives it.

```text
Controller
    ↓
next(error)
    ↓
Error Middleware
    ↓
HTTP Response
```

---

# 27. Async Error Handling in Express

A reusable async handler can reduce repeated `try...catch` blocks.

```js
const asyncHandler = (requestHandler) => {
  return (req, res, next) => {
    Promise.resolve(
      requestHandler(req, res, next)
    ).catch(next);
  };
};
```

Then:

```js
const getUsers = asyncHandler(async (req, res) => {
  const users = await User.find();

  res.json({
    success: true,
    data: users
  });
});
```

If the async function rejects, the error is passed to Express.

---

# 28. Promise Error Handling

Promises can handle errors using `.catch()`:

```js
getUser()
  .then((user) => {
    return getOrders(user.id);
  })
  .then((orders) => {
    console.log(orders);
  })
  .catch((error) => {
    console.error(error);
  });
```

Errors from the chain can propagate to the `catch`.

---

# 29. Async/Await Error Handling

With `async/await`:

```js
async function loadOrders() {
  try {
    const user = await getUser();

    const orders = await getOrders(user.id);

    return orders;
  } catch (error) {
    console.error(error);
  }
}
```

This is often easier to read when several operations depend on one another.

---

# 30. Network Error Handling

API requests can fail because of:

* no internet connection
* DNS problems
* server unavailable
* connection timeout
* request cancellation

Example:

```js
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    console.error("Network/API error:", error.message);

    throw error;
  }
}
```

---

# 31. HTTP Errors vs JavaScript Errors

These are not always the same thing.

For example:

```text
404 Not Found
```

is an HTTP response status.

A JavaScript `Error` object is a JavaScript runtime/application error.

With `fetch()`:

```js
const response = await fetch("/api/users");
```

a `404` normally still gives you a response.

Therefore:

```js
if (!response.ok) {
  throw new Error(`HTTP ${response.status}`);
}
```

converts the HTTP failure into a JavaScript exception.

---

# 32. Validation Errors

Input validation should happen before processing invalid data.

```js
function createUser(email) {
  if (!email) {
    throw new ValidationError("Email is required");
  }

  if (!email.includes("@")) {
    throw new ValidationError("Invalid email");
  }

  return {
    email
  };
}
```

Then:

```js
try {
  const user = createUser("");
} catch (error) {
  console.error(error.message);
}
```

---

# 33. Business Logic Errors

Not every application error is a programming error.

For example, in a hotel system:

```js
if (table.status !== "available") {
  throw new AppError(
    "Table is not available",
    409
  );
}
```

This is a business-rule failure.

Another example:

```js
if (!food.isAvailable) {
  throw new AppError(
    "Food is currently unavailable",
    409
  );
}
```

---

# 34. Authentication Errors

```js
if (!user) {
  throw new AppError(
    "Invalid email or password",
    401
  );
}
```

The application can then convert the error into an appropriate HTTP response.

---

# 35. Authorization Errors

Authentication and authorization are different.

Authentication:

```text
Who are you?
```

Authorization:

```text
Are you allowed to perform this action?
```

Example:

```js
if (user.role !== "admin") {
  throw new AppError(
    "You are not authorized",
    403
  );
}
```

---

# 36. Database Error Handling

Example:

```js
async function getUser(id) {
  try {
    const user = await User.findById(id);

    return user;
  } catch (error) {
    throw new AppError(
      "Failed to retrieve user",
      500,
      {
        cause: error
      }
    );
  }
}
```

The exact implementation of application error classes can vary.

---

# 37. Error Handling Layers

A backend application commonly has several layers:

```text
Request
   ↓
Route
   ↓
Controller
   ↓
Service
   ↓
Database
   ↓
Error
   ↓
Error Handler
   ↓
Response
```

Each layer can add useful context while allowing a centralized error handler to produce the final response.

---

# 38. Do Not Expose Sensitive Errors

Avoid sending internal details to clients:

```js
res.status(500).json({
  message: error.stack
});
```

A safer response is:

```js
res.status(500).json({
  success: false,
  message: "Internal server error"
});
```

Detailed stack traces should generally remain in server-side logs during development/operations.

---

# 39. Logging

A basic development example:

```js
console.error("Database error:", error);
```

For production applications, structured logging systems are often more appropriate than relying only on `console.log()`.

Useful information may include:

```text
timestamp
error type
message
request method
request path
user/request identifier where appropriate
stack trace
```

Avoid logging passwords, tokens, secrets, or other sensitive data.

---

# 40. Error Handling Strategy

A practical structure:

```text
Validation Error
       ↓
Business Error
       ↓
Database/API Error
       ↓
Catch / Propagate
       ↓
Central Error Handler
       ↓
Safe Client Response
       ↓
Detailed Server Log
```

---

# 41. Good Error Messages

Bad:

```js
throw new Error("Error");
```

Better:

```js
throw new Error("Failed to create order");
```

Even better when useful:

```js
throw new AppError(
  "Food item is unavailable",
  409
);
```

A useful error message should explain the problem without exposing sensitive internal information.

---

# 42. Error Handling Example

A complete simple backend pattern:

```js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);

    this.name = "AppError";
    this.statusCode = statusCode;
  }
}

const getUser = async (req, res, next) => {
  try {
    const user = await User.findById(req.params.id);

    if (!user) {
      throw new AppError("User not found", 404);
    }

    res.status(200).json({
      success: true,
      data: user
    });
  } catch (error) {
    next(error);
  }
};

const errorHandler = (error, req, res, next) => {
  const statusCode = error.statusCode || 500;

  res.status(statusCode).json({
    success: false,
    message: error.message || "Internal server error"
  });
};
```

The structure is:

```text
Controller
    ↓
try
    ↓
Error occurs
    ↓
catch
    ↓
next(error)
    ↓
errorHandler
    ↓
HTTP response
```

---

# 43. Error Handling Principles

### 1. Detect errors

```js
if (!user) {
  throw new AppError("User not found", 404);
}
```

### 2. Add useful context

```js
throw new Error(`Failed to load user: ${error.message}`);
```

### 3. Handle errors at the appropriate layer

```js
catch (error) {
  next(error);
}
```

### 4. Do not silently ignore important errors

```js
catch (error) {
  console.error(error);
}
```

### 5. Do not expose sensitive internal details

```js
message: "Internal server error"
```

### 6. Preserve useful original information

```js
new Error("Operation failed", {
  cause: error
});
```

---

# 44. Common Mistakes

## Ignoring Errors

```js
try {
  await saveData();
} catch {
}
```

This can hide failures.

---

## Exposing Stack Traces

```js
res.json({
  error: error.stack
});
```

Do not expose internal stack traces to normal users.

---

## Using Generic Errors Everywhere

```js
throw new Error("Something went wrong");
```

Specific application errors can provide better handling.

---

## Catching and Not Rethrowing

```js
try {
  await databaseOperation();
} catch (error) {
  console.error(error);
}
```

If the caller needs to know that the operation failed, rethrow or propagate the error.

---

# 45. Error Handling in a Hotel System

A hotel management system may have errors such as:

```text
ValidationError
    ↓
Invalid food quantity

AuthenticationError
    ↓
Invalid login

AuthorizationError
    ↓
Waiter tries admin-only operation

NotFoundError
    ↓
Food/table/order does not exist

ConflictError
    ↓
Table already occupied

DatabaseError
    ↓
Database operation failed
```

These can eventually be converted into appropriate HTTP responses.

---

# 46. Error Handling Mental Model

```text
              Application
                   │
                   ↓
              Operation
                   │
            ┌──────┴──────┐
            ↓             ↓
         Success        Error
            │             │
            │          Detect
            │             ↓
            │          Handle
            │             ↓
            │        Add context
            │             ↓
            │        Propagate
            │             ↓
            └──────→ Response
```

---

# 47. Key Takeaways

* Error handling makes applications more reliable and maintainable.
* `Error` is the standard JavaScript error object.
* Use `throw` to signal an error.
* Use `try...catch` to handle errors.
* Use `finally` for cleanup.
* JavaScript provides built-in error types such as `TypeError`, `ReferenceError`, and `SyntaxError`.
* Use `instanceof` when you need to distinguish error types.
* Custom error classes are useful for application-specific failures.
* Promises use `.catch()` for rejection handling.
* `async/await` works naturally with `try...catch`.
* HTTP errors and JavaScript exceptions are different concepts.
* `fetch()` does not normally reject just because the server returns `404` or `500`.
* Validate HTTP responses with `response.ok` when appropriate.
* Backend applications can use centralized error middleware.
* Rethrow errors when higher-level code needs to handle them.
* Use error causes when preserving the original failure is useful.
* Do not expose sensitive internal details to clients.
* Do not silently ignore important errors.
* Good error handling separates internal diagnostics from safe client responses.

## Simple Pattern

```js
async function operation() {
  try {
    const result = await doSomething();

    return result;
  } catch (error) {
    console.error("Operation failed:", error);

    throw error;
  } finally {
    cleanup();
  }
}
```
