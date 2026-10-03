# JavaScript `try...catch`

## What is `try...catch`?

`try...catch` is used to **handle errors** in JavaScript without stopping the entire program unexpectedly.

Basic structure:

```js
try {
  // code that may cause an error
} catch (error) {
  // handle the error
}
```

---

# 1. Basic Example

```js
try {
  const result = someUndefinedFunction();

  console.log(result);
} catch (error) {
  console.log("An error occurred");
}
```

Instead of the program immediately stopping, the error is caught by `catch`.

---

# 2. How `try...catch` Works

The flow is:

```text
try
 │
 ├── No error → continue
 │
 └── Error
      ↓
    catch
      ↓
   handle error
```

Example:

```js
try {
  console.log("Start");

  throw new Error("Something went wrong");

  console.log("End");
} catch (error) {
  console.log(error.message);
}
```

Output:

```text
Start
Something went wrong
```

`"End"` does not execute because an error occurred before it.

---

# 3. The `error` Object

The `catch` block receives the error object.

```js
try {
  throw new Error("Invalid data");
} catch (error) {
  console.log(error);
}
```

You can inspect:

```js
console.log(error.name);
console.log(error.message);
console.log(error.stack);
```

Example:

```text
name    → Error
message → Invalid data
stack   → Error: Invalid data ...
```

---

# 4. `error.name`

```js
try {
  JSON.parse("invalid json");
} catch (error) {
  console.log(error.name);
}
```

Possible output:

```text
SyntaxError
```

---

# 5. `error.message`

```js
try {
  JSON.parse("invalid json");
} catch (error) {
  console.log(error.message);
}
```

The message explains what went wrong.

---

# 6. `error.stack`

The `stack` property contains information about where the error occurred.

```js
try {
  throw new Error("Database failed");
} catch (error) {
  console.log(error.stack);
}
```

A stack trace is especially useful during debugging.

---

# 7. `try...catch` with JSON

`JSON.parse()` throws an error when the string is not valid JSON.

```js
try {
  const data = JSON.parse('{"name":"Sandip"}');

  console.log(data);
} catch (error) {
  console.error("Invalid JSON:", error.message);
}
```

Invalid JSON:

```js
try {
  const data = JSON.parse("{invalid}");

  console.log(data);
} catch (error) {
  console.error("Could not parse JSON");
}
```

---

# 8. `try...catch` with `JSON.parse()`

A useful function:

```js
function parseJSON(value) {
  try {
    return JSON.parse(value);
  } catch (error) {
    console.error("Invalid JSON");
    return null;
  }
}
```

Use:

```js
const result = parseJSON('{"name":"Sandip"}');

console.log(result);
```

---

# 9. `finally`

JavaScript also provides `finally`.

```js
try {
  console.log("Trying...");
} catch (error) {
  console.log("Error...");
} finally {
  console.log("Finished");
}
```

`finally` runs whether an error occurs or not.

---

# 10. `try...catch...finally`

Complete structure:

```js
try {
  // risky code
} catch (error) {
  // error handling
} finally {
  // cleanup
}
```

Flow:

```text
          try
           │
      ┌────┴────┐
      ↓         ↓
   success     error
      │         │
      │       catch
      │         │
      └────┬────┘
           ↓
        finally
```

---

# 11. Example with `finally`

```js
try {
  console.log("Opening resource");
} catch (error) {
  console.error(error);
} finally {
  console.log("Closing resource");
}
```

The cleanup code runs regardless of whether the `try` block succeeds or fails.

---

# 12. `finally` Without `catch`

You can use `try...finally` without `catch`.

```js
try {
  console.log("Start");
} finally {
  console.log("Cleanup");
}
```

If the `try` block throws an error, it is not handled by `catch` because there is no `catch`.

The error continues after `finally`.

---

# 13. `catch` Without a Binding

Modern JavaScript allows:

```js
try {
  riskyOperation();
} catch {
  console.log("Something went wrong");
}
```

Use this when you don't need the actual error object.

Instead of:

```js
try {
  riskyOperation();
} catch (error) {
  console.log("Something went wrong");
}
```

you can write:

```js
try {
  riskyOperation();
} catch {
  console.log("Something went wrong");
}
```

---

# 14. Throwing an Error

You can manually create an error using `throw`.

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
  const remaining = withdraw(1000, 1500);

  console.log(remaining);
} catch (error) {
  console.error(error.message);
}
```

---

# 15. `throw` Stops the Current Flow

```js
try {
  console.log("Before");

  throw new Error("Failed");

  console.log("After");
} catch (error) {
  console.log(error.message);
}
```

Output:

```text
Before
Failed
```

The statement after `throw` is not executed.

---

# 16. Different Error Types

JavaScript provides built-in error types such as:

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

Example:

```js
try {
  null.toUpperCase();
} catch (error) {
  console.log(error.name);
}
```

Output:

```text
TypeError
```

---

# 17. `try...catch` and `async/await`

`try...catch` is especially useful with `async/await`.

```js
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    const users = await response.json();

    return users;
  } catch (error) {
    console.error("Failed to get users:", error);
  }
}
```

If an awaited Promise rejects, control moves to `catch`.

---

# 18. Fetch Error Handling

A basic fetch request:

```js
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    const users = await response.json();

    return users;
  } catch (error) {
    console.error(error.message);
  }
}
```

This handles both:

* network/request errors
* HTTP status errors that you explicitly turn into errors

---

# 19. Why Check `response.ok`?

`fetch()` normally rejects for certain network failures, but HTTP statuses such as:

```text
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
```

do not automatically reject the Fetch Promise.

So:

```js
if (!response.ok) {
  throw new Error(`HTTP error: ${response.status}`);
}
```

is a useful pattern.

---

# 20. Async Function Error Flow

```js
async function process() {
  try {
    const user = await getUser();

    const orders = await getOrders(user.id);

    return orders;
  } catch (error) {
    console.error(error);
  }
}
```

Flow:

```text
getUser()
    ↓
 await
    ↓
getOrders()
    ↓
 await
    ↓
result
```

If any awaited operation rejects:

```text
getUser()
    ↓
getOrders()
    ↓
  Error
    ↓
 catch
```

---

# 21. Rethrowing an Error

Sometimes you want to log an error locally but let another function handle it.

```js
async function getUser() {
  try {
    return await fetchUser();
  } catch (error) {
    console.error("User request failed");

    throw error;
  }
}
```

The `throw error` sends the error to the caller.

---

# 22. Handling the Rethrown Error

```js
async function main() {
  try {
    const user = await getUser();

    console.log(user);
  } catch (error) {
    console.error("Final error handler:", error.message);
  }
}
```

Flow:

```text
getUser()
   ↓
error
   ↓
local catch
   ↓
throw error
   ↓
caller catch
```

---

# 23. Adding Context to an Error

Instead of simply rethrowing:

```js
throw error;
```

you can create a more descriptive error:

```js
throw new Error(`Failed to load user: ${error.message}`);
```

Example:

```js
async function getUser() {
  try {
    return await fetchUser();
  } catch (error) {
    throw new Error(`User service failed: ${error.message}`);
  }
}
```

This can make application-level errors easier to understand.

---

# 24. Nested `try...catch`

You can have nested error handling:

```js
try {
  try {
    throw new Error("Inner error");
  } catch (error) {
    console.log("Inner:", error.message);
  }

  console.log("Outer continues");
} catch (error) {
  console.log("Outer:", error.message);
}
```

The inner `catch` handles the inner error.

The outer `catch` does not receive it because it was already handled.

---

# 25. Rethrowing from Nested `catch`

```js
try {
  try {
    throw new Error("Database error");
  } catch (error) {
    console.log("Logging error");
    throw error;
  }
} catch (error) {
  console.log("Outer handler:", error.message);
}
```

The inner handler logs the error and rethrows it.

The outer handler then receives it.

---

# 26. Scope of `try...catch`

Variables declared with `let` or `const` inside `try` are block-scoped.

```js
try {
  const user = {
    name: "Sandip"
  };

  console.log(user);
} catch (error) {
  console.log(error);
}
```

You cannot normally access `user` outside the `try` block:

```js
console.log(user); // ReferenceError
```

If you need the value outside:

```js
let user;

