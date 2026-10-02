# JavaScript Function Basics

A **function** is a reusable block of code designed to perform a specific task.

Functions are one of the most important concepts in JavaScript because they help us:

* Reuse code
* Organize programs
* Reduce duplication
* Make code easier to maintain
* Break large problems into smaller parts

---

# 1. What is a Function?

A function is a block of code that runs when it is **called** or **invoked**.

Example:

```javascript
function greet() {
    console.log("Hello, Sandip!");
}
```

The function above is defined, but it does not run yet.

To execute it:

```javascript
greet();
```

Output:

```text
Hello, Sandip!
```

---

# 2. Basic Function Syntax

```javascript
function functionName() {
    // code
}
```

Example:

```javascript
function sayHello() {
    console.log("Hello!");
}
```

Calling the function:

```javascript
sayHello();
```

Output:

```text
Hello!
```

---

# 3. Parts of a Function

Consider:

```javascript
function greet() {
    console.log("Hello!");
}
```

The parts are:

```text
function       → function keyword
greet          → function name
()             → parameter list
{ }            → function body
console.log()  → code executed when called
```

---

# 4. Function Declaration

A function created using the `function` keyword is called a **function declaration**.

```javascript
function greet() {
    console.log("Hello!");
}
```

Then call it:

```javascript
greet();
```

Another example:

```javascript
function showMessage() {
    console.log("Welcome to JavaScript!");
}

showMessage();
```

Output:

```text
Welcome to JavaScript!
```

---

# 5. Calling a Function

Defining a function does not execute it.

```javascript
function greet() {
    console.log("Hello!");
}
```

Nothing is printed yet.

You need to call it:

```javascript
greet();
```

The complete example:

```javascript
function greet() {
    console.log("Hello!");
}

greet();
```

Output:

```text
Hello!
```

---

# 6. A Function Can Be Called Multiple Times

One major advantage of functions is code reuse.

```javascript
function greet() {
    console.log("Hello!");
}

greet();
greet();
greet();
```

Output:

```text
Hello!
Hello!
Hello!
```

The same function can be reused many times.

---

# 7. Function with Parameters

A function can receive information through **parameters**.

### Syntax

```javascript
function functionName(parameter) {
    // code
}
```

Example:

```javascript
function greet(name) {
    console.log("Hello " + name);
}

greet("Sandip");
```

Output:

```text
Hello Sandip
```

Here:

```text
name → parameter
"Sandip" → argument
```

---

# 8. Parameter vs Argument

These two terms are related but different.

### Parameter

A parameter is the variable written in the function definition.

```javascript
function greet(name) {
    console.log(name);
}
```

Here:

```text
name
```

is a parameter.

### Argument

An argument is the actual value passed when calling the function.

```javascript
greet("Sandip");
```

Here:

```text
"Sandip"
```

is an argument.

---

# 9. Multiple Parameters

A function can accept multiple parameters.

```javascript
function add(a, b) {
    console.log(a + b);
}

add(10, 20);
```

Output:

```text
30
```

Here:

```text
a → first parameter
b → second parameter
10 → first argument
20 → second argument
```

Another example:

```javascript
function introduce(name, age, city) {
    console.log(name);
    console.log(age);
    console.log(city);
}

introduce("Sandip", 22, "Birgunj");
```

---

# 10. Returning a Value

A function can send a result back using the `return` statement.

Example:

```javascript
function add(a, b) {
    return a + b;
}
```

Calling:

```javascript
const result = add(10, 20);

console.log(result);
```

Output:

```text
30
```

The flow is:

```text
add(10, 20)
     ↓
a + b
     ↓
30
     ↓
return 30
     ↓
result
```

---

# 11. `return` Statement

The `return` statement sends a value back to the place where the function was called.

```javascript
function multiply(a, b) {
    return a * b;
}

const result = multiply(5, 4);

console.log(result);
```

Output:

```text
20
```

---

# 12. `return` Stops Function Execution

When JavaScript reaches `return`, the function immediately finishes.

```javascript
function test() {
    console.log("Before return");

    return;

    console.log("After return");
}

test();
```

Output:

