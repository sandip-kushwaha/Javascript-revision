# JavaScript Custom Errors

Custom errors allow you to create your own error types for specific situations in an application.

Instead of using generic:

```javascript
throw new Error("Something went wrong");
```

you can create meaningful errors such as:

```text
ValidationError
AuthenticationError
AuthorizationError
NotFoundError
DatabaseError
ApiError
```

Custom errors are especially useful in larger applications such as:

* Node.js
* Express
* REST APIs
* Authentication systems
* Database applications
* Full-stack applications

---

# 1. Why Custom Errors?

A generic error:

```javascript
throw new Error("User not found");
```

contains a message, but the application may also need to know:

```text
What type of error?
What HTTP status?
What operation failed?
Should the error be exposed to the client?
```

A custom error can store this additional information.

Example:

```javascript
throw new NotFoundError("User not found");
```

Now the application can identify the error type separately from its message.

---

# 2. Creating a Custom Error

Custom errors are usually created by extending the built-in `Error` class.

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

---

# 3. Handling a Custom Error

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);

        this.name = "ValidationError";
    }
}

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

# 4. Why Extend Error?

The built-in `Error` class already provides useful behavior.

By using:

```javascript
class ValidationError extends Error
```

your custom error gets standard error properties such as:

```text
message
name
stack
cause
```

when applicable.

You can then add your own properties.

---

# 5. Adding Custom Properties

Example:

```javascript
class ApiError extends Error {
    constructor(statusCode, message) {
        super(message);

        this.name = "ApiError";
        this.statusCode = statusCode;
    }
}
```

Usage:

```javascript
throw new ApiError(
    404,
    "User not found"
);
```

Now the error contains:

```javascript
error.name;
error.message;
error.statusCode;
```

---

# 6. Checking Custom Error Properties

```javascript
try {
    throw new ApiError(
        404,
        "User not found"
    );
} catch (error) {
    console.log(error.name);
    console.log(error.message);
    console.log(error.statusCode);
}
```

Output:

```text
ApiError
User not found
404
```

---

# 7. ValidationError

A validation error represents invalid input.

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);

        this.name = "ValidationError";
        this.statusCode = 400;
    }
}
```

Example:

```javascript
function createUser(user) {
    if (!user.email) {
        throw new ValidationError(
            "Email is required"
        );
    }

    return user;
}
```

---

# 8. NotFoundError

A `NotFoundError` can represent a missing resource.

```javascript
class NotFoundError extends Error {
    constructor(message) {
        super(message);

        this.name = "NotFoundError";
        this.statusCode = 404;
    }
}
```

Example:

```javascript
function findUser(user) {
    if (!user) {
        throw new NotFoundError(
            "User not found"
        );
    }

    return user;
}
```

---

# 9. AuthenticationError

Authentication errors represent situations where the user cannot be authenticated.

```javascript
class AuthenticationError extends Error {
    constructor(message = "Authentication required") {
        super(message);

        this.name = "AuthenticationError";
        this.statusCode = 401;
    }
}
```

Usage:

```javascript
throw new AuthenticationError();
```

---

# 10. AuthorizationError

Authorization is different from authentication.

A user may be logged in but not allowed to perform an operation.

```javascript
class AuthorizationError extends Error {
    constructor(message = "Access denied") {
        super(message);

        this.name = "AuthorizationError";
        this.statusCode = 403;
    }
}
```

Usage:

```javascript
throw new AuthorizationError(
    "Admin access required"
);
```

---

# 11. DatabaseError

You can create a custom error for database-related failures.

```javascript
class DatabaseError extends Error {
    constructor(message) {
        super(message);

        this.name = "DatabaseError";
        this.statusCode = 500;
    }
}
```

Example:

```javascript
try {
    await User.findById(userId);
} catch (error) {
    throw new DatabaseError(
        "Failed to access user data"
    );
}
```

---

# 12. Base Application Error

Instead of defining every property repeatedly, create a base error class.

```javascript
class AppError extends Error {
    constructor(
        message,
        statusCode = 500
    ) {
        super(message);

        this.name = "AppError";
        this.statusCode = statusCode;
        this.isOperational = true;
    }
}
```

Now other errors can extend it.

---

# 13. Extending AppError

```javascript
class ValidationError extends AppError {
    constructor(message) {
        super(message, 400);

        this.name = "ValidationError";
    }
}
```

Another:

```javascript
class NotFoundError extends AppError {
    constructor(message) {
        super(message, 404);

        this.name = "NotFoundError";
    }
}
```

Now both errors share the same base behavior.

---

# 14. Complete Error Hierarchy

A common structure is:

```text
Error
  │
  └── AppError
       │
       ├── ValidationError
       ├── AuthenticationError
       ├── AuthorizationError
       ├── NotFoundError
       └── DatabaseError
