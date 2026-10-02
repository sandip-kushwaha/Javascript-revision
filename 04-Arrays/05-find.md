# JavaScript Array `find()` Method

The `find()` method is used to **find the first element in an array that satisfies a condition**.

It returns the **first matching element** and stops searching once a match is found.

---

# 1. What is `find()`?

Example:

```javascript
const numbers = [10, 20, 30, 40, 50];

const result = numbers.find(number => number > 25);

console.log(result);
```

Output:

```text
30
```

Why?

```text
10 → false
20 → false
30 → true → STOP
```

`find()` returns `30` and does not continue looking for `40` or `50`.

---

# 2. Basic Syntax

```javascript
const result = array.find(callback);
```

The callback returns a condition:

```javascript
const result = numbers.find(number => number > 25);
```

The first element for which the condition is truthy is returned.

---

# 3. How `find()` Works

Consider:

```javascript
const numbers = [5, 10, 15, 20];
```

Find the first number greater than `10`:

```javascript
const result = numbers.find(number => number > 10);
```

Process:

```text
5  → false
10 → false
15 → true → RETURN 15
```

Result:

```text
15
```

---

# 4. `find()` Returns Only One Element

Suppose:

```javascript
const numbers = [10, 20, 20, 30];
```

Using `find()`:

```javascript
const result = numbers.find(number => number === 20);

console.log(result);
```

Output:

```text
20
```

Even though there are two `20` values, `find()` returns only the **first matching element**.

---

# 5. `find()` vs `filter()`

This difference is very important.

### `find()`

Returns the first matching element:

```javascript
const numbers = [10, 20, 20, 30];

const result = numbers.find(number => number === 20);

console.log(result);
```

Output:

```text
20
```

### `filter()`

Returns all matching elements:

```javascript
const result = numbers.filter(number => number === 20);

console.log(result);
```

Output:

```text
[20, 20]
```

Remember:

```text
find()   → first matching element
filter() → all matching elements
```

---

# 6. What Happens When Nothing Is Found?

If no element satisfies the condition, `find()` returns:

```text
undefined
```

Example:

```javascript
const numbers = [10, 20, 30];

const result = numbers.find(number => number > 100);

console.log(result);
```

Output:

```text
undefined
```

This is different from `filter()`:

```javascript
const result = numbers.filter(number => number > 100);

console.log(result);
```

Output:

```text
[]
```

---

# 7. Finding a Number

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.find(number => number === 30);

console.log(result);
```

Output:

```text
30
```

---

# 8. Finding an Even Number

```javascript
const numbers = [1, 3, 5, 8, 10, 12];

const result = numbers.find(number => number % 2 === 0);

console.log(result);
```

Output:

```text
8
```

`8` is the first even number.

---

# 9. Finding an Odd Number

```javascript
const numbers = [2, 4, 6, 7, 9];

const result = numbers.find(number => number % 2 !== 0);

console.log(result);
```

Output:

```text
7
```

---

# 10. Finding a String

```javascript
const names = [
    "Ram",
    "Sita",
    "Sandip",
    "Suman"
];

const result = names.find(name => name === "Sandip");

console.log(result);
```

Output:

```text
Sandip
```

---

# 11. Finding by String Condition

You can use string methods inside the callback.

```javascript
const names = [
    "Ram",
    "Sita",
    "Sandip",
    "Suman"
];

const result = names.find(name =>
    name.startsWith("Sa")
);

console.log(result);
```

Output:

```text
Sandip
```

---

# 12. Finding an Object

`find()` becomes especially useful when working with arrays of objects.

```javascript
const users = [
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Ram"
    },
    {
        id: 3,
        name: "Sita"
    }
];
```

Find the user with ID `2`:

```javascript
const user = users.find(user => user.id === 2);

console.log(user);
```

Output:

```text
{
    id: 2,
    name: "Ram"
}
```

---

# 13. Finding User by Email

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

const user = users.find(
    user => user.email === "ram@example.com"
);

console.log(user);
```

Result:

```text
{
    id: 2,
    name: "Ram",
    email: "ram@example.com"
}
```

This pattern is common when working with user data.

---

# 14. Finding a Product

```javascript
const products = [
    {
        id: 101,
        name: "Laptop",
        price: 80000
    },
    {
        id: 102,
        name: "Mouse",
        price: 1500
    },
    {
        id: 103,
        name: "Keyboard",
        price: 3000
    }
];
```

Find product by ID:

```javascript
const product = products.find(
    product => product.id === 102
);

console.log(product);
```

Output:

```text
{
    id: 102,
    name: "Mouse",
    price: 1500
}
```

---

# 15. Finding a Hotel Table

For a hotel management system:

```javascript
const tables = [
    {
        id: 1,
        tableNumber: "T-01",
        status: "available"
    },
    {
        id: 2,
        tableNumber: "T-02",
        status: "occupied"
    },
    {
        id: 3,
        tableNumber: "T-03",
        status: "available"
    }
];
```

Find table `T-02`:

```javascript
const table = tables.find(
    table => table.tableNumber === "T-02"
);

console.log(table);
```

Result:

```text
{
    id: 2,
    tableNumber: "T-02",
    status: "occupied"
}
```

---

# 16. Finding an Available Table

```javascript
const availableTable = tables.find(
    table => table.status === "available"
);

console.log(availableTable);
```

Result:

```text
{
    id: 1,
    tableNumber: "T-01",
    status: "available"
}
```

Notice that `T-03` is also available, but `find()` returns only the first available table.

---

# 17. Finding an Order

```javascript
const orders = [
    {
        id: 1,
        status: "pending"
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

const order = orders.find(order => order.id === 2);

console.log(order);
```

Output:

```text
{
    id: 2,
    status: "preparing"
}
```

---

# 18. Finding a Pending Order

```javascript
const pendingOrder = orders.find(
    order => order.status === "pending"
);

console.log(pendingOrder);
```

Output:

```text
{
    id: 1,
    status: "pending"
}
```

If several orders are pending, only the first one is returned.

---

# 19. Finding by Multiple Conditions

You can use multiple conditions.

```javascript
const users = [
    {
        name: "Sandip",
        role: "admin",
        isActive: true
    },
    {
        name: "Ram",
        role: "waiter",
        isActive: true
    },
    {
        name: "Sita",
        role: "admin",
        isActive: false
    }
];
```

Find an active admin:

```javascript
const admin = users.find(
    user => user.role === "admin" && user.isActive
);

console.log(admin);
```

Result:

```text
{
    name: "Sandip",
    role: "admin",
    isActive: true
}
```

---

# 20. Finding by Range

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
        name: "Monitor",
        price: 25000
    }
];

const product = products.find(
    product => product.price > 10000
);

