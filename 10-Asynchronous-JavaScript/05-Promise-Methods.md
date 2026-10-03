# JavaScript Promise Methods

JavaScript provides several static methods on the `Promise` object for working with one or multiple Promises.

The main methods are:

```text
Promise.all()
Promise.allSettled()
Promise.race()
Promise.any()
Promise.resolve()
Promise.reject()
```

---

# 1. `Promise.all()`

`Promise.all()` waits for **all Promises to fulfill**.

```js
const p1 = Promise.resolve("Users");
const p2 = Promise.resolve("Foods");
const p3 = Promise.resolve("Orders");

Promise.all([p1, p2, p3])
  .then((results) => {
    console.log(results);
  });
```

Output:

```js
[
  "Users",
  "Foods",
  "Orders"
]
```

The results are returned in the **same order as the input Promises**.

---

# 2. `Promise.all()` with API Requests

Suppose a dashboard needs three independent resources:

```js
const users = fetch("/api/users");
const foods = fetch("/api/foods");
const orders = fetch("/api/orders");
```

You can wait for all three:

```js
Promise.all([users, foods, orders])
  .then((responses) => {
    console.log(responses);
  })
  .catch((error) => {
    console.error(error);
  });
```

This is useful when all results are required before continuing.

---

# 3. `Promise.all()` Rejects if One Fails

