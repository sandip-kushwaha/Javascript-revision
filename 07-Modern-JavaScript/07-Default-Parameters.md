# JavaScript Default Parameters

**Default parameters** allow a function to use a default value when an argument is not provided, or when the argument is explicitly `undefined`.

Syntax:

```javascript
function functionName(parameter = defaultValue) {
  // function body
}
```

---

# 1. Basic Example

```javascript
function greet(name = "Guest") {
  return `Hello, ${name}`;
}
```

Calling without an argument:

```javascript
console.log(greet());
```

Output:

```text
Hello, Guest
```

Calling with an argument:

```javascript
console.log(greet("Sandip"));
```

Output:

```text
Hello, Sandip
```

---

# 2. Why Use Default Parameters?

Without a default parameter:

```javascript
function greet(name) {
  return `Hello, ${name}`;
}

console.log(greet());
```

Output:

```text
Hello, undefined
```

With a default:

```javascript
function greet(name = "Guest") {
  return `Hello, ${name}`;
}
```

Now:

```text
Hello, Guest
```

Default parameters make functions safer and easier to use.

---

# 3. Default Is Used for `undefined`

```javascript
function getRole(role = "user") {
  return role;
}

console.log(getRole(undefined));
```

Output:

```text
user
```

An explicitly passed `undefined` also triggers the default.

---

# 4. `null` Does Not Trigger the Default

```javascript
function getRole(role = "user") {
  return role;
}

console.log(getRole(null));
```

Output:

```text
null
```

This is an important distinction:

```text
undefined → default is used
null      → default is not used
```

---

# 5. Other Values Do Not Trigger the Default

Defaults are not used for:

```text
0
false
""
null
```

Example:

```javascript
function getValue(value = 100) {
  return value;
}

console.log(getValue(0));
console.log(getValue(false));
console.log(getValue(""));
console.log(getValue(null));
```

Output:

```text
0
false

null
```

Only `undefined` triggers the default.

---

# 6. Multiple Default Parameters

A function can have multiple defaults.

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
```

Calling:

```javascript
console.log(createUser());
```

Result:

```javascript
{
  name: "Guest",
  role: "user",
  active: true
}
```

---

# 7. Providing Some Arguments

```javascript
console.log(
  createUser("Sandip")
);
```

Result:

```javascript
{
  name: "Sandip",
  role: "user",
  active: true
}
```

Only the first parameter was supplied.

---

# 8. Skipping an Earlier Parameter

JavaScript does not have a special syntax for "skip this argument."

You can pass `undefined`:

```javascript
function createUser(
  name = "Guest",
  role = "user"
) {
  return {
    name,
    role
  };
}

const user = createUser(
  undefined,
  "admin"
);
```

Result:

```javascript
{
  name: "Guest",
  role: "admin"
}
```

---

# 9. Default Parameters With Expressions

The default value does not have to be a simple value.

```javascript
function getTimestamp(
  timestamp = Date.now()
) {
  return timestamp;
}

console.log(getTimestamp());
```

The default expression is evaluated when the function call needs it.

---

# 10. Default Parameter With Function Call

```javascript
function getName() {
  return "Guest";
}

function welcome(
  name = getName()
) {
  return `Welcome, ${name}`;
}

console.log(welcome());
```

Output:

```text
Welcome, Guest
```

The function `getName()` is used only when `name` is `undefined`.

---

# 11. Default Parameter With Another Parameter

A later parameter can use an earlier parameter.

```javascript
function calculatePrice(
  price,
  quantity = 1,
  total = price * quantity
) {
  return total;
}

console.log(calculatePrice(500));
```

Output:

```text
500
```

Here:

```text
price = 500
quantity = 1
total = 500 * 1
```

---

# 12. Parameter Order Matters

This works:

```javascript
function calculate(
  price,
  quantity = 1
) {
  return price * quantity;
}
```

But trying to use a later parameter as the default for an earlier parameter does not work:

```javascript
function calculate(
  total = quantity * price,
  price,
  quantity
) {
  // ...
}
```

The earlier parameter cannot access later parameters in its default expression.

---

# 13. Default Parameters With Objects

Default parameters are useful when a function expects an object.

```javascript
function showSettings(
  settings = {}
) {
  console.log(settings);
}

