# JavaScript `switch`

The `switch` statement is used to execute different blocks of code based on the value of an expression.

It is especially useful when you need to compare **one value against multiple possible values**.

---

# 1. What is `switch`?

Example:

```javascript
const role = "admin";

switch (role) {
    case "admin":
        console.log("Admin Dashboard");
        break;

    case "waiter":
        console.log("Waiter Dashboard");
        break;

    case "kitchen":
        console.log("Kitchen Dashboard");
        break;

    default:
        console.log("Unknown Role");
}
```

Output:

```text
Admin Dashboard
```

---

# 2. Syntax

```javascript
switch (expression) {
    case value1:
        // code
        break;

    case value2:
        // code
        break;

    default:
        // code
}
```

The main parts are:

```text
switch
case
break
default
```

---

# 3. How `switch` Works

Suppose:

```javascript
const day = 2;
```

JavaScript checks:

```text
day === 1
day === 2
day === 3
...
```

When a matching `case` is found, its code executes.

Example:

```javascript
const day = 2;

switch (day) {
    case 1:
        console.log("Sunday");
        break;

    case 2:
        console.log("Monday");
        break;

    case 3:
        console.log("Tuesday");
        break;
}
```

Output:

```text
Monday
```

---

# 4. `case`

A `case` represents one possible value.

```javascript
const status = "ready";

switch (status) {
    case "pending":
        console.log("Order is pending");
        break;

    case "ready":
        console.log("Order is ready");
        break;
}
```

Output:

```text
Order is ready
```

---

# 5. `break`

`break` stops the `switch` statement.

Example:

```javascript
const role = "admin";

switch (role) {
    case "admin":
        console.log("Admin");
        break;

    case "user":
        console.log("User");
        break;
}
```

Once `"admin"` matches:

```text
Admin
```

is printed and the `switch` stops.

---

# 6. What Happens Without `break`?

Consider:

```javascript
const number = 1;

switch (number) {
    case 1:
        console.log("One");

    case 2:
        console.log("Two");

    case 3:
        console.log("Three");
}
```

Output:

```text
One
Two
Three
```

Why?

Because there is no `break`.

JavaScript continues executing the following cases.

This behavior is called **fall-through**.

---

# 7. Fall-Through

Fall-through means execution continues into the next case after a match.

Example:

```javascript
const value = 1;

switch (value) {
    case 1:
        console.log("Case 1");

    case 2:
        console.log("Case 2");
}
```

Output:

```text
Case 1
Case 2
```

Normally, if you don't intentionally want fall-through, use:

```javascript
break;
```

---

# 8. `default`

`default` executes when none of the cases match.

Example:

```javascript
const role = "guest";

switch (role) {
    case "admin":
        console.log("Admin");
        break;

    case "user":
        console.log("User");
        break;

    default:
        console.log("Unknown role");
}
```

Output:

```text
Unknown role
```

---

# 9. `default` Is Optional

You can write:

```javascript
const number = 10;

switch (number) {
    case 1:
        console.log("One");
        break;

    case 2:
        console.log("Two");
        break;
}
```

If no case matches, nothing happens.

However, `default` is often useful when you need to handle unexpected values.

---

# 10. `switch` Uses Strict Matching

`switch` compares the expression with each case using strict equality semantics.

For example:

```javascript
const value = 5;

switch (value) {
    case "5":
        console.log("String");
        break;

    case 5:
        console.log("Number");
        break;
}
```

Output:

```text
Number
```

Because:

```javascript
5 === "5"
```

is:

```text
false
```

while:

```javascript
5 === 5
```

is:

```text
true
```

---

# 11. `switch` with Strings

Strings are commonly used with `switch`.

```javascript
const command = "start";

switch (command) {
    case "start":
        console.log("Starting...");
        break;

    case "stop":
        console.log("Stopping...");
        break;

    case "restart":
        console.log("Restarting...");
        break;

    default:
        console.log("Unknown command");
}
```

Output:

```text
Starting...
```

---

# 12. `switch` with Numbers

