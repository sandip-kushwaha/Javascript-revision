# JavaScript Array `findIndex()` Method

The `findIndex()` method is used to **find the index of the first element in an array that satisfies a condition**.

It returns:

* The **index** of the first matching element.
* `-1` if no element matches.

---

# 1. What is `findIndex()`?

Example:

```javascript
const numbers = [10, 20, 30, 40, 50];

const index = numbers.findIndex(number => number > 25);

console.log(index);
```

Output:

```text
2
```

Why?

```text
10 → index 0 → false
20 → index 1 → false
30 → index 2 → true → STOP
```

So the result is:

```text
2
```

---

# 2. Basic Syntax

```javascript
const index = array.findIndex(callback);
```

Example:

```javascript
const index = numbers.findIndex(
    number => number === 30
);
```

---

# 3. How `findIndex()` Works

Consider:

```javascript
const numbers = [5, 10, 15, 20];
```

Find the index of the first number greater than `10`:

```javascript
const index = numbers.findIndex(
    number => number > 10
);

console.log(index);
```

Process:

```text
5  → false → index 0
10 → false → index 1
15 → true  → index 2 → STOP
```

Result:

```text
2
```

---

# 4. `findIndex()` Returns an Index

Given:

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];
```

Find `"Mango"`:

```javascript
const index = fruits.findIndex(
    fruit => fruit === "Mango"
);

console.log(index);
```

Output:

```text
2
```

Array indexes start from `0`:

```text
Apple  → 0
Banana → 1
Mango  → 2
Orange → 3
```

---

# 5. What Happens When Nothing Is Found?

If no element satisfies the condition:

```javascript
const numbers = [10, 20, 30];

const index = numbers.findIndex(
    number => number > 100
);

console.log(index);
```

Output:

```text
-1
```

Remember:

```text
Match found    → index
No match       → -1
```

---

# 6. `findIndex()` vs `find()`

This is very important.

### `find()`

Returns the matching element:

```javascript
const numbers = [10, 20, 30];

const result = numbers.find(
    number => number > 15
);

console.log(result);
```

Output:

```text
20
```

### `findIndex()`

Returns the matching element's index:

```javascript
const result = numbers.findIndex(
    number => number > 15
);

console.log(result);
```

Output:

```text
1
```

Remember:

```text
find()       → element
findIndex()  → index
```

---

# 7. `findIndex()` vs `indexOf()`

Both can find indexes, but they work differently.

## `indexOf()`

Used when you know the exact value:

```javascript
const numbers = [10, 20, 30];

const index = numbers.indexOf(20);

console.log(index);
```

Output:

```text
1
```

## `findIndex()`

Used when you need a condition:

```javascript
const index = numbers.findIndex(
    number => number > 15
);

console.log(index);
```

Output:

```text
1
```

Remember:

```text
indexOf()      → exact value
findIndex()   → condition
```

---

# 8. Finding an Object's Index

`findIndex()` is especially useful with arrays of objects.

```javascript
const users = [
    {
        id: 101,
        name: "Sandip"
    },
    {
        id: 102,
        name: "Ram"
    },
    {
        id: 103,
        name: "Sita"
    }
];
```

Find the index of user `102`:

```javascript
const index = users.findIndex(
    user => user.id === 102
);

console.log(index);
```

Output:

```text
1
```

---

# 9. Finding a Product Index

```javascript
const products = [
    {
        id: 1,
        name: "Laptop"
    },
    {
        id: 2,
        name: "Mouse"
    },
    {
        id: 3,
        name: "Keyboard"
    }
];

const index = products.findIndex(
    product => product.id === 2
);

console.log(index);
```

Output:

```text
1
```

---

# 10. Finding a Hotel Table Index

For a hotel management system:

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

Find the index of `T-02`:

```javascript
const index = tables.findIndex(
    table => table.tableNumber === "T-02"
);

