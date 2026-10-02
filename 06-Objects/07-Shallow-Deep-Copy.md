# JavaScript Shallow Copy and Deep Copy

When working with objects and arrays, it is important to understand **copying**.

JavaScript has two important types of copying:

1. **Shallow Copy**
2. **Deep Copy**

Understanding the difference is especially important when working with:

* Objects
* Arrays
* Nested data
* React state
* API responses
* Databases
* JavaScript applications

---

# 1. What Is a Reference?

Objects and arrays are stored and accessed through **references**.

For example:

```javascript
const user = {
  name: "Sandip"
};
```

If you do:

```javascript
const copy = user;
```

you did **not** create a new object.

Both variables refer to the same object.

```text
user ──────┐
           ↓
       { name: "Sandip" }
           ↑
copy ──────┘
```

---

# 2. Assignment Does Not Create a Copy

Consider:

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const copy = user;

copy.age = 23;

console.log(user.age);
```

Output:

```text
23
```

Why?

Because:

```javascript
const copy = user;
```

copies the **reference**, not the object itself.

---

# 3. Object Reference

This comparison shows the difference:

```javascript
const user = {
  name: "Sandip"
};

const copy = user;

console.log(user === copy);
```

Output:

```text
true
```

Both variables point to the same object.

---

# 4. Creating a Shallow Copy

A shallow copy creates a new top-level object.

One common method is the spread operator:

```javascript
const user = {
  name: "Sandip",
  age: 22
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

Now they are different top-level objects.

---

# 5. Shallow Copy Example

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const copy = {
  ...user
};

copy.age = 23;

console.log(user.age);
console.log(copy.age);
```

Output:

```text
22
23
```

Changing the copied top-level property does not change the original.

---

# 6. Shallow Copy With `Object.assign()`

Another way to create a shallow copy is:

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const copy = Object.assign({}, user);

console.log(copy);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22
}
```

Both of these create shallow copies:

```javascript
const copy1 = { ...user };

const copy2 = Object.assign({}, user);
```

---

# 7. Shallow Copy With Arrays

Spread also creates a shallow copy of arrays.

```javascript
const numbers = [1, 2, 3];

const copy = [...numbers];

copy.push(4);

console.log(numbers);
console.log(copy);
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

The top-level arrays are different.

---

# 8. Array Reference

Without copying:

```javascript
const numbers = [1, 2, 3];

const copy = numbers;

copy.push(4);

console.log(numbers);
```

Output:

```text
[1, 2, 3, 4]
```

Because both variables refer to the same array.

---

# 9. What Does "Shallow" Mean?

Shallow means that **only the first/top level is copied**.

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

Create a shallow copy:

```javascript
const copy = {
  ...user
};
```

The structure is approximately:

```text
user
 │
 ├── name ──────> "Sandip"
 │
 └── address ───> { city, country }
                       ↑
copy                   │
 │                     │
 ├── name ──────> "Sandip"
 │
 └── address ──────────┘
```

The top-level object is different, but the nested `address` object is shared.

---

# 10. Shallow Copy With Nested Objects

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

copy.address.city = "Kathmandu";

console.log(user.address.city);
```

Output:

```text
Kathmandu
```

This may look surprising.

The reason is:

```javascript
user.address === copy.address
```

Output:

```text
true
```

---

# 11. Nested Arrays

The same problem can happen with nested arrays.

```javascript
const user = {
  name: "Sandip",
  skills: ["JavaScript", "React"]
};

const copy = {
  ...user
};

copy.skills.push("Node.js");

console.log(user.skills);
```

Output:

```text
["JavaScript", "React", "Node.js"]
```

The nested array is shared.

---

# 12. Copying a Nested Object Manually

If the object is only one level deep, you can copy the nested object too.

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const copy = {
  ...user,
  address: {
    ...user.address
  }
};

copy.address.city = "Kathmandu";

console.log(user.address.city);
console.log(copy.address.city);
```

Output:

```text
Birgunj
Kathmandu
```

Now the nested `address` objects are different.

---

# 13. Multiple Nested Levels

Suppose:

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj",
    location: {
      ward: 10
    }
  }
};
```

You would need to copy each nested level that you intend to change independently:

```javascript
const copy = {
  ...user,
  address: {
    ...user.address,
    location: {
      ...user.address.location
    }
  }
};
```

This can become difficult when the data is deeply nested.

---

# 14. What Is Deep Copy?

A **deep copy** creates independent copies of nested objects and arrays as well.

For example:

```javascript
const original = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};
```

A deep copy creates a structure where:

```text
original
 │
 └── address ──> separate object


copy
 │
 └── address ──> another separate object
```

Changing the nested object in the copy does not affect the original.

---

# 15. Deep Copy With `structuredClone()`

Modern JavaScript provides:

```javascript
structuredClone()
```

Example:

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const copy = structuredClone(user);

copy.address.city = "Kathmandu";

console.log(user.address.city);
console.log(copy.address.city);
```

Output:

```text
Birgunj
Kathmandu
```

The nested object is independent.

---

# 16. Comparing the Objects

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const copy = structuredClone(user);

console.log(user === copy);
```

Output:

```text
false
```

And:

```javascript
console.log(user.address === copy.address);
```

Output:

```text
false
```

Both the top-level and nested objects are different references.

---

# 17. Deep Copy With Arrays

`structuredClone()` also works with nested arrays.

```javascript
const data = {
  numbers: [1, 2, 3],
  users: [
    {
      name: "Sandip"
    }
  ]
};

const copy = structuredClone(data);

copy.numbers.push(4);
copy.users[0].name = "Ram";

console.log(data);
console.log(copy);
```

The original nested data remains independent.

---

# 18. `structuredClone()` and JSON

Another technique often seen in JavaScript code is:

```javascript
JSON.parse(JSON.stringify(object));
```

Example:

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const copy = JSON.parse(
  JSON.stringify(user)
);

copy.address.city = "Kathmandu";

console.log(user.address.city);
```

Output:

```text
Birgunj
```

This can create a deep copy for simple JSON-compatible data.

However, it has important limitations.

---

# 19. Problems With JSON Deep Copy

Consider:

```javascript
const data = {
  name: "Sandip",
  value: undefined,
  createdAt: new Date()
};
```

Using:

```javascript
JSON.parse(JSON.stringify(data));
```

can change or remove values that JSON cannot represent directly.

For example:

* `undefined` properties can be removed.
* `Date` becomes a string.
* Functions are not preserved.
* `Map` and `Set` are not preserved as their original types.
* Special values such as `NaN` and `Infinity` do not remain the same.
* Circular references cause `JSON.stringify()` to fail.

Therefore, `structuredClone()` is generally preferable when you need a built-in deep clone and the values are supported by the structured clone algorithm.

---

# 20. Shallow Copy vs Deep Copy

| Feature                     | Shallow Copy | Deep Copy              |
| --------------------------- | ------------ | ---------------------- |
| New top-level object        | Yes          | Yes                    |
| Top-level properties copied | Yes          | Yes                    |
| Nested objects independent  | No           | Yes                    |
| Nested arrays independent   | No           | Yes                    |
| Simple and fast             | Usually      | Usually more work      |
| Example                     | `{ ...obj }` | `structuredClone(obj)` |

---

# 21. Common Shallow Copy Methods

### Object spread

```javascript
const copy = {
  ...object
};
```

### `Object.assign()`

```javascript
const copy = Object.assign({}, object);
```

### Array spread

```javascript
const copy = [...array];
```

### Array `slice()`

```javascript
const copy = array.slice();
```

These create **shallow copies**.

---

# 22. Common Deep Copy Method

For supported structured-cloneable values:

```javascript
const copy = structuredClone(original);
```

This can copy nested objects and arrays independently.

---

# 23. Hotel Management Example

Consider a hotel table:

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "available",
  location: {
    area: "rooftop"
  }
};
```

Using shallow copy:

```javascript
const updatedTable = {
  ...table,
  status: "occupied"
};
```

This is fine because `status` is a top-level property.

---

# 24. Updating a Nested Hotel Property

Suppose you want to update the location:

```javascript
const updatedTable = {
  ...table,
  location: {
    ...table.location,
    area: "indoor"
  }
};
```

Now:

```javascript
console.log(table.location.area);
```

Output:

```text
rooftop
```

And:

```javascript
console.log(updatedTable.location.area);
```

Output:

```text
indoor
```

This is a common immutable update pattern.

---

# 25. Food Example

Suppose:

```javascript
const food = {
  name: "Chicken Momo",
  price: 180,
  category: {
    name: "Momo"
  }
};
```

To update the category name:

```javascript
const updatedFood = {
  ...food,
  category: {
    ...food.category,
    name: "Nepali Momo"
  }
};
```

The original remains unchanged.

---

# 26. React Example

Shallow copying is extremely common in React.

Suppose:

```javascript
const [user, setUser] = useState({
  name: "Sandip",
  age: 22
});
```

To update the age:

```javascript
setUser({
  ...user,
  age: 23
});
```

For nested data:

```javascript
setUser({
  ...user,
  address: {
    ...user.address,
    city: "Kathmandu"
  }
});
```

Each changed level is copied.

---

# 27. Why Copying Matters in React

React commonly relies on object references to determine whether state values have changed.

Instead of:

```javascript
user.age = 23;
```

use:

```javascript
setUser({
  ...user,
  age: 23
});
```

This creates a new object reference.

For nested state, copy the relevant levels.

---

# 28. Copying Arrays of Objects

Consider:

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

Copying the array:

```javascript
const copy = [...users];
```

creates a new array.

But:

```javascript
copy[0] === users[0]
```

is:

```text
true
```

The objects inside are still shared.

---

# 29. Updating an Object Inside an Array

You can create a new array and copy the object you want to change.

```javascript
const updatedUsers = users.map((user) =>
  user.id === 1
    ? {
        ...user,
        name: "Shyam"
      }
    : user
);
```

Now the updated object is a new object.

---

# 30. Shallow Copy Diagram

```text
Original
┌─────────────────────┐
│ name                │
│ address ────────────┼──────┐
└─────────────────────┘      │
                             ↓
                         { city }


Copy
┌─────────────────────┐
│ name                │
│ address ────────────┼──────┘
└─────────────────────┘
```

The top-level objects are different, but the nested object is shared.

---

# 31. Deep Copy Diagram

```text
Original
┌─────────────────────┐
│ name                │
│ address ────────────┼──────> { city }
└─────────────────────┘


Copy
┌─────────────────────┐
│ name                │
│ address ────────────┼──────> { city }
└─────────────────────┘
```

The nested objects are also different.

---

# 32. When to Use Shallow Copy

Shallow copying is usually enough when:

* You only need to change top-level properties.
* You are updating React state at one level.
* You are combining objects.
* You are adding or removing array items.
* Nested objects do not need independent modification.

Example:

```javascript
const updatedUser = {
  ...user,
  age: 23
};
```

---

# 33. When to Use Deep Copy

Deep copying can be useful when:

* You need a completely independent nested data structure.
* You are working with complex nested objects.
* You need to modify nested values without affecting the original.

Example:

```javascript
const copy = structuredClone(original);
```

But deep cloning an entire object is not always necessary. Often, copying only the parts you need is clearer and more efficient.

---

# 34. Do Not Copy Everything Automatically

Suppose:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  address: {
    city: "Birgunj"
  }
};
```

If you only need to update `age`, this is enough:

```javascript
const updatedUser = {
  ...user,
  age: 23
};
```

You do not need:

```javascript
const updatedUser = structuredClone(user);
```

for every small update.

---

# 35. Important Reference Rule

Remember:

```javascript
const a = object;
```

means:

```text
same reference
```

While:

```javascript
const b = { ...object };
```

means:

```text
new top-level object
```

And:

```javascript
const c = structuredClone(object);
```

creates an independent cloned structure for supported values.

---

# 36. Common Mistakes

## Mistake 1: Assuming assignment copies an object

```javascript
const copy = original;
```

This does not create a new object.

---

## Mistake 2: Assuming spread is deep copy

```javascript
const copy = {
  ...original
};
```

This is only a shallow copy.

---

## Mistake 3: Forgetting nested references

```javascript
copy.address.city = "Kathmandu";
```

The original can also change if `copy.address` and `original.address` refer to the same object.

---

## Mistake 4: Using JSON cloning for every situation

```javascript
JSON.parse(JSON.stringify(object));
```

It has limitations and can change or lose values that JSON cannot represent.

---

# 37. Quick Comparison

### Same reference

```javascript
const copy = original;
```

### Shallow copy

```javascript
const copy = {
  ...original
};
```

### Shallow copy with `Object.assign()`

```javascript
const copy = Object.assign({}, original);
```

### Deep copy

```javascript
const copy = structuredClone(original);
```

---

# 38. Cheat Sheet

```javascript
// Same reference
const copy = original;

// Shallow object copy
const copy = { ...original };

// Shallow array copy
const copy = [...original];

// Object.assign shallow copy
const copy = Object.assign({}, original);

// Deep copy
const copy = structuredClone(original);
```

---

# 39. Key Takeaways

* Objects and arrays are reference-based values.
* Assignment copies the reference.
* Shallow copy creates a new top-level object or array.
* Spread creates a shallow copy.
* `Object.assign()` creates a shallow copy.
* Array spread creates a shallow copy.
* Nested objects remain shared in a shallow copy.
* Deep copy creates independent nested structures.
* `structuredClone()` is a modern built-in option for supported data.
* `JSON.parse(JSON.stringify())` has limitations.
* In React, spread is commonly used for immutable state updates.
* You do not always need a deep copy.
* Copy only the levels that need independent changes.

---

## Simple Rule to Remember

```text
Assignment
    ↓
Same reference

Spread
    ↓
New top-level object/array
    ↓
Nested data may still be shared

structuredClone()
    ↓
Independent nested structure
```

---