```javascript
const month = 5;

switch (month) {
    case 1:
        console.log("January");
        break;

    case 2:
        console.log("February");
        break;

    case 3:
        console.log("March");
        break;

    case 4:
        console.log("April");
        break;

    case 5:
        console.log("May");
        break;

    default:
        console.log("Invalid month");
}
```

Output:

```text
May
```

---

# 13. Multiple Cases with the Same Code

You can intentionally group multiple cases.

Example:

```javascript
const day = "Saturday";

switch (day) {
    case "Saturday":
    case "Sunday":
        console.log("Weekend");
        break;

    default:
        console.log("Weekday");
}
```

Output:

```text
Weekend
```

Here:

```text
Saturday
Sunday
```

both execute the same block.

---

# 14. Grouping More Cases

```javascript
const day = "Friday";

switch (day) {
    case "Saturday":
    case "Sunday":
        console.log("Weekend");
        break;

    case "Monday":
    case "Tuesday":
    case "Wednesday":
    case "Thursday":
    case "Friday":
        console.log("Weekday");
        break;

    default:
        console.log("Invalid day");
}
```

Output:

```text
Weekday
```

This is intentional fall-through.

---

# 15. Practical Example — User Roles

```javascript
const role = "waiter";

switch (role) {
    case "admin":
        console.log("Open Admin Dashboard");
        break;

    case "waiter":
        console.log("Open Waiter Dashboard");
        break;

    case "kitchen":
        console.log("Open Kitchen Dashboard");
        break;

    default:
        console.log("Access denied");
}
```

Output:

```text
Open Waiter Dashboard
```

---

# 16. Practical Example — Order Status

A hotel ordering system can have several order statuses.

```javascript
const status = "preparing";

switch (status) {
    case "pending":
        console.log("Order is waiting for confirmation");
        break;

    case "confirmed":
        console.log("Order has been confirmed");
        break;

    case "preparing":
        console.log("Kitchen is preparing the order");
        break;

    case "ready":
        console.log("Order is ready");
        break;

    case "served":
        console.log("Order has been served");
        break;

    case "completed":
        console.log("Order completed");
        break;

    case "cancelled":
        console.log("Order cancelled");
        break;

    default:
        console.log("Unknown order status");
}
```

Output:

```text
Kitchen is preparing the order
```

---

# 17. Practical Example — Table Status

```javascript
const tableStatus = "occupied";

switch (tableStatus) {
    case "available":
        console.log("Table is available");
        break;

    case "occupied":
        console.log("Table is occupied");
        break;

    case "reserved":
        console.log("Table is reserved");
        break;

    case "cleaning":
        console.log("Table is being cleaned");
        break;

    case "maintenance":
        console.log("Table is under maintenance");
        break;

    default:
        console.log("Unknown table status");
}
```

Output:

```text
Table is occupied
```

---

# 18. Practical Example — HTTP Methods

```javascript
const method = "POST";

switch (method) {
    case "GET":
        console.log("Read data");
        break;

    case "POST":
        console.log("Create data");
        break;

    case "PATCH":
        console.log("Update data");
        break;

    case "DELETE":
        console.log("Delete data");
        break;

    default:
        console.log("Unsupported method");
}
```

Output:

```text
Create data
```

---

# 19. Practical Example — HTTP Status

```javascript
const statusCode = 404;

switch (statusCode) {
    case 200:
        console.log("Success");
        break;

    case 201:
        console.log("Created");
        break;

    case 400:
        console.log("Bad Request");
        break;

    case 401:
        console.log("Unauthorized");
        break;

    case 403:
        console.log("Forbidden");
        break;

    case 404:
        console.log("Not Found");
        break;

    case 500:
        console.log("Internal Server Error");
        break;

    default:
        console.log("Unknown status");
}
```

Output:

```text
Not Found
```

---

# 20. `switch` vs `if...else`

Both can solve similar problems.

### `if...else`

```javascript
if (role === "admin") {
    console.log("Admin");
} else if (role === "user") {
    console.log("User");
} else {
    console.log("Unknown");
}
```