showSettings();
```

Instead of receiving `undefined`, the function gets an empty object.

---

# 14. Object Destructuring + Default Parameter

This is a common pattern:

```javascript
function displayUser({
  name = "Guest",
  role = "user"
} = {}) {
  console.log(name);
  console.log(role);
}
```

Now this works:

```javascript
displayUser();
```

Output:

```text
Guest
user
```

And:

```javascript
displayUser({
  name: "Sandip",
  role: "admin"
});
```

Output:

```text
Sandip
admin
```

---

# 15. Why `= {}` Is Useful

Consider:

```javascript
function displayUser({
  name = "Guest"
}) {
  console.log(name);
}
```

Calling:

```javascript
displayUser();
```

causes an error because JavaScript tries to destructure `undefined`.

Adding:

```javascript
= {}
```

provides an empty object when no argument is supplied:

```javascript
function displayUser({
  name = "Guest"
} = {}) {
  console.log(name);
}
```

---

# 16. Default Parameters With Arrays

You can also provide a default array.

```javascript
function showItems(
  items = []
) {
  console.log(items);
}

showItems();
```

Result:

```text
[]
```

---

# 17. Default Parameter With Rest

Default parameters and rest parameters can be used together.

```javascript
function createMessage(
  prefix = "Message",
  ...parts
) {
  return `${prefix}: ${parts.join(" ")}`;
}

console.log(
  createMessage(
    "Order",
    "received",
    "successfully"
  )
);
```

Output:

```text
Order: received successfully
```

Here:

```text
prefix → "Order"
parts  → ["received", "successfully"]
```

---

# 18. Default Parameters and `arguments`

Default parameters change the behavior of the function's `arguments` object compared with old-style parameter handling.

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

The default value does not create an argument that was never passed.

---

# 19. Default Parameters and `arguments`

If an argument is actually passed:

```javascript
function example(value = 10) {
  console.log(value);
  console.log(arguments[0]);
}

example(50);
```

Output:

```text
50
50
```

---

# 20. Default Parameters With Arrow Functions

Default parameters work with arrow functions.

```javascript
const greet = (
  name = "Guest"
) => {
  return `Hello, ${name}`;
};

console.log(greet());
```

Output:

```text
Hello, Guest
```

---

# 21. Default Parameters With Function Expressions

They also work with function expressions.

```javascript
const calculateTax = function (
  amount,
  rate = 0.13
) {
  return amount * rate;
};

console.log(calculateTax(1000));
```

Output:

```text
130
```

---

# 22. Practical API Example

Suppose a function builds an API request:

```javascript
function getUsers(
  page = 1,
  limit = 10
) {
  return `/api/users?page=${page}&limit=${limit}`;
}
```

Calling:

```javascript
getUsers();
```

produces:

```text
/api/users?page=1&limit=10
```

Calling:

```javascript
getUsers(2, 20);
```

produces:

```text
/api/users?page=2&limit=20
```

---

# 23. Pagination Example

Default parameters are especially useful for pagination:

```javascript
function getNews(
  page = 1,
  limit = 10
) {
  console.log(`Page: ${page}`);
  console.log(`Limit: ${limit}`);
}
```

Then:

```javascript
getNews();
```

uses:

```text
Page: 1
Limit: 10
```

while:

```javascript
getNews(3, 20);
```

uses:

```text
Page: 3
Limit: 20
```

---

# 24. Hotel Example

Suppose an order needs a default status:

```javascript
function createOrder(
  tableNumber,
  status = "pending"
) {
  return {
    tableNumber,
    status
  };
}
```

Calling:

```javascript
createOrder("T-05");
```

returns:

```javascript
{
  tableNumber: "T-05",
  status: "pending"
}
```

If a status is provided:

```javascript
createOrder("T-05", "confirmed");
```

returns:

```javascript
{
  tableNumber: "T-05",
  status: "confirmed"
}
```

---

# 25. Default Values Can Be Objects

```javascript
function createConfig(
  config = {
    timeout: 5000,
    retries: 3
  }
) {
  return config;
}
```

Calling:

```javascript
createConfig();
```

uses the default object.

Be careful when using mutable objects as defaults; each function call evaluates the default expression when it is needed.

---

# 26. Default Expression Is Evaluated Per Call

Consider:

```javascript
function createList(
  items = []
) {
  return items;
}

