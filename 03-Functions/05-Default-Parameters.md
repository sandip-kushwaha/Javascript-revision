# JavaScript Default Parameters

Default parameters allow you to assign a **default value to a function parameter** when no value is provided or the argument is `undefined`.

They make functions safer and easier to use.

---

## 1. What Are Default Parameters?

Normally, if an argument is not provided, the parameter becomes `undefined`.

```javascript
function greet(name) {
    console.log(`Hello, ${name}`);
}

greet();
```

Output:

```text
Hello, undefined
```

With a default parameter:

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet();
```

Output:

```text
Hello, Guest
```

Here:

```text
name = "Guest"
```

is a **default parameter**.

---

## 2. Basic Syntax

```javascript
function functionName(parameter = defaultValue) {
    // code
}
```

Example:

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}
```

---

## 3. Providing an Argument

If you provide a value, the default value is not used.

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet("Sandip");
```

Output:

```text
Hello, Sandip
```

The provided value replaces the default value.

---

## 4. No Argument

If no argument is provided, the default value is used.

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet();
```

Output:

```text
Hello, Guest
```

---

# 5. `undefined` Uses the Default

Passing `undefined` also causes the default value to be used.

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet(undefined);
```

Output:

```text
Hello, Guest
```

So these behave similarly:

```javascript
greet();
greet(undefined);
```

---

# 6. `null` Does Not Use the Default

`null` is different from `undefined`.

```javascript
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet(null);
```

Output:

```text
Hello, null
```

The default value is used only when the argument is `undefined` or omitted.

---

# 7. Default Parameters with Numbers

```javascript
function calculateTotal(price, quantity = 1) {
    return price * quantity;
}

console.log(calculateTotal(500));
```

Output:

```text
500
```

Because:

```text
price = 500
quantity = 1
```

If you provide the quantity:

```javascript
console.log(calculateTotal(500, 3));
```

Output:

```text
1500
```

---

# 8. Multiple Default Parameters

A function can have multiple default parameters.

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

---

# 9. Override Default Values

You can override the defaults by passing arguments.

```javascript
function createUser(
    name = "Guest",
    role = "user",
    active = true
) {
    return {
        name,
        role,
        active
    };
}

console.log(
    createUser("Sandip", "admin", false)
);
```

Result:

```javascript
{
    name: "Sandip",
    role: "admin",
    active: false
}
```

---

# 10. Skip a Default Parameter

JavaScript does not have a special syntax for "skip this argument".

You can use `undefined`.

```javascript
function createUser(
    name = "Guest",
    role = "user",
    active = true
) {
    return {
        name,
        role,
        active
    };
}

createUser(
    "Sandip",
    undefined,
    false
);
```

Result:

```javascript
{
    name: "Sandip",
    role: "user",
    active: false
}
```

Here:

```text
name   → "Sandip"
role   → default "user"
active → false
```

---

# 11. Default Parameters Can Use Expressions

A default value does not have to be a simple value.

```javascript
function generateId(id = Math.random()) {
    console.log(id);
}

generateId();
```

The expression is evaluated when the default is needed.

---

# 12. Default Parameter Can Call a Function

```javascript
function getDefaultName() {
    return "Guest";
}

function greet(name = getDefaultName()) {
    console.log(`Hello, ${name}`);
}

greet();
```

Output:

```text
Hello, Guest
```

The function `getDefaultName()` is called because no `name` was supplied.

---

# 13. Default Parameter Evaluation

Default parameters are evaluated **when the function is called**, not when the function is created.

```javascript
function getTime() {
    return new Date().toLocaleTimeString();
}

function showTime(time = getTime()) {
    console.log(time);
}

showTime();
```

`getTime()` is evaluated when `showTime()` needs its default.

---

# 14. Default Parameters and Scope

Default parameter expressions have their own parameter scope.

For example:

```javascript
function example(value = 10) {
    console.log(value);
}

example();
```

Output:

```text
10
```

Parameters are available to later parameter defaults.

```javascript
function calculate(a = 10, b = a * 2) {
    return b;
}

console.log(calculate());
```

Output:

```text
20
```

Here:

```text
a = 10
b = a * 2
  = 20
```

---

# 15. Earlier Parameters Can Be Used

A later default parameter can use an earlier parameter.

```javascript
function multiply(
    number = 5,
    result = number * 2
) {
    return result;
}

