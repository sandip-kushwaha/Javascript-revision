# JavaScript Callbacks

## What is a Callback?

A **callback** is a function passed to another function as an argument so that it can be called later.

Simple idea:

```text id="4gk9p1"
Function A
    ↓
receives Function B
    ↓
Function A calls Function B
```

Example:

```js id="7x8m2q"
function greet(name, callback) {
  console.log(`Hello ${name}`);

  callback();
}

function finished() {
  console.log("Greeting finished");
}

greet("Sandip", finished);
```

Output:

```text id="e5v3ka"
Hello Sandip
Greeting finished
```

Here:

```js id="0p8h3x"
finished
```

is passed as a callback.

---

# 1. Function as an Argument

JavaScript functions are values, so they can be passed to other functions.

```js id="3m7q1z"
function sayHello() {
  console.log("Hello");
}

function execute(callback) {
  callback();
}

execute(sayHello);
```

Output:

```text id="4t6c9n"
Hello
```

Notice:

```js id="y8v1x4"
execute(sayHello);
```

not:

```js id="j2m5r7"
execute(sayHello());
```

The first passes the function.

The second calls the function immediately and passes its return value.

---

# 2. Callback with an Anonymous Function

You can create the callback directly.

```js id="w3c9p2"
function execute(callback) {
  callback();
}

execute(function () {
  console.log("Task completed");
});
```

This is useful when the callback is only needed in one place.

---

# 3. Callback with an Arrow Function

The same example can be shorter:

```js id="n6v2qa"
function execute(callback) {
  callback();
}

execute(() => {
  console.log("Task completed");
});
```

Arrow functions are commonly used as callbacks.

---

# 4. Callback with Parameters

A callback can receive values.

```js id="d7r4ks"
function calculate(a, b, callback) {
  const result = a + b;

  callback(result);
}

calculate(10, 20, (result) => {
  console.log(result);
});
```

Output:

```text id="z1m8cv"
30
```

The flow is:

```text id="3h7w2n"
calculate()
    ↓
result = 30
    ↓
callback(30)
    ↓
console.log(30)
```

---

# 5. Callback for Success and Error

Callbacks can be used to handle different outcomes.

```js id="k4p8sx"
function divide(a, b, callback) {
  if (b === 0) {
    callback(new Error("Cannot divide by zero"));
    return;
  }

  callback(null, a / b);
}

divide(10, 2, (error, result) => {
  if (error) {
    console.error(error.message);
    return;
  }

  console.log(result);
});
```

Output:

```text id="q9m2bd"
5
```

This pattern is commonly called an **error-first callback**.

The convention is:

```text id="6x1v9a"
callback(error, result)
```

If there is no error:

```js id="x3r7mc"
callback(null, result);
```

---

# 6. Callback Does Not Always Mean Asynchronous

This is important.

A callback can be completely synchronous.

```js id="r2f6kp"
function process(value, callback) {
  const result = value * 2;

  callback(result);
}

process(10, (result) => {
  console.log(result);
});
```

Output:

```text id="5q7w3e"
20
```

The callback executes immediately during the function call.

So:

```text id="n8c1mv"
Callback ≠ automatically asynchronous
```

A callback simply means:

> A function passed to another function to be invoked by that function.

---

# 7. Asynchronous Callback

Callbacks are also commonly used with asynchronous operations.

```js id="x6j2qa"
console.log("Start");

setTimeout(() => {
  console.log("Timer finished");
}, 1000);

console.log("End");
```

Output:

```text id="m4k8zs"
Start
End
Timer finished
```

The function passed to `setTimeout()` is a callback.

It runs later.

---

# 8. Callback with `setTimeout()`

```js id="u7p3hd"
function greet() {
  console.log("Hello");
}

setTimeout(greet, 1000);
```

After the timer becomes eligible to run, JavaScript executes:

```js id="x1d6qa"
greet();
```

The callback is:

```js id="z4m8cy"
greet
```

---

# 9. Callback with Arguments

You can pass values to a callback.

```js id="p5r2mx"
function processUser(user, callback) {
  callback(user);
}

const user = {
  name: "Sandip",
  role: "admin"
};

processUser(user, (user) => {
  console.log(user.name);
  console.log(user.role);
});
```

Output:

```text id="j8c4vk"
Sandip
admin
```

---

# 10. Callback Returning a Value

A callback can return a value.

```js id="n2w6pf"
function calculate(a, b, operation) {
  return operation(a, b);
}

const result = calculate(
  10,
  5,
  (a, b) => a * b
);

console.log(result);
```

Output:

```text id="h4x9ds"
50
```

The callback:

```js id="5m7q2c"
(a, b) => a * b
```

returns the calculated value.

---

# 11. Callback with Array Methods

Many JavaScript array methods accept callbacks.