```

This makes large applications easier to organize.

---

# 15. `isOperational`

A custom application error may contain:

```javascript
this.isOperational = true;
```

Example:

```javascript
class AppError extends Error {
    constructor(message, statusCode) {
        super(message);

        this.name = "AppError";
        this.statusCode = statusCode;
        this.isOperational = true;
    }
}
```

This can help distinguish expected application errors from unexpected programming errors.

For example:

```text
Expected:
User not found

Unexpected:
Cannot read properties of undefined
```

The exact error classification strategy depends on the application.

---

# 16. API Error Class

For REST APIs, a reusable API error is useful.

```javascript
class ApiError extends Error {
    constructor(
        statusCode,
        message,
        errors = []
    ) {
        super(message);

        this.name = "ApiError";
        this.statusCode = statusCode;
        this.errors = errors;
    }
}
```

Usage:

```javascript
throw new ApiError(
    400,
    "Invalid user data",
    [
        "Email is required",
        "Password is required"
    ]
);
```

---

# 17. Handling Validation Details

Suppose an API receives:

```javascript
const errors = [
    "Email is required",
    "Password is too short"
];
```

You can store them inside the error:

```javascript
class ValidationError extends AppError {
    constructor(message, errors = []) {
        super(message, 400);

        this.name = "ValidationError";
        this.errors = errors;
    }
}
```

Usage:

```javascript
throw new ValidationError(
    "Validation failed",
    errors
);
```

---

# 18. Express Error Middleware

A centralized Express error handler can inspect custom errors.

```javascript
const errorHandler = (
    error,
    req,
    res,
    next
) => {
    const statusCode =
        error.statusCode || 500;

    res.status(statusCode).json({
        success: false,
        message: error.message
    });
};
```

Register it after routes:

```javascript
app.use(errorHandler);
```

The custom error can then determine the response status.

---

# 19. Express Controller Example

Custom error:

```javascript
class NotFoundError extends AppError {
    constructor(message) {
        super(message, 404);

        this.name = "NotFoundError";
    }
}
```

Controller:

```javascript
const getUser = async (req, res, next) => {
    try {
        const user =
            await User.findById(req.params.id);

        if (!user) {
            throw new NotFoundError(
                "User not found"
            );
        }

        res.json(user);
    } catch (error) {
        next(error);
    }
};
```

Central middleware handles the response.

---

# 20. Using `instanceof`

You can check whether an error belongs to a custom class.

```javascript
try {
    throw new ValidationError(
        "Invalid email"
    );
} catch (error) {
    console.log(
        error instanceof ValidationError
    );
}
```

Output:

```text
true
```

You can also check the parent class:

```javascript
console.log(
    error instanceof AppError
);
```

If `ValidationError` extends `AppError`, this can also be `true`.

---

# 21. Handling Different Custom Errors

```javascript
try {
    createUser(data);
} catch (error) {
    if (error instanceof ValidationError) {
        console.log(
            "Validation failed"
        );
    } else if (
        error instanceof NotFoundError
    ) {
        console.log(
            "Resource not found"
        );
    } else {
        console.log(
            "Unexpected error"
        );
    }
}
```

For Express applications, centralized middleware is usually cleaner than repeating this logic in every controller.

---

# 22. Custom Error with `cause`

When wrapping an underlying error, preserve its cause.

```javascript
class DatabaseError extends AppError {
    constructor(message, options = {}) {
        super(message, 500);

        this.name = "DatabaseError";
        this.cause = options.cause;
    }
}
```

Usage:

```javascript
try {
    await User.findById(id);
} catch (error) {
    throw new DatabaseError(
        "Database operation failed",
        {
            cause: error
        }
    );
}
```

The original error remains available through:

```javascript
error.cause
```

---

# 23. Custom Error Factory

Sometimes a helper function is enough.

```javascript
function createApiError(
    statusCode,
    message
) {
    const error = new Error(message);

    error.statusCode = statusCode;

    return error;
}
```

Usage:

```javascript
throw createApiError(
    404,
    "User not found"
);
```

This is simpler than a custom class for small applications.

---

# 24. Custom Error Class vs Error Factory

| Custom Error Class           | Error Factory                  |
| ---------------------------- | ------------------------------ |
| Uses `class`                 | Uses a function                |
| Supports `instanceof`        | Usually checked by properties  |
| Good for many error types    | Good for simple cases          |
| Easier to build hierarchies  | Less boilerplate               |
| Useful in large applications | Useful in smaller applications |

Example class:

```javascript
class NotFoundError extends AppError {
    constructor(message) {
        super(message, 404);
    }
}
```

Example factory:

```javascript
function notFound(message) {
    const error = new Error(message);

    error.statusCode = 404;

    return error;
}
```

---

# 25. Custom Errors in a Hotel Management System

For a hotel backend, you might define:

```text
ValidationError
AuthenticationError
AuthorizationError
NotFoundError
ConflictError
SessionError
OrderError
DatabaseError
```

For example:

```javascript
class SessionError extends AppError {
    constructor(message) {
        super(message, 400);

        this.name = "SessionError";
    }
}
```

Usage:

```javascript
if (!session) {
    throw new SessionError(
        "Invalid or inactive table session"
    );
}
```

---

# 26. ConflictError

A conflict can occur when a resource already exists.

```javascript
class ConflictError extends AppError {
    constructor(message) {
        super(message, 409);

        this.name = "ConflictError";
    }
}
```

Example:

```javascript
if (existingUser) {
    throw new ConflictError(
        "Email already exists"
    );
}
```

---

# 27. Complete Backend Error File

A project may keep custom errors in:

```text
src/
├── errors/
│   ├── AppError.js
│   ├── ValidationError.js
│   ├── NotFoundError.js
│   ├── AuthenticationError.js
│   ├── AuthorizationError.js
│   └── ConflictError.js
```

Example `AppError.js`:

```javascript
class AppError extends Error {
    constructor(
        message,
        statusCode = 500
    ) {
        super(message);

        this.name = "AppError";
        this.statusCode = statusCode;
        this.isOperational = true;

        Error.captureStackTrace?.(
            this,
            this.constructor
        );
    }
}