console.log(multiply());
```

Output:

```text
10
```

This works because `number` appears before `result`.

---

# 16. Parameter Order Matters

This works:

```javascript
function example(a = 10, b = a + 5) {
    return b;
}
```

But reversing the dependency can cause an error:

```javascript
function example(a = b, b = 10) {
    return a;
}
```

The later parameter `b` is not available to the earlier default expression.

---

# 17. Default Parameters with Destructuring

Default parameters work well with object destructuring.

```javascript
function createUser({
    name = "Guest",
    role = "user"
} = {}) {
    return {
        name,
        role
    };
}

console.log(createUser());
```

Result:

```javascript
{
    name: "Guest",
    role: "user"
}
```

The `= {}` protects the function when no object is passed.

---

# 18. Default Values in Object Destructuring

```javascript
function displayUser({
    name = "Guest",
    age = 18
}) {
    console.log(name);
    console.log(age);
}

displayUser({
    name: "Sandip"
});
```

Output:

```text
Sandip
18
```

Only `age` uses its default value.

---

# 19. Default Parameters with Arrays

```javascript
function showNumbers(numbers = []) {
    console.log(numbers);
}

showNumbers();
```

Output:

```text
[]
```

You can provide an array:

```javascript
showNumbers([10, 20, 30]);
```

Output:

```text
[10, 20, 30]
```

---

# 20. Default Parameter vs `||`

A common older pattern is:

```javascript
function greet(name) {
    name = name || "Guest";

    console.log(name);
}
```

But `||` treats **all falsy values** as missing.

For example:

```javascript
function show(value) {
    value = value || "Default";
    console.log(value);
}

show(0);
```

Output:

```text
Default
```

But `0` may be a valid value.

Default parameters behave differently:

```javascript
function show(value = "Default") {
    console.log(value);
}

show(0);
```

Output:

```text
0
```

This is an important difference.

---

# 21. Default Parameter vs Nullish Coalescing

Default parameters use the default when the argument is:

```text
undefined
```

Nullish coalescing uses the right-hand value when the expression is:

```text
null
undefined
```

Example:

```javascript
function show(value = "Default") {
    console.log(value);
}

show(null);
```

Output:

```text
null
```

Using `??`:

```javascript
const value = null ?? "Default";

console.log(value);
```

Output:

```text
Default
```

---

# 22. Default Parameter vs Falsy Values

Default parameters do **not** replace these values:

```text
0
false
""
null
```

Example:

```javascript
function show(value = "Default") {
    console.log(value);
}

show(0);
show(false);
show("");
show(null);
```

Output:

```text
0
false

null
```

Only `undefined` triggers the default.

---

# 23. Practical Example — Hotel Order

Suppose a hotel order has a default quantity of `1`.

```javascript
function createOrder(foodName, quantity = 1) {
    return {
        foodName,
        quantity
    };
}

console.log(createOrder("Momo"));
```

Result:

```javascript
{
    foodName: "Momo",
    quantity: 1
}
```

If the customer orders three:

```javascript
console.log(createOrder("Momo", 3));
```

Result:

```javascript
{
    foodName: "Momo",
    quantity: 3
}
```

---

# 24. Practical Example — User Role

```javascript
function createUser(name, role = "user") {
    return {
        name,
        role
    };
}

const user1 = createUser("Sandip");
const user2 = createUser("Admin", "admin");

console.log(user1);
console.log(user2);
```

Result:

```javascript
{
    name: "Sandip",
    role: "user"
}

{
    name: "Admin",
    role: "admin"
}
```

---

# 25. Practical Example — API Function

Default parameters are useful for API-related functions.

```javascript
function fetchUsers(page = 1, limit = 10) {
    console.log(`Page: ${page}`);
    console.log(`Limit: ${limit}`);
}

fetchUsers();
```

Output:

```text
Page: 1
Limit: 10
```

You can customize them:

```javascript
fetchUsers(2, 20);
```

Output:

```text
Page: 2
Limit: 20
```

---

# 26. Practical Example — Configuration

```javascript
function startServer(
    port = 8000,
    environment = "development"
) {
    console.log(`Port: ${port}`);
    console.log(`Environment: ${environment}`);
}

startServer();
```

Output:

```text
Port: 8000
Environment: development
```

This pattern is common in Node.js applications.

---

# 27. Default Parameters with Arrow Functions

Default parameters also work with arrow functions.

```javascript
const greet = (name = "Guest") => {
    return `Hello, ${name}`;
};

