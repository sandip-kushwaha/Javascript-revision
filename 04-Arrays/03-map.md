# JavaScript Array `map()` Method

The `map()` method is used to **create a new array by transforming every element** of an existing array.

It is one of the most important array methods in JavaScript and is used heavily in **React, Node.js, and frontend development**.

---

# 1. What is `map()`?

`map()` goes through every element of an array, executes a callback function, and creates a **new array** containing the returned values.

### Basic syntax

```javascript
const newArray = array.map(callback);
```

Example:

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

---

# 2. How `map()` Works

Suppose:

```javascript
const numbers = [1, 2, 3];
```

We run:

```javascript
const result = numbers.map(number => number * 2);
```

Internally:

```text
1 → 1 × 2 → 2
2 → 2 × 2 → 4
3 → 3 × 2 → 6
```

Result:

```text
[2, 4, 6]
```

---

# 3. `map()` Does Not Modify the Original Array

This is an important feature.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);

console.log(numbers);
console.log(doubled);
```

Output:

```text
[1, 2, 3]
[2, 4, 6]
```

The original array remains unchanged.

---

# 4. Basic Example

```javascript
const numbers = [10, 20, 30];

const result = numbers.map(number => number + 5);

console.log(result);
```

Output:

```text
[15, 25, 35]
```

---

# 5. `map()` with a Normal Function

You don't have to use an arrow function.

```javascript
function double(number) {
    return number * 2;
}

const numbers = [1, 2, 3];

const result = numbers.map(double);

console.log(result);
```

Output:

```text
[2, 4, 6]
```

Here:

```javascript
map(double);
```

passes the function reference to `map()`.

---

# 6. `map()` Callback Parameters

The callback can receive three parameters:

```javascript
array.map((element, index, array) => {
    // ...
});
```

They are:

| Parameter | Meaning         |
| --------- | --------------- |
| `element` | Current element |
| `index`   | Current index   |
| `array`   | Original array  |

---

# 7. Using the Element

Most commonly, we only need the element.

```javascript
const numbers = [10, 20, 30];

const result = numbers.map(number => number * 2);

console.log(result);
```

---

# 8. Using the Index

```javascript
const fruits = ["Apple", "Banana", "Mango"];

const result = fruits.map((fruit, index) => {
    return `${index + 1}. ${fruit}`;
});

console.log(result);
```

Output:

```text
[
    "1. Apple",
    "2. Banana",
    "3. Mango"
]
```

---

# 9. Using the Original Array

The third parameter is the original array.

```javascript
const numbers = [10, 20, 30];

const result = numbers.map((number, index, array) => {
    console.log("Current:", number);
    console.log("Index:", index);
    console.log("Array:", array);

    return number * 2;
});
```

The third parameter is useful in some advanced transformations, but most of the time you only need the first one or two parameters.

---

# 10. `map()` Must Return a Value

This is very important.

Correct:

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(number => {
    return number * 2;
});

console.log(result);
```

Output:

```text
[2, 4, 6]
```

If you use braces with an arrow function, you normally need an explicit `return`.

---

# 11. Common `map()` Mistake

This:

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(number => {
    number * 2;
});

console.log(result);
```

produces:

```text
[undefined, undefined, undefined]
```

Why?

Because:

```javascript
{
    number * 2;
}
```

does not return the value.

Correct:

```javascript
const result = numbers.map(number => {
    return number * 2;
});
```

Or use an implicit return:

```javascript
const result = numbers.map(number => number * 2);
```

---

# 12. Transforming Strings

```javascript
const names = ["sandip", "ram", "sita"];

const upperNames = names.map(name => name.toUpperCase());

console.log(upperNames);
```

Output:

```text
["SANDIP", "RAM", "SITA"]
```

---

# 13. Converting Numbers to Strings

```javascript
const numbers = [10, 20, 30];

const strings = numbers.map(number => String(number));

console.log(strings);
```

Output:

```text
["10", "20", "30"]
```

---

# 14. Extracting Properties from Objects

This is one of the most common real-world uses.

```javascript
const users = [
    {
        name: "Sandip",
        age: 22
    },
    {
        name: "Ram",
        age: 25
    },
    {
        name: "Sita",
        age: 21
    }
];
```

Get only names:

```javascript
const names = users.map(user => user.name);

console.log(names);
```

Output:

```text
["Sandip", "Ram", "Sita"]
```

---

# 15. Creating New Objects with `map()`

You can transform each object into another object.

```javascript
const users = [
    {
        name: "Sandip",
        age: 22
    },
    {
        name: "Ram",
        age: 25
    }
];