console.log(index);
```

Output:

```text
1
```

---

# 11. Updating an Object Using `findIndex()`

This is one of the most useful practical patterns.

Suppose:

```javascript
const users = [
    {
        id: 1,
        name: "Sandip",
        isActive: true
    },
    {
        id: 2,
        name: "Ram",
        isActive: true
    }
];
```

Find the user index:

```javascript
const index = users.findIndex(
    user => user.id === 2
);
```

Then update:

```javascript
if (index !== -1) {
    users[index].isActive = false;
}

console.log(users);
```

Result:

```text
[
    {
        id: 1,
        name: "Sandip",
        isActive: true
    },
    {
        id: 2,
        name: "Ram",
        isActive: false
    }
]
```

---

# 12. Updating an Array Element

Example:

```javascript
const numbers = [10, 20, 30, 40];

const index = numbers.findIndex(
    number => number === 30
);

if (index !== -1) {
    numbers[index] = 35;
}

console.log(numbers);
```

Output:

```text
[10, 20, 35, 40]
```

---

# 13. Replacing an Object

```javascript
const users = [
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Ram"
    }
];

const index = users.findIndex(
    user => user.id === 2
);

if (index !== -1) {
    users[index] = {
        ...users[index],
        name: "Ram Sharma"
    };
}

console.log(users);
```

Result:

```text
[
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Ram Sharma"
    }
]
```

---

# 14. Why Check `index !== -1`?

Suppose the user doesn't exist:

```javascript
const index = users.findIndex(
    user => user.id === 100
);

console.log(index);
```

Result:

```text
-1
```

If you don't check:

```javascript
users[index].name = "New Name";
```

then you're effectively trying to access:

```javascript
users[-1]
```

which does not represent a normal array element.

Better:

```javascript
if (index !== -1) {
    users[index].name = "New Name";
}
```

---

# 15. Removing an Element Using `findIndex()`

You can combine `findIndex()` with `splice()`.

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

const index = users.findIndex(
    user => user.id === 2
);

if (index !== -1) {
    users.splice(index, 1);
}

console.log(users);
```

Result:

```text
[
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 3,
        name: "Sita"
    }
]
```

`splice()` modifies the original array.

---

# 16. Adding an Element at a Found Position

```javascript
const numbers = [10, 20, 40, 50];

const index = numbers.findIndex(
    number => number === 40
);

if (index !== -1) {
    numbers.splice(index, 0, 30);
}

console.log(numbers);
```

Output:

```text
[10, 20, 30, 40, 50]
```

---

# 17. Callback Parameters

The callback can receive:

```javascript
array.findIndex((element, index, array) => {
    // condition
});
```

| Parameter | Meaning         |
| --------- | --------------- |
| `element` | Current element |
| `index`   | Current index   |
| `array`   | Original array  |

Usually, only `element` is needed.

---

# 18. Finding an Index with Multiple Conditions

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

const index = users.findIndex(
    user => user.role === "admin" && user.isActive
);

console.log(index);
```

Output:

```text
0
```

---

# 19. Finding the First Matching Index

Consider:

```javascript
const numbers = [10, 20, 30, 20, 40];
```

Find the index of the first `20`:

```javascript
const index = numbers.findIndex(
    number => number === 20
);

console.log(index);
```

Output:

```text
1
```

Even though another `20` exists at index `3`, `findIndex()` returns the first match.

---

# 20. `findIndex()` Stops Searching

Example:

```javascript
const numbers = [10, 20, 30, 40, 50];