### `switch`

```javascript
switch (role) {
    case "admin":
        console.log("Admin");
        break;

    case "user":
        console.log("User");
        break;

    default:
        console.log("Unknown");
}
```

---

# 21. When to Use `switch`

`switch` can be useful when:

* Comparing one expression against many fixed values
* Handling status values
* Handling user roles
* Handling commands
* Handling menu choices
* Handling HTTP methods
* Handling application states

Example:

```text
role
status
command
day
month
menu option
HTTP method
```

---

# 22. When `if...else` Is Better

`if...else` is usually more suitable for ranges or complex Boolean conditions.

For example:

```javascript
const marks = 75;

if (marks >= 80) {
    console.log("A");
} else if (marks >= 60) {
    console.log("B");
} else {
    console.log("C");
}
```

This is naturally expressed using conditions and ranges.

A `switch` is generally more natural when you have fixed values such as:

```javascript
"pending"
"confirmed"
"preparing"
"ready"
```

---

# 23. `switch` with Boolean Expression

You can use `switch (true)` for condition-like behavior:

```javascript
const marks = 75;

switch (true) {
    case marks >= 80:
        console.log("A");
        break;

    case marks >= 60:
        console.log("B");
        break;

    case marks >= 40:
        console.log("C");
        break;

    default:
        console.log("Fail");
}
```

Output:

```text
B
```

However, for this type of range-based logic, `if...else if...else` is usually clearer.

---

# 24. `switch` with Expressions

The expression inside `switch` can be more than a variable.

```javascript
const age = 20;

switch (age >= 18) {
    case true:
        console.log("Adult");
        break;

    case false:
        console.log("Minor");
        break;
}
```

Output:

```text
Adult
```

But again, a normal `if...else` is usually clearer for this situation.

---

# 25. Using `return` Instead of `break`

Inside a function, you can use `return`.

```javascript
function getRoleMessage(role) {
    switch (role) {
        case "admin":
            return "Admin Dashboard";

        case "waiter":
            return "Waiter Dashboard";

        case "kitchen":
            return "Kitchen Dashboard";

        default:
            return "Unknown Role";
    }
}

console.log(getRoleMessage("admin"));
```

Output:

```text
Admin Dashboard
```

Because `return` exits the function.

---

# 26. Practical Function Example

```javascript
function getOrderMessage(status) {
    switch (status) {
        case "pending":
            return "Order is pending";

        case "confirmed":
            return "Order confirmed";

        case "preparing":
            return "Order is being prepared";

        case "ready":
            return "Order is ready";

        case "served":
            return "Order served";

        case "completed":
            return "Order completed";

        case "cancelled":
            return "Order cancelled";

        default:
            return "Unknown order status";
    }
}

console.log(getOrderMessage("ready"));
```

Output:

```text
Order is ready
```

---

# 27. Nested `switch`

A `switch` can technically be placed inside another `switch`.

```javascript
const role = "admin";
const action = "delete";

switch (role) {
    case "admin":
        switch (action) {
            case "delete":
                console.log("Delete allowed");
                break;

            case "update":
                console.log("Update allowed");
                break;
        }
        break;

    default:
        console.log("Access denied");
}
```

Nested structures can become difficult to maintain, so use them only when they genuinely improve the logic.

---

# 28. `switch` with `const`

The value being switched can be stored in a constant:

```javascript
const paymentStatus = "paid";

switch (paymentStatus) {
    case "pending":
        console.log("Payment pending");
        break;

    case "paid":
        console.log("Payment successful");
        break;

    case "failed":
        console.log("Payment failed");
        break;

    default:
        console.log("Unknown payment status");
}
```

---

# 29. Common Mistake — Forgetting `break`

Incorrect:

```javascript
switch (role) {
    case "admin":
        console.log("Admin");

    case "user":
        console.log("User");
}
```

If `role` is `"admin"`, both messages can execute.

Correct:

```javascript
switch (role) {
    case "admin":
        console.log("Admin");
        break;

    case "user":
        console.log("User");
        break;
}
```

---