const result = users.map(user => {
    return {
        username: user.name,
        age: user.age
    };
});

console.log(result);
```

Result:

```text
[
    {
        username: "Sandip",
        age: 22
    },
    {
        username: "Ram",
        age: 25
    }
]
```

---

# 16. Adding a Property

Suppose:

```javascript
const users = [
    {
        name: "Sandip",
        age: 22
    },
    {
        name: "Ram",
        age: 25
    }
];
```

Add a status:

```javascript
const updatedUsers = users.map(user => {
    return {
        ...user,
        status: "active"
    };
});
```

Result:

```text
[
    {
        name: "Sandip",
        age: 22,
        status: "active"
    },
    {
        name: "Ram",
        age: 25,
        status: "active"
    }
]
```

The spread operator creates a new object for each element.

---

# 17. Changing a Property

```javascript
const users = [
    {
        name: "Sandip",
        age: 22
    },
    {
        name: "Ram",
        age: 25
    }
];

const updatedUsers = users.map(user => {
    return {
        ...user,
        age: user.age + 1
    };
});
```

Result:

```text
[
    {
        name: "Sandip",
        age: 23
    },
    {
        name: "Ram",
        age: 26
    }
]
```

---

# 18. Practical Example: Hotel Menu

Suppose we have:

```javascript
const menu = [
    {
        name: "Pizza",
        price: 500
    },
    {
        name: "Burger",
        price: 300
    },
    {
        name: "Momo",
        price: 250
    }
];
```

Get food names:

```javascript
const foodNames = menu.map(food => food.name);

console.log(foodNames);
```

Output:

```text
["Pizza", "Burger", "Momo"]
```

---

# 19. Increase Food Prices

Suppose the hotel increases prices by 10%.

```javascript
const updatedMenu = menu.map(food => {
    return {
        ...food,
        price: food.price * 1.10
    };
});

console.log(updatedMenu);
```

The original `menu` remains unchanged.

---

# 20. Calculate Prices with Quantity

Suppose:

```javascript
const orders = [
    {
        item: "Pizza",
        price: 500,
        quantity: 2
    },
    {
        item: "Momo",
        price: 250,
        quantity: 3
    }
];
```

Calculate each order's total:

```javascript
const orderTotals = orders.map(order => {
    return {
        item: order.item,
        total: order.price * order.quantity
    };
});

console.log(orderTotals);
```

Result:

```text
[
    {
        item: "Pizza",
        total: 1000
    },
    {
        item: "Momo",
        total: 750
    }
]
```

---

# 21. Adding an ID

```javascript
const foods = [
    { name: "Pizza" },
    { name: "Burger" },
    { name: "Momo" }
];

const foodsWithId = foods.map((food, index) => {
    return {
        id: index + 1,
        ...food
    };
});

console.log(foodsWithId);
```

Result:

```text
[
    { id: 1, name: "Pizza" },
    { id: 2, name: "Burger" },
    { id: 3, name: "Momo" }
]
```

---

# 22. Formatting Data

`map()` is useful for preparing data before displaying it.

```javascript
const users = [
    { firstName: "Sandip", lastName: "Kushwaha" },
    { firstName: "Ram", lastName: "Sharma" }
];

const fullNames = users.map(user => {
    return `${user.firstName} ${user.lastName}`;
});

console.log(fullNames);
```

Output:

```text
[
    "Sandip Kushwaha",
    "Ram Sharma"
]
```

---

# 23. `map()` with Conditions

You can use conditions inside the callback.

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.map(number => {
    if (number % 2 === 0) {
        return "Even";
    }

    return "Odd";
});

console.log(result);
```

Output:

```text
["Odd", "Even", "Odd", "Even"]
```

However, if your goal is to remove elements rather than transform them, use `filter()`.

---

# 24. `map()` with Ternary Operator

The previous example can be shortened:

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.map(number =>
    number % 2 === 0 ? "Even" : "Odd"
);

console.log(result);
```

Output:

```text
["Odd", "Even", "Odd", "Even"]
```

---

# 25. Mapping Nested Data

Suppose:

```javascript
const hotels = [
    {
        name: "Hotel A",
        rooms: [
            { number: 101 },
            { number: 102 }
        ]
    },
    {
        name: "Hotel B",
        rooms: [
            { number: 201 },
            { number: 202 }
        ]
    }
];
```

Get room numbers for each hotel:

```javascript
const rooms = hotels.map(hotel => {
    return hotel.rooms.map(room => room.number);
});