const first = createList();
const second = createList();

console.log(first === second);
```

Output:

```text
false
```

Each call creates a new default array.

Similarly:

```javascript
function createUser(
  user = {}
) {
  return user;
}

const a = createUser();
const b = createUser();

console.log(a === b);
```

Output:

```text
false
```

---

# 27. Default Parameters vs `||`

These two are not equivalent.

Using `||`:

```javascript
function getLimit(limit) {
  return limit || 10;
}
```

If:

```javascript
getLimit(0);
```

the result is:

```text
10
```

Using a default parameter:

```javascript
function getLimit(limit = 10) {
  return limit;
}
```

Now:

```javascript
getLimit(0);
```

returns:

```text
0
```

The default parameter only applies to `undefined`.

---

# 28. Default Parameters vs `??`

You can also compare:

```javascript
function getLimit(limit = 10) {
  return limit;
}
```

with:

```javascript
function getLimit(limit) {
  return limit ?? 10;
}
```

Important difference:

```javascript
getLimit(null);
```

With a default parameter:

```text
null
```

With `??`:

```text
10
```

So:

```text
Default parameter → undefined
??                → undefined + null
```

---

# 29. Practical Comparison

| Situation | Default Parameter | `??` | `||` |
|---|---:|---:|---:|
| `undefined` | Default | Default | Default |
| `null` | `null` | Default | Default |
| `0` | `0` | `0` | Default |
| `false` | `false` | `false` | Default |
| `""` | `""` | `""` | Default |

---

# 30. Common Mistakes

## Mistake 1: Thinking `null` triggers a default

```javascript
function test(value = 10) {
  return value;
}

test(null);
```

Result:

```text
null
```

Only `undefined` triggers the default.

---

## Mistake 2: Forgetting argument order

```javascript
function example(a, b = 10, c = 20) {
  // ...
}
```

To use the default for `b` while providing `c`, pass:

```javascript
example(1, undefined, 30);
```

---

## Mistake 3: Destructuring without a default object

This can fail:

```javascript
function showUser({ name }) {
  console.log(name);
}

showUser();
```

Safer:

```javascript
function showUser({ name } = {}) {
  console.log(name);
}
```

---

## Mistake 4: Using `||` when `0` or `false` is valid

```javascript
function getCount(count) {
  return count || 10;
}
```

If `0` is valid, this is usually not what you want.

Use:

```javascript
function getCount(count = 10) {
  return count;
}
```

or:

```javascript
function getCount(count) {
  return count ?? 10;
}
```

depending on whether `null` should also trigger the fallback.

---

# 31. Quick Reference

### Simple default

```javascript
function greet(name = "Guest") {
  // ...
}
```

### Multiple defaults

```javascript
function createUser(
  name = "Guest",
  role = "user"
) {
  // ...
}
```

### Default object

```javascript
function config(
  options = {}
) {
  // ...
}
```

### Default array

```javascript
function process(
  items = []
) {
  // ...
}
```

### Destructuring + default

```javascript
function showUser({
  name = "Guest"
} = {}) {
  // ...
}
```

### Default with arrow function

```javascript
const greet = (
  name = "Guest"
) => `Hello ${name}`;
```

---

# 32. Key Takeaways

* Default parameters provide fallback values for function parameters.
* They are used when the argument is `undefined`.
* `null` does not trigger a default parameter.
* `0`, `false`, and `""` are preserved.
* Default expressions are evaluated when needed.
* Default parameters work with regular functions, function expressions, and arrow functions.
* They work with destructuring and rest parameters.
* `= {}` is useful when destructuring an optional object parameter.
* Default parameters are different from `||` and `??`.

## Remember

```text
Default parameter → fallback for undefined

??                 → fallback for null/undefined

||                 → fallback for falsy values
```

Example:

```javascript
function getPage(page = 1) {
  return page;
}
```

```javascript
function getPage(page) {
  return page ?? 1;
}
```

Both are useful, but they handle `null` differently.

---
