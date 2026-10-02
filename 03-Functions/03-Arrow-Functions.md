# JavaScript Arrow Functions

**Arrow functions** are a shorter syntax for writing functions in JavaScript.

They were introduced in **ES6 (ECMAScript 2015)**.

Arrow functions are widely used in modern JavaScript, especially in:

* React
* Node.js
* Array methods
* Callbacks
* Promises
* Event handling
* Functional programming

---

# 1. What is an Arrow Function?

A normal function expression:

```javascript
const greet = function () {
    console.log("Hello!");
};
```

The same function using an arrow function:

```javascript
const greet = () => {
    console.log("Hello!");
};
```

Call it:

```javascript
greet();
```

Output:

```text
Hello!
```

---

# 2. Basic Syntax

```javascript
const functionName = () => {
    // code
};
```

Example:

```javascript
const sayHello = () => {
    console.log("Hello, JavaScript!");
};

sayHello();
```

Output:

```text
Hello, JavaScript!
```

The `=>` symbol is called the **arrow**.

---

# 3. Arrow Function Parts

Consider:

```javascript
const greet = () => {
    console.log("Hello!");
};
```

The parts are:

```text
const       → variable declaration
greet       → function variable
()          → parameter list
=>          → arrow
{ }         → function body
```

---

# 4. Arrow Function with No Parameters

When there are no parameters, use empty parentheses:

```javascript
const greet = () => {
    console.log("Hello!");
};
```

Call it:

```javascript
greet();
```

---

# 5. Arrow Function with One Parameter

When there is exactly **one parameter**, parentheses can be omitted.

```javascript
const greet = name => {
    console.log(`Hello ${name}`);
};

greet("Sandip");
```

Output:

```text
Hello Sandip
```

Parentheses are also valid:

```javascript
const greet = (name) => {
    console.log(`Hello ${name}`);
};
```

Both forms work.

### Recommended style

Using parentheses consistently can make code easier to format and maintain:

```javascript
const greet = (name) => {
    console.log(`Hello ${name}`);
};
```

---

# 6. Arrow Function with Multiple Parameters

For multiple parameters, parentheses are required.

```javascript
const add = (a, b) => {
    return a + b;
};

console.log(add(10, 20));
```

Output:

```text
30
```

Another example:

```javascript
const calculateTotal = (price, quantity) => {
    return price * quantity;
};

console.log(calculateTotal(500, 3));
```

Output:

```text
1500
```

---

# 7. Arrow Function with `return`

A normal arrow function can use `return`:

```javascript
const add = (a, b) => {
    return a + b;
};
```

The braces create a **block body**.

With a block body, if you want a returned value, you normally write `return` explicitly.

---

# 8. Implicit Return

Arrow functions have a shorter return syntax called an **implicit return**.

Instead of:

```javascript
const add = (a, b) => {
    return a + b;
};
```

You can write:

```javascript
const add = (a, b) => a + b;
```

Then:

```javascript
console.log(add(10, 20));
```

Output:

```text
30
```

The expression after `=>` is automatically returned.

---

# 9. Explicit vs Implicit Return

### Explicit return

```javascript
const square = (number) => {
    return number * number;
};
```

### Implicit return

```javascript
const square = (number) => number * number;
```

Both return the same value.

The implicit version is useful when the function contains a simple expression.

---

# 10. Multiple Statements Require a Block Body

If you need multiple statements, use `{}`.

```javascript
const calculate = (price, quantity) => {
    const subtotal = price * quantity;
    const tax = subtotal * 0.13;

    return subtotal + tax;
};
```

Here there are multiple statements, so a block body is appropriate.

---

# 11. Returning an Object

There is an important syntax rule when implicitly returning an object.

This is incorrect:

```javascript
const createUser = () => {
    name: "Sandip",
    role: "admin"
};
```

The `{}` is interpreted as a function block rather than an object expression.

Wrap the object in parentheses:

```javascript
const createUser = () => ({
    name: "Sandip",
    role: "admin"
});
```

Now:

```javascript
console.log(createUser());
```

Output:

```text
{
    name: "Sandip",
    role: "admin"
}
```

---

# 12. Arrow Function Returning an Array

You can implicitly return an array:

```javascript
const getNumbers = () => [10, 20, 30];

console.log(getNumbers());
```

Output:

```text
[10, 20, 30]
```

---

# 13. Arrow Functions with Default Parameters

Arrow functions support default parameters.

```javascript
const greet = (name = "Guest") => {
    return `Hello ${name}`;
};

console.log(greet());
console.log(greet("Sandip"));
```

Output:

```text
Hello Guest
Hello Sandip
```

---

# 14. Arrow Functions with Rest Parameters

Arrow functions can also use rest parameters.

```javascript
const addAll = (...numbers) => {
    let total = 0;

    for (const number of numbers) {
        total += number;
    }

    return total;
};

console.log(addAll(10, 20, 30));
```

Output:

```text
60
```

The `...numbers` collects multiple arguments into an array.

---

# 15. Arrow Functions and Array Methods

Arrow functions are commonly used with array methods.

For example:

```javascript
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map((number) => number * 2);

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8, 10]
```

Another example:

```javascript
const numbers = [10, 15, 20, 25, 30];

const result = numbers.filter((number) => number > 20);

console.log(result);
```

Output:

```text
[25, 30]
```

---

# 16. Arrow Function with `forEach()`

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits.forEach((fruit) => {
    console.log(fruit);
});
```

Output:

```text
Apple
Banana
Mango
```

This is one of the most common uses of arrow functions.

---

# 17. Arrow Function with `find()`

```javascript
const users = [
    { name: "Ram", age: 20 },
    { name: "Shyam", age: 25 },
    { name: "Hari", age: 30 }
];

const user = users.find((user) => user.age === 25);

console.log(user);
```

Output:

```text
{ name: "Shyam", age: 25 }
```

---

# 18. Arrow Function with `reduce()`

```javascript
const prices = [100, 200, 300];

const total = prices.reduce(
    (sum, price) => sum + price,
    0
);

console.log(total);
```

Output:

```text
600
```

---

# 19. Arrow Functions with Callbacks

A callback is a function passed to another function.

Example:

```javascript
function execute(callback) {
    callback();
}

execute(() => {
    console.log("Callback executed!");
});
```

Output:

```text
Callback executed!
```

Arrow functions are commonly used as callbacks because their syntax is concise.

---

# 20. Arrow Functions with `setTimeout()`

```javascript
setTimeout(() => {
    console.log("Executed after 2 seconds");
}, 2000);
```

The arrow function is passed as a callback.

---

# 21. Arrow Functions with Promises

Arrow functions are commonly used with promises.

```javascript
Promise.resolve("Success")
    .then((result) => {
        console.log(result);
    });
```

Output:

```text
Success
```

They are also common with `catch()`:

```javascript
somePromise
    .catch((error) => {
        console.error(error);
    });
```

---

# 22. Arrow Functions in React

Arrow functions are very common in React.

Example:

```jsx
const UserCard = ({ name }) => {
    return <h2>Hello {name}</h2>;
};
```

A shorter version:

```jsx
const UserCard = ({ name }) => <h2>Hello {name}</h2>;
```

Event handlers also commonly use arrow functions:

```jsx
<button onClick={() => console.log("Clicked")}>
    Click
</button>
```

---

# 23. Arrow Function vs Normal Function

### Normal function

```javascript
const add = function (a, b) {
    return a + b;
};
```

### Arrow function

```javascript
const add = (a, b) => {
    return a + b;
};
```

### Short arrow version

```javascript
const add = (a, b) => a + b;
```

All three can produce the same result in this simple case.

However, arrow functions are **not completely equivalent** to normal functions.

The most important differences involve:

* `this`
* `arguments`
* `new`
* `prototype`
* constructor behavior

---

# 24. Arrow Functions Do Not Have Their Own `this`

This is one of the most important differences.

Normal functions can have their own `this` depending on how they are called.

Arrow functions do **not** create their own `this`.

Instead, an arrow function uses `this` from its surrounding lexical scope.

Example:

```javascript
const user = {
    name: "Sandip",

    greet: function () {
        console.log(this.name);
    }
};

