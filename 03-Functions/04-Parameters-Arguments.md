# JavaScript Parameters and Arguments

Parameters and arguments are used to **pass data into functions**.

They allow a function to work with different values instead of using fixed values.

---

## 1. What Are Parameters?

A **parameter** is a variable defined inside a function declaration.

```javascript
function greet(name) {
    console.log(`Hello, ${name}`);
}
```

Here:

```text
name → parameter
```

When we call the function, we provide a value for the parameter.

```javascript
greet("Sandip");
```

Output:

```text
Hello, Sandip
```

---

## 2. What Are Arguments?

An **argument** is the actual value passed to a function when calling it.

```javascript
function greet(name) {
    console.log(`Hello, ${name}`);
}

greet("Sandip");
```

Here:

```text
name   → parameter
"Sandip" → argument
```

### Simple Difference

| Parameter            | Argument                     |
| -------------------- | ---------------------------- |
| Defined in function  | Passed when calling function |
| Acts like a variable | Actual value                 |
| Example: `name`      | Example: `"Sandip"`          |

---

# 3. Basic Example

```javascript
function add(a, b) {
    return a + b;
}

const result = add(10, 20);

console.log(result);
```

Output:

```text
30
```

Here:

```text
a → parameter
b → parameter

10 → argument
20 → argument
```

---

# 4. Multiple Parameters

A function can have multiple parameters.

```javascript
function introduce(name, age, city) {
    console.log(`My name is ${name}`);
    console.log(`I am ${age} years old`);
    console.log(`I live in ${city}`);
}

introduce("Sandip", 22, "Birgunj");
```

Output:

```text
My name is Sandip
I am 22 years old
I live in Birgunj
```

---

# 5. Parameter Order Matters

Arguments are assigned to parameters according to their position.

```javascript
function student(name, age) {
    console.log(name);
    console.log(age);
}

student("Sandip", 22);
```

Mapping:

```text
name → "Sandip"
age  → 22
```

If the order changes:

```javascript
student(22, "Sandip");
```

Then:

```text
name → 22
age  → "Sandip"
```

JavaScript does not automatically understand your intended meaning.

---

# 6. Missing Arguments

JavaScript allows you to call a function without providing all arguments.

```javascript
function greet(name) {
    console.log(name);
}

greet();
```

Output:

```text
undefined
```

Because no value was provided for `name`.

---

# 7. Extra Arguments

You can also provide more arguments than the function has parameters.

```javascript
function add(a, b) {
    return a + b;
}

console.log(add(10, 20, 30));
```

Output:

```text
30
```

The parameters are:

```text
a = 10
b = 20
```

The extra `30` is not assigned to a named parameter.

However, extra arguments can be accessed using the **rest parameter**.

---

# 8. Default Parameters

A parameter can have a default value.

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet("Sandip");
greet();
```

Output:

```text
Hello, Sandip
Hello, Guest
```

The default value is used when the argument is `undefined` or omitted.

```javascript
greet(undefined);
```

Output:

```text
Hello, Guest
```

But `null` is different:

```javascript
greet(null);
```

Output:

```text
Hello, null
```

---

# 9. Multiple Default Parameters

```javascript
function createUser(
    name = "Guest",
    role = "user",
    active = true
) {
    console.log(name);
    console.log(role);
    console.log(active);
}

createUser();
```

Output:

```text
Guest
user
true
```

You can also override selected values by passing `undefined`.

```javascript
createUser("Sandip", undefined, false);
```

Result:

```text
Sandip
user
false
```

---

# 10. Parameters Can Accept Any Data Type

JavaScript functions can accept different types of values.

### String

```javascript
function show(value) {
    console.log(value);
}

show("Hello");
```

### Number

```javascript
show(100);
```

### Boolean

```javascript
show(true);
```

### Array

```javascript
show([1, 2, 3]);
```

### Object

```javascript
show({
    name: "Sandip",
    age: 22
});
```

### Function

Functions can also be passed as arguments.

```javascript
function execute(callback) {
    callback();
}