console.log(product);
```

Output:

```text
{
    name: "Laptop",
    price: 80000
}
```

It returns the first product above `10000`.

---

# 21. Callback Parameters

The callback can receive three parameters:

```javascript
array.find((element, index, array) => {
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

const result = numbers.find((number, index) => {
    console.log(index, number);

    return number > 15;
});
```

Output from the logs:

```text
0 10
1 20
```

The search stops after `20` matches.

---

# 22. `find()` Stops Early

This is an important characteristic.

```javascript
const numbers = [10, 20, 30, 40, 50];

const result = numbers.find(number => {
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

It does not check `40` or `50`.

This happens because `30` satisfies the condition.

---

# 23. `find()` Does Not Modify the Array

```javascript
const numbers = [10, 20, 30];

const result = numbers.find(number => number > 15);

console.log(numbers);
```

Output:

```text
[10, 20, 30]
```

The original array remains unchanged.

---

# 24. Finding Nested Properties

Suppose:

```javascript
const users = [
    {
        name: "Sandip",
        profile: {
            city: "Birgunj"
        }
    },
    {
        name: "Ram",
        profile: {
            city: "Kathmandu"
        }
    }
];
```

Find a user from Birgunj:

```javascript
const user = users.find(
    user => user.profile.city === "Birgunj"
);

console.log(user);
```

Result:

```text
{
    name: "Sandip",
    profile: {
        city: "Birgunj"
    }
}
```

---

# 25. Optional Chaining with `find()`

If `profile` may not exist:

```javascript
const users = [
    {
        name: "Sandip",
        profile: {
            city: "Birgunj"
        }
    },
    {
        name: "Ram",
        profile: null
    }
];

const user = users.find(
    user => user.profile?.city === "Birgunj"
);

console.log(user);
```

Optional chaining:

```javascript
user.profile?.city
```

prevents an error when `profile` is `null` or `undefined`.

---

# 26. Case-Insensitive Search

Suppose:

```javascript
const users = [
    {
        name: "Sandip"
    },
    {
        name: "Ram"
    },
    {
        name: "Sita"
    }
];
```

Search for `"RAM"`:

```javascript
const search = "RAM";

const user = users.find(
    user => user.name.toLowerCase() === search.toLowerCase()
);

console.log(user);
```

Result:

```text
{
    name: "Ram"
}
```

---

# 27. Searching by Partial Text

```javascript
const users = [
    {
        name: "Sandip Kushwaha"
    },
    {
        name: "Ram Sharma"
    },
    {
        name: "Sita Thapa"
    }
];

const search = "kush";

const user = users.find(
    user => user.name.toLowerCase().includes(search.toLowerCase())
);

console.log(user);
```

Result:

```text
{
    name: "Sandip Kushwaha"
}
```

---

# 28. `find()` with IDs

A very common application pattern:

```javascript
const id = 3;

const user = users.find(
    user => user.id === id
);
```

Be careful about data types.

For example:

```javascript
const id = "3";

user.id === id;
```

is `false` if:

```javascript
user.id === 3
```

because strict equality does not convert types.

---

# 29. Finding a Boolean Condition

Suppose:

```javascript
const users = [
    {
        name: "Sandip",
        isActive: false
    },
    {
        name: "Ram",
        isActive: true
    }
];
```

Find the first active user:

```javascript
const activeUser = users.find(
    user => user.isActive
);

console.log(activeUser);
```

Result:

```text
{
    name: "Ram",
    isActive: true
}
```

---

# 30. `find()` vs `some()`

These methods are related but return different things.

### `find()`

Returns the matching element:

```javascript
const user = users.find(
    user => user.isActive
);
```

Result:

```text
{
    name: "Ram",
    isActive: true
}
```

### `some()`

Returns only `true` or `false`:

```javascript
const exists = users.some(
    user => user.isActive
);
```

Result:

```text
true
```

Remember:

```text
find() → Give me the matching element.
some() → Tell me whether at least one exists.
```

---

# 31. `find()` vs `findIndex()`

`find()` returns the element:

```javascript
const users = [
    { id: 10, name: "Sandip" },
    { id: 20, name: "Ram" },
    { id: 30, name: "Sita" }
];

const user = users.find(user => user.id === 20);

console.log(user);
```

Result:

```text
{
    id: 20,
    name: "Ram"
}
```

`findIndex()` returns the position:

```javascript
const index = users.findIndex(
    user => user.id === 20
);

console.log(index);
```

Result:

```text
1
```

Remember:

```text
find()       → element
findIndex()  → index
```

---

# 32. `find()` vs `filter()`

| Method        | Returns | Number of Results        |
| ------------- | ------- | ------------------------ |
| `find()`      | Element | First match              |
| `filter()`    | Array   | All matches              |
| `findIndex()` | Number  | First matching index     |
| `some()`      | Boolean | Whether any match exists |
| `every()`     | Boolean | Whether all match        |

Example:

```javascript
const numbers = [10, 20, 20, 30];
```

```javascript
numbers.find(n => n === 20);
// 20
```

```javascript
numbers.filter(n => n === 20);
// [20, 20]
```

```javascript
numbers.findIndex(n => n === 20);
// 1
```

```javascript
numbers.some(n => n === 20);
// true
```

---

# 33. Practical API Data Example

Imagine an API returns:

```javascript
const products = [
    {
        id: "p101",
        name: "Laptop"
    },
    {
        id: "p102",
        name: "Mouse"
    },
    {
        id: "p103",
        name: "Keyboard"
    }
];
```

You receive a product ID:

```javascript
const productId = "p102";
```

Find the product:

```javascript
const product = products.find(
    product => product.id === productId
);

console.log(product);
```

Result:

```text
{
    id: "p102",
    name: "Mouse"
}
```

This pattern is common when displaying a selected item.

---

# 34. Practical React Example

Suppose:

```javascript
const products = [
    {
        id: 1,
        name: "Laptop"
    },
    {
        id: 2,
        name: "Mouse"
    }
];
```

Selected ID:

```javascript
const selectedId = 2;
```

Find selected product:

```javascript
const selectedProduct = products.find(
    product => product.id === selectedId
);
```

Now:

```javascript
console.log(selectedProduct.name);
```

Output:

```text
Mouse
```

---

# 35. Finding a Category

```javascript
const categories = [
    {
        id: 1,
        name: "Pizza"
    },
    {
        id: 2,
        name: "Momo"
    },
    {
        id: 3,
        name: "Drinks"
    }
];

const category = categories.find(
    category => category.name === "Momo"
);

console.log(category);
```

Output:

```text
{
    id: 2,
    name: "Momo"
}
```

---

# 36. Finding a Food Item

```javascript
const foods = [
    {
        id: 1,
        name: "Chicken Momo",
        price: 250
    },
    {
        id: 2,
        name: "Veg Momo",
        price: 200
    }
];

const food = foods.find(
    food => food.id === 2
);

console.log(food);
```

Result:

```text
{
    id: 2,
    name: "Veg Momo",
    price: 200
}
```

---

# 37. Finding the First Available Table

```javascript
const tables = [
    {
        tableNumber: "T-01",
        status: "occupied"
    },
    {
        tableNumber: "T-02",
        status: "cleaning"
    },
    {
        tableNumber: "T-03",
        status: "available"
    },
    {
        tableNumber: "T-04",
        status: "available"
    }
];

const table = tables.find(
    table => table.status === "available"
);

console.log(table.tableNumber);
```

Output:

```text
T-03
```

Only the first available table is returned.

---

# 38. Checking the Result

Because `find()` can return `undefined`, you should sometimes check the result.

```javascript
const user = users.find(
    user => user.id === 100
);

if (user) {
    console.log(user.name);
} else {
    console.log("User not found");
}
```

This prevents errors when the expected element doesn't exist.

---

# 39. Using Optional Chaining After `find()`

Instead of:

```javascript
const user = users.find(
    user => user.id === 100
);

if (user) {
    console.log(user.name);
}
```

You can sometimes use:

```javascript
const name = users.find(
    user => user.id === 100
)?.name;

console.log(name);
```

If no user is found:

```text
undefined
```

is returned instead of causing an error.

---

# 40. Using Nullish Coalescing

You can provide a fallback:

```javascript
const name = users.find(
    user => user.id === 100
)?.name ?? "User not found";

console.log(name);
```

If the user doesn't exist:

```text
User not found
```

This combines:

```text
find()
   ↓
optional chaining ?.
   ↓
nullish coalescing ??
```

---

# 41. Important: `find()` Does Not Search by Value Automatically

This:

```javascript
const numbers = [10, 20, 30];

numbers.find(20);
```

is incorrect.

`find()` expects a **callback function**.

Correct:

```javascript
numbers.find(number => number === 20);
```

---

# 42. Common Mistake: Using `==`

You may see:

```javascript
const user = users.find(
    user => user.id == id
);
```

It may work because `==` performs type coercion.

Prefer strict comparison when the types are known:

```javascript
const user = users.find(
    user => user.id === id
);
```

If necessary, normalize the ID first:

```javascript
const numericId = Number(id);

const user = users.find(
    user => user.id === numericId
);
```

---

# 43. Common Mistake: Expecting All Matches

Wrong expectation:

```javascript
const result = users.find(
    user => user.isActive
);
```

This does **not** return all active users.

It returns only the first active user.

For all active users:

```javascript
const result = users.filter(
    user => user.isActive
);
```

---

# 44. Common Mistake: Expecting an Index

`find()` returns an element:

```javascript
const result = users.find(
    user => user.id === 2
);
```

If you need the index:

```javascript
const index = users.findIndex(
    user => user.id === 2
);
```

---

# 45. Best Practices

### 1. Use `find()` when you need one element

```javascript
const user = users.find(user => user.id === id);
```

### 2. Use `filter()` for multiple elements

```javascript
const activeUsers = users.filter(user => user.isActive);
```

### 3. Handle `undefined`

```javascript
const user = users.find(user => user.id === id);

if (!user) {
    console.log("User not found");
}
```

### 4. Use strict equality

```javascript
user.id === id
```

when the types are consistent.

### 5. Keep conditions readable

```javascript
const availableTable = tables.find(
    table => table.status === "available"
);
```

---

# 46. Quick Revision

```text
find()
   │
   ├── Checks array elements
   │
   ├── Executes callback
   │
   ├── First truthy result
   │       ↓
   │    returned
   │
   ├── Stops searching
   │
   └── No match
           ↓
       undefined
```

Example:

```javascript
const numbers = [5, 10, 15, 20];

const result = numbers.find(
    number => number > 10
);

console.log(result);
```

Output:

```text
15
```

---

# 47. `find()` Cheat Sheet

```javascript
// Find exact value
numbers.find(n => n === 20);

// Find greater value
numbers.find(n => n > 100);

// Find even number
numbers.find(n => n % 2 === 0);

// Find user by ID
users.find(user => user.id === id);

// Find user by email
users.find(user => user.email === email);

// Find active user
users.find(user => user.isActive);

// Find admin
users.find(user => user.role === "admin");

// Find available table
tables.find(table => table.status === "available");

// Find product
products.find(product => product.id === productId);

// Case-insensitive search
users.find(user =>
    user.name.toLowerCase() === search.toLowerCase()
);

// Safe property access
users.find(user => user.id === id)?.name;
```

---

# 48. Key Takeaways

* `find()` searches an array for an element.
* It returns the **first matching element**.
* It stops searching after finding a match.
* If no element matches, it returns `undefined`.
* It does not directly modify the original array.
* It is especially useful with arrays of objects.
* Use `filter()` when you need all matching elements.
* Use `findIndex()` when you need the matching index.
* Use `some()` when you only need a boolean result.
* `find()` is commonly used for users, products, orders, tables, categories, and API data.
* Always consider the possibility of `undefined`.

---