const index = numbers.findIndex(number => {
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
2
```

It stops after finding the first match.

---

# 21. Searching by String

```javascript
const names = [
    "Ram",
    "Sita",
    "Sandip",
    "Suman"
];

const index = names.findIndex(
    name => name === "Sandip"
);

console.log(index);
```

Output:

```text
2
```

---

# 22. Case-Insensitive Search

```javascript
const names = [
    "Ram",
    "Sita",
    "Sandip"
];

const search = "SANDIP";

const index = names.findIndex(
    name => name.toLowerCase() === search.toLowerCase()
);

console.log(index);
```

Output:

```text
2
```

---

# 23. Partial String Search

```javascript
const names = [
    "Sandip Kushwaha",
    "Ram Sharma",
    "Sita Thapa"
];

const search = "kush";

const index = names.findIndex(
    name => name.toLowerCase().includes(search.toLowerCase())
);

console.log(index);
```

Output:

```text
0
```

---

# 24. Finding the First Available Table

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

const index = tables.findIndex(
    table => table.status === "available"
);

console.log(index);
```

Output:

```text
2
```

The first available table is at index `2`.

---

# 25. Changing Table Status

Using the previous example:

```javascript
if (index !== -1) {
    tables[index].status = "occupied";
}

console.log(tables[index]);
```

Result:

```text
{
    tableNumber: "T-03",
    status: "occupied"
}
```

---

# 26. Updating an Order

Suppose:

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
        status: "ready"
    }
];
```

Find order `2`:

```javascript
const index = orders.findIndex(
    order => order.id === 2
);
```

Update its status:

```javascript
if (index !== -1) {
    orders[index].status = "ready";
}
```

Now:

```javascript
console.log(orders[index]);
```

Output:

```text
{
    id: 2,
    status: "ready"
}
```

---

# 27. React and Immutable Updates

In React, you usually avoid directly mutating the existing state array.

Suppose:

```javascript
const users = [
    {
        id: 1,
        name: "Sandip",
        isActive: true
    },
    {
        id: 2,
        name: "Ram",
        isActive: true
    }
];
```

Find the index:

```javascript
const index = users.findIndex(
    user => user.id === 2
);
```

A common immutable update pattern is:

```javascript
const updatedUsers = users.map((user, i) =>
    i === index
        ? { ...user, isActive: false }
        : user
);
```

This creates a new array instead of changing the original array.

---

# 28. `findIndex()` vs `indexOf()`

Use `indexOf()` when searching for an exact value:

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango"
];

const index = fruits.indexOf("Mango");
```

Use `findIndex()` when searching using a condition:

```javascript
const users = [
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Ram"
    }
];

const index = users.findIndex(
    user => user.id === 2
);
```

---

# 29. `findIndex()` vs `find()`

```javascript
const users = [
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Ram"
    }
];
```

### `find()`

```javascript
const user = users.find(
    user => user.id === 2
);
```

Result:

```text
{
    id: 2,
    name: "Ram"
}
```

### `findIndex()`

```javascript
const index = users.findIndex(
    user => user.id === 2
);
```

Result:

```text
1
```

---

# 30. `findIndex()` vs `filter()`

`filter()` returns all matching elements:

```javascript
const result = users.filter(
    user => user.isActive
);
```

`findIndex()` returns the position of the first matching element:

```javascript
const index = users.findIndex(
    user => user.isActive
);
```

Remember:

```text
filter()      → matching elements
findIndex()   → first matching index
```

---

# 31. `findIndex()` vs `some()`

`some()`:

```javascript
const exists = users.some(
    user => user.id === 2
);
```

Result:

```text
true
```

`findIndex()`:

```javascript
const index = users.findIndex(
    user => user.id === 2
);
```

Result:

```text
1
```

Use `some()` when you only need to know whether a match exists.

Use `findIndex()` when you need the position.

---

# 32. Practical CRUD Pattern

`findIndex()` is useful when working with local arrays in CRUD operations.

### Update

```javascript
const index = users.findIndex(
    user => user.id === id
);

if (index !== -1) {
    users[index] = {
        ...users[index],
        name: "Updated Name"
    };
}
```

### Delete

```javascript
const index = users.findIndex(
    user => user.id === id
);

if (index !== -1) {
    users.splice(index, 1);
}
```

This pattern is useful for understanding how array-based CRUD works.

---

# 33. Using `findIndex()` with Status

