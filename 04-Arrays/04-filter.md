# JavaScript Array `filter()` Method

The `filter()` method is used to **select elements from an array that satisfy a condition**.

It creates a **new array** containing only the elements for which the callback returns `true`.

---

# 1. What is `filter()`?

Suppose we have:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
```

We want only even numbers.

Using `filter()`:

```javascript
const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

The original array remains:

```text
[1, 2, 3, 4, 5, 6]
```

---

# 2. Basic Syntax

```javascript
const newArray = array.filter(callback);
```

The callback should return a **truthy or falsy value**.

```javascript
const result = numbers.filter(number => number > 10);
```

For each element:

```text
condition true  → included
condition false → excluded
```

---

# 3. How `filter()` Works

Example:

```javascript
const numbers = [1, 2, 3, 4, 5];
```

Condition:

```javascript
number % 2 === 0
```

Process:

```text
1 → false → excluded
2 → true  → included
3 → false → excluded
4 → true  → included
5 → false → excluded
```

Result:

```text
[2, 4]
```

---

# 4. `filter()` Does Not Modify the Original Array

```javascript
const numbers = [1, 2, 3, 4];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(numbers);
console.log(evenNumbers);
```

Output:

```text
[1, 2, 3, 4]
[2, 4]
```

`filter()` creates a new array.

---

# 5. Filtering Numbers

## Greater than a value

```javascript
const numbers = [10, 20, 30, 40, 50];

const result = numbers.filter(number => number > 25);

console.log(result);
```

Output:

```text
[30, 40, 50]
```

---

## Less than a value

```javascript
const result = numbers.filter(number => number < 35);

console.log(result);
```

Output:

```text
[10, 20, 30]
```

---

## Equal to a value

```javascript
const numbers = [10, 20, 20, 30];

const result = numbers.filter(number => number === 20);

console.log(result);
```

Output:

```text
[20, 20]
```

---

# 6. Filtering Even Numbers

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

---

# 7. Filtering Odd Numbers

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const oddNumbers = numbers.filter(number => number % 2 !== 0);

console.log(oddNumbers);
```

Output:

```text
[1, 3, 5]
```

---

# 8. Filtering Strings

```javascript
const names = [
    "Sandip",
    "Ram",
    "Sita",
    "Suman"
];

const longNames = names.filter(name => name.length > 4);

console.log(longNames);
```

Output:

```text
["Sandip", "Suman"]
```

---

# 9. Filtering by String Content

```javascript
const names = [
    "Sandip",
    "Ram",
    "Sita",
    "Suman"
];

const namesWithS = names.filter(name =>
    name.startsWith("S")
);

console.log(namesWithS);
```

Output:

```text
["Sandip", "Sita", "Suman"]
```

Another example:

```javascript
const names = ["Sandip", "Ram", "Sita"];

const result = names.filter(name =>
    name.includes("a")
);

console.log(result);
```

Output:

```text
["Sandip", "Ram", "Sita"]
```

---

# 10. Filtering Objects

This is one of the most important real-world uses of `filter()`.

```javascript
const users = [
    {
        name: "Sandip",
        age: 22
    },
    {
        name: "Ram",
        age: 17
    },
    {
        name: "Sita",
        age: 25
    }
];
```

Find adults:

```javascript
const adults = users.filter(user => user.age >= 18);

console.log(adults);
```

Result:

```text
[
    {
        name: "Sandip",
        age: 22
    },
    {
        name: "Sita",
        age: 25
    }
]
```

---

# 11. Filtering Active Users

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

const activeUsers = users.filter(user => user.isActive);

console.log(activeUsers);
```

Result:

```text
[
    {
        name: "Sandip",
        isActive: true
    },
    {
        name: "Sita",
        isActive: true
    }
]
```

---

# 12. Filtering Inactive Users

Use the `!` operator:

```javascript
const inactiveUsers = users.filter(user => !user.isActive);

console.log(inactiveUsers);
```

Result:

```text
[
    {
        name: "Ram",
        isActive: false
    }
]
```

---

# 13. Filtering by Role

