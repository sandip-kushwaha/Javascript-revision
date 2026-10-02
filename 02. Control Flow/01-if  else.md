# JavaScript if-else

Control flow determines **which code JavaScript should execute** based on conditions.

The most common decision-making statements are:

```text
if
if...else
if...else if...else
nested if
```

---

# 1. What is `if`?

The `if` statement executes a block of code **only when a condition is true**.

### Syntax

```javascript
if (condition) {
    // code
}
```

Example:

```javascript
const age = 20;

if (age >= 18) {
    console.log("You are an adult");
}
```

Output:

```text
You are an adult
```

Because:

```text
20 >= 18
```

is `true`.

---

# 2. Basic `if`

```javascript
const temperature = 30;

if (temperature > 25) {
    console.log("It is hot");
}
```

Output:

```text
It is hot
```

If the condition is false, the block is skipped.

```javascript
const temperature = 20;

if (temperature > 25) {
    console.log("It is hot");
}
```

No output.

---

# 3. Conditions Use Boolean Values

An `if` condition is evaluated as either:

```text
true
```

or:

```text
false
```

Example:

```javascript
const age = 20;

console.log(age >= 18);
```

Output:

```text
true
```

Therefore:

```javascript
if (age >= 18) {
    console.log("Allowed");
}
```

---

# 4. `if...else`

Use `else` when you want one block to execute if the condition is false.

### Syntax

```javascript
if (condition) {
    // if true
} else {
    // if false
}
```

Example:

```javascript
const age = 16;

if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}
```

Output:

```text
Minor
```

---

# 5. Example with Login

```javascript
const isLoggedIn = true;

if (isLoggedIn) {
    console.log("Welcome");
} else {
    console.log("Please login");
}
```

Output:

```text
Welcome
```

If:

```javascript
const isLoggedIn = false;
```

Output:

```text
Please login
```

---

# 6. `if...else if...else`

Use `else if` when there are multiple conditions.

### Syntax

```javascript
if (condition1) {

} else if (condition2) {

} else if (condition3) {

} else {

}
```

Example:

```javascript
const marks = 75;

if (marks >= 80) {
    console.log("A");
} else if (marks >= 60) {
    console.log("B");
} else if (marks >= 40) {
    console.log("C");
} else {
    console.log("Fail");
}
```

Output:

```text
B
```

---

# 7. How `else if` Works

JavaScript checks conditions from **top to bottom**.

Example:

```javascript
const marks = 85;

if (marks >= 80) {
    console.log("A");
} else if (marks >= 60) {
    console.log("B");
} else {
    console.log("Fail");
}
```

The first condition is true:

```text
85 >= 80
```

So JavaScript executes:

```text
A
```

and skips the remaining conditions.

---

# 8. Important: Order Matters

Consider:

```javascript
const marks = 85;

if (marks >= 40) {
    console.log("Pass");
} else if (marks >= 80) {
    console.log("A");
}
```

Output:

```text
Pass
```

Why?

Because:

```text
85 >= 40
```

is already true.

The later condition is never checked.

Better:

```javascript
if (marks >= 80) {
    console.log("A");
} else if (marks >= 40) {
    console.log("Pass");
}
```

---

# 9. Multiple Conditions with `&&`

The `&&` operator means **AND**.

Both conditions must be true.

```javascript
const age = 25;
const hasLicense = true;

if (age >= 18 && hasLicense) {
    console.log("You can drive");
}
```

Output:

```text
You can drive
```

---

# 10. Multiple Conditions with `||`

The `||` operator means **OR**.

At least one condition must be true.

```javascript
const isAdmin = false;
const isManager = true;

if (isAdmin || isManager) {
    console.log("Access granted");
}
```

Output:

```text
Access granted
```

---

# 11. NOT Operator `!`

The `!` operator reverses a Boolean value.

```javascript
const isLoggedIn = false;

if (!isLoggedIn) {
    console.log("Please login");
}
```

Output:

```text
Please login
```

Because:

```text
!false → true
```

---

# 12. Truthy Values in `if`

JavaScript automatically converts values to Boolean in conditions.

```javascript
const username = "Sandip";

if (username) {
    console.log("Username exists");
}
```

Output:

```text
Username exists
```

Because a non-empty string is truthy.

---

# 13. Falsy Values in `if`

```javascript
const username = "";

if (username) {
    console.log("Username exists");
} else {
    console.log("Username is missing");
}
```

Output:

```text
Username is missing
```

Because:

```text
"" → falsy
```

---

# 14. Common Falsy Values

```text
false
0
-0
0n
""
null
undefined
NaN
```

Example:

```javascript
if (0) {
    console.log("True");
} else {
    console.log("False");
}
```

Output:

```text
False
```

---

# 15. Empty Array and Object

An empty array is truthy:

```javascript
if ([]) {
    console.log("Array is truthy");
}
```

Output:

```text
Array is truthy
```