function sayHello() {
    console.log("Hello");
}

execute(sayHello);
```

---

# 11. Passing Objects as Arguments

Objects are commonly passed to functions.

```javascript
function displayUser(user) {
    console.log(user.name);
    console.log(user.email);
}

const user = {
    name: "Sandip",
    email: "sandip@example.com"
};

displayUser(user);
```

Output:

```text
Sandip
sandip@example.com
```

This is very common in real applications.

---

# 12. Passing Arrays as Arguments

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

# 13. Passing Multiple Values

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

# 14. Rest Parameters

Rest parameters allow a function to receive multiple arguments as an array.

Syntax:

```javascript
function functionName(...parameters) {
    // code
}
```

Example:

```javascript
function sum(...numbers) {
    let total = 0;

    for (const number of numbers) {
        total += number;
    }

    return total;
}

console.log(sum(10, 20, 30));
```

Output:

```text
60
```

You can pass any number of arguments:

```javascript
console.log(sum(1, 2));
console.log(sum(1, 2, 3, 4));
console.log(sum(10, 20, 30, 40, 50));
```

---

# 15. Rest Parameter with Normal Parameters

Rest parameters can come after normal parameters.

```javascript
function introduce(name, ...skills) {
    console.log(`Name: ${name}`);
    console.log("Skills:", skills);
}

introduce(
    "Sandip",
    "JavaScript",
    "React",
    "Node.js"
);
```

Output:

```text
Name: Sandip
Skills: [ 'JavaScript', 'React', 'Node.js' ]
```

The first argument goes to `name`.

The remaining arguments go into `skills`.

---

# 16. Rest Parameter Must Be Last

Correct:

```javascript
function example(a, b, ...rest) {
    console.log(a, b, rest);
}
```

Incorrect:

```javascript
function example(...rest, a) {
    // SyntaxError
}
```

The rest parameter must always be the **last parameter**.

---

# 17. `arguments` Object

Traditional functions have an `arguments` object.

```javascript
function showArguments() {
    console.log(arguments);
}

showArguments(10, 20, 30);
```

It contains the arguments passed to the function.

You can access individual values:

```javascript
function showArguments() {
    console.log(arguments[0]);
    console.log(arguments[1]);
}

showArguments("JavaScript", "React");
```

Output:

```text
JavaScript
React
```

---

# 18. `arguments` vs Rest Parameters

Modern JavaScript generally prefers rest parameters when you need variable numbers of arguments.

### `arguments`

```javascript
function sum() {
    let total = 0;

    for (const number of arguments) {
        total += number;
    }

    return total;
}
```

### Rest parameter

```javascript
function sum(...numbers) {
    let total = 0;

    for (const number of numbers) {
        total += number;
    }

    return total;
}
```

Rest parameters are usually clearer because `numbers` is a real array.

---

# 19. Arrow Functions and Arguments

Arrow functions do **not** have their own `arguments` object.

This is why you should use rest parameters with arrow functions.

```javascript
const sum = (...numbers) => {
    return numbers.reduce((total, number) => total + number, 0);
};

console.log(sum(10, 20, 30));
```

Output:

```text
60
```

---

# 20. Destructuring Parameters

You can destructure objects directly inside function parameters.

```javascript
function displayUser({ name, age }) {
    console.log(name);
    console.log(age);
}

const user = {
    name: "Sandip",
    age: 22
};

displayUser(user);
```

Output:

```text
Sandip
22
```

This is very useful in React components and backend functions.

---

# 21. Array Destructuring Parameters

You can also destructure arrays.

```javascript
function displayNumbers([first, second]) {
    console.log(first);
    console.log(second);
}

displayNumbers([10, 20]);
```

Output:

```text
10
20
```

---

# 22. Default Value with Destructuring

You can combine destructuring and default values.

```javascript
function createUser({
    name = "Guest",
    role = "user"
}) {
    console.log(name);
    console.log(role);
}

