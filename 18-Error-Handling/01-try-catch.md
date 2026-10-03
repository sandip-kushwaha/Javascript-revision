# JavaScript try...catch

`try...catch` is used to handle errors without stopping the entire JavaScript program.

It allows you to:

* Detect runtime errors
* Handle errors safely
* Show useful error messages
* Prevent application crashes
* Perform cleanup with `finally`

Basic structure:

```javascript
try {
    // code that may cause an error
} catch (error) {
    // handle the error
}
```

---

# 1. Basic try...catch

Example:

```javascript
try {
    console.log("Start");

    const result = 10 / 2;

    console.log(result);
} catch (error) {
    console.log("Something went wrong");
}
```

Output:

```text
Start
5
```

Because no error occurred, the `catch` block does not execute.

---

# 2. Handling an Error

Consider:

```javascript
try {
    console.log(user.name);
} catch (error) {
    console.log("An error occurred");
}
```

If `user` does not exist, JavaScript throws a `ReferenceError`.

Instead of stopping the program immediately, `catch` handles the error.

---

# 3. The catch Error Object

The `catch` block receives an error object.

```javascript
try {
    console.log(user.name);
} catch (error) {
    console.log(error);
}
```

The error object commonly contains:

```text
name
message
stack
```

---

# 4. error.name

`error.name` tells you the type of error.

```javascript
try {
    console.log(user.name);
} catch (error) {
    console.log(error.name);
}
```

Possible output:

```text
ReferenceError
```

---

# 5. error.message

`error.message` contains the error description.

```javascript
try {
    console.log(user.name);
} catch (error) {
    console.log(error.message);
}
```

Example output may look like:

```text
user is not defined
```

The exact message can vary between JavaScript engines.

---

# 6. error.stack

`error.stack` provides debugging information about where the error occurred.

```javascript
try {
    JSON.parse("invalid json");
} catch (error) {
    console.log(error.stack);
}
```

A stack trace can show:

```text
Error type
Error message
File location
Line information
Call path
```

For development, stack traces are very useful.

---

# 7. Complete Error Information

```javascript
try {
    JSON.parse("Hello");
} catch (error) {
    console.log("Name:", error.name);
    console.log("Message:", error.message);
    console.log("Stack:", error.stack);
}
```

This is useful when debugging.

---

# 8. try...catch with JSON.parse()

`JSON.parse()` throws an error when the input is invalid JSON.

```javascript
const data = '{"name":"Sandip"}';

try {
    const user = JSON.parse(data);

    console.log(user.name);
} catch (error) {
    console.log("Invalid JSON");
}
```

Output:

```text
Sandip
```

---

## Invalid JSON

```javascript
const data = '{"name":}';

try {
    const user = JSON.parse(data);

    console.log(user);
} catch (error) {
    console.log("Invalid JSON");
}
```

Output:

```text
Invalid JSON
```

---

# 9. try...catch Does Not Catch Every Kind of Failure

`try...catch` handles exceptions thrown during the execution of the `try` block.

For example:

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

However, an error that occurs asynchronously later needs to be handled in the appropriate asynchronous callback or Promise chain.

For example:

```javascript
try {
    setTimeout(() => {
        throw new Error("Async error");
    }, 1000);
} catch (error) {
    console.log("Caught");
}
```

The outer `catch` does not catch that later timer error.

For Promises, use:

```javascript
promise.catch(...)
```

or:

```javascript
try {
    await promise;
} catch (error) {
    // handle error
}
```

---

# 10. finally

`finally` runs whether an error occurs or not.

Syntax:

```javascript
try {
    // code
} catch (error) {
    // handle error
} finally {
    // cleanup
}
```

Example:

```javascript
try {
    console.log("Trying");
} catch (error) {
    console.log("Error");
} finally {
    console.log("Finished");
}
```

Output:

```text
Trying
Finished
```

---

# 11. finally When an Error Occurs

```javascript
try {
    throw new Error("Failed");
} catch (error) {
    console.log(error.message);
} finally {
    console.log("Cleanup complete");
}
```

Output:

```text
Failed
Cleanup complete
```

---

# 12. Why Use finally?

`finally` is useful for cleanup operations.

Common examples:

```text
Close a resource
Reset loading state
Release a lock
Stop a timer
Clean temporary state
Close a connection
```

Example:

```javascript
let loading = true;

try {
    console.log("Loading data...");
} catch (error) {
    console.log(error.message);
} finally {
    loading = false;
}
```

---

# 13. try...finally Without catch

You can use `try` with `finally` without `catch`.

