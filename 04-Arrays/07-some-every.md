# JavaScript Array `some()` and `every()` Methods

The `some()` and `every()` methods are used to **check conditions on array elements**.

Both methods return a **Boolean value**:

```text
true
false
```

The main difference is:

```text
some()  → Is at least ONE element matching?
every() → Are ALL elements matching?
```

---

# 1. `some()` Method

The `some()` method checks whether **at least one element** in an array satisfies a condition.

If at least one element matches:

```text
true
```

If no element matches:

```text
false
```

Example:

```javascript
const numbers = [1, 2, 3, 4, 5];

const result = numbers.some(number => number > 4);

console.log(result);
```

Output:

```text
true
```

Because `5` is greater than `4`.

---

# 2. Basic Syntax of `some()`

```javascript
const result = array.some(callback);
```

Example:

```javascript
const result = numbers.some(number => number > 10);
```

The callback should return a condition.

---

# 3. How `some()` Works

Consider:

```javascript
const numbers = [1, 3, 5, 8, 9];
```

Check whether there is an even number:

```javascript
const result = numbers.some(
    number => number % 2 === 0
);

console.log(result);
```

Process:

```text
1 → false
3 → false
5 → false
8 → true → STOP
```

Result:

```text
true
```

`some()` stops as soon as it finds one matching element.

---

# 4. `some()` Returns Boolean

```javascript
const numbers = [10, 20, 30];

const result = numbers.some(
    number => number > 15
);

console.log(result);
```

Output:

```text
true
```

It does **not** return:

```text
20
```

or:

```text
[20, 30]
```

It only returns:

```text
true
```

or:

```text
false
```

---

# 5. Checking Whether a Number Exists

```javascript
const numbers = [10, 20, 30, 40];

const exists = numbers.some(
    number => number === 30
);

console.log(exists);
```

Output:

```text
true
```

---

# 6. Checking Whether a Number Does Not Exist

```javascript
const numbers = [10, 20, 30, 40];

const exists = numbers.some(
    number => number === 100
);

console.log(exists);
```

Output:

```text
false
```

---

# 7. Checking for Even Numbers

```javascript
const numbers = [1, 3, 5, 7, 8];

const hasEvenNumber = numbers.some(
    number => number % 2 === 0
);

console.log(hasEvenNumber);
```

Output:

```text
true
```

---

# 8. Checking for Odd Numbers

```javascript
const numbers = [2, 4, 6, 9];

const hasOddNumber = numbers.some(
    number => number % 2 !== 0
);

console.log(hasOddNumber);
```

Output:

```text
true
```

---

# 9. `some()` with Strings

```javascript
const names = [
    "Ram",
    "Sita",
    "Sandip"
];

const hasSandip = names.some(
    name => name === "Sandip"
);

console.log(hasSandip);
```

Output:

```text
true
```

---

# 10. Checking String Content

```javascript
const names = [
    "Ram Sharma",
    "Sita Thapa",
    "Sandip Kushwaha"
];

const hasKushwaha = names.some(
    name => name.includes("Kushwaha")
);

console.log(hasKushwaha);
```

Output:

```text
true
```

---

# 11. `some()` with Objects

`some()` is very useful with arrays of objects.

```javascript
const users = [
    {
        name: "Sandip",
        isActive: true
    },
    {
        name: "Ram",
        isActive: false
    }
];

const hasActiveUser = users.some(
    user => user.isActive
);

console.log(hasActiveUser);
```

Output:

```text
true
```

---

# 12. Checking for an Admin

```javascript
const users = [
    {
        name: "Ram",
        role: "waiter"
    },
    {
        name: "Sandip",
        role: "admin"
    }
];

const hasAdmin = users.some(
    user => user.role === "admin"
);

console.log(hasAdmin);
```

Output:

```text
true
```

This is useful when checking whether a collection contains a particular role.

---

# 13. Checking Whether a Product Is Available

```javascript
const products = [
    {
        name: "Laptop",
        isAvailable: false
    },
    {
        name: "Mouse",
        isAvailable: true
    },
    {
        name: "Keyboard",
        isAvailable: false
    }
];

const hasAvailableProduct = products.some(
    product => product.isAvailable
);

console.log(hasAvailableProduct);
```

Output:

```text
true
```

---