```javascript
const orders = [
    {
        id: 1,
        status: "pending"
    },
    {
        id: 2,
        status: "ready"
    },
    {
        id: 3,
        status: "pending"
    }
];

const index = orders.findIndex(
    order => order.status === "pending"
);

console.log(index);
```

Output:

```text
0
```

Only the first pending order is found.

---

# 34. No Match Check

Always remember that `-1` means no match.

```javascript
const index = users.findIndex(
    user => user.id === 999
);

if (index === -1) {
    console.log("User not found");
}
```

Output:

```text
User not found
```

---

# 35. Important Difference Between `-1` and `undefined`

`find()`:

```javascript
const user = users.find(
    user => user.id === 999
);

console.log(user);
```

Result:

```text
undefined
```

`findIndex()`:

```javascript
const index = users.findIndex(
    user => user.id === 999
);

console.log(index);
```

Result:

```text
-1
```

Remember:

```text
find()       → undefined
findIndex()  → -1
```

when no match exists.

---

# 36. Common Mistakes

## Mistake 1: Expecting the object

Wrong expectation:

```javascript
const result = users.findIndex(
    user => user.id === 2
);
```

The result is not the user object.

It is:

```text
1
```

Use `find()` if you need the object.

---

## Mistake 2: Forgetting the `-1` check

Avoid:

```javascript
users[index].name = "New Name";
```

without checking whether `index` exists.

Better:

```javascript
if (index !== -1) {
    users[index].name = "New Name";
}
```

---

## Mistake 3: Expecting all matching indexes

`findIndex()` returns only the **first matching index**.

For all matching elements:

```javascript
const result = users.filter(
    user => user.isActive
);
```

---

## Mistake 4: Using `findIndex()` for an exact primitive value

For a simple exact value:

```javascript
const index = numbers.indexOf(20);
```

is usually simpler.

Use `findIndex()` when you need a condition.

---

# 37. Best Practices

### Use `findIndex()` when:

* You need the position of an element.
* You need to update an array element.
* You need to remove an element using `splice()`.
* You are searching objects by ID or another property.
* You need a condition rather than exact value matching.

Example:

```javascript
const index = users.findIndex(
    user => user.id === id
);
```

Always handle:

```javascript
index === -1
```

when a match may not exist.

---

# 38. Quick Revision

```text
findIndex()
     │
     ├── Searches array
     │
     ├── Runs callback
     │
     ├── First matching element
     │       ↓
     │    returns index
     │
     └── No match
             ↓
            -1
```

Example:

```javascript
const numbers = [10, 20, 30, 40];

const index = numbers.findIndex(
    number => number > 25
);

console.log(index);
```

Output:

```text
2
```

---

# 39. Cheat Sheet

```javascript
// Find index of exact value
numbers.indexOf(20);

// Find index using a condition
numbers.findIndex(n => n > 20);

// Find user by ID
users.findIndex(user => user.id === id);

// Find active user index
users.findIndex(user => user.isActive);

// Find product index
products.findIndex(product => product.id === productId);

// Find available table index
tables.findIndex(table => table.status === "available");

// Check whether found
const index = users.findIndex(user => user.id === id);

if (index !== -1) {
    console.log("Found at:", index);
}

// Update element
if (index !== -1) {
    users[index] = {
        ...users[index],
        name: "Updated"
    };
}

// Remove element
if (index !== -1) {
    users.splice(index, 1);
}
```

---

# 40. Key Takeaways

* `findIndex()` returns the **index of the first matching element**.
* It accepts a callback function.
* It stops after the first match.
* It returns `-1` when no match is found.
* It does not directly modify the original array.
* It is useful for arrays of objects.
* It is commonly used for updating and removing array elements.
* `find()` returns the element.
* `findIndex()` returns the index.
* `indexOf()` is useful for finding an exact value.
* `filter()` returns all matching elements.
* `some()` only tells you whether a match exists.
* Always check for `-1` before using the returned index for an update or deletion.

---
