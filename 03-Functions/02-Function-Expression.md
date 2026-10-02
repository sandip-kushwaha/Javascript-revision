# JavaScript Function Expressions

A **function expression** is a function that is created and assigned to a variable.

Unlike a function declaration, the function itself is treated as a value and can be stored in a variable.

---

# 1. What is a Function Expression?

Example:

```javascript
const greet = function () {
    console.log("Hello, Sandip!");
};
```

Here:

```text
const greet       → variable
function () {}    → function expression
```

You execute the function using:

```javascript
greet();
```

Output:

```text
Hello, Sandip!
```

---

# 2. Basic Syntax

```javascript
const functionName = function () {
    // code
};
```

Example:

```javascript
const greet = function () {
    console.log("Hello!");
};

greet();
```

Output:

```text
Hello!
```

Notice the semicolon:

```javascript
};
```

The function expression is part of a variable assignment statement.

---

# 3. Function Declaration vs Function Expression

### Function Declaration

```javascript
function greet() {
    console.log("Hello!");
}
```

### Function Expression

```javascript
const greet = function () {
    console.log("Hello!");
};
```

Both can be called like this:

```javascript
greet();
```

But they have important differences, especially regarding hoisting.

---

# 4. Function Expression with Parameters

Function expressions can accept parameters.

```javascript
const add = function (a, b) {
    return a + b;
};

console.log(add(10, 20));
```

Output:

```text
30
```

The function is stored inside the variable `add`.

---

# 5. Function Expression with One Parameter

```javascript
const square = function (number) {
    return number * number;
};

console.log(square(5));
```

Output:

```text
25
```

---

# 6. Function Expression with Multiple Parameters

```javascript
const calculateTotal = function (price, quantity) {
    return price * quantity;
};

const total = calculateTotal(500, 3);

console.log(total);
```

Output:

```text
1500
```

---

# 7. Calling a Function Expression

First define it:

```javascript
const greet = function () {
    console.log("Hello!");
};
```

Then call it:

```javascript
greet();
```

You can call it multiple times:

```javascript
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

---

# 8. Function Expression is a Value

In JavaScript, functions are values.

For example:

```javascript
const message = "Hello";
```

The string is stored in `message`.

Similarly:

```javascript
const greet = function () {
    console.log("Hello!");
};
```

The function is stored in `greet`.

You can think of:

```text
Variable
   ↓
Function value
```

---

# 9. Function Expressions Can Be Assigned to `let`

You can also use `let`.

```javascript
let greet = function () {
    console.log("Hello!");
};

greet();
```

Since `let` allows reassignment, the function can later be replaced:

```javascript
greet = function () {
    console.log("Goodbye!");
};

greet();
```

Output:

```text
Goodbye!
```

---

# 10. Function Expressions with `const`

`const` is commonly preferred when the function variable does not need to be reassigned.

```javascript
const greet = function () {
    console.log("Hello!");
};
```

You cannot reassign it:

```javascript
greet = function () {
    console.log("Hi!");
};
```

This causes an error because `greet` was declared using `const`.

Important:

`const` prevents reassignment of the variable binding. It does not mean functions themselves are somehow immutable.

---

# 11. Anonymous Function Expression

A function expression does not need a function name.

Example:

```javascript
const greet = function () {
    console.log("Hello!");
};
```

The function has no name after the `function` keyword.

This is called an **anonymous function**.

```text
function () {
    ...
}
```

The variable name is:

```text
greet
```

---

# 12. Named Function Expression

A function expression can also have its own name.

```javascript
const greet = function sayHello() {
    console.log("Hello!");
};

greet();
```

Here:

```text
greet       → variable containing the function
sayHello    → function's internal name
```

The function name can be useful for debugging and recursion.

Example:

```javascript
const factorial = function calculateFactorial(number) {
    if (number <= 1) {
        return 1;
    }

    return number * calculateFactorial(number - 1);
};

console.log(factorial(5));
```

Output:

```text
120
```

---

# 13. Function Expression and Hoisting

This is an important difference between function declarations and function expressions.

A function declaration can generally be called before its declaration:

```javascript
greet();

function greet() {
    console.log("Hello!");
}
```

This works because function declarations are hoisted.

But this does not work:

```javascript
greet();

const greet = function () {
    console.log("Hello!");
};
```

You cannot access `greet` before its `const` initialization.

The same applies to:

```javascript
let greet = function () {
    console.log("Hello!");
};
```

The variable is in the **Temporal Dead Zone** before its declaration is initialized.

---

# 14. Function Expression Execution Order

Consider:

```javascript
const greet = function () {
    console.log("Hello!");
};

greet();
```

JavaScript processes the variable declaration and initializes it with the function.

Then:

```javascript
greet();
```

calls the stored function.

Conceptually:

```text
Create variable
      ↓
Store function
      ↓
Call function
      ↓
