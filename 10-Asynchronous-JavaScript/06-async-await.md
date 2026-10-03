# JavaScript `async` / `await`

## What is `async/await`?

`async/await` is a modern way to work with **Promises**.

It makes asynchronous code easier to read because it can look similar to normal synchronous code.

Example:

```js
async function getUser() {
  const response = await fetch("/api/users");

  const users = await response.json();

  console.log(users);
}
```

`async/await` does **not** remove Promises.

It is built on top of the Promise system.

---

# 1. The `async` Keyword

The `async` keyword is used before a function:

```js
async function greet() {
  return "Hello";
}
```

An `async` function **always returns a Promise**.

```js
const result = greet();

console.log(result);
```

Conceptually:

```text
async function
      ↓
returns Promise
      ↓
fulfilled with "Hello"
```

---

# 2. `async` Function Returns a Promise

Consider:

```js
async function getMessage() {
  return "Hello World";
}
```

This:

```js
const result = getMessage();
```

does not directly give:

```js
"Hello World"
```

Instead, it gives a Promise.

You can use:

```js
getMessage().then((message) => {
  console.log(message);
});
```

Output:

```text
Hello World
```

---

# 3. `async` with an Explicit Promise

An async function can also return a Promise directly:

```js
async function getData() {
  return Promise.resolve("Data loaded");
}
```

Using it:

```js
getData().then((data) => {
  console.log(data);
});
```

---

# 4. The `await` Keyword

`await` waits for a Promise to settle before continuing the async function.

Example:

```js
async function loadData() {
  const response = await fetch("/api/users");

  console.log(response);
}
```

The function waits for the `fetch()` Promise before assigning the response.

---

# 5. `await` Works with Promises

```js
async function example() {
  const result = await Promise.resolve("Success");

  console.log(result);
}

example();
```

Output:

```text
Success
```

The Promise is fulfilled with:

```text
Success
```

so `await` gives that value to `result`.

---

# 6. Basic `async/await` Flow

```js
async function loadUsers() {
  const response = await fetch("/api/users");

  const users = await response.json();

  console.log(users);
}
```

Flow:

```text
loadUsers()
    ↓
fetch()
    ↓
await response
    ↓
response.json()
    ↓
await users
    ↓
console.log()
```

---

# 7. `async/await` vs Promise Chain

### Promise chain

```js
function loadUsers() {
  return fetch("/api/users")
    .then((response) => response.json())
    .then((users) => {
      console.log(users);
    });
}
```

### `async/await`

```js
async function loadUsers() {
  const response = await fetch("/api/users");

  const users = await response.json();

  console.log(users);
}
```

Both use Promises.

The second style often makes sequential workflows easier to read.

---

# 8. `await` Pauses the Async Function

Consider:

```js
async function process() {
  console.log("Start");

  const result = await Promise.resolve("Done");

  console.log(result);

  console.log("End");
}

process();
```

The `await` pauses the execution of **that async function** until the Promise settles.

It does not block the entire JavaScript runtime.

---

# 9. Important: `await` Does Not Block the Whole Program

Consider:

```js
async function load() {
  console.log("Loading...");

  await new Promise((resolve) => {
    setTimeout(resolve, 2000);
  });

  console.log("Loaded");
}

load();

console.log("Other code");
```

Output:

```text
Loading...
Other code
Loaded
```

The async function pauses at `await`, while other JavaScript work can continue.

---

# 10. Error Handling with `try...catch`

Rejected Promises can be handled with `try...catch`.

```js
async function loadUsers() {
  try {
    const response = await fetch("/api/users");

    const users = await response.json();

    console.log(users);
  } catch (error) {
    console.error(error);
  }
}
```

If an awaited Promise rejects, execution moves to `catch`.

---

# 11. `try...catch` with Multiple Operations

```js
async function processOrder() {
  try {
    const user = await getUser();

    const orders = await getOrders(user.id);

    const order = await getOrderDetails(orders[0].id);

    console.log(order);
  } catch (error) {
    console.error("Process failed:", error);
  }
}
```

One `catch` can handle errors from the awaited operations inside the `try` block.

---

# 12. `finally` with `async/await`

You can also use `finally`:

```js
async function loadData() {
  try {
    const response = await fetch("/api/users");

    return await response.json();
  } catch (error) {
    console.error(error);
  } finally {
    console.log("Request finished");
  }
}
```

`finally` runs after the `try` or `catch` section completes.

---

# 13. `await` and `fetch()`

A common API pattern is:

```js
async function getUsers() {
  const response = await fetch("/api/users");

  const users = await response.json();

  return users;
}
```

Then:

```js
getUsers().then((users) => {
  console.log(users);
});
```

The function itself still returns a Promise.

---

# 14. Check `response.ok`

Remember that `fetch()` does not automatically reject for HTTP error status codes such as `404` or `500`.

A safer pattern:

```js
async function getUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
  }

  return await response.json();
}
```

Now HTTP errors become rejected Promises.

---

# 15. `await` and Return Values