createUser({
    name: "Sandip"
});
```

Output:

```text
Sandip
user
```

---

# 23. Default Object Parameter

If the entire object may be omitted, give the parameter a default object.

```javascript
function createUser({
    name = "Guest",
    role = "user"
} = {}) {
    console.log(name);
    console.log(role);
}

createUser();
```

Output:

```text
Guest
user
```

Without `= {}`, calling `createUser()` would try to destructure `undefined` and throw an error.

---

# 24. Passing Functions as Arguments

A function can be passed as an argument.

```javascript
function processUser(name, callback) {
    console.log(`Processing ${name}`);
    callback();
}

function completed() {
    console.log("Completed");
}

processUser("Sandip", completed);
```

Output:

```text
Processing Sandip
Completed
```

This concept is called a **callback**.

---

# 25. Callback with Parameters

```javascript
function processUser(name, callback) {
    callback(name);
}

function showName(name) {
    console.log(`User: ${name}`);
}

processUser("Sandip", showName);
```

Output:

```text
User: Sandip
```

---

# 26. Practical Example — Hotel Order

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

Here:

```text
price    → parameter
quantity → parameter

250      → argument
3        → argument
```

---

# 27. Practical Example — User Creation

```javascript
function createUser(name, email, role = "user") {
    return {
        name,
        email,
        role
    };
}

const user = createUser(
    "Sandip",
    "sandip@example.com"
);

console.log(user);
```

Output:

```javascript
{
    name: "Sandip",
    email: "sandip@example.com",
    role: "user"
}
```

---

# 28. Practical Example — Flexible Order Items

```javascript
function createOrder(customerName, ...items) {
    return {
        customerName,
        items
    };
}

const order = createOrder(
    "Sandip",
    "Momo",
    "Pizza",
    "Coffee"
);

console.log(order);
```

Result:

```javascript
{
    customerName: "Sandip",
    items: ["Momo", "Pizza", "Coffee"]
}
```

---

# 29. Parameters Can Be Expressions

Arguments don't have to be simple values.

You can pass expressions:

```javascript
function square(number) {
    return number * number;
}

console.log(square(5 + 5));
```

Output:

```text
100
```

You can also pass function calls:

```javascript
function double(number) {
    return number * 2;
}

function getNumber() {
    return 10;
}

console.log(double(getNumber()));
```

Output:

```text
20
```

---

# 30. Primitive Values and Parameters

Primitive values such as numbers and strings are passed by value.

```javascript
function changeNumber(number) {
    number = 100;
}

let value = 10;

changeNumber(value);

console.log(value);
```

Output:

```text
10
```

Changing the parameter does not change the original variable.

---

# 31. Objects and Arrays

Objects and arrays are values too, but their contents can be mutated through a parameter because the parameter receives a reference to the same object.

```javascript
function changeUser(user) {
    user.name = "Ram";
}

const user = {
    name: "Sandip"
};

changeUser(user);

console.log(user.name);
```

Output:

```text
Ram
```

The function modified the same object.

This distinction is important when working with JavaScript applications.

---

# 32. Avoid Unnecessary Mutation

Instead of modifying an object directly:

```javascript
function updateUser(user) {
    user.name = "Ram";
}
```

You can return a new object:

```javascript
function updateUser(user) {
    return {
        ...user,
        name: "Ram"
    };
}

const user = {
    name: "Sandip"
};

const updatedUser = updateUser(user);

console.log(user.name);
console.log(updatedUser.name);
```

Output:

```text
Sandip
Ram
```

This approach is especially useful in React applications.

---

# 33. Parameter Naming

Use descriptive parameter names.

Less clear:

```javascript
function calculate(a, b) {
    return a * b;
}
```

Better:

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}
```

Descriptive names make functions easier to understand.

---

# 34. Too Many Parameters

Avoid functions with a very large number of parameters.

Instead of:

```javascript
function createUser(
    name,
    email,
    phone,
    age,
    city,
    role,
    active
) {
    // ...
}
```