```text
Before return
```

This code never runs:

```javascript
console.log("After return");
```

because execution already returned from the function.

---

# 13. Returning Different Data Types

A function can return different types of values.

### String

```javascript
function getName() {
    return "Sandip";
}
```

### Number

```javascript
function getAge() {
    return 22;
}
```

### Boolean

```javascript
function isActive() {
    return true;
}
```

### Array

```javascript
function getNumbers() {
    return [10, 20, 30];
}
```

### Object

```javascript
function getUser() {
    return {
        name: "Sandip",
        role: "admin"
    };
}
```

---

# 14. Function Without `return`

A function does not always need to return a value.

Example:

```javascript
function greet() {
    console.log("Hello!");
}

greet();
```

This function performs an action but does not explicitly return a value.

If you store its result:

```javascript
const result = greet();

console.log(result);
```

The output is:

```text
Hello!
undefined
```

When a function reaches its end without returning a value, its result is `undefined`.

---

# 15. `console.log()` vs `return`

These are not the same.

### `console.log()`

Displays a value in the console.

```javascript
function add(a, b) {
    console.log(a + b);
}
```

### `return`

Sends a value back to the caller.

```javascript
function add(a, b) {
    return a + b;
}
```

For example:

```javascript
const result = add(10, 20);

console.log(result);
```

Using `return` allows the result to be reused:

```javascript
const result = add(10, 20);

const doubled = result * 2;

console.log(doubled);
```

Output:

```text
60
```

---

# 16. Function with No Parameters

A function does not have to receive data.

```javascript
function showDate() {
    console.log(new Date());
}

showDate();
```

Another example:

```javascript
function welcome() {
    return "Welcome to my application!";
}

console.log(welcome());
```

---

# 17. Function with One Parameter

```javascript
function square(number) {
    return number * number;
}

console.log(square(5));
```

Output:

```text
25
```

---

# 18. Function with Multiple Parameters

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}

const total = calculateTotal(500, 3);

console.log(total);
```

Output:

```text
1500
```

---

# 19. Function Parameters Can Have Different Types

JavaScript functions can receive different types of values.

```javascript
function display(value) {
    console.log(value);
}

display("Hello");
display(100);
display(true);
display([1, 2, 3]);
display({ name: "Sandip" });
```

JavaScript is dynamically typed, so the parameter does not need a declared type.

---

# 20. Function with an Object

Functions commonly receive objects.

```javascript
function showUser(user) {
    console.log(user.name);
    console.log(user.email);
}

const user = {
    name: "Sandip",
    email: "sandip@example.com"
};

showUser(user);
```

Output:

```text
Sandip
sandip@example.com
```

---

# 21. Function with an Array

A function can receive an array.

```javascript
function calculateTotal(numbers) {
    let total = 0;

    for (const number of numbers) {
        total += number;
    }

    return total;
}

const numbers = [10, 20, 30];

console.log(calculateTotal(numbers));
```

Output:

```text
60
```

---

# 22. Functions Can Call Other Functions

One function can call another function.

```javascript
function add(a, b) {
    return a + b;
}

function showResult() {
    const result = add(10, 20);

    console.log(result);
}

showResult();
```

Output:

```text
30
```

This is very useful for organizing larger applications.

---

# 23. Function Calling Another Function

Example:

```javascript
function getPrice() {
    return 500;
}

function calculateTotal() {
    const price = getPrice();

    return price * 2;
}

console.log(calculateTotal());
```

Output:

```text
1000
```

The execution flow is:

```text
calculateTotal()
       ↓
   getPrice()
       ↓
      500
       ↓
   500 × 2
       ↓
     1000
```

---

# 24. Function Reusability

Without a function:

```javascript
console.log(10 * 5);
console.log(20 * 5);
console.log(30 * 5);
```

With a function:

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}

console.log(calculateTotal(10, 5));
console.log(calculateTotal(20, 5));
console.log(calculateTotal(30, 5));
```

The function can be reused with different values.

---

# 25. Practical Example: Hotel Order

Suppose a hotel needs to calculate an order total.