user.greet();
```

Output:

```text
Sandip
```

The normal function receives `this` based on the object call.

---

# 25. Arrow Function and `this`

Consider:

```javascript
const user = {
    name: "Sandip",

    greet: () => {
        console.log(this.name);
    }
};

user.greet();
```

Do not expect `this` inside the arrow function to refer to `user`.

Arrow functions capture `this` from the surrounding scope.

This behavior makes arrow functions useful for callbacks where you want to preserve the surrounding `this`.

---

# 26. Practical `this` Example

A common use is inside a method with a nested callback.

```javascript
const user = {
    name: "Sandip",

    greet() {
        setTimeout(() => {
            console.log(this.name);
        }, 1000);
    }
};

user.greet();
```

The arrow function inside `setTimeout()` does not create a new `this`.

It uses the `this` from `greet()`.

After one second:

```text
Sandip
```

---

# 27. Arrow Functions Do Not Have Their Own `arguments`

Normal functions have an `arguments` object.

```javascript
function showArguments() {
    console.log(arguments);
}

showArguments(10, 20, 30);
```

Arrow functions do not have their own `arguments`.

Instead, use rest parameters:

```javascript
const showArguments = (...args) => {
    console.log(args);
};

showArguments(10, 20, 30);
```

Output:

```text
[10, 20, 30]
```

---

# 28. Arrow Functions Cannot Be Used as Constructors

Normal functions can be used with `new` when they are constructible.

Example:

```javascript
function User(name) {
    this.name = name;
}

const user = new User("Sandip");

console.log(user.name);
```

Output:

```text
Sandip
```

Arrow functions cannot be used this way:

```javascript
const User = (name) => {
    this.name = name;
};

// new User("Sandip");
```

Using `new` with an arrow function causes a `TypeError`.

Classes or constructor functions should be used when constructor behavior is needed.

---

# 29. Arrow Functions Do Not Have Their Own `prototype`

Normal constructor functions have a `prototype` property.

```javascript
function User() {}

console.log(User.prototype);
```

Arrow functions do not have their own `prototype` property:

```javascript
const User = () => {};

console.log(User.prototype);
```

The result is:

```text
undefined
```

This is another reason arrow functions are not constructor functions.

---

# 30. Arrow Function with One Parameter

These are equivalent:

```javascript
const square = (number) => number * number;
```

and:

```javascript
const square = number => number * number;
```

Parentheses around a single parameter are optional.

For consistency, many codebases prefer:

```javascript
const square = (number) => number * number;
```

---

# 31. Arrow Function with No Parameters

Parentheses are required:

```javascript
const greet = () => {
    console.log("Hello!");
};
```

You cannot write:

```javascript
const greet = => {
    console.log("Hello!");
};
```

---

# 32. Arrow Function with Multiple Parameters

Parentheses are required:

```javascript
const add = (a, b) => a + b;
```

This is invalid:

```javascript
const add = a, b => a + b;
```

---

# 33. Parentheses Around Expressions

You can use parentheses when returning complex expressions.

```javascript
const calculate = (price, quantity) => (
    price * quantity
);
```

This is useful when the returned expression spans multiple lines.

---

# 34. Practical Example: Hotel Order

```javascript
const calculateOrderTotal = (price, quantity) =>
    price * quantity;

const total = calculateOrderTotal(250, 3);

console.log(`Total: Rs. ${total}`);
```

Output:

```text
Total: Rs. 750
```

---

# 35. Practical Example: Hotel Table

```javascript
const isTableAvailable = (status) =>
    status === "available";