```javascript
const users = [
    {
        name: "Sandip",
        role: "admin"
    },
    {
        name: "Ram",
        role: "waiter"
    },
    {
        name: "Sita",
        role: "kitchen"
    }
];

const admins = users.filter(user => user.role === "admin");

console.log(admins);
```

Result:

```text
[
    {
        name: "Sandip",
        role: "admin"
    }
]
```

---

# 14. Practical Hotel Example

Suppose a hotel has tables:

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
    },
    {
        tableNumber: "T-04",
        status: "cleaning"
    }
];
```

Get available tables:

```javascript
const availableTables = tables.filter(
    table => table.status === "available"
);

console.log(availableTables);
```

Result:

```text
[
    {
        tableNumber: "T-01",
        status: "available"
    },
    {
        tableNumber: "T-03",
        status: "available"
    }
]
```

---

# 15. Filter Hotel Food

```javascript
const menu = [
    {
        name: "Pizza",
        price: 500,
        isVeg: false
    },
    {
        name: "Paneer Momo",
        price: 300,
        isVeg: true
    },
    {
        name: "Veg Burger",
        price: 350,
        isVeg: true
    }
];
```

Get vegetarian food:

```javascript
const vegetarianFood = menu.filter(food => food.isVeg);

console.log(vegetarianFood);
```

---

# 16. Filter Food by Price

Food costing less than or equal to `350`:

```javascript
const affordableFood = menu.filter(food => food.price <= 350);

console.log(affordableFood);
```

Result:

```text
[
    {
        name: "Paneer Momo",
        price: 300,
        isVeg: true
    },
    {
        name: "Veg Burger",
        price: 350,
        isVeg: true
    }
]
```

---

# 17. Multiple Conditions

You can combine conditions using `&&`.

```javascript
const affordableVegFood = menu.filter(food =>
    food.isVeg && food.price <= 350
);
```

This means:

```text
isVeg must be true
AND
price must be <= 350
```

---

# 18. Using OR Conditions

Use `||` when either condition can be true.

```javascript
const selectedFood = menu.filter(food =>
    food.price < 300 || food.name === "Pizza"
);
```

This keeps food that:

* costs less than `300`, OR
* is `"Pizza"`.

---

# 19. Filtering Orders

Suppose:

```javascript
const orders = [
    {
        id: 1,
        status: "pending"
    },
    {
        id: 2,
        status: "completed"
    },
    {
        id: 3,
        status: "pending"
    }
];
```

Get pending orders:

```javascript
const pendingOrders = orders.filter(
    order => order.status === "pending"
);

console.log(pendingOrders);
```

Result:

```text
[
    {
        id: 1,
        status: "pending"
    },
    {
        id: 3,
        status: "pending"
    }
]
```

---

# 20. Filtering Orders by Amount

```javascript
const orders = [
    {
        id: 1,
        total: 500
    },
    {
        id: 2,
        total: 1200
    },
    {
        id: 3,
        total: 800
    }
];

const expensiveOrders = orders.filter(
    order => order.total > 700
);

console.log(expensiveOrders);
```

Result:

```text
[
    {
        id: 2,
        total: 1200
    },
    {
        id: 3,
        total: 800
    }
]
```

---

# 21. Filtering with the Index

The callback receives the index as the second parameter.

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];

const result = fruits.filter((fruit, index) => {
    return index % 2 === 0;
});

console.log(result);
```

Output:

```text
["Apple", "Mango"]
```

Indexes:

```text
Apple  → 0 → included
Banana → 1 → excluded
Mango  → 2 → included
Orange → 3 → excluded
```

---

# 22. Callback Parameters

The callback can receive:

```javascript
array.filter((element, index, array) => {
    // condition
});
```

Parameters:

| Parameter | Meaning         |
| --------- | --------------- |
| `element` | Current element |
| `index`   | Current index   |
| `array`   | Original array  |

Most of the time, only `element` is needed.

---

# 23. Filtering with a Normal Function

You can pass a named function.

