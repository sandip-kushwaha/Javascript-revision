# Immutability in JavaScript

**Immutability** means avoiding direct modification of existing data.

Instead of changing the original value, we create a **new value** containing the required changes.

Immutability is especially important in:

* React
* State management
* Functional programming
* Frontend applications
* Predictable application logic

---

# 1. Mutable vs Immutable

## Mutable

A mutable value can be changed directly.

```javascript
const user = {
    name: "Sandip",
    age: 22
};

user.age = 23;

console.log(user);
```

The original object was modified.

---

## Immutable Approach

Create a new object:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

const updatedUser = {
    ...user,
    age: 23
};

console.log(user);
console.log(updatedUser);
```

The original `user` remains unchanged.

---

# 2. Why Immutability Matters

Without immutability, changing shared data can make applications difficult to understand.

For example:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

function updateUser(user) {
    user.age = 23;
}

updateUser(user);

console.log(user.age);
```

The function directly changed the original object.

With immutability:

```javascript
function updateUser(user) {
    return {
        ...user,
        age: 23
    };
}

const updatedUser = updateUser(user);
```

Now the original object is preserved.

---

# 3. `const` Does Not Mean Immutable

This is important.

```javascript
const user = {
    name: "Sandip"
};

user.name = "Ram";
```

This is allowed.

Why?

Because `const` prevents reassignment of the variable:

```javascript
user = {};
```

But it does not automatically make the object immutable.

So:

```text
const
    ↓
Cannot reassign the variable

Immutability
    ↓
Do not directly modify the data
```

---

# 4. Immutable Primitive Values

Primitive values are immutable.

Examples:

```text
string
number
boolean
bigint
symbol
undefined
null
```

Consider:

```javascript
let name = "Sandip";

name = "Ram";
```

The original string `"Sandip"` is not modified.

A new string value is assigned.

---

# 5. Strings Are Immutable

You cannot directly modify a character inside a string.

```javascript
let name = "Sandip";

name[0] = "R";

console.log(name);
```

The string remains:

```text
Sandip
```

Instead, create a new string:

```javascript
const name = "Sandip";

const updatedName = "Ram";

console.log(updatedName);
```

String methods also return new strings:

```javascript
const text = "javascript";

const upper = text.toUpperCase();

console.log(text);
console.log(upper);
```

Output:

```text
javascript
JAVASCRIPT
```

The original string was not changed.

---

# 6. Arrays Can Be Mutated

Arrays are mutable.

For example:

```javascript
const numbers = [1, 2, 3];

numbers.push(4);

console.log(numbers);
```

Output:

```text
[1, 2, 3, 4]
```

The original array was modified.

Other mutating methods include:

```text
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
```

---

# 7. Immutable Array Update

Instead of:

```javascript
const numbers = [1, 2, 3];

numbers.push(4);
```

Create a new array:

```javascript
const numbers = [1, 2, 3];

const updatedNumbers = [
    ...numbers,
    4
];

console.log(updatedNumbers);
```

Result:

```text
[1, 2, 3, 4]
```

Original:

```javascript
console.log(numbers);
```

Result:

```text
[1, 2, 3]
```

---

# 8. Adding an Item

Original array:

```javascript
const users = [
    "Sandip",
    "Ram"
];
```

Immutable addition:

```javascript
const updatedUsers = [
    ...users,
    "Hari"
];
```

Result:

```text
["Sandip", "Ram", "Hari"]
```

---

# 9. Removing an Item

Avoid:

```javascript
users.splice(1, 1);
```

Instead use `filter()`:

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
        name: "Hari"
    }
];

const updatedUsers = users.filter(
    (user) => user.id !== 2
);
```

Result:

```javascript
[
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 3,
        name: "Hari"
    }
]
```

The original array remains unchanged.

---

# 10. Updating an Array Item

Suppose:

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

Update the second user:

```javascript
const updatedUsers = users.map((user) => {
    if (user.id === 2) {
        return {
            ...user,
            name: "Hari"
        };
    }

    return user;
});
```

Result:

```javascript
[
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Hari"
    }
]
```

---

# 11. Updating an Object

Original:

```javascript
const user = {
    name: "Sandip",
    age: 22,
    role: "developer"
};
```

Immutable update:

```javascript
const updatedUser = {
    ...user,
    age: 23
};
```

You can update multiple properties:

```javascript
const updatedUser = {
    ...user,
    age: 23,
    role: "full-stack developer"
};
```

---

# 12. Removing an Object Property

You can use object destructuring with rest:

```javascript
const user = {
    name: "Sandip",
    age: 22,
    role: "developer"
};

const { role, ...userWithoutRole } = user;