An empty object is also truthy:

```javascript
if ({}) {
    console.log("Object is truthy");
}
```

Output:

```text
Object is truthy
```

---

# 16. Comparing Values

Conditions commonly use comparison operators.

```javascript
const age = 20;

if (age === 20) {
    console.log("Age is 20");
}
```

Common comparison operators:

| Operator | Meaning               |
| -------- | --------------------- |
| `===`    | Strictly equal        |
| `!==`    | Strictly not equal    |
| `>`      | Greater than          |
| `<`      | Less than             |
| `>=`     | Greater than or equal |
| `<=`     | Less than or equal    |

---

# 17. Example with `>=`

```javascript
const age = 20;

if (age >= 18) {
    console.log("Eligible");
}
```

Output:

```text
Eligible
```

---

# 18. Example with `!==`

```javascript
const role = "user";

if (role !== "admin") {
    console.log("Admin access required");
}
```

Output:

```text
Admin access required
```

---

# 19. Nested `if`

An `if` statement inside another `if` is called a **nested if**.

Example:

```javascript
const isLoggedIn = true;
const role = "admin";

if (isLoggedIn) {
    if (role === "admin") {
        console.log("Admin dashboard");
    }
}
```

Output:

```text
Admin dashboard
```

---

# 20. Nested `if...else`

```javascript
const isLoggedIn = true;
const role = "user";

if (isLoggedIn) {
    if (role === "admin") {
        console.log("Admin dashboard");
    } else {
        console.log("User dashboard");
    }
} else {
    console.log("Please login");
}
```

Output:

```text
User dashboard
```

---

# 21. Practical Login Example

```javascript
const email = "sandip@example.com";
const password = "123456";

if (email && password) {
    console.log("Login request can be submitted");
} else {
    console.log("Email and password are required");
}
```

---

# 22. Practical Authentication Example

```javascript
const isLoggedIn = true;
const role = "admin";

if (!isLoggedIn) {
    console.log("Please login");
} else if (role === "admin") {
    console.log("Admin dashboard");
} else if (role === "waiter") {
    console.log("Waiter dashboard");
} else if (role === "kitchen") {
    console.log("Kitchen dashboard");
} else {
    console.log("Unauthorized role");
}
```

Output:

```text
Admin dashboard
```

---

# 23. Practical Hotel Table Example

```javascript
const tableStatus = "available";

if (tableStatus === "available") {
    console.log("Table can be booked");
} else if (tableStatus === "occupied") {
    console.log("Table is occupied");
} else if (tableStatus === "reserved") {
    console.log("Table is reserved");
} else {
    console.log("Table is unavailable");
}
```

Output:

```text
Table can be booked
```

---

# 24. Practical Hotel Capacity Example

```javascript
const customerCount = 4;
const tableCapacity = 6;

if (customerCount <= tableCapacity) {
    console.log("Booking allowed");
} else {
    console.log("Table capacity exceeded");
}
```

Output:

```text
Booking allowed
```

---

# 25. Grade Calculator

```javascript
const marks = 85;

if (marks >= 80) {
    console.log("Grade A");
} else if (marks >= 70) {
    console.log("Grade B");
} else if (marks >= 60) {
    console.log("Grade C");
} else if (marks >= 40) {
    console.log("Grade D");
} else {
    console.log("Fail");
}
```

Output:

```text
Grade A
```

---

# 26. Positive, Negative, or Zero

```javascript
const number = -5;

if (number > 0) {
    console.log("Positive");
} else if (number < 0) {
    console.log("Negative");
} else {
    console.log("Zero");
}
```

Output:

```text
Negative
```

---

# 27. Even or Odd

```javascript
const number = 10;

if (number % 2 === 0) {
    console.log("Even");
} else {
    console.log("Odd");
}
```

Output:

```text
Even
```

---

# 28. Age Category

```javascript
const age = 22;

if (age < 13) {
    console.log("Child");
} else if (age < 20) {
    console.log("Teenager");
} else {
    console.log("Adult");
}
```

Output:

```text
Adult
```

---

# 29. Checking an Array

```javascript
const users = ["Sandip", "Ram", "Hari"];

if (users.length > 0) {
    console.log("Users found");
} else {
    console.log("No users found");
}
```

Output:

```text
Users found
```

This is better than relying on:

```javascript
if (users) {
    // ...
}
```

because an empty array is still truthy.

---

# 30. Checking an Object

```javascript
const user = {
    name: "Sandip",
    role: "admin"
};

if (user.role === "admin") {
    console.log("Admin user");
}
```

Output:

```text
Admin user
```

---

# 31. Multiple Conditions

You can combine several conditions.

```javascript
const age = 25;
const isLoggedIn = true;
const role = "admin";

if (age >= 18 && isLoggedIn && role === "admin") {
    console.log("Access granted");
}
```

Output:

```text
Access granted
```

---

# 32. Grouping Conditions