export default AppError;
```

---

# 28. Reusable Error Classes

Example:

```javascript
class NotFoundError extends AppError {
    constructor(message = "Resource not found") {
        super(message, 404);

        this.name = "NotFoundError";
    }
}

class ValidationError extends AppError {
    constructor(message = "Validation failed") {
        super(message, 400);

        this.name = "ValidationError";
    }
}

class AuthenticationError extends AppError {
    constructor(
        message = "Authentication required"
    ) {
        super(message, 401);

        this.name = "AuthenticationError";
    }
}

class AuthorizationError extends AppError {
    constructor(message = "Access denied") {
        super(message, 403);

        this.name = "AuthorizationError";
    }
}
```

---

# 29. Centralized Error Response

A backend can standardize responses:

```javascript
const errorHandler = (
    error,
    req,
    res,
    next
) => {
    const statusCode =
        error.statusCode || 500;

    res.status(statusCode).json({
        success: false,
        statusCode,
        message: error.message
    });
};
```

Example response:

```json
{
    "success": false,
    "statusCode": 404,
    "message": "User not found"
}
```

---

# 30. Development vs Production

During development, detailed errors can help debugging:

```javascript
console.error(error.stack);
```

In production, avoid sending internal details to clients.

For example, do not expose:

```text
Database connection details
File system paths
Internal stack traces
Environment variables
JWT secrets
Passwords
```

A production response can instead be:

```json
{
    "success": false,
    "message": "Internal server error"
}
```

while the detailed error is logged securely on the server.

---

# 31. Custom Error Design

A good custom error usually contains:

```text
Error type
Message
Status code
Optional details
Optional cause
```

Example:

```javascript
class ApiError extends Error {
    constructor(
        statusCode,
        message,
        details = [],
        options = {}
    ) {
        super(message, options);

        this.name = "ApiError";
        this.statusCode = statusCode;
        this.details = details;
    }
}
```

Usage:

```javascript
throw new ApiError(
    400,
    "Validation failed",
    [
        "Email is required"
    ]
);
```

---

# 32. Error Structure

A useful application error can look like:

```text
ApiError
│
├── name
│     → ApiError
│
├── message
│     → User not found
│
├── statusCode
│     → 404
│
├── details
│     → Additional information
│
├── isOperational
│     → true
│
└── cause
      → Original error