Consider an object:

```javascript
function createUser({
    name,
    email,
    phone,
    age,
    city,
    role,
    active
}) {
    // ...
}
```

Call it:

```javascript
createUser({
    name: "Sandip",
    email: "sandip@example.com",
    phone: "9800000000",
    age: 22,
    city: "Birgunj",
    role: "user",
    active: true
});
```

This makes larger functions easier to maintain.

---

# 35. Parameters vs Return Values

Parameters send data **into** a function.

`return` sends data **out of** a function.

```javascript
function add(a, b) {
    return a + b;
}

const result = add(10, 20);
```

Flow:

```text
10 ─────┐
        ├──> function ───> 30
20 ─────┘
```

So:

```text
Arguments → Function → Return Value
```

---

# 36. Complete Example

```javascript
function calculateOrder(
    customerName,
    price,
    quantity = 1,
    ...items
) {
    const total = price * quantity;

    return {
        customerName,
        price,
        quantity,
        items,
        total
    };
}

const order = calculateOrder(
    "Sandip",
    500,
    2,
    "Momo",
    "Coffee"
);

console.log(order);
```

Result:

```javascript
{
    customerName: "Sandip",
    price: 500,
    quantity: 2,
    items: ["Momo", "Coffee"],
    total: 1000
}
```

This example combines:

* Normal parameters
* Default parameters
* Rest parameters
* Arguments
* Return values
* Objects

---

# 37. Common Mistakes

### Mistake 1: Confusing Parameters and Arguments

```javascript
function greet(name) {
    // name is parameter
}

greet("Sandip");
// "Sandip" is argument
```

---

### Mistake 2: Forgetting That Missing Arguments Become `undefined`

```javascript
function greet(name) {
    console.log(name);
}

greet();
```

Output:

```text
undefined
```

---

### Mistake 3: Putting Rest Parameter in the Middle

Incorrect:

```javascript
function test(...values, name) {
}
```

Correct:

```javascript
function test(name, ...values) {
}
```

---

### Mistake 4: Using `arguments` in an Arrow Function

Avoid:

```javascript
const test = () => {
    console.log(arguments);
};
```

Use:

```javascript
const test = (...values) => {
    console.log(values);
};
```

---

### Mistake 5: Too Many Parameters

Avoid:

```javascript
function createUser(a, b, c, d, e, f, g) {
}
```

Prefer an object:

```javascript
function createUser({
    name,
    email,
    phone,
    role
}) {
}
```

---

# 38. Quick Revision

```text
Parameter
    ↓
Variable defined in a function

Argument
    ↓
Actual value passed to the function

Default Parameter
    ↓
Parameter with a fallback value

Rest Parameter
    ↓
Collects remaining arguments into an array

arguments
    ↓
Array-like object available in traditional functions

Destructured Parameter
    ↓
Extracts values directly from objects/arrays

return
    ↓
Sends a value back to the caller
```

### Basic Syntax

```javascript
function functionName(parameter1, parameter2) {
    return parameter1 + parameter2;
}

functionName(argument1, argument2);
```

### Default Parameter

```javascript
function greet(name = "Guest") {
}
```

### Rest Parameter

```javascript
function sum(...numbers) {
}
```

### Object Parameter

```javascript
function createUser({ name, email }) {
}
```

---

# Key Takeaways

* **Parameters** are variables defined in a function.
* **Arguments** are values passed when calling a function.
* Arguments are assigned to parameters by position.
* Missing arguments normally become `undefined`.
* Default parameters provide fallback values.
* Rest parameters collect remaining arguments into an array.
* Rest parameters must be the last parameters.
* Traditional functions have an `arguments` object.
* Arrow functions do not have their own `arguments`.
* Objects and arrays can be mutated through parameters because they can refer to the same object.
* Object destructuring is useful when a function has many related inputs.
* Parameters send data **into** a function.
* `return` sends data **out of** a function.

---
