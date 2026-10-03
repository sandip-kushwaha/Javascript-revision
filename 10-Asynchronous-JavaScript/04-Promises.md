# JavaScript Promises

## What is a Promise?

A **Promise** is a JavaScript object that represents the eventual result of an asynchronous operation.

For example:

```js
const promise = fetch("/api/users");
```

The result is not available immediately. The Promise represents the future result.

A Promise can be:

```text
Pending
   ↓
 ┌───────────────┐
 ↓               ↓
Fulfilled      Rejected
```

---

# 1. Promise States

A Promise has three states.

| State       | Meaning                          |
| ----------- | -------------------------------- |
| `pending`   | Operation is still running       |
| `fulfilled` | Operation completed successfully |
| `rejected`  | Operation failed                 |

Example:

```js
const promise = new Promise((resolve, reject) => {
  // asynchronous operation
});
```

Initially:

```text
pending
```

After success:

```text
fulfilled
```

After failure:

```text
rejected
```

A settled Promise cannot change to another state.

```text
pending → fulfilled
pending → rejected
```

But not:

```text
fulfilled → rejected
rejected → fulfilled
```

---

# 2. Creating a Promise

Use the `Promise` constructor:

```js
const promise = new Promise((resolve, reject) => {
  // operation
});
```

It receives a function called the **executor**.

The executor receives two functions:

```js
resolve
reject
```

---

# 3. `resolve()`

Call `resolve()` when the operation succeeds.

```js
const promise = new Promise((resolve, reject) => {
  resolve("Operation successful");
});
```

The Promise becomes fulfilled.

---

# 4. `reject()`

Call `reject()` when the operation fails.

```js
const promise = new Promise((resolve, reject) => {
  reject("Operation failed");
});
```

The Promise becomes rejected.

Usually, an `Error` object is preferred:

```js
const promise = new Promise((resolve, reject) => {
  reject(new Error("Something went wrong"));
});
```

---

# 5. Using `.then()`

Use `.then()` to handle a fulfilled Promise.

```js
const promise = Promise.resolve("Data received");

promise.then((data) => {
  console.log(data);
});
```

Output:

```text
Data received
```

---

# 6. Using `.catch()`

Use `.catch()` to handle rejection.

```js
const promise = Promise.reject(
  new Error("Request failed")
);

promise.catch((error) => {
  console.error(error.message);
});
```

Output:

```text
Request failed
```

---

# 7. Using `.finally()`

`.finally()` runs after the Promise settles, whether it succeeds or fails.

```js
fetch("/api/users")
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error(error);
  })
  .finally(() => {
    console.log("Request finished");
  });
```

This is useful for cleanup.

For example:

```text
Start loading
     ↓
Request
     ↓
Success / Error
     ↓
Stop loading
```

---

# 8. Promise Example

```js
const orderPromise = new Promise((resolve, reject) => {
  const orderCreated = true;

  if (orderCreated) {
    resolve({
      id: "ORD-101",
      status: "pending"
    });
  } else {
    reject(new Error("Order creation failed"));
  }
});

orderPromise
  .then((order) => {
    console.log(order);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

---

# 9. Asynchronous Promise

Promises are commonly used with asynchronous operations.

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Data loaded");
  }, 1000);
});

promise.then((message) => {
  console.log(message);
});
```

The output appears after the timer completes.

---

# 10. Promise Flow

Consider:

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success");
  }, 1000);
});
```

The flow is:

```text
Promise created
      ↓
   pending
      ↓
setTimeout finishes
      ↓
   resolve()
      ↓
  fulfilled
      ↓
   .then()
```

---

# 11. Promise Rejection Flow

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error("Server error"));
  }, 1000);
});

promise
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

Flow:

```text
Promise created
      ↓
   pending
      ↓
   reject()
      ↓
  rejected
      ↓
  .catch()
```

---

# 12. Promise Chaining

One of the most useful features of Promises is **chaining**.

```js
getUser()
  .then((user) => {
    return getOrders(user.id);
  })
  .then((orders) => {
    return getOrderDetails(orders[0].id);
  })
  .then((order) => {
    console.log(order);
  })
  .catch((error) => {
    console.error(error);
  });
```

The result returned from one `.then()` becomes the input of the next `.then()`.

---

# 13. Returning a Value from `.then()`

```js
Promise.resolve(10)
  .then((value) => {
    return value * 2;
  })
  .then((value) => {
    console.log(value);
  });
```

Output:

```text
20
```

The first `.then()` returns:

```js
20
```

That value becomes available to the next `.then()`.

---

# 14. Returning Another Promise

A `.then()` callback can return another Promise.

```js
Promise.resolve("User")
  .then((value) => {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve(`${value} loaded`);
      }, 1000);
    });
  })
  .then((result) => {
    console.log(result);
  });