# 14. Hotel Example: Available Table

```javascript
const tables = [
    {
        tableNumber: "T-01",
        status: "occupied"
    },
    {
        tableNumber: "T-02",
        status: "occupied"
    },
    {
        tableNumber: "T-03",
        status: "available"
    }
];

const hasAvailableTable = tables.some(
    table => table.status === "available"
);

console.log(hasAvailableTable);
```

Output:

```text
true
```

This answers:

> Is there at least one available table?

---

# 15. Hotel Example: Pending Orders

```javascript
const orders = [
    {
        id: 1,
        status: "completed"
    },
    {
        id: 2,
        status: "preparing"
    },
    {
        id: 3,
        status: "completed"
    }
];

const hasPendingOrder = orders.some(
    order => order.status === "pending"
);

console.log(hasPendingOrder);
```

Output:

```text
false
```

---

# 16. `some()` with Multiple Conditions

```javascript
const users = [
    {
        name: "Ram",
        role: "waiter",
        isActive: true
    },
    {
        name: "Sandip",
        role: "admin",
        isActive: true
    }
];

const hasActiveAdmin = users.some(
    user => user.role === "admin" && user.isActive
);

console.log(hasActiveAdmin);
```

Output:

```text
true
```

---

# 17. `some()` Stops Early

Example:

```javascript
const numbers = [10, 20, 30, 40, 50];

const result = numbers.some(number => {
    console.log("Checking:", number);

    return number >= 30;
});
```

Output:

```text
Checking: 10
Checking: 20
Checking: 30
```

Result:

```text
true
```

It does not need to check `40` or `50`.

---

# 18. Empty Array with `some()`

For an empty array:

```javascript
const numbers = [];

const result = numbers.some(
    number => number > 10
);

console.log(result);
```

Output:

```text
false
```

There is no element that satisfies the condition.

---

# 19. Callback Parameters for `some()`

The callback can receive:

```javascript
array.some((element, index, array) => {
    // condition
});
```

| Parameter | Meaning         |
| --------- | --------------- |
| `element` | Current element |
| `index`   | Current index   |
| `array`   | Original array  |

Example:

```javascript
const numbers = [10, 20, 30];

numbers.some((number, index) => {
    console.log(index, number);

    return number > 15;
});
```

Output:

```text
0 10
1 20
```

The method stops after `20` satisfies the condition.

---

# 20. `every()` Method

The `every()` method checks whether **all elements** satisfy a condition.

If every element matches:

```text
true
```

If even one element fails:

```text
false
```

Example:

```javascript
const numbers = [2, 4, 6, 8];

const result = numbers.every(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
true
```

All numbers are even.

---

# 21. Basic Syntax of `every()`

```javascript
const result = array.every(callback);
```

Example:

```javascript
const result = numbers.every(
    number => number > 0
);
```

---

# 22. How `every()` Works

Consider:

```javascript
const numbers = [2, 4, 6, 7, 8];
```

Check whether all numbers are even:

```javascript
const result = numbers.every(
    number => number % 2 === 0
);
```

Process:

```text
2 → true
4 → true
6 → true
7 → false → STOP
```

Result:

```text
false
```

`every()` stops when it finds the first element that does not satisfy the condition.

---

# 23. Checking All Numbers Are Positive

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.every(
    number => number > 0
);

console.log(result);
```

Output:

```text
true
```

---

# 24. Checking All Numbers Are Even

```javascript
const numbers = [2, 4, 6, 8];