```javascript
try {
    console.log("Start");
} finally {
    console.log("Cleanup");
}
```

Output:

```text
Start
Cleanup
```

If an error occurs, `finally` still runs before the error continues outward.

---

# 14. Nested try...catch

A `try...catch` can exist inside another `try` block.

```javascript
try {
    try {
        JSON.parse("invalid");
    } catch (error) {
        console.log("Inner error:", error.message);
    }

    console.log("Outer block continues");
} catch (error) {
    console.log("Outer error:", error.message);
}
```

The inner `catch` handles the JSON parsing error.

---

# 15. Rethrowing an Error

Sometimes you catch an error but decide that another part of the application should handle it.

You can throw it again.

```javascript
try {
    JSON.parse("invalid");
} catch (error) {
    console.log("Logging error");

    throw error;
}
```

The error is handled locally first and then passed to the outer error-handling system.

---

# 16. Rethrowing with Additional Context

You can create a new error with more useful information.

```javascript
try {
    JSON.parse("invalid");
} catch (error) {
    throw new Error(
        `Failed to process user data: ${error.message}`
    );
}
```

This can make errors easier to understand at higher application layers.

---

# 17. Optional Catch Binding

If you do not need the error object, you can omit it.

Instead of:

```javascript
try {
    riskyOperation();
} catch (error) {
    console.log("Operation failed");
}
```

You can write:

```javascript
try {
    riskyOperation();
} catch {
    console.log("Operation failed");
}
```

This is called **optional catch binding**.

---

# 18. Handling Different Errors

You can inspect `error.name` to handle different error types.

```javascript
try {
    JSON.parse("invalid");
} catch (error) {
    if (error.name === "SyntaxError") {
        console.log("Invalid JSON");
    } else {
        console.log("Unknown error");
    }
}
```

---

# 19. TypeError Example

```javascript
try {
    const user = null;

    console.log(user.name);
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

The operation attempts to access a property from `null`, which causes a `TypeError`.

---

# 20. ReferenceError Example

```javascript
try {
    console.log(username);
} catch (error) {
    console.log(error.name);
}
```

If `username` has not been declared, JavaScript throws a `ReferenceError`.

---

# 21. Syntax Errors

Syntax errors generally prevent code from being parsed successfully.

For example, malformed JavaScript such as:

```javascript
const = 10;
```

cannot normally be rescued by placing the same invalid syntax inside a `try` block because the program must first be parsed.

However, dynamically evaluated code can produce a syntax error at runtime:

```javascript
try {
    eval("const = 10");
} catch (error) {
    console.log(error.name);
}
```

Output:

```text
SyntaxError
```

Avoid `eval()` in normal application code.

---

# 22. try...catch with Functions

```javascript
function parseUser(data) {
    try {
        return JSON.parse(data);
    } catch (error) {
        console.error("Invalid user data");

        return null;
    }
}

const user = parseUser('{"name":"Sandip"}');

console.log(user);
```

Output:

```text
{ name: "Sandip" }
```

---

# 23. Returning from try

A function can return from inside `try`.

```javascript
function getValue() {
    try {
        return 100;
    } catch (error) {
        return 0;
    }
}

console.log(getValue());
```

Output:

```text
100
```

---

# 24. finally and return

`finally` still executes even when `try` returns.

```javascript
function test() {
    try {
        return "Success";
    } finally {
        console.log("Cleanup");
    }
}

console.log(test());
```

Output:

```text
Cleanup
Success
```

The `finally` block runs before the function finishes.

Avoid returning a different value from `finally`, because it can override the earlier return.

Example:

```javascript
function test() {
    try {
        return "Success";
    } finally {
        return "Changed";
    }
}

console.log(test());
```

Output:

```text
Changed
```

Returning from `finally` can hide the original result or error, so it should generally be avoided.

---

# 25. Error Handling with User Input

Suppose a user enters JSON text:

```javascript
const input = '{"name":"Sandip"}';

try {
    const user = JSON.parse(input);

    console.log(`Welcome ${user.name}`);
} catch (error) {
    console.log("Please enter valid JSON");
}
```

This prevents invalid input from breaking the normal program flow.

---

# 26. Error Handling in API Code

A common server-side pattern is:

```javascript
async function getUser() {
    try {
        const response = await fetch("/api/users/1");

        if (!response.ok) {
            throw new Error(
                `HTTP error: ${response.status}`
            );
        }

        const user = await response.json();

        return user;
    } catch (error) {
        console.error("Failed to get user:", error);

        throw error;
    }
}
```

The important point is that a failed HTTP status is not automatically a JavaScript exception from `fetch()`.

You may need to check:

```javascript
response.ok
```

and throw an error yourself when appropriate.

---

# 27. Error Handling in a Controller

A backend controller may use:

```javascript
const getUser = async (req, res) => {
    try {
        const user = await User.findById(req.params.id);

        if (!user) {
            return res.status(404).json({
                message: "User not found"
            });
        }

        res.status(200).json(user);
    } catch (error) {
        console.error(error);

        res.status(500).json({
            message: "Internal server error"
        });
    }
};
```

This separates:

```text
Expected application condition
        ↓