```

The next `.then()` waits for the returned Promise.

---

# 15. Error Propagation

Errors can move through a Promise chain until they are handled.

```js
Promise.resolve()
  .then(() => {
    throw new Error("Something failed");
  })
  .then(() => {
    console.log("This will not run");
  })
  .catch((error) => {
    console.error(error.message);
  });
```

Output:

```text
Something failed
```

The error skips the next successful `.then()` and reaches `.catch()`.

---

# 16. `.catch()` Can Also Return a Value

```js
Promise.reject(new Error("Failed"))
  .catch((error) => {
    console.log(error.message);

    return "Fallback value";
  })
  .then((value) => {
    console.log(value);
  });
```

Output:

```text
Failed
Fallback value
```

The rejected chain becomes fulfilled if the `.catch()` handler successfully returns a value.

---

# 17. `.finally()`

Example:

```js
fetch("/api/orders")
  .then((response) => {
    return response.json();
  })
  .then((orders) => {
    console.log(orders);
  })
  .catch((error) => {
    console.error(error);
  })
  .finally(() => {
    console.log("Loading finished");
  });
```

`finally()` is useful for operations such as:

* hiding loading indicators
* closing resources
* resetting temporary state
* cleanup

---

# 18. Promise Resolution

Consider:

```js
const promise = Promise.resolve(100);
```

This creates an already fulfilled Promise.

```js
promise.then((value) => {
  console.log(value);
});
```

Output:

```text
100
```

Similarly:

```js
const promise = Promise.reject(
  new Error("Failed")
);
```

creates an already rejected Promise.

---

# 19. `Promise.resolve()`

`Promise.resolve()` creates a fulfilled Promise.

```js
Promise.resolve("Hello")
  .then((value) => {
    console.log(value);
  });
```

It is useful when you need to convert a value into a Promise.

```js
const promise = Promise.resolve(42);
```

---

# 20. `Promise.reject()`

`Promise.reject()` creates a rejected Promise.

```js
Promise.reject(new Error("Request failed"))
  .catch((error) => {
    console.error(error.message);
  });
```

---

# 21. Promise and `fetch()`

The Fetch API returns a Promise.

```js
fetch("/api/users")
  .then((response) => {
    return response.json();
  })
  .then((users) => {
    console.log(users);
  })
  .catch((error) => {
    console.error(error);
  });
```

The flow is:

```text
fetch()
  ↓
Response Promise
  ↓
response.json()
  ↓
JSON Promise
  ↓
users
```

---

# 22. Important `fetch()` Detail

A common mistake is assuming HTTP errors automatically reject `fetch()`.

For example:

```text
404 Not Found
500 Internal Server Error
```

do not normally cause `fetch()` itself to reject.

You should check:

```js
fetch("/api/users")
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }

    return response.json();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```

Network-level failures can reject the Fetch Promise.

---

# 23. Multiple Promises

Suppose you need three independent requests:

```js
const usersPromise = fetch("/api/users");
const categoriesPromise = fetch("/api/categories");
const foodsPromise = fetch("/api/foods");
```

You can handle them together with `Promise.all()`.

```js
Promise.all([
  usersPromise,
  categoriesPromise,
  foodsPromise
])
  .then((responses) => {
    console.log(responses);
  })
  .catch((error) => {
    console.error(error);
  });
```

---

# 24. Promise Execution Is Not Automatically Sequential

Consider:

```js
const promise1 = fetch("/api/users");
const promise2 = fetch("/api/categories");
```

Both requests can start without waiting for the other.

Promises represent asynchronous results; the way you create and chain operations determines their execution relationship.

---

# 25. Promise Callback Types

A `.then()` can receive:

```js
promise.then(
  (value) => {
    // fulfilled
  },
  (error) => {
    // rejected
  }
);
```

Example:

```js
Promise.resolve("Success").then(
  (value) => {
    console.log(value);
  },
  (error) => {
    console.error(error);
  }
);
```

However, `.catch()` is generally clearer for handling errors across a chain:

```js
promise
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.error(error);
  });
```

---

# 26. Promise Methods

JavaScript provides several useful static Promise methods:

```text
Promise.all()
Promise.allSettled()
Promise.race()
Promise.any()
Promise.resolve()
Promise.reject()
```

They are useful when working with multiple asynchronous operations.

Detailed usage belongs in the Promise methods topic.

---

# 27. `Promise.all()`

`Promise.all()` waits for all Promises to fulfill.

```js
const p1 = Promise.resolve("Users");
const p2 = Promise.resolve("Foods");
const p3 = Promise.resolve("Orders");

