# JavaScript Optional Chaining

**Optional chaining (`?.`)** allows you to safely access properties, array elements, methods, or function calls when a value might be `null` or `undefined`.

Without optional chaining, accessing a missing nested property can cause an error.

With optional chaining, JavaScript stops the operation and returns `undefined`.

---

# 1. Basic Syntax

```javascript
const user = {
  name: "Sandip"
};

console.log(user?.name);
```

Output:

```text
Sandip
```

If `user` is `null` or `undefined`:

```javascript
const user = null;

console.log(user?.name);
```

Output:

```text
undefined
```

Instead of throwing an error.

---

# 2. The Problem Without Optional Chaining

Suppose:

```javascript
const user = {};
```

This is unsafe:

```javascript
console.log(user.address.city);
```

Because `user.address` is `undefined`.

JavaScript throws an error similar to:

```text
Cannot read properties of undefined
```

Using optional chaining:

```javascript
console.log(user.address?.city);
```

Output:

```text
undefined
```

If `address` itself might be missing, an even safer form is:

```javascript
console.log(user?.address?.city);
```

---

# 3. Chaining Multiple Properties

Consider an API response:

```javascript
const response = {
  data: {
    user: {
      profile: {
        name: "Sandip"
      }
    }
  }
};
```

You can safely access:

```javascript
const name =
  response?.data?.user?.profile?.name;

console.log(name);
```

Output:

```text
Sandip
```

If any link in the chain is `null` or `undefined`, the result becomes `undefined`.

---

# 4. Optional Chaining With `null`

```javascript
const user = null;

const name = user?.name;

console.log(name);
```

Result:

```text
undefined
```

No error is thrown.

---

# 5. Optional Chaining With `undefined`

```javascript
let settings;

console.log(settings?.theme);
```

Result:

```text
undefined
```

This is useful when a variable has not received an object yet.

---

# 6. Optional Chaining With Arrays

You can safely access an array element:

```javascript
const foods = [
  "Momo",
  "Chowmein"
];

console.log(foods?.[0]);
```

Output:

```text
Momo
```

If the array itself is missing:

```javascript
let foods;

console.log(foods?.[0]);
```

Output:

```text
undefined
```

---

# 7. Optional Chaining With Dynamic Indexes

```javascript
const users = [
  "Sandip",
  "Ram"
];

const index = 1;

console.log(users?.[index]);
```

Output:

```text
Ram
```

The syntax is:

```javascript
array?.[expression]
```

---

# 8. Optional Chaining With Object Keys

You can use a variable as the property name.

```javascript
const user = {
  name: "Sandip",
  role: "admin"
};

const key = "role";

console.log(user?.[key]);
```

Output:

```text
admin
```

---

# 9. Optional Method Calls

Optional chaining can safely call a method that may not exist.

```javascript
const user = {
  name: "Sandip"
};

user.login?.();
```

If `login` does not exist, nothing happens.

Without optional chaining:

```javascript
user.login();
```

would throw an error because `login` is not a function.

---

# 10. Optional Function Calls

Suppose a callback is optional:

```javascript
function processUser(user, callback) {
  callback?.(user);
}
```

If a callback is provided:

```javascript
processUser(
  { name: "Sandip" },
  user => console.log(user.name)
);
```

Output:

```text
Sandip
```

If no callback is provided:

```javascript
processUser({
  name: "Sandip"
});
```

No error occurs.

---

# 11. Optional Chaining With `this`

Inside an object method, optional chaining can safely access optional data.

```javascript
const order = {
  customer: {
    name: "Sandip"
  },

  showCustomer() {
    console.log(
      this.customer?.name
    );
  }
};

order.showCustomer();
```

Output:

```text
Sandip
```

---

# 12. API Response Example

A common use case is handling API data.

Suppose the response may be:

```javascript
const response = {
  data: {
    user: {
      name: "Sandip"
    }
  }
};
```

Instead of assuming every property exists:

