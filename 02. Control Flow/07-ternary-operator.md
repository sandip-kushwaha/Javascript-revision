# JavaScript Ternary Operator

The **ternary operator** is a short way to write a simple `if...else` condition.

It is called **ternary** because it has three parts:

1. Condition
2. Result when condition is `true`
3. Result when condition is `false`

---

## 1. What is the Ternary Operator?

The ternary operator is a **conditional operator** used to choose between two values or expressions.

### Syntax

```javascript
condition ? expressionIfTrue : expressionIfFalse;
```

Example:

```javascript
const age = 20;

const result = age >= 18 ? "Adult" : "Minor";

console.log(result);
```

Output:

```text
Adult
```

The same logic using `if...else`:

```javascript
const age = 20;
let result;

if (age >= 18) {
    result = "Adult";
} else {
    result = "Minor";
}
```

The ternary operator makes simple conditions shorter.

---

# 2. How Ternary Operator Works

Consider:

```javascript
const age = 20;

const result = age >= 18 ? "Adult" : "Minor";
```

It works like this:

```text
             condition
                 ↓
          age >= 18
           /      \
       true       false
        ↓           ↓
    "Adult"      "Minor"
```

Since `age >= 18` is `true`:

```javascript
result = "Adult";
```

---

# 3. Basic Example

```javascript
const number = 10;

const result = number > 5 ? "Greater" : "Smaller";

console.log(result);
```

Output:

```text
Greater
```

Another example:

```javascript
const isLoggedIn = true;

const message = isLoggedIn ? "Welcome!" : "Please login.";

console.log(message);
```

Output:

```text
Welcome!
```

---

# 4. Ternary Operator with Variables

The result of a ternary expression can be stored in a variable.

```javascript
const age = 16;

const status = age >= 18 ? "Adult" : "Minor";

console.log(status);
```

Output:

```text
Minor
```

Another example:

```javascript
const score = 75;

const result = score >= 40 ? "Pass" : "Fail";

console.log(result);
```

Output:

```text
Pass
```

---

# 5. Ternary Operator with Comparison

You can use comparison operators inside a ternary expression.

```javascript
const a = 10;
const b = 20;

const result = a > b ? "A is greater" : "B is greater";

console.log(result);
```

Output:

```text
B is greater
```

Using strict equality:

```javascript
const role = "admin";

const message = role === "admin"
    ? "Admin Dashboard"
    : "User Dashboard";

console.log(message);
```

Output:

```text
Admin Dashboard
```

---

# 6. Ternary Operator with Boolean Values

Ternary operators are commonly used with boolean conditions.

```javascript
const isActive = true;

const status = isActive ? "Active" : "Inactive";

console.log(status);
```

Output:

```text
Active
```

Another example:

```javascript
const isAvailable = false;

const message = isAvailable ? "Available" : "Not Available";

console.log(message);
```

Output:

```text
Not Available
```

---

# 7. Ternary Operator with Truthy and Falsy Values

The condition does not have to explicitly return `true` or `false`.

JavaScript evaluates the condition using **truthy/falsy** rules.

```javascript
const username = "Sandip";

const message = username ? "User exists" : "No username";

console.log(message);
```

Output:

```text
User exists
```

Because a non-empty string is truthy.

Example with an empty string:

```javascript
const username = "";

const message = username ? "User exists" : "No username";

console.log(message);
```

Output:

```text
No username
```

---

# 8. Common Truthy and Falsy Values

### Falsy values

```javascript
false
0
-0
0n
""
null
undefined
NaN
```

### Truthy values

Almost everything else is truthy.

For example:

```javascript
"hello"
42
[]
{}
true
```

Important:

```javascript
const result = [] ? "Truthy" : "Falsy";

console.log(result);
```

Output:

```text
Truthy
```

An empty array is truthy.

Similarly:

```javascript
const result = {} ? "Truthy" : "Falsy";

console.log(result);
```

Output:

```text
Truthy
```

---

# 9. Ternary Operator with Functions

A ternary expression can be returned from a function.

```javascript
function getStatus(age) {
    return age >= 18 ? "Adult" : "Minor";
}

console.log(getStatus(25));
```

Output:

```text
Adult
```

Another example:

```javascript
function getOrderStatus(isReady) {
    return isReady ? "Ready to serve" : "Still preparing";
}

console.log(getOrderStatus(true));
```

Output:

```text
Ready to serve
```

---

# 10. Ternary Operator with `return`

You can directly return a ternary expression.

```javascript
function checkNumber(number) {
    return number > 0 ? "Positive" : "Not positive";
}
```

This is shorter than:

```javascript
function checkNumber(number) {
    if (number > 0) {
        return "Positive";
    } else {
        return "Not positive";
    }
}
```

---

# 11. Ternary Operator with `console.log()`

You can use a ternary expression directly inside `console.log()`.

```javascript
const age = 22;

console.log(age >= 18 ? "Adult" : "Minor");
```

Output:

```text
Adult
```

Another example:

```javascript
const isOnline = true;

console.log(isOnline ? "Online" : "Offline");
```

Output:

```text
Online
```

---

# 12. Nested Ternary Operator

A ternary operator can be placed inside another ternary operator.

Example:

```javascript
const score = 85;

const grade =
    score >= 90
        ? "A"
        : score >= 80
            ? "B"
            : score >= 70
                ? "C"
                : "D";

console.log(grade);
```

Output:

```text
B
```

This is called a **nested ternary**.

### Be careful

Nested ternaries can become difficult to read.

For example:

```javascript
const result =
    condition1
        ? value1
        : condition2
            ? value2
            : condition3
                ? value3
                : value4;
```

For many conditions, `if...else if...else` or `switch` is usually easier to understand.

---

# 13. Ternary vs `if...else`

### Ternary

```javascript
const age = 20;

const status = age >= 18 ? "Adult" : "Minor";
```

### `if...else`

```javascript
const age = 20;
let status;

if (age >= 18) {
    status = "Adult";
} else {
    status = "Minor";
}
```

### General difference

| Ternary                          | `if...else`                    |
| -------------------------------- | ------------------------------ |
| Short                            | More verbose                   |
| Expression                       | Statement                      |
| Good for simple choices          | Good for complex logic         |
| Returns a value                  | Controls execution             |
| Can become confusing when nested | Easier for multiple conditions |

---

# 14. Ternary is an Expression

One important concept is that the ternary operator produces a **value**.

Example:

```javascript
const result = true ? "Yes" : "No";

console.log(result);
```

The ternary expression produces:

```text
"Yes"
```

Therefore it can be assigned:

```javascript
const result = condition ? value1 : value2;
```

It can also be returned:

```javascript
return condition ? value1 : value2;
```

And passed to a function:

```javascript
console.log(condition ? value1 : value2);
```

---

# 15. Ternary with Multiple Conditions

You can combine conditions using logical operators.

```javascript
const age = 25;
const hasID = true;

const result =
    age >= 18 && hasID
        ? "Entry allowed"
        : "Entry denied";

console.log(result);
```

Output:

```text
Entry allowed
```

Another example:

```javascript
const username = "Sandip";
const passwordCorrect = true;

const message =
    username && passwordCorrect
        ? "Login successful"
        : "Login failed";

console.log(message);
```

---

# 16. Ternary with `null` and `undefined`

Example:

```javascript
const username = null;

const displayName = username !== null
    ? username
    : "Guest";

console.log(displayName);
```

Output:

```text
Guest
```

You can also use nullish coalescing when you specifically want to handle `null` or `undefined`:

```javascript
const username = null;

const displayName = username ?? "Guest";

console.log(displayName);
```

Output:

```text
Guest
```

### Difference

Ternary:

```javascript
condition ? value1 : value2;
```

Nullish coalescing:

```javascript
value ?? fallback;
```

`??` only falls back when the value is:

```text
null
undefined
```

It does **not** treat these as missing:

```javascript
0
""
false
```

Example:

```javascript
const count = 0;

console.log(count ?? 10);
```

Output:

```text
0
```

---

# 17. Ternary vs `||`

Consider:

```javascript
const count = 0;

const result = count || 10;

console.log(result);
```

Output:

```text
10
```

Because `0` is falsy.

Using `??`:

```javascript
const result = count ?? 10;

console.log(result);
```

Output:

```text
0
```

Using a ternary:

```javascript
const result = count === undefined
    ? 10
    : count;
```

Output:

```text
0
```

Choose the operator based on what your condition actually means.

---

# 18. Practical Example: Hotel Table Status

Suppose a hotel table has a status:

```javascript
const tableStatus = "occupied";

const message =
    tableStatus === "available"
        ? "Table is available"
        : "Table is occupied";

console.log(message);
```

Output:

```text
Table is occupied
```

---

# 19. Practical Example: Order Status

```javascript
const kitchenStatus = "ready";

const message =
    kitchenStatus === "ready"
        ? "Order is ready to serve"
        : "Order is still preparing";

console.log(message);
```

Output:

```text
Order is ready to serve
```

---

# 20. Practical Example: User Role

```javascript
const role = "admin";

const dashboard =
    role === "admin"
        ? "/admin"
        : "/user";

console.log(dashboard);
```

Output:

```text
/admin
```

For several roles, a more structured approach is often clearer than deeply nested ternaries.

---

# 21. Practical Example: Product Availability

```javascript
const isAvailable = true;

const buttonText =
    isAvailable
        ? "Add to Cart"
        : "Out of Stock";

console.log(buttonText);
```

Output:

```text
Add to Cart
```

---

# 22. Practical Example: React

Ternary operators are commonly used in React for conditional rendering.

```jsx
function UserStatus({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? <p>Welcome!</p> : <p>Please login.</p>}
        </div>
    );
}
```

If:

```javascript
isLoggedIn = true;
```

React displays:

```text
Welcome!
```

If:

```javascript
isLoggedIn = false;
```

React displays:

```text
Please login.
```

---