```js
async function calculate() {
  const value = await Promise.resolve(10);

  return value * 2;
}
```

The function returns a Promise:

```js
calculate().then((result) => {
  console.log(result);
});
```

Output:

```text
20
```

---

# 16. Multiple `await` Statements

```js
async function loadOrder() {
  const user = await getUser();

  const orders = await getOrders(user.id);

  const order = await getOrderDetails(orders[0].id);

  return order;
}
```

Each operation depends on the previous result.

```text
getUser()
   ↓
user
   ↓
getOrders(user.id)
   ↓
orders
   ↓
getOrderDetails()
   ↓
order
```

This is a good use of sequential `await`.

---

# 17. Sequential `await`

Consider:

```js
const users = await getUsers();
const categories = await getCategories();
const foods = await getFoods();
```

These operations execute sequentially.

Conceptually:

```text
getUsers()
   ↓
getCategories()
   ↓
getFoods()
```

This is appropriate when a later operation depends on an earlier one.

---

# 18. Avoid Unnecessary Sequential `await`

Suppose these requests are independent:

```js
const users = await getUsers();
const categories = await getCategories();
const foods = await getFoods();
```

If none depends on another, this can unnecessarily wait.

Instead:

```js
const [users, categories, foods] = await Promise.all([
  getUsers(),
  getCategories(),
  getFoods()
]);
```

Now the independent operations can proceed concurrently.

---

# 19. Sequential vs Concurrent

### Sequential

```js
const user = await getUser();
const foods = await getFoods(user.id);
```

Here the second operation needs the first result.

```text
getUser()
   ↓
user
   ↓
getFoods(user.id)
```

### Concurrent

```js
const [users, foods] = await Promise.all([
  getUsers(),
  getFoods()
]);
```

Neither operation depends on the other.

```text
getUsers() ────────┐
                   ├──→ results
getFoods() ────────┘
```

---

# 20. Async Function with Parameters

```js
async function getUserOrders(userId) {
  const orders = await getOrders(userId);

  return orders;
}
```

Use it:

```js
const orders = await getUserOrders(10);
```

This `await` must be used inside an async context, except where top-level `await` is supported.

---

# 21. Async Arrow Functions

You can use `async` with arrow functions:

```js
const getUsers = async () => {
  const response = await fetch("/api/users");

  return response.json();
};
```

Another example:

```js
const calculateTotal = async (price, quantity) => {
  return price * quantity;
};
```

Because it is async, the result is still a Promise.

---

# 22. Async Methods

Object methods can also be async:

```js
const userService = {
  async getUser(id) {
    const response = await fetch(`/api/users/${id}`);

    return response.json();
  }
};
```

Use:

```js
const user = await userService.getUser(10);
```

---

# 23. Async Class Methods

```js
class UserService {
  async getUser(id) {
    const response = await fetch(`/api/users/${id}`);

    return response.json();
  }
}
```

Use:

```js
const service = new UserService();

const user = await service.getUser(10);
```

---

# 24. `await` with Non-Promise Values

`await` can technically be used with normal values.

```js
async function example() {
  const value = await 100;

  console.log(value);
}

example();
```

Output:

```text
100
```

JavaScript treats the value similarly to a fulfilled Promise.

However, `await` is mainly useful with asynchronous operations.

---

# 25. Async Function Errors

An error thrown inside an async function causes the returned Promise to reject.

```js
async function test() {
  throw new Error("Something failed");
}
```

Handle it with:

```js
test().catch((error) => {
  console.error(error.message);
});
```

Or:

```js
async function main() {
  try {
    await test();
  } catch (error) {
    console.error(error.message);
  }
}
```

---

# 26. `await` with Rejected Promise

```js
async function test() {
  const result = await Promise.reject(
    new Error("Request failed")
  );

  console.log(result);
}
```

The function's execution does not continue to the next statement.

Without handling the rejection, the async function returns a rejected Promise.

Better:

```js
async function test() {
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

---

# 27. `async/await` in a Hotel Order Flow

A hotel system might process an order like this:

```js
async function completeOrder(orderData) {
  try {
    const order = await createOrder(orderData);

    const payment = await processPayment(order);

    const notification = await sendNotification(payment);

    return notification;
  } catch (error) {
    console.error("Order process failed:", error);

    throw error;
  }
}
```

The flow is:

```text
Create Order
      ↓
Process Payment
      ↓
Send Notification
      ↓