# 30. Common Mistake — Incorrect `case` Syntax

Incorrect:

```javascript
switch (role) {
    case:
        "admin"
        console.log("Admin");
}
```

Correct:

```javascript
switch (role) {
    case "admin":
        console.log("Admin");
        break;
}
```

The value comes immediately after `case`.

---

# 31. Common Mistake — Assignment

A `case` is not written using assignment.

Incorrect:

```javascript
case role = "admin":
```

Correct:

```javascript
case "admin":
```

The `switch` expression already contains the value being compared.

---

# 32. `switch` and Strict Matching

Remember:

```javascript
switch (value)
```

compares cases using strict matching semantics.

Example:

```javascript
const value = "1";

switch (value) {
    case 1:
        console.log("Number");
        break;

    case "1":
        console.log("String");
        break;
}
```

Output:

```text
String
```

Because:

```javascript
"1" === 1
```

is false.

---

# 33. Menu Example

```javascript
const option = 2;

switch (option) {
    case 1:
        console.log("View Profile");
        break;

    case 2:
        console.log("Edit Profile");
        break;

    case 3:
        console.log("Change Password");
        break;

    case 4:
        console.log("Logout");
        break;

    default:
        console.log("Invalid option");
}
```

Output:

```text
Edit Profile
```

---

# 34. Day Example

```javascript
const day = 1;

switch (day) {
    case 1:
        console.log("Sunday");
        break;

    case 2:
        console.log("Monday");
        break;

    case 3:
        console.log("Tuesday");
        break;

    case 4:
        console.log("Wednesday");
        break;

    case 5:
        console.log("Thursday");
        break;

    case 6:
        console.log("Friday");
        break;

    case 7:
        console.log("Saturday");
        break;

    default:
        console.log("Invalid day");
}
```

Output:

```text
Sunday
```

---

# 35. Calculator Example

```javascript
const a = 10;
const b = 5;
const operator = "*";

switch (operator) {
    case "+":
        console.log(a + b);
        break;

    case "-":
        console.log(a - b);
        break;

    case "*":
        console.log(a * b);
        break;

    case "/":
        console.log(a / b);
        break;

    default:
        console.log("Invalid operator");
}
```

Output:

```text
50
```

---

# 36. Intentional Fall-Through

Fall-through isn't always a mistake.

Example:

```javascript
const role = "admin";

switch (role) {
    case "admin":
    case "manager":
        console.log("Management access");
        break;

    case "user":
        console.log("User access");
        break;

    default:
        console.log("No access");
}
```

Here both:

```text
admin
manager
```

intentionally use the same code.

---

# 37. Best Practices

### Use `break` when cases should be independent

```javascript
case "admin":
    console.log("Admin");
    break;
```

### Use grouped cases for shared behavior

```javascript
case "admin":
case "manager":
    console.log("Management");
    break;
```

### Use `default` for unexpected values

```javascript
default:
    console.log("Unknown value");
```

### Keep cases simple

If a case contains complicated business logic, consider moving that logic into a function.

---

# 38. `switch` Decision Flow

```text
             switch(value)
                  │
       ┌──────────┼──────────┐
       │          │          │
     case 1     case 2     case 3
       │          │          │
       ↓          ↓          ↓
     code       code       code
       │          │          │
      break      break      break
       │          │          │
       └──────────┴──────────┘
                  │
                end
```

If no case matches:

```text
             switch(value)
                  │
            no case matches
                  │
               default
                  │
                 code
```

---

# Key Takeaways

* `switch` is used for multiple possible values of one expression.
* `case` defines a possible matching value.
* `break` stops execution after a case.
* Missing `break` can cause fall-through.
* Fall-through can also be intentional when multiple cases share the same code.
* `default` handles values that do not match any case.
* `switch` uses strict matching semantics.
* `"5"` and `5` are different cases.
* Multiple cases can share one block.
* `return` can be used inside a `switch` within a function.
* `switch` is useful for fixed values such as roles, statuses, commands, and menu options.
* `if...else` is generally clearer for ranges and complex Boolean conditions.