console.log(isTableAvailable("available"));
```

Output:

```text
true
```

---

# 36. Practical Example: Order Status

```javascript
const canServeOrder = (kitchenStatus) =>
    kitchenStatus === "ready";

console.log(canServeOrder("ready"));
```

Output:

```text
true
```

---

# 37. Practical Example: User Role

```javascript
const getDashboard = (role) =>
    role === "admin"
        ? "/admin"
        : "/user";

console.log(getDashboard("admin"));
```

Output:

```text
/admin
```

Here an arrow function and ternary operator are used together.

---

# 38. Practical Example: Product Prices

```javascript
const prices = [100, 200, 300, 400];

const discountedPrices = prices.map(
    (price) => price * 0.9
);

console.log(discountedPrices);
```

Output:

```text
[90, 180, 270, 360]
```

---

# 39. Practical Example: Filter Available Foods

```javascript
const foods = [
    { name: "Pizza", available: true },
    { name: "Burger", available: false },
    { name: "Momo", available: true }
];

const availableFoods = foods.filter(
    (food) => food.available
);

console.log(availableFoods);
```

Result:

```text
[
    { name: "Pizza", available: true },
    { name: "Momo", available: true }
]
```

---

# 40. Arrow Function with Destructuring

Arrow functions can use destructuring in parameters.

Example:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

const greetUser = ({ name, age }) => {
    console.log(`${name} is ${age} years old.`);
};

greetUser(user);
```

Output:

```text
Sandip is 22 years old.
```

This pattern is very common in React components.

---

# 41. Arrow Function with Object Return

```javascript
const createUser = (name, role) => ({
    name,
    role
});

const user = createUser("Sandip", "admin");

console.log(user);
```

Output:

```text
{
    name: "Sandip",
    role: "admin"
}
```

The parentheses around the object are important.

---

# 42. Arrow Function with Conditional Logic

```javascript
const getStatus = (isActive) =>
    isActive ? "Active" : "Inactive";

console.log(getStatus(true));
```

Output:

```text
Active
```

For more complex logic, use a block body:

```javascript
const getStatus = (user) => {
    if (!user) {
        return "Unknown";
    }

    if (!user.isActive) {
        return "Inactive";
    }

    return "Active";
};
```

---

# 43. Common Mistakes

## Mistake 1: Forgetting `return` with a block body

This does not return the result:

```javascript
const add = (a, b) => {
    a + b;
};
```

The function returns `undefined`.

Correct:

```javascript
const add = (a, b) => {
    return a + b;
};
```

Or use implicit return:

```javascript
const add = (a, b) => a + b;
```

---

## Mistake 2: Incorrect Object Return

Incorrect:

```javascript
const getUser = () => {
    name: "Sandip"
};
```

Correct:

```javascript
const getUser = () => ({
    name: "Sandip"
});
```

---

## Mistake 3: Expecting Arrow Function `this` to Refer to the Object

Do not assume:

```javascript
const user = {
    name: "Sandip",

    greet: () => {
        console.log(this.name);
    }
};
```

will make `this` refer to `user`.

Arrow functions inherit `this` from their surrounding scope.

---

## Mistake 4: Using Arrow Functions as Constructors

This is invalid:

```javascript
const User = (name) => {
    this.name = name;
};

new User("Sandip");
```

Arrow functions cannot be used with `new`.

---

## Mistake 5: Making Simple Code Too Complicated

This:

```javascript
const isAdult = (age) => {
    return age >= 18 ? true : false;
};
```

can simply be:

```javascript
const isAdult = (age) => age >= 18;
```

---

# 44. Best Practices

### 1. Use implicit return for simple expressions

Good:

```javascript
const add = (a, b) => a + b;
```

### 2. Use block bodies for complex logic

```javascript
const processOrder = (order) => {
    if (!order) {
        return null;
    }

    // additional logic

    return order;
};
```