Execute function body
```

---

# 15. Returning a Value

A function expression can return a value just like a function declaration.

```javascript
const add = function (a, b) {
    return a + b;
};

const result = add(10, 20);

console.log(result);
```

Output:

```text
30
```

---

# 16. Function Expression with `return`

Example:

```javascript
const multiply = function (a, b) {
    return a * b;
};

console.log(multiply(5, 4));
```

Output:

```text
20
```

Another example:

```javascript
const isAdult = function (age) {
    return age >= 18;
};

console.log(isAdult(25));
```

Output:

```text
true
```

---

# 17. Function Expressions Can Be Passed Around

Because functions are values, you can store them in variables and pass them to other functions.

Example:

```javascript
const greet = function () {
    console.log("Hello!");
};

function executeFunction(fn) {
    fn();
}

executeFunction(greet);
```

Output:

```text
Hello!
```

Here:

```text
greet
  ↓
function value
  ↓
passed to executeFunction()
  ↓
fn()
  ↓
Hello!
```

This concept becomes very important when learning **callbacks** and **higher-order functions**.

---

# 18. Function Expression as an Argument

You can directly provide a function expression as an argument.

```javascript
function execute(fn) {
    fn();
}

execute(function () {
    console.log("Hello!");
});
```

Output:

```text
Hello!
```

The function expression:

```javascript
function () {
    console.log("Hello!");
}
```

is passed directly to `execute()`.

---

# 19. Function Expression Inside an Object

Functions can be stored as object properties.

```javascript
const user = {
    name: "Sandip",

    greet: function () {
        console.log("Hello!");
    }
};

user.greet();
```

Output:

```text
Hello!
```

The function is stored in the `greet` property.

---

# 20. Function Expression Inside an Array

Functions can also be stored inside arrays.

```javascript
const operations = [
    function () {
        return "Add";
    },

    function () {
        return "Subtract";
    }
];

console.log(operations[0]());
console.log(operations[1]());
```

Output:

```text
Add
Subtract
```

The array contains function values.

---

# 21. Practical Example: Hotel System

Suppose we have a function for calculating an order total.

```javascript
const calculateOrderTotal = function (price, quantity) {
    return price * quantity;
};

const total = calculateOrderTotal(250, 3);

console.log(`Total: Rs. ${total}`);
```

Output:

```text
Total: Rs. 750
```

---

# 22. Practical Example: Check Table Availability

```javascript
const isTableAvailable = function (status) {
    return status === "available";
};

console.log(isTableAvailable("available"));
```

Output:

```text
true
```

Another example:

```javascript
const getTableMessage = function (status) {
    return status === "available"
        ? "Table is available"
        : "Table is occupied";
};

console.log(getTableMessage("occupied"));
```

Output:

```text
Table is occupied
```

---

# 23. Practical Example: Order Status

```javascript
const canServeOrder = function (kitchenStatus) {
    return kitchenStatus === "ready";
};

const status = canServeOrder("ready");

if (status) {
    console.log("Order can be served.");
}
```

Output:

```text
Order can be served.
```

---

# 24. Practical Example: User Validation

```javascript
const isValidUser = function (user) {
    return user && user.name && user.email;
};

const user = {
    name: "Sandip",
    email: "sandip@example.com"
};

console.log(isValidUser(user));
```

Output:

```text
sandip@example.com
```

A more explicit version can be clearer:

```javascript
const isValidUser = function (user) {
    return Boolean(
        user &&
        user.name &&
        user.email
    );
};
```

This returns a boolean.

---

# 25. Function Expression vs Arrow Function

A function expression:

```javascript
const add = function (a, b) {
    return a + b;
};
```

An arrow function:

```javascript
const add = (a, b) => {
    return a + b;
};
```

Arrow functions are a shorter function syntax introduced in modern JavaScript.

They have important differences involving `this`, `arguments`, constructors, and other behavior, which will be covered separately.

---

# 26. Function Expression vs Function Declaration

| Feature                   | Function Declaration            | Function Expression                                         |
| ------------------------- | ------------------------------- | ----------------------------------------------------------- |
| Syntax                    | `function greet() {}`           | `const greet = function() {}`                               |
| Stored in variable        | Not required                    | Usually yes                                                 |
| Function name             | Usually declared directly       | Can be anonymous or named                                   |
| Called before declaration | Generally yes                   | No with `let`/`const` variable access before initialization |
| Hoisting                  | Function declaration is hoisted | Variable follows `let`/`const`/`var` rules                  |
| Can be passed around      | Yes                             | Yes                                                         |
| Can be returned           | Yes                             | Yes                                                         |
| Can be stored in objects  | Yes                             | Yes                                                         |
| Common use                | Named reusable functions        | Callbacks and assigning functions to variables              |

---

# 27. `var` with Function Expressions

You can technically use `var`:

```javascript
var greet = function () {
    console.log("Hello!");
};
```

But be careful with hoisting:

```javascript
greet();