console.log(rooms);
```

Result:

```text
[
    [101, 102],
    [201, 202]
]
```

Notice that nested `map()` produces nested arrays.

---

# 26. `map()` vs `forEach()`

This is an important difference.

### `map()`

Used when you want a **new transformed array**.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);
```

Result:

```text
[2, 4, 6]
```

### `forEach()`

Used when you want to **perform an action**.

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

It does not return a transformed array.

---

# 27. Comparison

| Feature                    | `map()`        | `forEach()`  |
| -------------------------- | -------------- | ------------ |
| Executes callback          | Yes            | Yes          |
| Creates new array          | Yes            | No           |
| Returns transformed values | Yes            | No           |
| Usually used for           | Transformation | Side effects |
| Changes original array     | No*            | No*          |

*The array itself is not modified by the method, but the callback can still mutate objects or other referenced values if you explicitly do so.

---

# 28. `map()` vs `filter()`

`map()` transforms every element.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => number * 2);
```

Result:

```text
[2, 4, 6, 8]
```

`filter()` selects elements.

```javascript
const even = numbers.filter(number => number % 2 === 0);
```

Result:

```text
[2, 4]
```

Remember:

```text
map()    → transform
filter() → select
```

---

# 29. `map()` vs `find()`

`map()` returns an array with one result for each visited element.

```javascript
const numbers = [10, 20, 30];

const result = numbers.map(number => number * 2);

console.log(result);
```

Output:

```text
[20, 40, 60]
```

`find()` returns the first matching element.

```javascript
const result = numbers.find(number => number > 15);

console.log(result);
```

Output:

```text
20
```

---

# 30. `map()` vs `reduce()`

`map()` normally produces an array of transformed values.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);
```

Result:

```text
[2, 4, 6]
```

`reduce()` combines values into a single result.

```javascript
const total = numbers.reduce(
    (sum, number) => sum + number,
    0
);
```

Result:

```text
6
```

Remember:

```text
map()    → array
reduce() → one accumulated result
```

---

# 31. Chaining `map()`

You can call another array method after `map()`.

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers
    .map(number => number * 2)
    .map(number => number + 1);

console.log(result);
```

Process:

```text
[1, 2, 3, 4]
       ↓ map × 2
[2, 4, 6, 8]
       ↓ map + 1
[3, 5, 7, 9]
```

---

# 32. Chaining `filter()` and `map()`

This is extremely common.

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 2);

console.log(result);
```

Process:

```text
[1, 2, 3, 4, 5, 6]
        ↓ filter
[2, 4, 6]
        ↓ map
[4, 8, 12]
```

---

# 33. Practical React Example

`map()` is one of the most important methods in React.

Suppose:

```javascript
const products = [
    { id: 1, name: "Laptop" },
    { id: 2, name: "Mouse" },
    { id: 3, name: "Keyboard" }
];
```

You can render them:

```jsx
products.map(product => (
    <div key={product.id}>
        {product.name}
    </div>
))
```

React uses `map()` to transform an array of data into an array of UI elements.

---

# 34. React List Example

```jsx
function ProductList() {
    const products = [
        { id: 1, name: "Laptop" },
        { id: 2, name: "Mouse" },
        { id: 3, name: "Keyboard" }
    ];

    return (
        <div>
            {products.map(product => (
                <p key={product.id}>
                    {product.name}
                </p>
            ))}
        </div>
    );
}
```

The important part is:

```jsx
products.map(product => (
    <p key={product.id}>
        {product.name}
    </p>
))
```

---

# 35. Why React Needs `key`

When rendering lists with `map()`, React commonly expects a `key` for each rendered element.

Example:

```jsx
products.map(product => (
    <div key={product.id}>
        {product.name}
    </div>
))
```

A stable unique ID is generally preferable to using the array index when items can be inserted, removed, or reordered.

---

# 36. Mapping API Data

Suppose an API returns:

```javascript
const response = {
    users: [
        {
            _id: "101",
            fullName: "Sandip Kushwaha"
        },
        {
            _id: "102",
            fullName: "Ram Sharma"
        }
    ]
};
```

Get IDs:

```javascript
const ids = response.users.map(user => user._id);
```

Get names:

```javascript
const names = response.users.map(user => user.fullName);
```

Transform for a dropdown:

```javascript
const options = response.users.map(user => ({
    value: user._id,
    label: user.fullName
}));
```

Result:

```text
[
    {
        value: "101",
        label: "Sandip Kushwaha"
    },
    {
        value: "102",
        label: "Ram Sharma"
    }
]
```

---

# 37. `map()` with Optional Chaining