try {
  user = {
    name: "Sandip"
  };
} catch (error) {
  console.error(error);
}

console.log(user);
```

---

# 27. `try...catch` Does Not Catch Every Error Everywhere

Consider asynchronous callback code:

```js
try {
  setTimeout(() => {
    throw new Error("Failed");
  }, 1000);
} catch (error) {
  console.log("Caught");
}
```

The outer `catch` does not catch the error thrown later inside the timer callback.

The callback runs asynchronously after the `try` block has already finished.

Handle the error inside the callback or use a Promise-based approach.

---

# 28. Callback Error Handling

With a callback API:

```js
getUser((error, user) => {
  if (error) {
    console.error(error);
    return;
  }

  console.log(user);
});
```

This is the common **error-first callback** pattern.

The callback receives:

```text
callback(error, result)
```

---

# 29. Promise Error Handling

With Promises:

```js
getUser()
  .then((user) => {
    console.log(user);
  })
  .catch((error) => {
    console.error(error);
  });
```

With `async/await`:

```js
async function load() {
  try {
    const user = await getUser();

    console.log(user);
  } catch (error) {
    console.error(error);
  }
}
```

---

# 30. Error Handling Comparison

### Callback

```js
getData((error, data) => {
  if (error) {
    return handleError(error);
  }

  console.log(data);
});
```

### Promise

```js
getData()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    handleError(error);
  });
```

### Async/Await

```js
async function load() {
  try {
    const data = await getData();

    console.log(data);
  } catch (error) {
    handleError(error);
  }
}
```

---

# 31. `finally` in Real Applications

A common loading-state pattern:

```js
async function loadUsers() {
  isLoading = true;

  try {
    const response = await fetch("/api/users");

    if (!response.ok) {
      throw new Error("Failed to load users");
    }

    return await response.json();
  } catch (error) {
    console.error(error);
  } finally {
    isLoading = false;
  }
}
```

Whether the request succeeds or fails:

```text
isLoading = false
```

will be executed.

---

# 32. Hotel Management Example

Suppose a hotel system creates an order:

```js
async function createHotelOrder(orderData) {
  try {
    const order = await createOrder(orderData);

    const payment = await processPayment(order);

    await sendNotification(payment);

    return order;
  } catch (error) {
    console.error("Order processing failed:", error);

    throw error;
  } finally {
    console.log("Order process finished");
  }
}
```

Flow:

```text
Create Order
     ↓
Process Payment
     ↓
Send Notification
     ↓
   Success
     ↓
  finally
```

If payment fails:

```text
Create Order
     ↓
Process Payment
     ↓
   Error
     ↓
  catch
     ↓
 finally
```

---

# 33. Node.js / Express Example

A controller can use:

```js
const getUser = async (req, res) => {
  try {
    const user = await User.findById(req.params.id);

    if (!user) {
      return res.status(404).json({
        success: false,
        message: "User not found"
      });
    }

    return res.status(200).json({
      success: true,
      data: user
    });
  } catch (error) {
    return res.status(500).json({
      success: false,
      message: error.message
    });
  }
};
```

The database operation may reject, so the `catch` handles the error.

In larger Express applications, centralized error middleware can reduce repeated error-response code.

---

# 34. What Should Be Caught?

Use `try...catch` when you can meaningfully handle or add context to an error.

Good example:

```js
try {
  const data = JSON.parse(input);
} catch (error) {
  console.error("Invalid configuration:", error.message);
}
```

Avoid catching an error only to silently ignore it:

```js
try {
  riskyOperation();
} catch (error) {
  // nothing
}
```

Silent failures can make applications difficult to debug.

---

# 35. Logging Errors

During development:

```js
catch (error) {
  console.error(error);
}
```

For more context:

```js
catch (error) {
  console.error("Failed to load dashboard:", error);
}
```

Avoid exposing sensitive internal details directly to users.

For example, instead of returning:

```text
MongoDB connection string...
```

send a safe message:

```js
res.status(500).json({
  success: false,
  message: "Internal server error"
});
```

Log detailed information on the server where appropriate.

---

# 36. Error Handling Pattern

A useful general pattern:

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

The responsibilities are:

```text
try
→ perform operation