var greet = function () {
    console.log("Hello!");
};
```

This does not successfully call the function.

Conceptually, the `var` declaration is hoisted:

```javascript
var greet;

greet(); // greet is undefined here

greet = function () {
    console.log("Hello!");
};
```

Calling `undefined` as a function causes a `TypeError`.

Using `const` or `let` is generally clearer for modern JavaScript function expressions.

---

# 28. Function Expression with Conditional Logic

```javascript
const getAccess = function (role) {
    if (role === "admin") {
        return "Full access";
    }

    return "Limited access";
};

console.log(getAccess("admin"));
```

Output:

```text
Full access
```

---

# 29. Function Expression with Multiple Operations

```javascript
const calculateFinalPrice = function (price, discount) {
    const discountAmount = price * discount / 100;
    const finalPrice = price - discountAmount;

    return finalPrice;
};

console.log(calculateFinalPrice(1000, 10));
```

Output:

```text
900
```

---

# 30. Function Expression and Reassignment

With `let`:

```javascript
let operation = function () {
    return "First operation";
};

console.log(operation());
```

You can replace the function:

```javascript
operation = function () {
    return "Second operation";
};

console.log(operation());
```

Output:

```text
First operation
Second operation
```

With `const`, reassignment is not allowed:

```javascript
const operation = function () {
    return "First operation";
};

// operation = function () {};
```

---

# 31. Functions as First-Class Values

JavaScript treats functions as **first-class values**.

This means functions can be:

* Stored in variables
* Stored in objects
* Stored in arrays
* Passed as arguments
* Returned from functions

Example:

```javascript
const greet = function () {
    return "Hello!";
};

const message = greet;

console.log(message());
```

Output:

```text
Hello!
```

Both variables refer to the same function.

---

# 32. Copying a Function Reference

Consider:

```javascript
const greet = function () {
    console.log("Hello!");
};

const anotherGreet = greet;

anotherGreet();
```

Output:

```text
Hello!
```

This does not create a new function.

Both variables refer to the same function object.

```text
greet
  │
  └──────► function

anotherGreet
  │
  └──────► same function
```

---

# 33. Function Reference vs Function Call

This is an important distinction.

### Function reference

```javascript
const fn = greet;
```

This stores the function reference.

### Function call

```javascript
const result = greet();
```

This executes the function and stores its returned value.

Consider:

```javascript
function greet() {
    return "Hello";
}

const a = greet;
const b = greet();

console.log(a);
console.log(b);
```

Conceptually:

```text
a → function itself
b → "Hello"
```

---

# 34. Common Mistakes

## Mistake 1: Calling Before Initialization

Incorrect:

```javascript
greet();

const greet = function () {
    console.log("Hello!");
};
```

The `const` variable cannot be accessed before initialization.

Correct:

```javascript
const greet = function () {
    console.log("Hello!");
};

greet();
```

---

## Mistake 2: Forgetting the Semicolon

Usually JavaScript can handle this through automatic semicolon insertion, but consistent formatting is recommended.

Prefer:

```javascript
const greet = function () {
    console.log("Hello!");
};
```

---

## Mistake 3: Confusing Reference and Call

Incorrect when passing a function:

```javascript
execute(greet());
```

This calls `greet` immediately and passes its returned value.

If you want to pass the function itself:

```javascript
execute(greet);
```

---

## Mistake 4: Reassigning a `const` Function Variable

```javascript
const greet = function () {
    console.log("Hello!");
};

greet = function () {
    console.log("Hi!");
};
```

This causes an error because the `greet` binding cannot be reassigned.

---

# 36. Quick Revision

| Concept                      | Example                        |
| ---------------------------- | ------------------------------ |
| Function expression          | `const greet = function() {};` |
| Anonymous function           | `function() {}`                |
| Named function expression    | `function greetUser() {}`      |
| Function call                | `greet()`                      |
| Parameter                    | `function(a) {}`               |
| Return                       | `return value`                 |
| Store function               | `const fn = function() {};`    |
| Pass function                | `execute(greet)`               |
| Function in object           | `{ greet: function() {} }`     |
| Function in array            | `[function() {}]`              |
| Reassign with `let`          | `fn = anotherFunction`         |
| No reassignment with `const` | `const fn = ...`               |

---

# 37. Key Takeaways

* A **function expression** creates a function and assigns it to a variable.
* Basic syntax:

  ```javascript
  const greet = function () {
      console.log("Hello!");
  };
  ```
* Function expressions are commonly stored in `const` variables.
* They can have parameters and return values.
* They can be anonymous or named.
* Function expressions are values and can be passed around.
* They can be stored in objects and arrays.
* A function expression assigned to `let` can be reassigned.
* A function expression assigned to `const` cannot be reassigned.
* Function expressions are not callable before their variable has been initialized.
* Function expressions are frequently used with callbacks and higher-order functions.
* Arrow functions provide a shorter syntax but have different behavior in some important areas.

---