```javascript
function calculateOrderTotal(price, quantity) {
    return price * quantity;
}

const total = calculateOrderTotal(250, 3);

console.log(`Total: Rs. ${total}`);
```

Output:

```text
Total: Rs. 750
```

---

# 26. Practical Example: Food Price

```javascript
function calculateFoodPrice(price, quantity) {
    return price * quantity;
}

const foodPrice = calculateFoodPrice(350, 2);

console.log(`Food Price: Rs. ${foodPrice}`);
```

Output:

```text
Food Price: Rs. 700
```

---

# 27. Practical Example: Check User Role

```javascript
function isAdmin(role) {
    return role === "admin";
}

console.log(isAdmin("admin"));
```

Output:

```text
true
```

The returned boolean can then be reused:

```javascript
const userIsAdmin = isAdmin("admin");

if (userIsAdmin) {
    console.log("Show admin dashboard");
}
```

---

# 28. Practical Example: Check Order Status

```javascript
function isOrderReady(status) {
    return status === "ready";
}

const ready = isOrderReady("ready");

if (ready) {
    console.log("Order can be served.");
}
```

Output:

```text
Order can be served.
```

---

# 29. Practical Example: Calculate Discount

```javascript
function calculateDiscount(price, discountPercentage) {
    return price * discountPercentage / 100;
}

const discount = calculateDiscount(1000, 10);

console.log(discount);
```

Output:

```text
100
```

Calculate the final price:

```javascript
function calculateFinalPrice(price, discountPercentage) {
    const discount = price * discountPercentage / 100;

    return price - discount;
}

console.log(calculateFinalPrice(1000, 10));
```

Output:

```text
900
```

---

# 30. Function Scope

Variables declared inside a function normally belong to that function's scope.

```javascript
function test() {
    const message = "Hello";

    console.log(message);
}

test();
```

This works.

But:

```javascript
function test() {
    const message = "Hello";
}

console.log(message);
```

This causes an error because `message` is not accessible outside the function.

Functions create their own **function scope**.

---

# 31. Local Variables

A variable declared inside a function is called a local variable.

```javascript
function calculate() {
    const price = 500;
    const quantity = 2;

    return price * quantity;
}
```

`price` and `quantity` are local to the function.

They cannot normally be accessed directly outside it.

---

# 32. Global Variables and Functions

A variable declared outside a function can be accessed inside the function.

```javascript
const appName = "Hotel Management System";

function showAppName() {
    console.log(appName);
}

showAppName();
```

Output:

```text
Hotel Management System
```

The function can access the outer variable because of JavaScript's lexical scoping rules.

---

# 33. Local Variable Can Shadow Outer Variable

Example:

```javascript
const name = "Global";

function showName() {
    const name = "Local";

    console.log(name);
}

showName();

console.log(name);
```

Output:

```text
Local
Global
```

The local `name` temporarily hides the outer `name` inside the function.

This is called **shadowing**.

---

# 34. Function Naming

Function names should describe what the function does.

Good examples:

```javascript
getUser();
createOrder();
calculateTotal();
validateEmail();
deleteUser();
sendEmail();
```

Avoid unclear names:

```javascript
doSomething();
abc();
test1();
x();
```

Clear names make code easier to understand.

---

# 35. Functions Should Usually Do One Main Job

Good:

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}
```

Another:

```javascript
function validateOrder(order) {
    return order.items.length > 0;
}
```

Avoid putting many unrelated responsibilities into one large function.

Small focused functions are easier to test, reuse, and maintain.

---

# 36. Function Declaration Hoisting

Function declarations can be called before they appear in the source code.

Example:

```javascript
greet();

function greet() {
    console.log("Hello!");
}
```

Output:

```text
Hello!
```

This happens because function declarations are hoisted.

However, this behavior is specific to function declarations and should not be confused with all function forms.

---

# 37. Function Declaration vs Function Call

Declaration:

```javascript
function greet() {
    console.log("Hello!");
}
```

Call:

```javascript
greet();
```

Think of it as:

```text
Declaration → create the function

