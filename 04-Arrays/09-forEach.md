# JavaScript `forEach()` Method

The `forEach()` method is used to **execute a function once for each element in an array**.

It is mainly used when you want to perform an **action or side effect** for every array element.

---

# 1. What is `forEach()`?

`forEach()` loops through an array and executes a callback function for every element.

### Example

```javascript
const numbers = [10, 20, 30];

numbers.forEach((number) => {
    console.log(number);
});
```

Output:

```text
10
20
30
```

The callback runs once for each element.

---

# 2. Syntax

```javascript
array.forEach((element, index, array) => {
    // code
});
```

The callback can receive three parameters:

| Parameter | Description           |
| --------- | --------------------- |
| `element` | Current array element |
| `index`   | Current element index |
| `array`   | Original array        |

You usually only need the `element`.

---

# 3. Basic Example

```javascript
const fruits = ["Apple", "Banana", "Orange"];

fruits.forEach((fruit) => {
    console.log(fruit);
});
```

Output:

```text
Apple
Banana
Orange
```

---

# 4. `forEach()` with Index

```javascript
const fruits = ["Apple", "Banana", "Orange"];

fruits.forEach((fruit, index) => {
    console.log(index, fruit);
});
```

Output:

```text
0 Apple
1 Banana
2 Orange
```

The index starts from `0`.

---

# 5. `forEach()` with All Parameters

```javascript
const numbers = [10, 20, 30];

numbers.forEach((number, index, array) => {
    console.log("Value:", number);
    console.log("Index:", index);
    console.log("Array:", array);
});
```

The callback receives:

```text
element
index
array
```

---

# 6. Using a Regular Function

You can use a normal function:

```javascript
const numbers = [1, 2, 3];

numbers.forEach(function (number) {
    console.log(number);
});
```

---

# 7. Using an Arrow Function

A shorter version:

```javascript
const numbers = [1, 2, 3];

numbers.forEach(number => {
    console.log(number);
});
```

Both approaches work.

---

# 8. `forEach()` with Objects

Consider:

```javascript
const users = [
    { name: "Ram", age: 20 },
    { name: "Shyam", age: 22 },
    { name: "Hari", age: 21 }
];
```

You can access every object:

```javascript
users.forEach(user => {
    console.log(user.name);
});
```

Output:

```text
Ram
Shyam
Hari
```

---

# 9. Display Object Properties

```javascript
const products = [
    { name: "Laptop", price: 80000 },
    { name: "Mouse", price: 1500 },
    { name: "Keyboard", price: 3000 }
];

products.forEach(product => {
    console.log(`${product.name}: Rs. ${product.price}`);
});
```

Output:

```text
Laptop: Rs. 80000
Mouse: Rs. 1500
Keyboard: Rs. 3000
```

---

# 10. `forEach()` for Calculations

You can use an external variable to calculate a result:

```javascript
const numbers = [10, 20, 30];

let total = 0;

numbers.forEach(number => {
    total += number;
});

console.log(total);
```

Output:

```text
60
```

However, when the main goal is to produce an accumulated value, `reduce()` is usually more expressive:

```javascript
const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);
```

---

# 11. `forEach()` for Side Effects

A **side effect** means an operation that affects something outside the callback's local calculation.

Examples:

* Logging
* Updating the DOM
* Updating an external variable
* Sending data
* Updating application state
* Calling another function

Example:

```javascript
const users = ["Ram", "Shyam", "Hari"];

users.forEach(user => {
    console.log(`Welcome ${user}`);
});
```

---

# 12. Updating the DOM

Suppose HTML contains:

```html
<ul id="userList"></ul>
```

JavaScript:

```javascript
const users = ["Ram", "Shyam", "Hari"];

const userList = document.getElementById("userList");

users.forEach(user => {
    const li = document.createElement("li");

    li.textContent = user;

    userList.appendChild(li);
});
```

This creates:

```text
Ram
Shyam
Hari
```

inside the `<ul>`.

---

# 13. Hotel Food Example

Suppose:

```javascript
const foods = [
    { name: "Momo", price: 150 },
    { name: "Chowmein", price: 180 },
    { name: "Pizza", price: 500 }
];
```