### 3. Remember the `this` difference

Use arrow functions when lexical `this` is useful.

Use a normal function or method syntax when you need a function's own dynamic `this`.

### 4. Use `const` when the function variable does not need reassignment

```javascript
const calculateTotal = (price, quantity) =>
    price * quantity;
```

### 5. Keep arrow functions readable

Shorter does not always mean better.

Prefer:

```javascript
const calculateFinalPrice = (price, discount) => {
    const discountAmount = price * discount / 100;

    return price - discountAmount;
};
```

over forcing complicated logic into one expression.

---

# 45. Function Declaration, Function Expression, and Arrow Function

| Feature                | Function Declaration            | Function Expression                        | Arrow Function         |
| ---------------------- | ------------------------------- | ------------------------------------------ | ---------------------- |
| Example                | `function add() {}`             | `const add = function() {}`                | `const add = () => {}` |
| Short syntax           | No                              | No                                         | Yes                    |
| Can have parameters    | Yes                             | Yes                                        | Yes                    |
| Can return values      | Yes                             | Yes                                        | Yes                    |
| Own `this`             | Yes, depending on call          | Yes, depending on call                     | No                     |
| Own `arguments`        | Yes                             | Yes                                        | No                     |
| Constructor with `new` | Yes, when constructible         | Yes, when constructible                    | No                     |
| Own `prototype`        | Yes for constructible functions | Yes for constructible function expressions | No                     |
| Common callback use    | Sometimes                       | Common                                     | Very common            |

---

# 46. Arrow Function Syntax Cheat Sheet

### No parameters

```javascript
const greet = () => "Hello";
```

### One parameter

```javascript
const square = (number) => number * number;
```

### One parameter without parentheses

```javascript
const square = number => number * number;
```

### Multiple parameters

```javascript
const add = (a, b) => a + b;
```

### Block body

```javascript
const add = (a, b) => {
    return a + b;
};
```

### Object return

```javascript
const createUser = (name) => ({
    name
});
```

### Multiple statements

```javascript
const calculate = (price, quantity) => {
    const total = price * quantity;

    return total;
};
```

### Rest parameters

```javascript
const sum = (...numbers) => {
    return numbers.reduce((total, number) => total + number, 0);
};
```

---

# 47. Quick Revision

| Concept             | Example                                          |
| ------------------- | ------------------------------------------------ |
| Basic arrow         | `const greet = () => {}`                         |
| No parameters       | `() => {}`                                       |
| One parameter       | `(name) => {}`                                   |
| Multiple parameters | `(a, b) => {}`                                   |
| Implicit return     | `(a, b) => a + b`                                |
| Explicit return     | `(a, b) => { return a + b; }`                    |
| Object return       | `() => ({ name: "Sandip" })`                     |
| Rest parameters     | `(...args) => {}`                                |
| Callback            | `items.map((item) => item)`                      |
| Lexical `this`      | Arrow functions don't create their own `this`    |
| Constructor         | Arrow functions cannot be used with `new`        |
| `arguments`         | Arrow functions don't have their own `arguments` |

---

# 48. Key Takeaways

* Arrow functions were introduced in **ES6**.
* They provide a shorter way to write functions.
* Basic syntax:

  ```javascript
  const add = (a, b) => a + b;
  ```
* A single parameter can omit parentheses.
* Multiple parameters require parentheses.
* An expression body provides an **implicit return**.
* A block body requires `return` when you want to return a value.
* Objects returned implicitly need parentheses:

  ```javascript
  () => ({ key: "value" })
  ```
* Arrow functions are commonly used with `map()`, `filter()`, `reduce()`, `forEach()`, promises, and React.
* Arrow functions do **not** have their own `this`.
* Arrow functions do **not** have their own `arguments`.
* Arrow functions cannot be used as constructors with `new`.
* Arrow functions do not have their own `prototype`.
* Arrow functions are not simply a shorter version of normal functions; their behavior is different in important ways.

---