```javascript
const name =
  response.data.user.name;
```

Use:

```javascript
const name =
  response?.data?.user?.name;
```

This is safer when the response structure may be incomplete.

---

# 13. React Example

Suppose user data is loaded asynchronously:

```jsx
function Profile({ user }) {
  return (
    <h2>{user?.name}</h2>
  );
}
```

During the initial render, `user` might be `undefined`.

Instead of:

```jsx
<h2>{user.name}</h2>
```

use:

```jsx
<h2>{user?.name}</h2>
```

This prevents an error while the data is loading.

---

# 14. React Nested Data

```jsx
function Profile({ user }) {
  return (
    <p>
      {user?.profile?.address?.city}
    </p>
  );
}
```

If `profile`, `address`, or `city` is missing, the expression evaluates to `undefined`.

---

# 15. Optional Chaining With `map()`

Suppose an API may not return an array:

```javascript
const response = {};
```

You can write:

```javascript
const users = response?.data?.users;

users?.map(user => {
  console.log(user.name);
});
```

If `users` is undefined, the `map()` call is skipped.

---

# 16. Optional Chaining With `length`

```javascript
const foods = null;

console.log(foods?.length);
```

Output:

```text
undefined
```

This can be useful when an array or string may not exist.

---

# 17. Optional Chaining With Strings

```javascript
const username = null;

console.log(
  username?.toUpperCase()
);
```

Output:

```text
undefined
```

Without optional chaining, calling the method would cause an error.

---

# 18. Combining `?.` With `??`

Optional chaining often works together with the **nullish coalescing operator (`??`)**.

```javascript
const user = {};

const name =
  user?.profile?.name ?? "Guest";

console.log(name);
```

Output:

```text
Guest
```

The logic is:

```text
Try to get user.profile.name
        ↓
If null/undefined
        ↓
Use "Guest"
```

---

# 19. `?.` vs `??`

They solve different problems.

### Optional chaining

Safely accesses something:

```javascript
user?.profile?.name
```

### Nullish coalescing

Provides a fallback:

```javascript
user?.profile?.name ?? "Guest"
```

Together they are very useful for API and UI data.

---

# 20. `?.` Does Not Check Every Falsy Value

Optional chaining only stops when the value is:

```text
null
undefined
```

It does **not** stop for:

```text
false
0
""
```

For example:

```javascript
const data = {
  count: 0
};

console.log(data?.count);
```

Output:

```text
0
```

The value `0` is valid and is not replaced.

---

# 21. Difference From `&&`

Before optional chaining, developers often wrote:

```javascript
const city =
  user &&
  user.profile &&
  user.profile.address &&
  user.profile.address.city;
```

Optional chaining is much cleaner:

```javascript
const city =
  user?.profile?.address?.city;
```

The second version is easier to read.

---

# 22. Optional Chaining Is Short-Circuiting

When JavaScript encounters `null` or `undefined` in an optional chain, it stops evaluating the remaining chain.

Example:

```javascript
const user = null;

const result =
  user?.profile?.name;
```

JavaScript does not continue trying to access `profile` or `name`.

The result is:

```text
undefined
```

---

# 23. Grouping Can Change the Behavior

Be careful when using parentheses.

This is safely chained:

```javascript
const city =
  user?.address?.city;
```

But:

```javascript
const address =
  user?.address;

const city =
  address.city;
```

can fail if `address` is `undefined`.

Optional chaining protects the chain where it is actually used.

---

# 24. Optional Chaining Cannot Be Used for Assignment

This is invalid:

```javascript
user?.name = "Sandip";
```

Optional chaining is for reading/accessing or safely calling.

To update a property, first ensure the object exists:

```javascript
if (user) {
  user.name = "Sandip";
}
```

---

# 25. Optional Chaining With `delete`

Optional chaining can be used with `delete`.

```javascript
const user = {
  name: "Sandip"
};

delete user?.name;

console.log(user);
```

Result:

```text
{}
```