Display each food:

```javascript
foods.forEach(food => {
    console.log(`${food.name} - Rs. ${food.price}`);
});
```

Output:

```text
Momo - Rs. 150
Chowmein - Rs. 180
Pizza - Rs. 500
```

---

# 14. Order Items Example

```javascript
const orderItems = [
    { name: "Momo", quantity: 2 },
    { name: "Coke", quantity: 1 },
    { name: "Pizza", quantity: 1 }
];

orderItems.forEach(item => {
    console.log(
        `${item.name} × ${item.quantity}`
    );
});
```

Output:

```text
Momo × 2
Coke × 1
Pizza × 1
```

---

# 15. Modifying Array Elements

You can modify an array element through its index.

```javascript
const numbers = [1, 2, 3];

numbers.forEach((number, index) => {
    numbers[index] = number * 2;
});

console.log(numbers);
```

Output:

```javascript
[2, 4, 6]
```

However, for creating a transformed array, `map()` is normally clearer:

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
```

---

# 16. Important: `forEach()` Returns `undefined`

Consider:

```javascript
const numbers = [1, 2, 3];

const result = numbers.forEach(number => {
    return number * 2;
});

console.log(result);
```

Output:

```text
undefined
```

The `return` inside the callback does **not** make `forEach()` return an array.

If you want a new array:

```javascript
const result = numbers.map(number => {
    return number * 2;
});

console.log(result);
```

Output:

```javascript
[2, 4, 6]
```

---

# 17. `forEach()` vs `map()`

### `forEach()`

Use it when you want to perform an action:

```javascript
const numbers = [1, 2, 3];

numbers.forEach(number => {
    console.log(number);
});
```

### `map()`

Use it when you want a new transformed array:

```javascript
const doubled = numbers.map(number => {
    return number * 2;
});
```

### Main Difference

```text
forEach()
    ↓
perform an action
    ↓
returns undefined

map()
    ↓
transform elements
    ↓
returns a new array
```

---

# 18. `forEach()` vs `filter()`

`filter()` selects elements and returns a new array:

```javascript
const numbers = [1, 2, 3, 4];

const evenNumbers = numbers.filter(number => {
    return number % 2 === 0;
});

console.log(evenNumbers);
```

Output:

```javascript
[2, 4]
```

`forEach()` does not create the filtered array automatically.

---

# 19. `forEach()` vs `reduce()`

Use `forEach()` for side effects:

```javascript
const numbers = [10, 20, 30];

numbers.forEach(number => {
    console.log(number);
});
```

Use `reduce()` for accumulation:

```javascript
const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);
```

### Simple Rule

```text
Need to perform an action?
→ forEach()

Need one accumulated result?
→ reduce()
```

---

# 20. `forEach()` vs `for...of`

You can also iterate using `for...of`:

```javascript
const numbers = [10, 20, 30];

for (const number of numbers) {
    console.log(number);
}
```

This can be preferable when you need:

* `break`
* `continue`
* `await` in sequential async operations

Example:

```javascript
for (const number of numbers) {
    if (number === 20) {
        break;
    }

    console.log(number);
}
```

Output:

```text
10
```

---

# 21. Cannot Use `break` with `forEach()`

This is invalid:

```javascript
numbers.forEach(number => {
    if (number === 20) {
        break;
    }
});
```

You cannot directly use `break` to stop a `forEach()` loop.

If you need to stop iteration, use:

```javascript
for...of
```

or an appropriate array method such as:

```javascript
find()
some()
every()
```

depending on your goal.

---

# 22. `continue` and `forEach()`

You also cannot use `continue` directly inside a `forEach()` callback.

Instead, you can use `return` to skip the current callback execution:

```javascript
const numbers = [1, 2, 3, 4];

numbers.forEach(number => {
    if (number === 2) {
        return;
    }

    console.log(number);
});
```

Output:

```text
1
3
4
```

Here, `return` exits only the current callback invocation.

It does not stop the entire `forEach()`.

---

# 23. Empty Arrays

If the array is empty:

```javascript
const numbers = [];