```javascript
function isAdult(user) {
    return user.age >= 18;
}

const users = [
    { name: "Sandip", age: 22 },
    { name: "Ram", age: 17 }
];

const adults = users.filter(isAdult);

console.log(adults);
```

The function reference is passed to `filter()`.

---

# 24. `filter()` Returns a New Array

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.filter(number => number > 2);

console.log(result);
```

Output:

```text
[3, 4]
```

The original remains:

```text
[1, 2, 3, 4]
```

---

# 25. What Happens When Nothing Matches?

If no element satisfies the condition, `filter()` returns an empty array.

```javascript
const numbers = [1, 2, 3];

const result = numbers.filter(number => number > 10);

console.log(result);
```

Output:

```text
[]
```

It does **not** return `null` or `undefined`.

---

# 26. What Happens with an Empty Array?

```javascript
const numbers = [];

const result = numbers.filter(number => number > 10);

console.log(result);
```

Output:

```text
[]
```

---

# 27. `filter()` Uses Truthy and Falsy Values

The callback does not have to explicitly return `true` or `false`.

Example:

```javascript
const values = [
    "Hello",
    "",
    "JavaScript",
    "",
    "React"
];

const result = values.filter(value => value);

console.log(result);
```

Output:

```text
["Hello", "JavaScript", "React"]
```

Empty strings are falsy, so they are excluded.

However, for readability, explicit conditions are often preferable in application code.

---

# 28. Removing Falsy Values

A common pattern:

```javascript
const values = [
    "Hello",
    null,
    "JavaScript",
    undefined,
    "",
    "React"
];

const result = values.filter(Boolean);

console.log(result);
```

Output:

```text
["Hello", "JavaScript", "React"]
```

`Boolean` is being used as the callback.

It converts each value to `true` or `false`.

---

# 29. Removing `null` and `undefined`

If you only want to remove `null` and `undefined`, don't use `filter(Boolean)` because that also removes values such as `0`, `false`, and `""`.

Use:

```javascript
const values = [
    0,
    1,
    null,
    2,
    undefined,
    false
];

const result = values.filter(
    value => value !== null && value !== undefined
);

console.log(result);
```

Output:

```text
[0, 1, 2, false]
```

---

# 30. `filter()` vs `map()`

This is one of the most important differences.

### `filter()`

Selects elements.

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.filter(number => number > 2);
```

Result:

```text
[3, 4]
```

### `map()`

Transforms elements.

```javascript
const result = numbers.map(number => number * 2);
```

Result:

```text
[2, 4, 6, 8]
```

Remember:

```text
filter() → Which elements should remain?
map()    → What should each element become?
```

---

# 31. `filter()` vs `find()`

`filter()` returns **all matching elements**.

```javascript
const numbers = [10, 20, 20, 30];

const result = numbers.filter(number => number === 20);

console.log(result);
```

Output:

```text
[20, 20]
```

`find()` returns the **first matching element**.

```javascript
const result = numbers.find(number => number === 20);

console.log(result);
```

Output:

```text
20
```

If nothing is found:

```javascript
numbers.find(number => number === 100);
```

returns:

```text
undefined
```

Whereas:

```javascript
numbers.filter(number => number === 100);
```

returns:

```text
[]
```

---

# 32. `filter()` vs `some()`

`filter()` returns the matching elements.

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.filter(number => number > 2);

console.log(result);
```

Output:

```text
[3, 4]
```

`some()` returns a boolean indicating whether at least one element matches.

```javascript
const result = numbers.some(number => number > 2);

console.log(result);
```

Output:

```text
true
```

---

# 33. `filter()` vs `every()`

`filter()` returns matching elements:

```javascript
const numbers = [2, 4, 6, 7];

const result = numbers.filter(number => number % 2 === 0);

console.log(result);
```

Output:

```text
[2, 4, 6]
```

`every()` checks whether all elements satisfy the condition:

```javascript
const result = numbers.every(number => number % 2 === 0);

console.log(result);
```

Output:

```text
false
```

---

# 34. Chaining `filter()` and `map()`

A very common pattern is:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 10);

console.log(result);
```

Output:

```text
[20, 40, 60]
```

Process:

```text
[1, 2, 3, 4, 5, 6]
            ↓
         filter()
            ↓
       [2, 4, 6]
            ↓
          map()
            ↓
       [20, 40, 60]
```

---

# 35. Practical React Example

Suppose a React application contains:

```javascript
const products = [
    {
        id: 1,
        name: "Laptop",
        inStock: true
    },
    {
        id: 2,
        name: "Mouse",
        inStock: false
    },
    {
        id: 3,
        name: "Keyboard",
        inStock: true
    }
];
```

Display only products in stock:

```jsx
products
    .filter(product => product.inStock)
    .map(product => (
        <div key={product.id}>
            {product.name}
        </div>
    ))
```

This is a very common React pattern.

---

# 36. Practical Search Example

Suppose:

```javascript
const foods = [
    "Pizza",
    "Burger",
    "Momo",
    "Chowmein"
];
```

Search for `"mo"`:

```javascript
const search = "mo";

const result = foods.filter(food =>
    food.toLowerCase().includes(search.toLowerCase())
);

console.log(result);
```

Output:

```text
["Momo"]
```

This pattern is commonly used for search boxes.

---

# 37. Practical User Search

```javascript
const users = [
    { name: "Sandip Kushwaha" },
    { name: "Ram Sharma" },
    { name: "Sita Thapa" }
];

const search = "ram";

const result = users.filter(user =>
    user.name.toLowerCase().includes(search.toLowerCase())
);

console.log(result);
```

Result:

```text
[
    {
        name: "Ram Sharma"
    }
]
```

---

# 38. Practical Category Filtering

```javascript
const products = [
    {
        name: "Laptop",
        category: "electronics"
    },
    {
        name: "Shirt",
        category: "clothing"
    },
    {
        name: "Mouse",
        category: "electronics"
    }
];

const electronics = products.filter(
    product => product.category === "electronics"
);

console.log(electronics);
```

Result:

```text
[
    {
        name: "Laptop",
        category: "electronics"
    },
    {
        name: "Mouse",
        category: "electronics"
    }
]
```

---

# 39. Combining Search and Category

You can combine multiple conditions.

```javascript
const search = "lap";
const category = "electronics";

const result = products.filter(product =>
    product.category === category &&
    product.name.toLowerCase().includes(search.toLowerCase())
);

console.log(result);
```

This pattern is useful for dashboards and ecommerce applications.

---

# 40. Filter by Multiple Statuses

Suppose orders can have:

```text
pending
confirmed
preparing
ready
completed
cancelled
```

Get orders that are currently active:

```javascript
const activeStatuses = [
    "pending",
    "confirmed",
    "preparing",
    "ready"
];

const activeOrders = orders.filter(order =>
    activeStatuses.includes(order.status)
);
```

This is cleaner than writing many `||` conditions.

---

# 41. Filter by Date

Suppose:

```javascript
const orders = [
    {
        id: 1,
        date: "2026-10-01"
    },
    {
        id: 2,
        date: "2026-10-02"
    },
    {
        id: 3,
        date: "2026-09-30"
    }
];
```

Get orders from October 2:

```javascript
const result = orders.filter(
    order => order.date === "2026-10-02"
);

console.log(result);
```

Result:

```text
[
    {
        id: 2,
        date: "2026-10-02"
    }
]
```

---

# 42. Filter Nested Properties

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

Filter by city:

```javascript
const result = users.filter(
    user => user.profile.city === "Birgunj"
);

console.log(result);
```

---

# 43. Optional Chaining with `filter()`

If nested data may be missing:

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

const result = users.filter(
    user => user.profile?.city === "Birgunj"
);

console.log(result);
```

Optional chaining prevents an error when `profile` is `null` or `undefined`.

---

# 44. `filter()` and Object References

`filter()` creates a **new array**, but the objects inside it are the same object references.

Example:

```javascript
const users = [
    {
        name: "Sandip",
        active: true
    }
];

const activeUsers = users.filter(user => user.active);

activeUsers[0].name = "Changed";