For example:

```js id="v8k3mz"
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((number) => {
  return number * 2;
});

console.log(doubled);
```

Output:

```text id="p6y2kr"
[2, 4, 6, 8]
```

The function:

```js id="c5q9xd"
(number) => number * 2
```

is the callback passed to `map()`.

---

# 12. Callback with `filter()`

```js id="w4n7ps"
const prices = [100, 450, 200, 800];

const expensive = prices.filter((price) => {
  return price >= 400;
});

console.log(expensive);
```

Output:

```text id="k2v8mc"
[450, 800]
```

The callback determines whether each element should remain in the result.

---

# 13. Callback with `find()`

```js id="x9r4bt"
const users = [
  { id: 1, name: "Ram" },
  { id: 2, name: "Sandip" },
  { id: 3, name: "Hari" }
];

const user = users.find((user) => {
  return user.id === 2;
});

console.log(user);
```

Output:

```text id="j7c3mz"
{ id: 2, name: "Sandip" }
```

The callback is executed for each element until a matching element is found.

---

# 14. Callback with `forEach()`

```js id="q5n8sv"
const foods = [
  "Pizza",
  "Burger",
  "Coffee"
];

foods.forEach((food) => {
  console.log(food);
});
```

Output:

```text id="r1m6kd"
Pizza
Burger
Coffee
```

The callback runs once for each array element.

---

# 15. Callback Receives Multiple Arguments

Array callbacks can receive:

```text id="7p4x2n"
element
index
array
```

Example:

```js id="m8q3yc"
const foods = [
  "Pizza",
  "Burger",
  "Coffee"
];

foods.forEach((food, index, array) => {
  console.log(food);
  console.log(index);
  console.log(array);
});
```

The callback signature can be:

```js id="c2v7mn"
(food, index, array)
```

You do not have to use all of the arguments.

---

# 16. Callback with Event Listeners

Browser events commonly use callbacks.

```js id="y4k8pc"
const button = document.querySelector("#saveButton");

button.addEventListener("click", () => {
  console.log("Button clicked");
});
```

The function:

```js id="g5m1vx"
() => {
  console.log("Button clicked");
}
```

is a callback.

The browser calls it when the event occurs.

---

# 17. Event Callback with Event Object

The browser can pass an event object to the callback.

```js id="f7q2mz"
button.addEventListener("click", (event) => {
  console.log(event.type);
});
```

Output:

```text id="b9v4kc"
click
```

The callback receives information about the event.

---

# 18. Custom Callback Function

You can design your own API using callbacks.

```js id="d3m8wp"
function processOrder(order, onSuccess) {
  console.log(`Processing ${order}`);

  onSuccess();
}

processOrder("ORD-101", () => {
  console.log("Order completed");
});
```

Output:

```text id="k6x1rz"
Processing ORD-101
Order completed
```

This pattern is useful when a function should allow the caller to decide what happens next.

---

# 19. Success and Error Callbacks

A simple asynchronous-style function can use two callbacks.

```js id="s8q5nv"
function login(username, password, onSuccess, onError) {
  if (username === "admin" && password === "1234") {
    onSuccess({
      username,
      role: "admin"
    });

    return;
  }

  onError("Invalid credentials");
}

login(
  "admin",
  "1234",
  (user) => {
    console.log("Login successful");
    console.log(user);
  },
  (error) => {
    console.error(error);
  }
);
```

Output:

```text id="f2m7xc"
Login successful
{ username: "admin", role: "admin" }
```

---

# 20. Error-First Callback Pattern

Node.js historically uses the error-first callback pattern extensively.

Basic structure:

```js id="a6w3pk"
function callback(error, result) {
  if (error) {
    // handle error
    return;
  }

  // use result
}
```

Example:

```js id="z9r5mt"
function getUser(callback) {
  const user = {
    id: 1,
    name: "Sandip"
  };

  callback(null, user);
}

getUser((error, user) => {
  if (error) {
    console.error(error);
    return;
  }

  console.log(user);
});
```

The convention is:

```text id="n4c8qy"
First argument  → error
Second argument → successful result
```

---

# 21. Callback Execution Order

Consider:

```js id="u5x2nr"
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

Output:

```text id="k8m3vp"
A
C
B
```

The callback is scheduled for later.

The current synchronous code completes first.

---

# 22. Nested Callbacks

Callbacks can be nested.

```js id="p2v7mc"
getUser((user) => {
  getOrders(user.id, (orders) => {
    getPayment(orders[0].id, (payment) => {
      console.log(payment);
    });
  });
});
```

This creates deeply nested code.

It can become difficult to:

* read
* maintain
* handle errors
* debug

This problem is commonly called **callback hell**.

The next file covers it in detail.

---

# 23. Callbacks and Promises

Callbacks were widely used for asynchronous programming.

Modern JavaScript commonly uses **Promises** for asynchronous operations.

Callback style:

```js id="h4q8zs"
getUser((user) => {
  getOrders(user.id, (orders) => {
    console.log(orders);
  });
});
```

Promise style:

```js id="j6n2rx"
getUser()
  .then((user) => getOrders(user.id))
  .then((orders) => {
    console.log(orders);
  });