# 23. Ternary for Conditional Class Names

Example:

```javascript
const isActive = true;

const className = isActive
    ? "active"
    : "inactive";

console.log(className);
```

Output:

```text
active
```

This pattern is commonly used in frontend applications.

---

# 24. Ternary for Conditional Values

You can choose different values based on a condition.

```javascript
const isDarkMode = true;

const background = isDarkMode ? "black" : "white";

console.log(background);
```

Output:

```text
black
```

Another example:

```javascript
const isAdmin = false;

const permissions = isAdmin
    ? "full-access"
    : "limited-access";

console.log(permissions);
```

---

# 25. Ternary with Template Literals

Ternary expressions can be used inside template literals.

```javascript
const name = "Sandip";
const isAdmin = true;

const message = `Hello ${name}, you have ${
    isAdmin ? "admin" : "user"
} access.`;

console.log(message);
```

Output:

```text
Hello Sandip, you have admin access.
```

---

# 26. Ternary with Object Properties

```javascript
const user = {
    name: "Sandip",
    isActive: true
};

const status = user.isActive
    ? "Active"
    : "Inactive";

console.log(status);
```

Output:

```text
Active
```

---

# 27. Common Mistakes

## Mistake 1: Forgetting `:`

Incorrect:

```javascript
const result = age >= 18 ? "Adult";
```

A ternary requires both outcomes.

Correct:

```javascript
const result = age >= 18 ? "Adult" : "Minor";
```

---

## Mistake 2: Using Statements as Ternary Results

A ternary is intended for expressions.

Avoid trying to write complex statement blocks inside it:

```javascript
condition ? ifSomething() : ifSomethingElse();
```

This can be valid if the functions are expressions/calls, but complex logic is usually clearer with `if...else`.

---

## Mistake 3: Too Many Nested Ternaries

Avoid code like:

```javascript
const result =
    a ? x :
    b ? y :
    c ? z :
    d ? p :
    q;
```

For complicated business logic, use:

```javascript
if (a) {
    // ...
} else if (b) {
    // ...
} else if (c) {
    // ...
} else {
    // ...
}
```

Readable code is more important than making code as short as possible.

---

## Mistake 4: Unnecessary Ternary

Avoid:

```javascript
const isAdult = age >= 18
    ? true
    : false;
```

Simply write:

```javascript
const isAdult = age >= 18;
```

The comparison already produces a boolean.

---

## Mistake 5: Confusing Ternary with `if...else`

This:

```javascript
condition ? value1 : value2;
```

is an expression that produces a value.

This:

```javascript
if (condition) {
    // code
} else {
    // code
}
```

is a control-flow statement.

They can solve similar problems, but they are not exactly the same construct.

---

# 28. Best Practices

### 1. Use ternary for simple conditions

Good:

```javascript
const status = isActive ? "Active" : "Inactive";
```

### 2. Avoid deeply nested ternaries

If the logic becomes difficult to read, use `if...else`.

### 3. Keep both outcomes meaningful

Good:

```javascript
const message = isLoggedIn
    ? "Welcome back"
    : "Please login";
```

### 4. Avoid unnecessary ternaries

Instead of:

```javascript
const result = isValid ? true : false;
```

Use:

```javascript
const result = isValid;
```

### 5. Use parentheses when expressions become complex

```javascript
const result =
    (age >= 18 && hasID)
        ? "Allowed"
        : "Denied";
```

Parentheses can make the condition easier to understand.

---

# 29. Ternary Operator Quick Syntax

```javascript
condition ? trueValue : falseValue;
```

Example:

```javascript
const age = 20;

const status = age >= 18 ? "Adult" : "Minor";
```

Think of it as:

```text
condition
   ?
value if TRUE
   :
value if FALSE
```

---

# 30. Quick Revision

| Concept             | Example                            |
| ------------------- | ---------------------------------- |
| Basic ternary       | `condition ? a : b`                |
| True result         | `condition ? "Yes" : "No"`         |
| Store result        | `const x = condition ? a : b`      |
| Return result       | `return condition ? a : b`         |
| Boolean condition   | `isActive ? "Active" : "Inactive"` |
| Comparison          | `age >= 18 ? "Adult" : "Minor"`    |
| Nested ternary      | `a ? x : b ? y : z`                |
| Nullish alternative | `value ?? fallback`                |
| React rendering     | `{condition ? <A /> : <B />}`      |

---

# 31. Key Takeaways

* The **ternary operator** is JavaScript's conditional operator.
* It has **three parts**:

  ```javascript
  condition ? trueValue : falseValue
  ```
* It is useful for **simple conditional values**.
* The ternary operator produces a **value**.
* It can be assigned to variables.
* It can be returned from functions.
* It can be used inside template literals.
* It is widely used in React conditional rendering.
* Avoid deeply nested ternary expressions.
* Don't use a ternary when a simple boolean expression is enough.
* For complex business logic, `if...else` is generally easier to read.
* `??` is different from ternary and is specifically useful for `null`/`undefined` fallbacks.

---