console.log(userWithoutRole);
```

Result:

```javascript
{
    name: "Sandip",
    age: 22
}
```

The original object is unchanged.

---

# 13. Nested Objects

Consider:

```javascript
const user = {
    name: "Sandip",
    address: {
        city: "Birgunj",
        country: "Nepal"
    }
};
```

To update the nested city immutably:

```javascript
const updatedUser = {
    ...user,
    address: {
        ...user.address,
        city: "Kathmandu"
    }
};
```

This creates new objects for the changed levels.

---

# 14. Nested Arrays and Objects

Consider a shopping cart:

```javascript
const cart = {
    items: [
        {
            id: 1,
            name: "Laptop",
            quantity: 1
        },
        {
            id: 2,
            name: "Mouse",
            quantity: 2
        }
    ]
};
```

Update the quantity of the mouse:

```javascript
const updatedCart = {
    ...cart,

    items: cart.items.map((item) => {
        if (item.id === 2) {
            return {
                ...item,
                quantity: 3
            };
        }

        return item;
    })
};
```

The original cart remains unchanged.

---

# 15. React State and Immutability

Immutability is especially important in React.

Avoid directly changing state.

Bad:

```javascript
user.name = "Ram";
```

Better:

```javascript
setUser({
    ...user,
    name: "Ram"
});
```

---

# 16. Updating Array State in React

Suppose:

```javascript
const [users, setUsers] = useState([
    {
        id: 1,
        name: "Sandip"
    },
    {
        id: 2,
        name: "Ram"
    }
]);
```

Update a user:

```javascript
setUsers((currentUsers) => {
    return currentUsers.map((user) => {
        if (user.id === 2) {
            return {
                ...user,
                name: "Hari"
            };
        }

        return user;
    });
});
```

---

# 17. Adding to React State

```javascript
setUsers((currentUsers) => {
    return [
        ...currentUsers,
        {
            id: 3,
            name: "Hari"
        }
    ];
});
```

The previous array is not directly modified.

---

# 18. Removing from React State

```javascript
setUsers((currentUsers) => {
    return currentUsers.filter(
        (user) => user.id !== 2
    );
});
```

This creates a new array without the selected user.

---

# 19. Updating Objects in React

Example:

```javascript
const [user, setUser] = useState({
    name: "Sandip",
    age: 22
});
```

Update:

```javascript
setUser((currentUser) => ({
    ...currentUser,
    age: 23
}));
```

---

# 20. Why React Uses Immutable Updates

Immutable updates make it easier for React and developers to detect changes.

For example:

```javascript
setUser({
    ...user,
    name: "Ram"
});
```

creates a new object reference.

Conceptually:

```text
Old Object
    ↓
Create new object
    ↓
React receives new state
    ↓
React can compare references
```

This helps React determine when state has changed.

---

# 21. Reference Comparison

Consider:

```javascript
const user = {
    name: "Sandip"
};

const sameUser = user;

console.log(user === sameUser);
```

Output:

```text
true
```

Both variables reference the same object.

---

Now:

```javascript
const user = {
    name: "Sandip"
};

const updatedUser = {
    ...user
};

console.log(user === updatedUser);
```

Output:

```text
false
```

The values may be the same, but they are different object references.

---

# 22. Shallow Copy

Spread syntax creates a shallow copy:

```javascript
const copy = {
    ...user
};
```

For nested objects, references may still be shared.

Example:

```javascript
const user = {
    name: "Sandip",
    address: {
        city: "Birgunj"
    }
};

const copy = {
    ...user
};

console.log(user === copy);
```

Output:

```text
false
```

But:

```javascript
console.log(
    user.address === copy.address
);
```

Output:

```text
true
```

The top-level object is new, but the nested `address` object is shared.

---

# 23. Deep Immutable Updates

For nested data, copy each level that you change.

```javascript
const updatedUser = {
    ...user,
    address: {
        ...user.address,
        city: "Kathmandu"
    }
};
```

Now:

```javascript
console.log(
    user.address === updatedUser.address
);
```

Output:

```text
false
```

Both the user object and changed address object have new references.

---

# 24. Non-Mutating Array Methods

Useful methods for immutable operations include:

```text
map()
filter()
slice()
concat()
```

Examples:

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(
    (number) => number * 2
);

const filtered = numbers.filter(
    (number) => number > 1
);

const copied = numbers.slice();

const combined = numbers.concat([4, 5]);
```

These operations create new arrays.

---

# 25. Mutating vs Non-Mutating

| Mutating    | Non-Mutating Alternative         |
| ----------- | -------------------------------- |
| `push()`    | `[...array, value]`              |
| `pop()`     | `slice()` / spread               |
| `shift()`   | `slice()` / spread               |
| `unshift()` | `[value, ...array]`              |
| `splice()`  | `slice()` / `filter()` / `map()` |
| `sort()`    | `toSorted()`                     |
| `reverse()` | `toReversed()`                   |

Modern JavaScript also provides:

```javascript
toSorted()
toReversed()
toSpliced()
```

These return a new array instead of modifying the original.

---

# 26. `sort()` vs `toSorted()`

Traditional:

```javascript
const numbers = [3, 1, 2];

numbers.sort();

console.log(numbers);
```

`sort()` modifies the original array.

Using `toSorted()`:

```javascript
const numbers = [3, 1, 2];

const sortedNumbers = numbers.toSorted();

console.log(numbers);
console.log(sortedNumbers);
```

The original array remains unchanged.

---

# 27. `reverse()` vs `toReversed()`

Traditional:

```javascript
const numbers = [1, 2, 3];

numbers.reverse();
```

The original array changes.

Modern approach:

```javascript
const numbers = [1, 2, 3];

const reversedNumbers = numbers.toReversed();

console.log(numbers);
console.log(reversedNumbers);
```

---

# 28. `splice()` vs `toSpliced()`

Traditional:

```javascript
const numbers = [1, 2, 3, 4];

numbers.splice(1, 1);
```

The original array changes.

Using `toSpliced()`:

```javascript
const numbers = [1, 2, 3, 4];

const updatedNumbers = numbers.toSpliced(1, 1);

console.log(numbers);
console.log(updatedNumbers);
```

The original array remains unchanged.

---

# 29. Object.freeze()

`Object.freeze()` prevents direct modification of an object at the top level.

```javascript
const user = {
    name: "Sandip",
    age: 22
};

Object.freeze(user);

user.age = 23;

console.log(user.age);
```

The property cannot be changed in the normal way.

However, `Object.freeze()` is shallow.

Nested objects can still be modified unless they are also frozen.

---

# 30. Object.seal()

`Object.seal()` prevents adding or deleting properties.

```javascript
const user = {
    name: "Sandip",
    age: 22
};

Object.seal(user);
```

Existing properties can generally still be changed.

```text
Object.freeze()
    ↓
Cannot add, delete, or change properties

Object.seal()
    ↓
Cannot add or delete properties
    ↓
Existing properties can still be changed
```

Both are shallow.

---

# 31. Immutable Function Design

A function is easier to reason about when it does not modify its input.

Avoid:

```javascript
function increaseAge(user) {
    user.age++;
    return user;
}
```

Prefer:

```javascript
function increaseAge(user) {
    return {
        ...user,
        age: user.age + 1
    };
}
```

Now the function returns a new object.

---

# 32. Immutability in API Data

Suppose API data is:

```javascript
const product = {
    name: "Laptop",
    price: 800
};
```

Instead of changing it directly:

```javascript
product.price = 750;
```

Create an updated value:

```javascript
const updatedProduct = {
    ...product,
    price: 750
};
```

This approach is useful when transforming API responses before displaying them.

---

# 33. Immutability in a Shopping Cart

Original:

```javascript
const cart = [
    {
        id: 1,
        name: "Laptop",
        quantity: 1
    }
];
```

Add an item:

```javascript
const updatedCart = [
    ...cart,
    {
        id: 2,
        name: "Mouse",
        quantity: 1
    }
];
```

Update quantity:

```javascript
const updatedCart = cart.map((item) => {
    if (item.id === 1) {
        return {
            ...item,
            quantity: item.quantity + 1
        };
    }

    return item;
});
```

Remove an item:

```javascript
const updatedCart = cart.filter(
    (item) => item.id !== 1
);
```

---

# 34. Immutability Pattern

For arrays:

```text
Add
    → spread

Update
    → map

Remove
    → filter
```

For objects:

```text
Update
    → spread

Remove property
    → destructuring + rest
```

For nested data:

```text
Copy each changed level
    ↓
Create new references
```

---

# 35. Important Rules

### Rule 1

Do not directly modify shared application state.

### Rule 2

Use spread syntax for simple object and array updates.

### Rule 3

Use `map()` to update array elements.

### Rule 4

Use `filter()` to remove array elements.

### Rule 5

Copy every nested level that you modify.

### Rule 6

Remember that `const` does not make objects immutable.

### Rule 7

Remember that spread creates a shallow copy.

---

# 36. Quick Reference

```javascript
// Object update
const updatedUser = {
    ...user,
    age: 23
};
```

```javascript
// Add array item
const updated = [
    ...items,
    newItem
];
```

```javascript
// Remove array item
const updated = items.filter(
    (item) => item.id !== id
);
```

```javascript
// Update array item
const updated = items.map((item) =>
    item.id === id
        ? { ...item, name: "New Name" }
        : item
);
```

```javascript
// Nested update
const updated = {
    ...user,
    address: {
        ...user.address,
        city: "Kathmandu"
    }
};
```

---

# Key Takeaways

* Immutability means avoiding direct modification of existing data.
* `const` does not make objects or arrays immutable.
* Objects and arrays can be changed unless you use an immutable update pattern.
* Spread syntax creates a shallow copy.
* `map()` is useful for updating array items.
* `filter()` is useful for removing array items.
* Spread is useful for adding array items.
* Nested updates require copying each changed level.
* `sort()`, `reverse()`, and `splice()` mutate arrays.
* `toSorted()`, `toReversed()`, and `toSpliced()` return new arrays.
* React state should generally be updated without directly mutating the existing state.
* Immutable updates create new references, making state changes easier to track.