numbers.forEach(number => {
    console.log(number);
});
```

Nothing happens.

It does not throw an error.

---

# 24. Sparse Arrays

Consider:

```javascript
const numbers = [];

numbers[0] = 10;
numbers[2] = 30;

numbers.forEach(number => {
    console.log(number);
});
```

Output:

```text
10
30
```

The empty slot at index `1` is skipped.

---

# 25. `forEach()` and Array Mutation

You can modify the original array:

```javascript
const numbers = [1, 2, 3];

numbers.forEach((number, index) => {
    numbers[index] = number * 2;
});

console.log(numbers);
```

Output:

```javascript
[2, 4, 6]
```

However, modifying the array while iterating can make code difficult to understand.

### Best Practice

Avoid changing the structure of the array while `forEach()` is running.

---

# 26. `forEach()` and Object Mutation

Suppose:

```javascript
const users = [
    { name: "Ram", active: false },
    { name: "Shyam", active: false }
];
```

You can modify object properties:

```javascript
users.forEach(user => {
    user.active = true;
});

console.log(users);
```

Result:

```javascript
[
    { name: "Ram", active: true },
    { name: "Shyam", active: true }
]
```

Remember that objects are reference values, so modifying the object modifies the referenced object.

---

# 27. Nested `forEach()`

You can use one `forEach()` inside another.

```javascript
const categories = [
    {
        name: "Food",
        items: ["Momo", "Pizza"]
    },
    {
        name: "Drinks",
        items: ["Coke", "Juice"]
    }
];

categories.forEach(category => {
    console.log(category.name);

    category.items.forEach(item => {
        console.log("-", item);
    });
});
```

Output:

```text
Food
- Momo
- Pizza
Drinks
- Coke
- Juice
```

Nested loops should be kept readable and not unnecessarily deep.

---

# 28. `forEach()` with Function Calls

You can call another function for each element:

```javascript
function greetUser(name) {
    console.log(`Hello ${name}`);
}

const users = ["Ram", "Shyam", "Hari"];

users.forEach(greetUser);
```

Output:

```text
Hello Ram
Hello Shyam
Hello Hari
```

This passes the function itself as a callback.

---

# 29. `forEach()` and Callbacks

`forEach()` uses a callback function:

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

The callback is called once for each element.

Conceptually:

```text
Array
  ↓
forEach()
  ↓
callback(element 1)
  ↓
callback(element 2)
  ↓
callback(element 3)
```

---

# 30. `forEach()` with Asynchronous Code

A common mistake is assuming `forEach()` waits for asynchronous callbacks.

For example:

```javascript
const users = [1, 2, 3];

users.forEach(async user => {
    await fetchUser(user);

    console.log(user);
});

console.log("Done");
```

`forEach()` does not wait for those promises.

So this pattern should not be used when you need sequential asynchronous processing.

---

# 31. Sequential Async Processing

If each asynchronous operation must finish before the next starts, use:

```javascript
for (const user of users) {
    await fetchUser(user);
}
```

This is often clearer for sequential async work.

---

# 32. Parallel Async Processing

If the operations are independent, use:

```javascript
const results = await Promise.all(
    users.map(user => fetchUser(user))
);
```

This starts the operations without waiting for each one sequentially.

---

# 33. React Example

In React, `map()` is commonly used to create a list of JSX elements:

```jsx
const users = ["Ram", "Shyam", "Hari"];

return (
    <ul>
        {users.map(user => (
            <li key={user}>{user}</li>
        ))}
    </ul>
);
```

Do not use `forEach()` directly for producing JSX:

```jsx
{
    users.forEach(user => (
        <li>{user}</li>
    ))
}
```

`forEach()` returns `undefined`, so it does not produce the array React needs for rendering.

---

# 34. Real-World Example: Logging Orders

```javascript
const orders = [
    { id: 101, status: "pending" },
    { id: 102, status: "confirmed" },
    { id: 103, status: "ready" }
];