Call → execute the function
```

---

# 38. Functions Can Return Expressions

You can return calculations directly.

```javascript
function add(a, b) {
    return a + b;
}
```

Another example:

```javascript
function calculateArea(length, width) {
    return length * width;
}
```

Another:

```javascript
function isAdult(age) {
    return age >= 18;
}
```

The last function returns either:

```text
true
```

or:

```text
false
```

---

# 39. Early Return

A function can return early when a condition is met.

```javascript
function checkUser(user) {
    if (!user) {
        return "User not found";
    }

    return "User found";
}
```

This can make validation logic easier to read.

Another example:

```javascript
function processOrder(order) {
    if (!order) {
        return "Invalid order";
    }

    if (order.status === "cancelled") {
        return "Order is cancelled";
    }

    return "Order can be processed";
}
```

---

# 40. Functions and `undefined`

Consider:

```javascript
function greet() {
    console.log("Hello");
}

const result = greet();

console.log(result);
```

Output:

```text
Hello
undefined
```

Why?

Because the function does not explicitly return a value.

Equivalent conceptually:

```javascript
function greet() {
    console.log("Hello");

    return undefined;
}
```

---

# 41. Function Execution Flow

Consider:

```javascript
function add(a, b) {
    const result = a + b;

    return result;
}

const answer = add(10, 20);

console.log(answer);
```

Execution:

```text
1. JavaScript defines add()
        ↓
2. add(10, 20) is called
        ↓
3. a = 10
        ↓
4. b = 20
        ↓
5. result = 30
        ↓
6. return 30
        ↓
7. answer = 30
        ↓
8. console.log(answer)
```

Output:

```text
30
```

---

# 42. Functions Are Reusable Building Blocks

A large application can be divided into smaller functions.

For example:

```text
Application
│
├── Authentication
│   ├── login()
│   ├── logout()
│   └── validateUser()
│
├── Users
│   ├── createUser()
│   ├── getUser()
│   └── updateUser()
│
├── Orders
│   ├── createOrder()
│   ├── calculateTotal()
│   └── updateOrderStatus()
│
└── Products
    ├── createProduct()
    ├── getProduct()
    └── deleteProduct()
```

This makes a large application easier to manage.

---

# 43. Function Best Practices

### 1. Use meaningful names

```javascript
function calculateTotal() {}
```

is better than:

```javascript
function calc() {}
```

### 2. Keep functions focused

A function should preferably have one clear responsibility.

### 3. Use parameters instead of hardcoding values

Avoid:

```javascript
function calculate() {
    return 500 * 2;
}
```

Prefer:

```javascript
function calculate(price, quantity) {
    return price * quantity;
}
```

### 4. Return values when the result needs to be reused

```javascript
function add(a, b) {
    return a + b;
}
```

### 5. Avoid unnecessarily large functions

If a function becomes too large, divide it into smaller functions.

---

# 44. Quick Revision

| Concept                       | Example                                     |
| ----------------------------- | ------------------------------------------- |
| Function declaration          | `function greet() {}`                       |
| Function call                 | `greet()`                                   |
| Parameter                     | `function greet(name) {}`                   |
| Argument                      | `greet("Sandip")`                           |
| Return value                  | `return result`                             |
| No return                     | Returns `undefined`                         |
| Multiple parameters           | `function add(a, b) {}`                     |
| Local variable                | Variable declared inside function           |
| Function scope                | Variables local to function                 |
| Reusable code                 | Same function called multiple times         |
| Early return                  | `if (...) return ...`                       |
| Function declaration hoisting | Declaration can be called before it appears |

---

# 45. Key Takeaways

* A **function** is a reusable block of code.
* Define a function using the `function` keyword.
* Call a function using `functionName()`.
* Functions can accept **parameters**.
* Values passed to functions are called **arguments**.
* Functions can return values using `return`.
* `return` immediately stops function execution.
* A function without an explicit return value returns `undefined`.
* Functions can receive strings, numbers, booleans, arrays, objects, and other values.
* Functions can call other functions.
* Variables declared inside a function are normally local to that function.
* Function declarations are hoisted.
* Good functions should have clear names and focused responsibilities.
* Functions are fundamental to JavaScript, Node.js, React, and full-stack development.

---