console.log(users[0].name);
```

Output:

```text
Changed
```

Why?

Because both arrays contain a reference to the same object.

If you need independent object copies, you must explicitly copy the objects.

---

# 45. Common Mistakes

## Mistake 1: Forgetting the condition

Wrong:

```javascript
const result = numbers.filter(number => {
    number * 2;
});
```

This doesn't return a useful boolean condition.

Correct:

```javascript
const result = numbers.filter(number => number > 10);
```

---

## Mistake 2: Expecting `filter()` to transform values

Wrong:

```javascript
const result = numbers.filter(number => number * 2);
```

This doesn't mean "double every number."

Use:

```javascript
const result = numbers.map(number => number * 2);
```

---

## Mistake 3: Expecting `filter()` to return one object

`filter()` always returns an array.

```javascript
const result = users.filter(user => user.id === 1);
```

Result:

```text
[{ ... }]
```

If you need one matching object:

```javascript
const result = users.find(user => user.id === 1);
```

---

## Mistake 4: Using `filter(Boolean)` without understanding it

```javascript
values.filter(Boolean);
```

removes all falsy values, including:

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

Use an explicit condition when you need more precise filtering.

---

## Mistake 5: Mutating objects inside `filter()`

Avoid using `filter()` to perform unrelated mutations.

Bad:

```javascript
const result = users.filter(user => {
    user.active = true;
    return user.age >= 18;
});
```

Filtering should normally be focused on deciding whether an element belongs in the result.

---

# 46. Best Practices

### 1. Use `filter()` for selection

Good:

```javascript
const activeUsers = users.filter(user => user.isActive);
```

---

### 2. Keep the condition clear

Good:

```javascript
const affordable = products.filter(
    product => product.price <= 500
);
```

---

### 3. Use `find()` for one result

If you only need the first matching object:

```javascript
const user = users.find(user => user.id === id);
```

---

### 4. Combine with `map()` when appropriate

```javascript
const names = users
    .filter(user => user.isActive)
    .map(user => user.name);
```

---

### 5. Avoid unnecessary mutation

Treat the original array as unchanged when using `filter()`.

---

# 47. Quick Revision

```text
filter()
   │
   ├── Checks every visited element
   │
   ├── Executes a callback
   │
   ├── Truthy result → include element
   │
   ├── Falsy result  → exclude element
   │
   └── Returns a new array
```

Example:

```javascript
const numbers = [1, 2, 3, 4, 5];

const evenNumbers = numbers.filter(
    number => number % 2 === 0
);
```

Result:

```text
[2, 4]
```

---

# 48. `filter()` Cheat Sheet

```javascript
// Greater than
numbers.filter(n => n > 10);

// Less than
numbers.filter(n => n < 10);

// Even
numbers.filter(n => n % 2 === 0);

// Odd
numbers.filter(n => n % 2 !== 0);

// Active users
users.filter(user => user.isActive);

// Admin users
users.filter(user => user.role === "admin");

// Available food
foods.filter(food => food.isAvailable);

// Search
users.filter(user =>
    user.name.toLowerCase().includes(search.toLowerCase())
);

// Multiple conditions
products.filter(product =>
    product.isActive && product.price < 500
);

// Remove null/undefined only
values.filter(
    value => value !== null && value !== undefined
);
```

---

# 49. Key Takeaways

* `filter()` selects elements from an array.
* It returns a **new array**.
* The original array is not directly modified.
* The callback should determine whether an element should be included.
* Truthy callback result → element included.
* Falsy callback result → element excluded.
* `filter()` can receive `element`, `index`, and `array`.
* `filter()` always returns an array.
* If nothing matches, it returns `[]`.
* Use `map()` for transformation.
* Use `find()` when you need the first matching element.
* Use `some()` when you only need a true/false answer for whether at least one matches.
* `filter(Boolean)` removes all falsy values.
* `filter()` is commonly used for search, categories, statuses, permissions, and UI filtering.
* `filter()` is heavily used with React list rendering.
* `filter()` can be chained with `map()` and other array methods.

---