orders.forEach(order => {
    console.log(
        `Order #${order.id}: ${order.status}`
    );
});
```

Output:

```text
Order #101: pending
Order #102: confirmed
Order #103: ready
```

---

# 35. Real-World Example: Updating Status

```javascript
const tables = [
    { number: 1, status: "available" },
    { number: 2, status: "available" },
    { number: 3, status: "available" }
];

tables.forEach(table => {
    if (table.number === 2) {
        table.status = "occupied";
    }
});

console.log(tables);
```

Result:

```javascript
[
    { number: 1, status: "available" },
    { number: 2, status: "occupied" },
    { number: 3, status: "available" }
]
```

---

# 36. Common Mistakes

## Mistake 1: Expecting a returned array

Wrong:

```javascript
const result = numbers.forEach(number => {
    return number * 2;
});
```

`result` is:

```text
undefined
```

Use `map()` instead.

---

## Mistake 2: Trying to use `break`

Wrong:

```javascript
numbers.forEach(number => {
    if (number > 10) {
        break;
    }
});
```

Use `for...of` if you need `break`.

---

## Mistake 3: Expecting `async/await` to work sequentially

Wrong:

```javascript
items.forEach(async item => {
    await processItem(item);
});
```

Use `for...of` for sequential processing or `Promise.all()` for independent parallel processing.

---

## Mistake 4: Using `forEach()` when another method is clearer

For example, instead of:

```javascript
let result = [];

numbers.forEach(number => {
    if (number > 10) {
        result.push(number);
    }
});
```

Use:

```javascript
const result = numbers.filter(number => number > 10);
```

---

# 37. Best Practices

### Use `forEach()` when:

* You need to perform an action for every element.
* You need logging.
* You need to update the DOM.
* You need to call another function for each element.
* You do not need a returned array.

### Avoid `forEach()` when:

* You need a transformed array → use `map()`.
* You need a filtered array → use `filter()`.
* You need one accumulated value → use `reduce()`.
* You need to find one element → use `find()`.
* You need to stop early → use `for...of`, `find()`, `some()`, or `every()`.
* You need sequential `await` operations → use `for...of`.

---

# 38. Quick Comparison

| Method        | Purpose              | Return      |
| ------------- | -------------------- | ----------- |
| `forEach()`   | Perform action       | `undefined` |
| `map()`       | Transform            | New array   |
| `filter()`    | Select               | New array   |
| `find()`      | Find first match     | Element     |
| `findIndex()` | Find index           | Number      |
| `some()`      | At least one matches | Boolean     |
| `every()`     | All match            | Boolean     |
| `reduce()`    | Accumulate           | Any value   |

---

# 39. Quick Revision

```javascript
const numbers = [10, 20, 30];

numbers.forEach((number, index) => {
    console.log(index, number);
});
```

Output:

```text
0 10
1 20
2 30
```

Remember:

```text
forEach()
   ↓
visit every element
   ↓
execute callback
   ↓
perform an action
```

---

# 40. Cheat Sheet

### Basic

```javascript
array.forEach(item => {
    console.log(item);
});
```

### With index

```javascript
array.forEach((item, index) => {
    console.log(index, item);
});
```

### With all parameters

```javascript
array.forEach((item, index, array) => {
    console.log(item, index, array);
});
```

### Function reference

```javascript
function printItem(item) {
    console.log(item);
}

array.forEach(printItem);
```

### DOM example

```javascript
items.forEach(item => {
    const element = document.createElement("li");
    element.textContent = item;
    list.appendChild(element);
});
```

---

# 41. Key Takeaways

* `forEach()` executes a callback for each array element.
* It is mainly used for side effects.
* It receives `element`, `index`, and `array`.
* `forEach()` returns `undefined`.
* `forEach()` cannot be stopped with `break`.
* `return` only exits the current callback execution.
* Use `map()` when you need a new transformed array.
* Use `filter()` when you need selected elements.
* Use `reduce()` when you need one accumulated result.
* Use `for...of` when you need `break`, `continue`, or sequential `await`.
* `forEach()` does not wait for asynchronous callbacks.
* It is useful for DOM manipulation, logging, updating objects, and calling functions.
* Avoid unnecessary mutation while iterating.

---