Parentheses make complex conditions easier to understand.

```javascript
const age = 20;
const isStudent = true;

if (age >= 18 && (isStudent || age < 25)) {
    console.log("Condition matched");
}
```

---

# 33. `if` Without Braces

JavaScript allows:

```javascript
if (true)
    console.log("Hello");
```

However, for maintainability, prefer braces:

```javascript
if (true) {
    console.log("Hello");
}
```

Braces make code safer and easier to modify.

---

# 34. Common Mistake: Assignment Instead of Comparison

Incorrect:

```javascript
const role = "admin";

if (role = "user") {
    console.log("User");
}
```

`=` is assignment.

Use:

```javascript
if (role === "user") {
    console.log("User");
}
```

`===` compares values and types.

---

# 35. Common Mistake: Using `==`

You may see:

```javascript
if (age == "18") {
    console.log("Adult");
}
```

This can perform type coercion.

Prefer:

```javascript
if (age === 18) {
    console.log("Adult");
}
```

when `age` is expected to be a number.

---

# 36. Common Mistake with Strings

Suppose:

```javascript
const age = "18";
```

This is a string.

Therefore:

```javascript
age === 18
```

is:

```text
false
```

Convert it when appropriate:

```javascript
const age = Number("18");

if (age === 18) {
    console.log("Adult");
}
```

---

# 37. Early Return Pattern

In functions, you can reduce nested conditions with an early return.

Instead of:

```javascript
function checkUser(isLoggedIn) {
    if (isLoggedIn) {
        console.log("Welcome");
    } else {
        console.log("Please login");
    }
}
```

You can sometimes use:

```javascript
function checkUser(isLoggedIn) {
    if (!isLoggedIn) {
        console.log("Please login");
        return;
    }

    console.log("Welcome");
}
```

This becomes especially useful in backend code.

---

# 38. Practical Backend Example

```javascript
function getDashboard(user) {
    if (!user) {
        return "User not found";
    }

    if (!user.isActive) {
        return "Account is inactive";
    }

    if (user.role === "admin") {
        return "Admin dashboard";
    }

    if (user.role === "waiter") {
        return "Waiter dashboard";
    }

    return "User dashboard";
}
```

---

# 39. Ternary Operator Preview

For simple conditions, JavaScript also provides the ternary operator:

```javascript
const age = 20;

const result = age >= 18
    ? "Adult"
    : "Minor";

console.log(result);
```

Output:

```text
Adult
```

The detailed ternary operator topic will be covered separately.

---

# 40. `if` vs `if...else`

### `if`

Use when you only need to execute something when a condition is true.

```javascript
if (isLoggedIn) {
    console.log("Welcome");
}
```

### `if...else`

Use when you have two possible paths.

```javascript
if (isLoggedIn) {
    console.log("Welcome");
} else {
    console.log("Please login");
}
```

---

# 41. `if...else if...else`

Use when there are multiple possible conditions.

```javascript
if (score >= 80) {
    console.log("A");
} else if (score >= 60) {
    console.log("B");
} else if (score >= 40) {
    console.log("C");
} else {
    console.log("Fail");
}
```

---

# 42. Decision Flow

```text
              Condition
                  │
             ┌────┴────┐
           true       false
             │           │
          if block    else block
```

For multiple conditions:

```text
Condition 1?
   │
   ├── true  → Block 1
   │
   └── false
         │
      Condition 2?
         │
         ├── true  → Block 2
         │
         └── false
               │
             else
```

---

# 43. Best Practices

### 1. Prefer strict comparison

Use:

```javascript
===
!==
```

### 2. Use braces

Prefer:

```javascript
if (condition) {
    // code
}
```

### 3. Keep conditions readable

Instead of a very long condition:

```javascript
if (age >= 18 && isLoggedIn && isActive && role === "admin" && hasPermission) {
    // ...
}
```

consider using descriptive variables:

```javascript
const canAccess =
    age >= 18 &&
    isLoggedIn &&
    isActive &&
    role === "admin" &&
    hasPermission;

if (canAccess) {
    // ...
}
```

### 4. Order `else if` conditions carefully

Put more specific or higher-threshold conditions before broader ones.

### 5. Avoid unnecessary nesting

Use early returns when appropriate.

---

# Key Takeaways

* `if` executes code when a condition is truthy.
* `else` executes when the `if` condition is falsy.
* `else if` allows multiple conditions.
* Conditions are evaluated from top to bottom.
* Once an `if`/`else if` condition is true, the remaining branches are skipped.
* Use `&&` for AND conditions.
* Use `||` for OR conditions.
* Use `!` to negate a condition.
* JavaScript uses truthy/falsy conversion inside conditions.
* Empty arrays `[]` and objects `{}` are truthy.
* Prefer `===` and `!==` for comparisons.
* Use braces around conditional blocks.
* Avoid unnecessary nested conditions.
* Early returns can make complex functions easier to read.