catch
→ handle/log/rethrow error

finally
→ cleanup
```

---

# 37. Important Rules

### Rule 1

`try` contains code that may throw.

```js
try {
  riskyOperation();
}
```

### Rule 2

`catch` handles the error.

```js
catch (error) {
  console.error(error);
}
```

### Rule 3

`finally` runs regardless of success or failure.

```js
finally {
  cleanup();
}
```

### Rule 4

`throw` creates or forwards an error.

```js
throw new Error("Failed");
```

### Rule 5

An async function converts thrown errors into rejected Promises.

```js
async function test() {
  throw new Error("Failed");
}
```

---

# 38. Common Mistakes

## Mistake 1: Empty Catch

```js
try {
  doSomething();
} catch {
}
```

This can hide important failures.

---

## Mistake 2: Assuming `fetch()` Rejects for 404

```js
try {
  const response = await fetch("/missing");
} catch (error) {
  // 404 does not normally reach here
}
```

Check:

```js
if (!response.ok) {
  throw new Error(`HTTP ${response.status}`);
}
```

---

## Mistake 3: Catching the Wrong Async Error

```js
try {
  setTimeout(() => {
    throw new Error("Failed");
  }, 1000);
} catch (error) {
  // Does not catch the timer error
}
```

The asynchronous callback needs its own error-handling strategy.

---

## Mistake 4: Logging and Hiding the Error

```js
catch (error) {
  console.error(error);
}
```

If the caller needs to know the operation failed, rethrow:

```js
catch (error) {
  console.error(error);

  throw error;
}
```

---

# 39. `try...catch` with Synchronous Code

```js
function divide(a, b) {
  if (b === 0) {
    throw new Error("Cannot divide by zero");
  }

  return a / b;
}

try {
  const result = divide(10, 0);

  console.log(result);
} catch (error) {
  console.error(error.message);
}
```

Output:

```text
Cannot divide by zero
```

---

# 40. `try...catch` with Promises

Promise rejection can be handled with:

```js
async function load() {
  try {
    const result = await Promise.reject(
      new Error("Request failed")
    );

    console.log(result);
  } catch (error) {
    console.error(error.message);
  }
}
```

The rejected Promise is converted into an exception at the `await` expression.

---

# 41. `try...catch` Mental Model

```text
             try
              │
       ┌──────┴──────┐
       ↓             ↓
    success         error
       │             │
       │           catch
       │             │
       └──────┬──────┘
              ↓
           finally
              ↓
          continue
```

---

# 42. Key Takeaways

* `try...catch` handles JavaScript errors.
* `try` contains potentially failing code.
* `catch` handles an error.
* `finally` runs after `try`/`catch`.
* `throw` manually creates or forwards an error.
* `error.message` gives the error message.
* `error.name` identifies the error type.
* `error.stack` helps with debugging.
* `try...catch` works naturally with `async/await`.
* Rejected Promises can be caught with `try...catch` when using `await`.
* `fetch()` requires checking `response.ok` for HTTP errors.
* Errors inside asynchronous callbacks are not automatically caught by an outer synchronous `try...catch`.
* Avoid silently ignoring errors.
* Rethrow errors when higher-level code needs to handle them.
* `finally` is useful for cleanup and resetting state.

## Simple Example to Remember

```js
async function loadData() {
  try {
    const response = await fetch("/api/data");

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    const data = await response.json();

    return data;
  } catch (error) {
    console.error("Failed:", error.message);

    throw error;
  } finally {
    console.log("Request finished");
  }
}
```