Promise.all([p1, p2, p3])
  .then((results) => {
    console.log(results);
  });
```

Result:

```js
[
  "Users",
  "Foods",
  "Orders"
]
```

If one Promise rejects, `Promise.all()` rejects.

---

# 28. Promise Chain Example

A hotel system might have this flow:

```js
createOrder(orderData)
  .then((order) => {
    return processPayment(order);
  })
  .then((payment) => {
    return sendNotification(payment);
  })
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error("Order process failed:", error);
  })
  .finally(() => {
    console.log("Process finished");
  });
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
Finally
```

If an operation fails:

```text
Create Order
     ↓
Process Payment
     ↓
   Error
     ↓
  catch()
     ↓
 finally()
```

---

# 29. Promise vs Callback

### Callback style

```js
getUser((user) => {
  getOrders(user.id, (orders) => {
    console.log(orders);
  });
});
```

### Promise style

```js
getUser()
  .then((user) => getOrders(user.id))
  .then((orders) => {
    console.log(orders);
  })
  .catch((error) => {
    console.error(error);
  });
```

Promises can make dependent asynchronous workflows easier to organize.

---

# 30. Promise vs `async/await`

Promises:

```js
getUser()
  .then((user) => getOrders(user.id))
  .then((orders) => console.log(orders))
  .catch((error) => console.error(error));
```

`async/await`:

```js
async function loadOrders() {
  try {
    const user = await getUser();
    const orders = await getOrders(user.id);

    console.log(orders);
  } catch (error) {
    console.error(error);
  }
}
```

`async/await` is built on top of Promises.

It does not replace the Promise system.

---

# 31. Important Rules

### Rule 1: A Promise settles only once

```js
new Promise((resolve, reject) => {
  resolve("Success");
  reject(new Error("Failed"));
});
```

The rejection is ignored because the Promise was already fulfilled.

---

### Rule 2: `.then()` returns a new Promise

```js
const result = Promise.resolve(10)
  .then((value) => value * 2);

console.log(result instanceof Promise);
```

Output:

```text
true
```

---

### Rule 3: Returning a Promise waits for it

```js
doSomething()
  .then(() => {
    return doSomethingElse();
  })
  .then(() => {
    console.log("Finished");
  });
```

The second `.then()` waits for `doSomethingElse()`.

---

### Rule 4: Throwing inside `.then()` rejects the returned Promise

```js
Promise.resolve()
  .then(() => {
    throw new Error("Failed");
  })
  .catch((error) => {
    console.error(error.message);
  });
```

---

# 32. Common Mistake: Forgetting `return`

Consider:

```js
getUser()
  .then((user) => {
    getOrders(user.id);
  })
  .then((orders) => {
    console.log(orders);
  });
```

The Promise returned by `getOrders()` was not returned from the first `.then()`.

Better:

```js
getUser()
  .then((user) => {
    return getOrders(user.id);
  })
  .then((orders) => {
    console.log(orders);
  });
```

Or with an arrow function:

```js
getUser()
  .then((user) => getOrders(user.id))
  .then((orders) => {
    console.log(orders);
  });
```

---

# 33. Promise Chain Mental Model

Think of a Promise chain like a pipeline:

```text
Promise
   ↓
.then()
   ↓
new Promise
   ↓
.then()
   ↓
new Promise
   ↓
.catch()
   ↓
.finally()
```

Each `.then()` normally creates another Promise.

---

# 34. Real-World Uses

Promises are commonly used for:

* API requests
* database operations
* file operations
* authentication requests
* payment processing
* image uploads
* timers
* asynchronous calculations
* external services

Examples:

```js
fetch("/api/orders");
```

```js
User.find();
```

```js
cloudinary.uploader.upload();
```

Many modern JavaScript libraries return Promises.

---

# 35. Key Takeaways

* A Promise represents a future asynchronous result.
* A Promise has three states: `pending`, `fulfilled`, and `rejected`.
* `resolve()` fulfills a Promise.
* `reject()` rejects a Promise.
* `.then()` handles successful results.
* `.catch()` handles errors.
* `.finally()` runs after settlement.
* `.then()` returns a new Promise.
* Promise chaining helps organize dependent operations.
* Errors can propagate through a Promise chain.
* `Promise.resolve()` creates a fulfilled Promise.
* `Promise.reject()` creates a rejected Promise.
* `Promise.all()` handles multiple independent Promises.
* `fetch()` returns a Promise.
* `async/await` is built on top of Promises.

## Simple Mental Model

```text
             Promise
                │
          ┌─────┴─────┐
          ↓           ↓
      resolve()    reject()
          ↓           ↓
      fulfilled    rejected
          ↓           ↓
       .then()     .catch()
          └─────┬─────┘
                ↓
            .finally()
```