If the object is nullish, the operation does not throw.

---

# 26. Optional Chaining With Function Results

Suppose:

```javascript
function getUser() {
  return {
    profile: {
      name: "Sandip"
    }
  };
}
```

You can write:

```javascript
const name =
  getUser()?.profile?.name;

console.log(name);
```

Output:

```text
Sandip
```

---

# 27. Practical Hotel Example

Suppose an order may or may not contain customer information:

```javascript
const order = {
  orderNumber: "ORD-101",
  customer: {
    name: "Sandip"
  }
};
```

Safely access:

```javascript
const customerName =
  order?.customer?.name;
```

If `customer` is missing:

```javascript
const order = {
  orderNumber: "ORD-101"
};

const customerName =
  order?.customer?.name;
```

Result:

```text
undefined
```

---

# 28. Practical Food Example

Suppose food data may contain an optional category:

```javascript
const food = {
  name: "Momo",
  category: {
    name: "Snacks"
  }
};

const category =
  food?.category?.name;
```

This is useful when category information is populated conditionally by an API.

---

# 29. Practical User Example

```javascript
const user = {
  name: "Sandip",
  permissions: {
    dashboard: {
      view: true
    }
  }
};

const canView =
  user?.permissions?.dashboard?.view;

console.log(canView);
```

Output:

```text
true
```

If any intermediate property is missing, the result becomes `undefined`.

---

# 30. Common Mistakes

### Mistake 1: Using `?.` everywhere

Optional chaining is useful when something is genuinely optional.

Do not automatically write:

```javascript
user?.name
```

if your application guarantees that `user` always exists.

Sometimes:

```javascript
user.name
```

is clearer because it communicates that `user` is required.

---

### Mistake 2: Confusing `?.` with `??`

This:

```javascript
user?.name
```

accesses the property safely.

This:

```javascript
user?.name ?? "Guest"
```

accesses it safely **and** provides a fallback.

---

### Mistake 3: Expecting `?.` to handle errors inside a function

Optional chaining handles nullish values.

It does not catch arbitrary exceptions.

For example:

```javascript
user?.calculate();
```

If `calculate()` exists but throws an error internally, optional chaining does not catch that error.

Use `try...catch` when actual exception handling is required.

---

### Mistake 4: Using it for assignment

Invalid:

```javascript
user?.name = "Sandip";
```

Use a normal check before updating.

---

# 31. Quick Reference

### Property

```javascript
user?.name
```

### Nested property

```javascript
user?.profile?.name
```

### Array index

```javascript
users?.[0]
```

### Dynamic property

```javascript
user?.[key]
```

### Method

```javascript
user.login?.()
```

### Function call

```javascript
callback?.(data)
```

### With fallback

```javascript
user?.name ?? "Guest"
```

### Array method

```javascript
users?.map(...)
```

---

# 32. Optional Chaining vs Normal Access

| Code                    | Behavior                                   |
| ----------------------- | ------------------------------------------ |
| `user.name`             | Throws if `user` is nullish                |
| `user?.name`            | Returns `undefined`                        |
| `user.profile.name`     | Throws if an intermediate value is nullish |
| `user?.profile?.name`   | Safely returns `undefined`                 |
| `user?.name ?? "Guest"` | Safe access + fallback                     |

---

# 33. Key Takeaways

* Optional chaining uses `?.`.
* It safely accesses properties that may not exist.
* It works with nested objects.
* It works with arrays.
* It works with dynamic property names.
* It can safely call optional methods and callbacks.
* It is especially useful with API responses and React data.
* It only short-circuits on `null` and `undefined`.
* It does not replace error handling.
* It cannot be used as an assignment target.
* It works especially well with `??`.

## Remember

```text
?.  → safely access
??  → provide fallback
```

Example:

```javascript
const city =
  user?.profile?.address?.city ?? "Unknown";
```

This means:

```text
Safely find the city.
If it is null/undefined,
use "Unknown".
```

---