```

---

# 33. Custom Errors vs Generic Errors

### Generic

```javascript
throw new Error(
    "User not found"
);
```

The application mainly has:

```text
message
```

### Custom

```javascript
throw new NotFoundError(
    "User not found"
);
```

The application can identify:

```text
Error type
HTTP status
Message
Operational status
Additional details
```

---

# 34. Recommended Project Structure

For an Express backend:

```text
src/
├── controllers/
├── routes/
├── services/
├── models/
├── middlewares/
├── errors/
│   ├── AppError.js
│   ├── ApiError.js
│   ├── ValidationError.js
│   ├── NotFoundError.js
│   ├── AuthenticationError.js
│   ├── AuthorizationError.js
│   └── ConflictError.js
└── app.js
```

This keeps error definitions separate from business logic.

---

# 35. Common Mistakes

## Mistake 1 — Extending the wrong class

Avoid:

```javascript
class ValidationError {
    constructor(message) {
        this.message = message;
    }
}
```

Prefer:

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);

        this.name = "ValidationError";
    }
}
```

---

## Mistake 2 — Forgetting `super()`

When extending `Error`, call:

```javascript
super(message);
```

before using `this`.

---

## Mistake 3 — Using the wrong status code

Do not automatically return `500` for every problem.

For example:

```text
400 → invalid request
401 → authentication required
403 → access denied
404 → resource not found
409 → conflict
500 → unexpected server error
```

The exact response depends on the application's semantics.

---

## Mistake 4 — Exposing internal errors

Avoid returning:

```javascript
res.json({
    stack: error.stack
});
```

to production clients.

---

# 36. Best Practices

### Use meaningful error names

```text
ValidationError
NotFoundError
AuthenticationError
AuthorizationError
```

### Keep error classes reusable

Do not create a new class for every single message.

### Keep HTTP concerns separate when appropriate

Business logic can throw an application error while middleware decides how to convert it into an HTTP response.

### Preserve the original cause

When wrapping an underlying error, use the `cause` option when useful.

### Centralize API error handling

Express middleware can provide consistent responses.

---

# 37. Quick Cheat Sheet

```javascript
// Base error
class AppError extends Error {
    constructor(message, statusCode = 500) {
        super(message);

        this.name = "AppError";
        this.statusCode = statusCode;
        this.isOperational = true;
    }
}

// Validation
class ValidationError extends AppError {
    constructor(message) {
        super(message, 400);

        this.name = "ValidationError";
    }
}

// Not found
class NotFoundError extends AppError {
    constructor(message) {
        super(message, 404);

        this.name = "NotFoundError";
    }
}

// Authentication
class AuthenticationError extends AppError {
    constructor(message) {
        super(message, 401);

        this.name = "AuthenticationError";
    }
}

// Authorization
class AuthorizationError extends AppError {
    constructor(message) {
        super(message, 403);

        this.name = "AuthorizationError";
    }
}

// Conflict
class ConflictError extends AppError {
    constructor(message) {
        super(message, 409);

        this.name = "ConflictError";
    }
```

---

# 38. Key Takeaways

* Custom errors are specialized error types created for application-specific situations.
* Extend the built-in `Error` class when creating custom error classes.
* Always call `super(message)` in an `Error` subclass constructor.
* Custom errors can contain properties such as `statusCode`, `details`, and `isOperational`.
* `ValidationError` can represent invalid input.
* `AuthenticationError` can represent authentication failures.
* `AuthorizationError` can represent access-control failures.
* `NotFoundError` can represent missing resources.
* `ConflictError` can represent resource conflicts.
* `DatabaseError` can represent database failures.
* `instanceof` can identify custom error types.
* A base `AppError` can reduce repeated error-class logic.
* Express error middleware can convert custom errors into consistent HTTP responses.
* Preserve underlying errors with `cause` when wrapping errors.
* Avoid exposing sensitive internal information in production.
* Custom errors are especially useful as an application grows.