const result = numbers.every(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
true
```

If:

```javascript
const numbers = [2, 4, 7, 8];
```

then:

```javascript
const result = numbers.every(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
false
```

---

# 25. `every()` with Strings

Check whether all names have at least 3 characters:

```javascript
const names = [
    "Ram",
    "Sita",
    "Sandip"
];

const result = names.every(
    name => name.length >= 3
);

console.log(result);
```

Output:

```text
true
```

---

# 26. `every()` with Objects

```javascript
const users = [
    {
        name: "Sandip",
        isActive: true
    },
    {
        name: "Ram",
        isActive: true
    },
    {
        name: "Sita",
        isActive: true
    }
];

const allActive = users.every(
    user => user.isActive
);

console.log(allActive);
```

Output:

```text
true
```

---

# 27. Checking All Users Are Active

If one user is inactive:

```javascript
const users = [
    {
        name: "Sandip",
        isActive: true
    },
    {
        name: "Ram",
        isActive: false
    },
    {
        name: "Sita",
        isActive: true
    }
];

const allActive = users.every(
    user => user.isActive
);

console.log(allActive);
```

Output:

```text
false
```

---

# 28. Checking All Products Are Available

```javascript
const products = [
    {
        name: "Laptop",
        isAvailable: true
    },
    {
        name: "Mouse",
        isAvailable: true
    },
    {
        name: "Keyboard",
        isAvailable: true
    }
];

const allAvailable = products.every(
    product => product.isAvailable
);

console.log(allAvailable);
```

Output:

```text
true
```

---

# 29. Hotel Example: All Tables Available

```javascript
const tables = [
    {
        tableNumber: "T-01",
        status: "available"
    },
    {
        tableNumber: "T-02",
        status: "available"
    },
    {
        tableNumber: "T-03",
        status: "available"
    }
];

const allAvailable = tables.every(
    table => table.status === "available"
);

console.log(allAvailable);
```

Output:

```text
true
```

If one table is occupied:

```javascript
const tables = [
    {
        tableNumber: "T-01",
        status: "available"
    },
    {
        tableNumber: "T-02",
        status: "occupied"
    },
    {
        tableNumber: "T-03",
        status: "available"
    }
];
```

Then:

```javascript
const allAvailable = tables.every(
    table => table.status === "available"
);

console.log(allAvailable);
```

Output:

```text
false
```

---

# 30. Hotel Example: All Orders Completed

```javascript
const orders = [
    {
        id: 1,
        status: "completed"
    },
    {
        id: 2,
        status: "completed"
    },
    {
        id: 3,
        status: "completed"
    }
];

const allCompleted = orders.every(
    order => order.status === "completed"
);

console.log(allCompleted);
```

Output:

```text
true
```

---

# 31. Checking Minimum Price

```javascript
const products = [
    {
        name: "Laptop",
        price: 80000
    },
    {
        name: "Mouse",
        price: 1500
    },
    {
        name: "Keyboard",
        price: 3000
    }
];

const validPrices = products.every(
    product => product.price > 0
);

console.log(validPrices);
```

Output:

```text
true
```

---

# 32. Checking Required Properties

You can check whether every object contains a property:

```javascript
const users = [
    {
        name: "Sandip",
        email: "sandip@example.com"
    },
    {
        name: "Ram",
        email: "ram@example.com"
    }
];

const allHaveEmail = users.every(
    user => user.email
);

console.log(allHaveEmail);
```

Output:

```text
true
```

For more explicit validation:

```javascript
const allHaveEmail = users.every(
    user =>
        typeof user.email === "string" &&
        user.email.length > 0
);
```

---

# 33. `every()` Stops Early

Example:

```javascript
const numbers = [2, 4, 6, 7, 8];

const result = numbers.every(number => {
    console.log("Checking:", number);

    return number % 2 === 0;
});
```

Output:

```text
Checking: 2
Checking: 4
Checking: 6
Checking: 7
```

Result:

```text
false
```

It does not check `8`.

---

# 34. Empty Array with `every()`

An interesting behavior:

```javascript
const numbers = [];

const result = numbers.every(
    number => number > 10
);

console.log(result);
```

Output:

```text
true
```

Why?

There are no elements that violate the condition.

This behavior is called **vacuous truth**.

For normal application code, remember:

```text
[].some(...)  → false
[].every(...) → true
```

---

# 35. `some()` vs `every()`

This is the most important difference.

### `some()`

Checks whether **at least one** element matches.

```javascript
const numbers = [1, 2, 3, 4];

numbers.some(number => number % 2 === 0);
```

Result:

```text
true
```

Because `2` and `4` are even.

### `every()`

Checks whether **all** elements match.

```javascript
numbers.every(number => number % 2 === 0);
```

Result:

```text
false
```

Because `1` and `3` are odd.

Remember:

```text
some()  → ANY
every() → ALL
```

---

# 36. `some()` vs `find()`

`some()`:

```javascript
const exists = users.some(
    user => user.id === 2
);
```

Returns:

```text
true
```

`find()`:

```javascript
const user = users.find(
    user => user.id === 2
);
```

Returns:

```text
{
    id: 2,
    ...
}
```

Remember:

```text
some() → Does it exist?
find() → Give me the element.
```

---

# 37. `some()` vs `filter()`

`some()`:

```javascript
const result = users.some(
    user => user.isActive
);
```

Returns:

```text
true
```

`filter()`:

```javascript
const result = users.filter(
    user => user.isActive
);
```

Returns:

```text
[
    { ... },
    { ... }
]
```

Remember:

```text
some()   → boolean
filter() → array
```

---

# 38. `every()` vs `filter()`

Suppose:

```javascript
const numbers = [2, 4, 6];
```

Using `every()`:

```javascript
const result = numbers.every(
    number => number % 2 === 0
);
```

Result:

```text
true
```

Using `filter()`:

```javascript
const result = numbers.filter(
    number => number % 2 === 0
);
```

Result:

```text
[2, 4, 6]
```

Remember:

```text
every()  → Are all elements valid?
filter() → Give me the valid elements.
```

---

# 39. Combining `some()` and `every()`

You can use both when validating data.

Example:

```javascript
const products = [
    {
        name: "Laptop",
        price: 80000,
        isAvailable: true
    },
    {
        name: "Mouse",
        price: 1500,
        isAvailable: false
    }
];
```

Check whether at least one product is available:

```javascript
const hasAvailableProduct = products.some(
    product => product.isAvailable
);
```

Check whether every product has a valid price:

```javascript
const allPricesValid = products.every(
    product => product.price > 0
);
```

---

# 40. Combining with `filter()`

Suppose you want to check whether any active admin exists:

```javascript
const hasActiveAdmin = users
    .filter(user => user.isActive)
    .some(user => user.role === "admin");
```

But in this case, you can usually write the condition directly:

```javascript
const hasActiveAdmin = users.some(
    user => user.isActive && user.role === "admin"
);
```

The second version is simpler and avoids creating an intermediate array.

---

# 41. Combining with `map()`

Suppose:

```javascript
const users = [
    {
        name: "Sandip",
        isActive: true
    },
    {
        name: "Ram",
        isActive: true
    }
];
```

Extract names:

```javascript
const names = users.map(
    user => user.name
);
```

Then check:

```javascript
const allNamesValid = names.every(
    name => name.length > 0
);
```

Or directly:

```javascript
const allNamesValid = users.every(
    user => user.name.length > 0
);
```

The direct version is usually simpler.

---

# 42. Practical Form Validation

Suppose a form has fields:

```javascript
const fields = [
    {
        name: "email",
        value: "sandip@example.com"
    },
    {
        name: "password",
        value: "123456"
    },
    {
        name: "username",
        value: "sandip"
    }
];
```

Check whether every field has a value:

```javascript
const isValid = fields.every(
    field => field.value.trim() !== ""
);

console.log(isValid);
```

Output:

```text
true
```

---

# 43. Checking for Invalid Data

```javascript
const values = [10, 20, -5, 30];

const hasInvalidValue = values.some(
    value => value < 0
);

console.log(hasInvalidValue);
```

Output:

```text
true
```

This is useful for validation.

---

# 44. Checking All Values Are Valid

```javascript
const values = [10, 20, 30, 40];

const allValid = values.every(
    value => value >= 0
);

console.log(allValid);
```

Output:

```text
true
```

---

# 45. Practical Permission Example

Suppose:

```javascript
const permissions = [
    "read",
    "write",
    "delete"
];
```

Check whether the user can delete:

```javascript
const canDelete = permissions.some(
    permission => permission === "delete"
);

console.log(canDelete);
```

Output:

```text
true
```

---

# 46. Checking Required Permissions

Suppose:

```javascript
const permissions = [
    "read",
    "write",
    "delete"
];

const requiredPermissions = [
    "read",
    "write"
];
```

Check whether all required permissions exist:

```javascript
const hasAllPermissions = requiredPermissions.every(
    required =>
        permissions.includes(required)
);

console.log(hasAllPermissions);
```

Output:

```text
true
```

This pattern is useful in role-based access control.

---

# 47. Practical Shopping Cart Example

```javascript
const cart = [
    {
        name: "Laptop",
        quantity: 1
    },
    {
        name: "Mouse",
        quantity: 2
    }
];
```

Check whether the cart contains a laptop:

```javascript
const hasLaptop = cart.some(
    item => item.name === "Laptop"
);

console.log(hasLaptop);
```

Output:

```text
true
```

Check whether every cart item has a valid quantity:

```javascript
const validCart = cart.every(
    item => item.quantity > 0
);

console.log(validCart);
```

Output:

```text
true
```

---

# 48. Practical API Validation

Suppose API data contains users:

```javascript
const users = [
    {
        id: 1,
        name: "Sandip",
        email: "sandip@example.com"
    },
    {
        id: 2,
        name: "Ram",
        email: "ram@example.com"
    }
];
```

Check whether there is a user with a specific email:

```javascript
const emailExists = users.some(
    user => user.email === "ram@example.com"
);
```

Check whether every user has an email:

```javascript
const allEmailsValid = users.every(
    user => typeof user.email === "string"
);
```

---

# 49. Common Mistakes

## Mistake 1: Expecting `some()` to return the element

Wrong expectation:

```javascript
const result = users.some(
    user => user.id === 2
);
```

The result is:

```text
true
```

If you need the object:

```javascript
const user = users.find(
    user => user.id === 2
);
```

---

## Mistake 2: Expecting `every()` to return matching elements

```javascript
const result = users.every(
    user => user.isActive
);
```

The result is only:

```text
true
```

or:

```text
false
```

If you need the active users:

```javascript
const activeUsers = users.filter(
    user => user.isActive
);
```

---

## Mistake 3: Confusing `some()` with `every()`

```text
some()  → at least one
every() → all
```

---

## Mistake 4: Forgetting the Boolean result

Both methods return:

```text
true
false
```

They do not return an array.

---

# 50. Best Practices

### Use `some()` when:

You need to know whether **at least one** element satisfies a condition.

```javascript
const hasAdmin = users.some(
    user => user.role === "admin"
);
```

### Use `every()` when:

You need to know whether **all** elements satisfy a condition.

```javascript
const allActive = users.every(
    user => user.isActive
);
```

### Use `find()` when:

You need the actual matching element.

```javascript
const admin = users.find(
    user => user.role === "admin"
);
```

### Use `filter()` when:

You need all matching elements.

```javascript
const admins = users.filter(
    user => user.role === "admin"
);
```

---

# 51. Quick Comparison

| Method        | Returns | Purpose               |
| ------------- | ------- | --------------------- |
| `some()`      | Boolean | At least one matches  |
| `every()`     | Boolean | All match             |
| `find()`      | Element | First match           |
| `findIndex()` | Number  | First matching index  |
| `filter()`    | Array   | All matching elements |
| `map()`       | Array   | Transform elements    |

---

# 52. Quick Revision

```text
some()
   │
   ├── Checks elements
   ├── Finds first truthy condition
   ├── Stops early
   └── Returns true / false

every()
   │
   ├── Checks elements
   ├── Finds first falsy condition
   ├── Stops early
   └── Returns true / false
```

Remember:

```text
some()  → ANY?
every() → ALL?
```

---

# 53. Cheat Sheet

```javascript
// At least one number is greater than 10
numbers.some(n => n > 10);

// At least one number is even
numbers.some(n => n % 2 === 0);

// At least one active user
users.some(user => user.isActive);

// At least one admin
users.some(user => user.role === "admin");

// All numbers are positive
numbers.every(n => n > 0);

// All numbers are even
numbers.every(n => n % 2 === 0);

// All users are active
users.every(user => user.isActive);

// All products have a valid price
products.every(product => product.price > 0);

// All required permissions exist
requiredPermissions.every(
    permission => permissions.includes(permission)
);
```

---

# 54. Key Takeaways

* `some()` checks whether **at least one** element satisfies a condition.
* `every()` checks whether **all** elements satisfy a condition.
* Both return only `true` or `false`.
* Both can stop early once the result is known.
* `some()` stops at the first matching element.
* `every()` stops at the first element that fails.
* `some()` is useful for existence checks.
* `every()` is useful for validation.
* Empty array:

  * `some()` returns `false`.
  * `every()` returns `true`.
* Use `find()` when you need the actual element.
* Use `filter()` when you need all matching elements.
* These methods are commonly used in validation, permissions, forms, ecommerce, dashboards, and API data processing.

---