When data may be missing, optional chaining can help in specific cases.

```javascript
const users = [
    { profile: { name: "Sandip" } },
    { profile: null }
];

const names = users.map(user => user.profile?.name);

console.log(names);
```

Output:

```text
["Sandip", undefined]
```

Optional chaining prevents an error when `profile` is `null` or `undefined`.

---

# 38. `map()` and Object Mutation

Be careful when working with objects.

This code creates a new array:

```javascript
const updatedUsers = users.map(user => ({
    ...user,
    active: true
}));
```

But this code mutates each existing object:

```javascript
const updatedUsers = users.map(user => {
    user.active = true;
    return user;
});
```

The array returned by `map()` is new, but the objects inside it are the same objects that were in the original array.

When immutability matters, prefer creating new objects.

---

# 39. Sparse Arrays

`map()` preserves empty slots in sparse arrays rather than calling the callback for those missing elements.

For normal application code, avoid relying on sparse-array behavior unless you specifically need it.

---

# 40. Common Mistakes

## Mistake 1: Forgetting `return`

Wrong:

```javascript
const result = numbers.map(number => {
    number * 2;
});
```

Correct:

```javascript
const result = numbers.map(number => {
    return number * 2;
});
```

Or:

```javascript
const result = numbers.map(number => number * 2);
```

---

## Mistake 2: Expecting `map()` to modify the original array

```javascript
const numbers = [1, 2, 3];

numbers.map(number => number * 2);

console.log(numbers);
```

Output:

```text
[1, 2, 3]
```

Store the returned array:

```javascript
const doubled = numbers.map(number => number * 2);
```

---

## Mistake 3: Using `map()` when you don't need a returned array

Avoid:

```javascript
numbers.map(number => {
    console.log(number);
});
```

If you're only performing an action, use:

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

---

## Mistake 4: Expecting `map()` to remove elements

`map()` does not remove elements.

If you need to select certain elements, use:

```javascript
filter()
```

Example:

```javascript
const evenNumbers = numbers.filter(number => number % 2 === 0);
```

---

## Mistake 5: Returning objects incorrectly

This:

```javascript
const users = names.map(name => {
    name: name
});
```

does not return an object.

Use:

```javascript
const users = names.map(name => ({
    name: name
}));
```

Or:

```javascript
const users = names.map(name => ({
    name
}));
```

---

# 41. Best Practices

### 1. Use `map()` for transformation

Good:

```javascript
const prices = products.map(product => product.price);
```

---

### 2. Keep callbacks readable

Good:

```javascript
const names = users.map(user => user.name);
```

For complex transformations, use a named function.

```javascript
function formatUser(user) {
    return {
        id: user._id,
        name: user.fullName
    };
}

const formattedUsers = users.map(formatUser);
```

---

### 3. Don't mutate objects unnecessarily

Prefer:

```javascript
const updated = users.map(user => ({
    ...user,
    active: true
}));
```

instead of modifying the original objects.

---

### 4. Use stable keys in React

Prefer:

```jsx
items.map(item => (
    <div key={item.id}>
        {item.name}
    </div>
))
```

when a stable unique ID is available.

---

# 42. Quick Revision

```text
map()
 │
 ├── Iterates through an array
 │
 ├── Calls a callback for each visited element
 │
 ├── Uses the callback's returned value
 │
 ├── Creates a new array
 │
 └── Does not directly modify the original array
```

Example:

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
```

Result:

```text
[2, 4, 6]
```

---

# 43. `map()` Cheat Sheet

```javascript
// Numbers
[1, 2, 3].map(n => n * 2);

// Strings
["a", "b"].map(str => str.toUpperCase());

// Object property
users.map(user => user.name);

// New objects
users.map(user => ({
    ...user,
    active: true
}));

// Index
items.map((item, index) => `${index}: ${item}`);

// Chaining
items
    .filter(item => item.active)
    .map(item => item.name);
```

---

# 44. Key Takeaways

* `map()` creates a new array.
* It transforms each visited element.
* It receives a callback function.
* The callback's returned value becomes an element in the new array.
* The original array is not directly modified.
* The callback can receive `element`, `index`, and `array`.
* `map()` is commonly used with arrays of objects.
* `map()` is heavily used in React for rendering lists.
* Use `filter()` when you want to select/remove elements based on a condition.
* Use `forEach()` when you only need to perform an action.
* Use `reduce()` when you need to accumulate values into a single result.
* Always remember to return a value when using a block-bodied callback.
* Use object spread when creating updated object copies.
* `map()` can be chained with other array methods.

---