Return Result
```

This structure is easy to follow when each step depends on the previous step.

---

# 28. `async/await` with Express

In a Node.js/Express application, an async controller can look like:

```js
const getUsers = async (req, res) => {
  try {
    const users = await User.find();

    res.status(200).json({
      success: true,
      data: users
    });
  } catch (error) {
    res.status(500).json({
      success: false,
      message: error.message
    });
  }
};
```

The database operation returns a Promise.

`await` waits for the result.

---

# 29. Async Database Example

With Mongoose:

```js
const getFood = async (req, res) => {
  try {
    const food = await Food.findById(req.params.id);

    if (!food) {
      return res.status(404).json({
        message: "Food not found"
      });
    }

    res.status(200).json({
      data: food
    });
  } catch (error) {
    res.status(500).json({
      message: error.message
    });
  }
};
```

This is a common pattern in Node.js backend applications.

---

# 30. Async Function Does Not Make CPU Work Asynchronous

Consider:

```js
async function calculate() {
  let total = 0;

  for (let i = 0; i < 1000000000; i++) {
    total += i;
  }

  return total;
}
```

Adding `async` does not automatically move this CPU-heavy loop to another thread.

The JavaScript execution can still block while performing heavy synchronous work.

`async` mainly provides a convenient way to work with asynchronous Promise-based operations.

---

# 31. `await` and the Event Loop

When an async function reaches:

```js
await somePromise;
```

the function pauses until the Promise settles.

Other work can continue.

After the Promise settles, the continuation is scheduled according to JavaScript's Promise/microtask behavior.

Conceptually:

```text
async function
      ↓
    await
      ↓
function pauses
      ↓
other JavaScript work
      ↓
Promise settles
      ↓
async function continues
```

---

# 32. Top-Level `await`

In JavaScript modules, `await` can be used at the top level.

Example:

```js
const response = await fetch("/api/users");

const users = await response.json();

console.log(users);
```

This is called **top-level await**.

It is available in ES modules and supported in modern JavaScript environments.

---

# 33. Common Mistake: Forgetting `await`

Suppose:

```js
async function getUsers() {
  return fetch("/api/users");
}
```

The function returns a Promise for the fetch operation.

You can explicitly await:

```js
async function getUsers() {
  const response = await fetch("/api/users");

  return response;
}
```

Whether `await` is needed depends on what you want to do with the Promise.

For example, this is also valid:

```js
async function getUsers() {
  return fetch("/api/users");
}
```

The returned Promise is adopted by the async function.

---

# 34. Common Mistake: `await` Outside an Async Context

This usually causes an error:

```js
function loadUsers() {
  const users = await getUsers();
}
```

Use:

```js
async function loadUsers() {
  const users = await getUsers();
}
```

Or use top-level `await` in a supported ES module context.

---

# 35. Common Mistake: Unnecessary `await`

This:

```js
async function getData() {
  return await fetch("/api/users");
}
```

may be unnecessary if there is no reason to handle the result or error at that point.

You can write:

```js
async function getData() {
  return fetch("/api/users");
}
```

However, `return await` can be useful in some `try...catch` situations when you specifically need the rejection to be caught there.

---

# 36. `return await` and `try...catch`

Consider:

```js
async function getData() {
  try {
    return await fetch("/api/users");
  } catch (error) {
    console.error("Caught here:", error);
    throw error;
  }
}
```

The `await` makes the Promise rejection occur within the `try` block, so the local `catch` can handle it.

Without awaiting:

```js
async function getData() {
  try {
    return fetch("/api/users");
  } catch (error) {
    console.error(error);
  }
}
```

the `catch` does not catch a later rejection from that returned Promise.

---

# 37. Async/Await Best Practices

### Keep dependent operations sequential

```js
const user = await getUser();
const orders = await getOrders(user.id);
```

### Run independent operations together

```js
const [users, foods] = await Promise.all([
  getUsers(),
  getFoods()
]);
```

### Handle expected errors

```js
try {
  const data = await getData();
} catch (error) {
  console.error(error);
}
```

### Throw meaningful errors

```js
if (!response.ok) {
  throw new Error(`Request failed: ${response.status}`);
}
```

### Avoid deeply nested async functions

Prefer:

```js
async function process() {
  const user = await getUser();
  const orders = await getOrders(user.id);

  return orders;
}
```

instead of deeply nested callbacks.

---

# 38. Callback vs Promise vs Async/Await

### Callback

```js
getUser((user) => {
  getOrders(user.id, (orders) => {
    console.log(orders);
  });
});
```

### Promise

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

### Async/Await

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

All three can represent asynchronous workflows, but they organize the code differently.

---

# 39. Key Takeaways

* `async` makes a function return a Promise.
* `await` waits for a Promise inside an async function.
* `async/await` is built on top of Promises.
* `await` pauses the current async function, not the entire JavaScript runtime.
* Rejected awaited Promises can be handled with `try...catch`.
* An error thrown inside an async function causes its returned Promise to reject.
* Independent operations can often use `Promise.all()`.
* Dependent operations should generally be awaited sequentially.
* `async` does not automatically make CPU-heavy code non-blocking.
* `fetch()` and many Node.js APIs work naturally with `async/await`.
* Async functions always return Promises.
* Top-level `await` is supported in ES modules.
* `async/await` can make complex asynchronous workflows easier to read.

## Simple Mental Model

```text
async function
      │
      ↓
returns Promise
      │
      ↓
    await
      │
      ↓
wait for Promise
      │
      ├── fulfilled → continue
      │
      └── rejected  → catch / rejected Promise
```