```

Promises can make complex asynchronous flows easier to manage.

---

# 24. Callback vs Promise

| Callback                             | Promise                         |
| ------------------------------------ | ------------------------------- |
| Function passed to another function  | Represents future result        |
| Common in older APIs                 | Common in modern APIs           |
| Can become deeply nested             | Supports chaining               |
| Error handling can become repetitive | Centralized `.catch()` possible |
| Simple for small tasks               | Useful for complex async flows  |

Callbacks are still important because many JavaScript APIs use them.

---

# 25. Callback vs `async/await`

Callback:

```js id="b8w4km"
getUser((user) => {
  console.log(user);
});
```

Promise:

```js id="q3m7xp"
getUser().then((user) => {
  console.log(user);
});
```

Async/await:

```js id="v6n2rs"
const user = await getUser();

console.log(user);
```

All three approaches can represent asynchronous workflows, but they provide different programming styles.

---

# 26. Callback Context

A callback is just a function, so how it behaves with `this` depends on how it is called and whether it is an arrow function.

For example:

```js id="m9c4kv"
const user = {
  name: "Sandip",

  showName() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};

user.showName();
```

Output:

```text id="w7p2mc"
Sandip
```

The arrow callback uses the surrounding `this`.

This connects to the `this` topic covered earlier.

---

# 27. Callback Function Reference vs Callback Result

This distinction is very important.

Correct:

```js id="c5v8nx"
setTimeout(greet, 1000);
```

Here, the function itself is passed.

Incorrect:

```js id="r2m6kp"
setTimeout(greet(), 1000);
```

Here, `greet()` executes immediately.

General rule:

```text id="z1q7hd"
function → pass the function
function() → call the function
```

---

# 28. Practical Hotel Example

Imagine processing a customer order.

```js id="a8n4qs"
function createOrder(order, callback) {
  console.log("Creating order...");

  setTimeout(() => {
    const savedOrder = {
      ...order,
      status: "pending"
    };

    callback(savedOrder);
  }, 1000);
}

const order = {
  tableNumber: "T-03",
  items: [
    {
      name: "Pizza",
      price: 450
    }
  ]
};

createOrder(order, (savedOrder) => {
  console.log("Order created:");
  console.log(savedOrder);
});
```

The callback runs after the simulated order creation finishes.

---

# 29. Practical API-Style Example

```js id="v3m7xc"
function fetchUser(callback) {
  setTimeout(() => {
    const user = {
      id: 1,
      name: "Sandip",
      role: "admin"
    };

    callback(null, user);
  }, 1000);
}

fetchUser((error, user) => {
  if (error) {
    console.error(error);
    return;
  }

  console.log(user);
});
```

This resembles the structure of older Node.js asynchronous APIs.

---

# 30. Important Callback Rules

### Rule 1: Pass the function when you want it called later

```js id="m4x9vz"
doSomething(callback);
```

### Rule 2: Do not call it immediately

```js id="q7k2np"
doSomething(callback());
```

unless you intentionally want to pass the return value.

### Rule 3: Call the callback with the required data

```js id="b6r3ws"
callback(result);
```

### Rule 4: A callback is not automatically asynchronous

```js id="x8p5mt"
array.forEach(callback);
```

is normally synchronous.

### Rule 5: Keep callback responsibilities clear

A callback should generally handle the result rather than contain unrelated application logic.

---

# 31. Key Takeaways

* A **callback** is a function passed to another function.
* The receiving function decides when to call it.
* Callbacks can be synchronous or asynchronous.
* `setTimeout()` uses a callback.
* Array methods such as `map()`, `filter()`, `find()`, and `forEach()` use callbacks.
* Event listeners use callbacks.
* Callbacks can receive arguments.
* Error-first callbacks commonly use:

```js
callback(error, result);
```

* Passing `function` and calling `function()` are different.
* Too many nested callbacks can create callback hell.
* Promises and `async/await` provide alternative approaches for asynchronous workflows.
* Callbacks remain important for understanding JavaScript and Node.js.

## Simple Mental Model

```text id="7c2n5m"
function process(callback) {
    │
    ├── do something
    │
    └── callback(result)
              │
              ↓
        caller handles result
```

### Callback Flow

```text id="p6v9xr"
Main Code
   ↓
Call Function
   ↓
Pass Callback
   ↓
Operation Happens
   ↓
Callback Called
   ↓
Handle Result
```