404 User not found

Unexpected server error
        ↓
500 Internal Server Error
```

---

# 28. try...catch and Promise Errors

With a Promise:

```javascript
try {
    const result = await getData();

    console.log(result);
} catch (error) {
    console.error(error);
}
```

The `await` expression allows a rejected Promise to be handled by the surrounding `catch`.

Without `await`, use the Promise's rejection handling:

```javascript
getData()
    .then((result) => {
        console.log(result);
    })
    .catch((error) => {
        console.error(error);
    });
```

---

# 29. Cleanup Pattern

A useful pattern is:

```javascript
let resource;

try {
    resource = openResource();

    useResource(resource);
} catch (error) {
    console.error(error);
} finally {
    if (resource) {
        closeResource(resource);
    }
}
```

The important idea is:

```text
try
    → perform operation

catch
    → handle failure

finally
    → cleanup
```

---

# 30. Common Mistakes

## Mistake 1 — Empty catch

Avoid:

```javascript
try {
    riskyOperation();
} catch {
}
```

It hides the error and makes debugging difficult.

---

## Mistake 2 — Logging only a generic message

Instead of:

```javascript
catch {
    console.log("Error");
}
```

During development, prefer:

```javascript
catch (error) {
    console.error(error);
}
```

---

## Mistake 3 — Swallowing Errors

Avoid silently ignoring errors:

```javascript
try {
    saveUser();
} catch {
    return null;
}
```

unless ignoring the failure is intentionally part of the design.

---

## Mistake 4 — Returning from finally

Avoid:

```javascript
try {
    return value;
} finally {
    return anotherValue;
}
```

The `finally` return overrides the previous result.

---

# 31. Best Practices

### 1. Catch errors you can actually handle

Do not add `try...catch` everywhere without a reason.

### 2. Preserve useful error information

During development:

```javascript
console.error(error);
```

is more useful than:

```javascript
console.log("Error");
```

### 3. Use meaningful messages

```javascript
throw new Error("User ID is required");
```

is better than:

```javascript
throw new Error("Error");
```

### 4. Use `finally` for cleanup

Use it when something must happen regardless of success or failure.

### 5. Do not hide errors unnecessarily

If the current layer cannot handle the error, rethrow it or pass it to the application's central error handler.

---

# 32. Simple Error-Handling Flow

```text
            try
             │
             ▼
       Execute code
             │
       ┌─────┴─────┐
       │           │
     Success      Error
       │           │
       ▼           ▼
    Continue     catch
       │           │
       └─────┬─────┘
             ▼
          finally
             │
             ▼
          Continue
```

---

# 33. try...catch Syntax Cheat Sheet

### Basic

```javascript
try {
    // risky code
} catch (error) {
    // handle error
}
```

### With finally

```javascript
try {
    // risky code
} catch (error) {
    // handle error
} finally {
    // cleanup
}
```

### Without catch

```javascript
try {
    // code
} finally {
    // cleanup
}
```

### Without using the error object

```javascript
try {
    // code
} catch {
    // handle error
}
```

### Rethrow

```javascript
try {
    // code
} catch (error) {
    throw error;
}
```

---

# 34. Key Takeaways

* `try` contains code that may throw an error.
* `catch` handles an error thrown by the corresponding `try`.
* `error.name` identifies the error type.
* `error.message` describes the error.
* `error.stack` provides debugging information.
* `finally` runs after `try`/`catch` and is useful for cleanup.
* `try...finally` can be used without `catch`.
* Optional catch binding allows `catch {}`.
* Nested `try...catch` blocks are possible.
* Errors can be rethrown with `throw`.
* A synchronous outer `try...catch` does not automatically catch an error thrown later inside `setTimeout`.
* Rejected Promises can be handled with `.catch()` or `await` inside `try...catch`.
* `fetch()` does not automatically reject for ordinary HTTP error statuses such as 404 or 500; check `response.ok` when appropriate.
* Avoid swallowing errors or hiding useful debugging information.
* Avoid returning from `finally`.