console.log(greet());
```

Output:

```text
Hello, Guest
```

Short version:

```javascript
const greet = (name = "Guest") => `Hello, ${name}`;
```

---

# 28. Default Parameters with Function Expressions

They also work with function expressions.

```javascript
const greet = function(name = "Guest") {
    console.log(`Hello, ${name}`);
};

greet();
```

Output:

```text
Hello, Guest
```

---

# 29. Default Parameter with Rest Parameter

A function can combine normal, default, and rest parameters.

```javascript
function createOrder(
    customer = "Guest",
    quantity = 1,
    ...items
) {
    return {
        customer,
        quantity,
        items
    };
}

console.log(
    createOrder(
        undefined,
        2,
        "Momo",
        "Pizza"
    )
);
```

Result:

```javascript
{
    customer: "Guest",
    quantity: 2,
    items: ["Momo", "Pizza"]
}
```

---

# 30. Important Rule About Rest Parameters

A rest parameter must be last.

Correct:

```javascript
function example(
    name = "Guest",
    ...items
) {
}
```

Incorrect:

```javascript
function example(
    ...items,
    name = "Guest"
) {
}
```

---

# 31. Default Parameters and `arguments`

When default parameters are used, the relationship between named parameters and the `arguments` object is different from traditional simple parameters.

Example:

```javascript
function example(value = 10) {
    console.log(value);
    console.log(arguments[0]);
}

example();
```

Output:

```text
10
undefined
```

The parameter gets its default value, but no argument was actually passed.

---

# 32. Common Mistakes

### Mistake 1: Thinking `null` triggers the default

```javascript
function greet(name = "Guest") {
    console.log(name);
}

greet(null);
```

Output:

```text
null
```

Remember:

```text
undefined → default
null      → not default
```

---

### Mistake 2: Using `||` when `0` is valid

```javascript
function calculate(quantity) {
    quantity = quantity || 1;
}
```

If:

```javascript
calculate(0);
```

`quantity` becomes `1`.

If `0` is a meaningful value, a default parameter is usually clearer.

---

### Mistake 3: Forgetting `= {}` with destructuring

Potentially unsafe:

```javascript
function createUser({ name = "Guest" }) {
    console.log(name);
}

createUser();
```

This throws because there is no object to destructure.

Safer:

```javascript
function createUser({ name = "Guest" } = {}) {
    console.log(name);
}

createUser();
```

---

### Mistake 4: Depending on a later parameter

Avoid:

```javascript
function example(a = b, b = 10) {
}
```

Prefer:

```javascript
function example(a = 10, b = a) {
}
```

---

# 33. Best Practices

### 1. Use defaults for optional values

```javascript
function fetchUsers(page = 1, limit = 10) {
}
```

### 2. Choose meaningful defaults

```javascript
function createUser(role = "user") {
}
```

### 3. Remember that only `undefined` triggers a default

```javascript
function show(value = 100) {
}
```

### 4. Use object defaults for complex configuration

```javascript
function startServer({
    port = 8000,
    environment = "development"
} = {}) {
}
```

### 5. Avoid complicated default expressions

Keep defaults easy to understand.

### 6. Use `??` when you specifically want `null` and `undefined` to trigger a fallback

```javascript
const name = value ?? "Guest";
```

---

# 34. Quick Revision

```text
Default Parameter
        ↓
Fallback value for a parameter
        ↓
Used when argument is missing or undefined
```

Example:

```javascript
function greet(name = "Guest") {
    console.log(name);
}

greet();
```

Output:

```text
Guest
```

### Important behavior

```text
greet()           → "Guest"
greet(undefined)  → "Guest"
greet(null)       → null
greet("")         → ""
greet(0)          → 0
greet(false)      → false
```

### With multiple parameters

```javascript
function createUser(
    name = "Guest",
    role = "user"
) {
}
```

### With object destructuring

```javascript
function createUser({
    name = "Guest",
    role = "user"
} = {}) {
}
```

---

# Key Takeaways

* Default parameters provide fallback values for function parameters.
* They are used when the argument is omitted or `undefined`.
* `null` does not trigger a default parameter.
* `0`, `false`, and `""` also do not trigger the default.
* Multiple parameters can have defaults.
* Later default parameters can use earlier parameters.
* Default parameters work with normal functions, function expressions, and arrow functions.
* Default parameters work with destructuring.
* `= {}` is useful when destructuring an optional object.
* Rest parameters can be combined with default parameters.
* Default parameters are usually clearer than manually using `||` for optional arguments.
* Use `??` when both `null` and `undefined` should trigger a fallback.

---