```js
const p1 = Promise.resolve("Success");
const p2 = Promise.reject(new Error("Failed"));
const p3 = Promise.resolve("Success");

Promise.all([p1, p2, p3])
  .then((results) => {
    console.log(results);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

Output:

```text
Failed
```

If any Promise rejects, `Promise.all()` rejects.

Conceptually:

```text
Promise 1 ── fulfilled ──┐
Promise 2 ── rejected ───┼──→ Promise.all() rejected
Promise 3 ── fulfilled ──┘
```

---

# 4. `Promise.all()` Does Not Return Partial Results

Consider:

```js
Promise.all([
  Promise.resolve("A"),
  Promise.reject(new Error("B failed")),
  Promise.resolve("C")
])
  .then((results) => {
    console.log(results);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

The `.then()` handler does not receive:

```js
["A", "C"]
```

Instead, the combined Promise rejects.

If you need the result of every operation regardless of success or failure, use `Promise.allSettled()`.

---

# 5. `Promise.allSettled()`

`Promise.allSettled()` waits until **all Promises have settled**.

Settled means:

```text
fulfilled OR rejected
```

Example:

```js
const p1 = Promise.resolve("Users loaded");

const p2 = Promise.reject(
  new Error("Foods failed")
);

const p3 = Promise.resolve("Orders loaded");

Promise.allSettled([p1, p2, p3])
  .then((results) => {
    console.log(results);
  });
```

The result contains the status of every Promise.

Conceptually:

```js
[
  {
    status: "fulfilled",
    value: "Users loaded"
  },
  {
    status: "rejected",
    reason: Error
  },
  {
    status: "fulfilled",
    value: "Orders loaded"
  }
]
```

---

# 6. `Promise.all()` vs `Promise.allSettled()`

| Method                 | Waits for      | If one rejects            |
| ---------------------- | -------------- | ------------------------- |
| `Promise.all()`        | All to fulfill | Combined Promise rejects  |
| `Promise.allSettled()` | All to settle  | Still returns all results |

Use:

```js
Promise.all()
```

when every operation must succeed.

Use:

```js
Promise.allSettled()
```

when you want to inspect every operation, even if some fail.

---

# 7. Practical `Promise.allSettled()` Example

Suppose an admin dashboard loads:

```text
Users
Categories
Foods
Orders
```

You want the dashboard to know which requests succeeded and which failed.

```js
const requests = [
  fetch("/api/users"),
  fetch("/api/categories"),
  fetch("/api/foods"),
  fetch("/api/orders")
];

Promise.allSettled(requests)
  .then((results) => {
    results.forEach((result, index) => {
      if (result.status === "fulfilled") {
        console.log(`Request ${index + 1} succeeded`);
      } else {
        console.log(`Request ${index + 1} failed`);
      }
    });
  });
```

One failed request does not prevent the other results from being reported.

---

# 8. `Promise.race()`

`Promise.race()` settles as soon as the **first Promise settles**.

Important:

> The first Promise to **settle** wins, whether it fulfills or rejects.

Example:

```js
const p1 = new Promise((resolve) => {
  setTimeout(() => {
    resolve("First");
  }, 1000);
});

const p2 = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Second");
  }, 2000);
});

Promise.race([p1, p2])
  .then((result) => {
    console.log(result);
  });
```

Output:

```text
First
```

Because `p1` settles first.

---

# 9. `Promise.race()` with Rejection

The first settled Promise could also be rejected.

```js
const p1 = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Success");
  }, 2000);
});

const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error("Failed"));
  }, 1000);
});

Promise.race([p1, p2])
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

Output:

```text
Failed
```

Because the rejection happened first.

---

# 10. `Promise.race()` Mental Model

```text
Promise 1 ──────── 2 seconds
Promise 2 ── 1 second ──→ WIN
Promise 3 ───────── 3 seconds

          ↓

     Promise.race()
          ↓
     Promise 2 result
```

The remaining operations are **not automatically cancelled**.

This is an important distinction.

---

# 11. Practical Use of `Promise.race()`

A common use case is implementing a timeout.

```js
const timeout = new Promise((_, reject) => {
  setTimeout(() => {
    reject(new Error("Request timed out"));
  }, 5000);
});

Promise.race([
  fetch("/api/users"),
  timeout
])
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

If the request finishes first, you get the response.

If five seconds pass first, the timeout Promise rejects.

Note: this does not necessarily cancel the underlying `fetch()` request.

For actual request cancellation, `AbortController` can be used.

---

# 12. `Promise.any()`

`Promise.any()` waits for the **first fulfilled Promise**.

Unlike `Promise.race()`:

```text
Promise.race()
→ first settled

Promise.any()
→ first fulfilled
```

Example:

```js
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error("Server 1 failed"));
  }, 500);
});

const p2 = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Server 2 succeeded");
  }, 1000);
});

Promise.any([p1, p2])
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error(error);
  });
```

Output:

```text
Server 2 succeeded
```

The rejection of `p1` does not stop `Promise.any()` because `p2` eventually fulfills.

---

# 13. `Promise.any()` Mental Model

```text
Promise 1 ── rejected ────────┐
Promise 2 ── fulfilled ──→ WIN
Promise 3 ── fulfilled ──────┘
```

The first successful Promise determines the result.

---

# 14. If All Promises Reject

If every Promise rejects:

```js
Promise.any([
  Promise.reject(new Error("A")),
  Promise.reject(new Error("B")),
  Promise.reject(new Error("C"))
])
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  });
```

The returned Promise rejects with an `AggregateError`.

An `AggregateError` contains the individual errors in its `errors` property.

```js
Promise.any([
  Promise.reject(new Error("A")),
  Promise.reject(new Error("B"))
])
  .catch((error) => {
    console.log(error instanceof AggregateError);
    console.log(error.errors);
  });
```

---

# 15. `Promise.race()` vs `Promise.any()`

This distinction is important.

| Method           | What wins?      | Rejection can win? |
| ---------------- | --------------- | ------------------ |
| `Promise.race()` | First settled   | Yes                |
| `Promise.any()`  | First fulfilled | No                 |

Example:

```text
Promise A → rejected after 1s
Promise B → fulfilled after 2s
```

With:

```js
Promise.race([A, B])
```

Result:

```text
Rejected
```

With:

```js
Promise.any([A, B])
```

Result:

```text
Fulfilled
```

---

# 16. `Promise.resolve()`

`Promise.resolve()` creates a fulfilled Promise.

```js
const promise = Promise.resolve("Hello");

promise.then((value) => {
  console.log(value);
});
```

Output:

```text
Hello
```

It can also convert a normal value into a Promise:

```js
const promise = Promise.resolve(100);
```

---

# 17. `Promise.resolve()` with an Existing Promise

If you pass a Promise to `Promise.resolve()`, it adopts that Promise.

```js
const original = Promise.resolve("Hello");

const result = Promise.resolve(original);

console.log(original === result);
```

Output:

```text
true
```

---

# 18. `Promise.reject()`

`Promise.reject()` creates an immediately rejected Promise.

```js
const promise = Promise.reject(
  new Error("Something went wrong")
);

promise.catch((error) => {
  console.error(error.message);
});
```

Output:

```text
Something went wrong
```

---

# 19. Comparing the Main Methods

```text
Promise.all()
    ↓
All must fulfill

Promise.allSettled()
    ↓
Wait for all to settle

Promise.race()
    ↓
First settled wins

Promise.any()
    ↓
First fulfilled wins

Promise.resolve()
    ↓
Create/adopt fulfilled Promise

Promise.reject()
    ↓
Create rejected Promise
```

---

# 20. Practical API Example

Imagine a hotel dashboard needs data from several services.

```js
const usersRequest = fetch("/api/users");
const foodsRequest = fetch("/api/foods");
const ordersRequest = fetch("/api/orders");

Promise.all([
  usersRequest,
  foodsRequest,
  ordersRequest
])
  .then(([users, foods, orders]) => {
    console.log(users);
    console.log(foods);
    console.log(orders);
  })
  .catch((error) => {
    console.error("Dashboard loading failed:", error);
  });
```

This is appropriate when the dashboard requires all three resources.

---

# 21. Partial Success Example

Suppose a dashboard can still work when some optional services fail.

```js
Promise.allSettled([
  fetch("/api/users"),
  fetch("/api/foods"),
  fetch("/api/recommendations"),
  fetch("/api/notifications")
])
  .then((results) => {
    results.forEach((result) => {
      if (result.status === "fulfilled") {
        console.log("Success:", result.value);
      } else {
        console.error("Failed:", result.reason);
      }
    });
  });
```

Here, one failure does not discard the other results.

---

# 22. Multiple Servers with `Promise.any()`

Suppose the same data is available from multiple servers:

```js
const server1 = fetch("https://server-1.example/api/data");
const server2 = fetch("https://server-2.example/api/data");
const server3 = fetch("https://server-3.example/api/data");
```

You could use:

```js
Promise.any([
  server1,
  server2,
  server3
])
  .then((response) => {
    console.log("First successful response:", response);
  })
  .catch((error) => {
    console.error("All servers failed:", error);
  });
```

This can be useful when any successful source is acceptable.

---

# 23. Timeout Pattern with `Promise.race()`

A reusable helper:

```js
function timeout(ms) {
  return new Promise((_, reject) => {
    setTimeout(() => {
      reject(new Error("Operation timed out"));
    }, ms);
  });
}
```

Use it like:

```js
Promise.race([
  fetch("/api/orders"),
  timeout(5000)
])
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error(error.message);
  });
```

Again, the timeout Promise does not itself cancel the request.

---

# 24. Result Shapes

The methods return different types of results.

### `Promise.all()`

```js
[
  value1,
  value2,
  value3
]
```

### `Promise.allSettled()`

```js
[
  { status: "fulfilled", value: value1 },
  { status: "rejected", reason: error },
  { status: "fulfilled", value: value3 }
]
```

### `Promise.race()`

```text
single first-settled result
```

### `Promise.any()`

```text
single first-fulfilled result
```

---

# 25. Choosing the Right Method

Use `Promise.all()` when:

```text
You need every operation to succeed.
```

Use `Promise.allSettled()` when:

```text
You want the result of every operation.
```

Use `Promise.race()` when:

```text
The first settled operation should determine the result.
```

Use `Promise.any()` when:

```text
The first successful operation is enough.
```

Use `Promise.resolve()` when:

```text
You need a fulfilled Promise.
```

Use `Promise.reject()` when:

```text
You need a rejected Promise.
```

---

# 26. Quick Comparison

| Method         | Waits for       | Success condition          | Failure behavior                         |
| -------------- | --------------- | -------------------------- | ---------------------------------------- |
| `all()`        | All             | All fulfill                | Rejects when one rejects                 |
| `allSettled()` | All             | Always returns results     | Never rejects because of input rejection |
| `race()`       | First settled   | First settled result       | First rejection can win                  |
| `any()`        | First fulfilled | Any one fulfills           | Rejects if all reject                    |
| `resolve()`    | One value       | Creates/adopts fulfillment | —                                        |
| `reject()`     | One value       | Creates rejection          | —                                        |

---

# 27. Important Details

### `Promise.all()`

The result order follows the input order, not completion order.

```js
Promise.all([
  slowPromise,
  fastPromise
]);
```

Even if `fastPromise` finishes first, its result remains in the second position.

---

### `Promise.allSettled()`

Every input is allowed to finish.

```text
fulfilled
rejected
fulfilled
rejected
```

All results are returned.

---

### `Promise.race()`

First settlement wins:

```text
fulfilled first → fulfillment
rejected first  → rejection
```

---

### `Promise.any()`

First fulfillment wins:

```text
rejected
rejected
fulfilled first → result
```

---

# 28. Key Takeaways

* `Promise.all()` waits for all Promises and rejects if one rejects.
* `Promise.allSettled()` waits for every Promise to settle.
* `Promise.race()` returns the result of the first settled Promise.
* `Promise.any()` returns the first fulfilled Promise.
* `Promise.resolve()` creates or adopts a fulfilled Promise.
* `Promise.reject()` creates a rejected Promise.
* `Promise.race()` and `Promise.any()` are different.
* `Promise.race()` allows a rejection to win.
* `Promise.any()` ignores rejections until all inputs reject.
* `Promise.all()` preserves input order in its result array.
* `Promise.allSettled()` is useful when partial failures are acceptable.
* `Promise.race()` is useful for timeout-style patterns.
* These methods are especially useful when handling multiple asynchronous operations.

## Simple Mental Model

```text
                 Promise Methods
                       │
       ┌───────────────┼────────────────┐
       ↓               ↓                ↓
   Multiple          Multiple         Single
   Promises           Promises        Promise
       │               │                │
       ├─ all()        ├─ race()        ├─ resolve()
       ├─ allSettled()  └─ any()         └─ reject()
```
