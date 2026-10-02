# JavaScript Array — Adding and Removing Elements

JavaScript provides several methods for **adding, removing, and replacing elements** in arrays.

The most important methods are:

| Method      | Purpose                 | Changes Original Array? |
| ----------- | ----------------------- | ----------------------- |
| `push()`    | Add to end              | Yes                     |
| `pop()`     | Remove from end         | Yes                     |
| `unshift()` | Add to beginning        | Yes                     |
| `shift()`   | Remove from beginning   | Yes                     |
| `splice()`  | Add, remove, or replace | Yes                     |
| `slice()`   | Copy/extract part       | No                      |

---

# 1. `push()`

The `push()` method adds one or more elements to the **end** of an array.

### Syntax

```javascript
array.push(element);
```

Example:

```javascript
const fruits = ["Apple", "Banana"];

fruits.push("Mango");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

---

# 2. Adding Multiple Elements with `push()`

You can add multiple elements at once.

```javascript
const fruits = ["Apple"];

fruits.push("Banana", "Mango", "Orange");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango", "Orange"]
```

---

# 3. `push()` Returns the New Length

`push()` does not return the modified array.

It returns the **new length**.

```javascript
const fruits = ["Apple", "Banana"];

const length = fruits.push("Mango");

console.log(length);
```

Output:

```text
3
```

The array becomes:

```javascript
console.log(fruits);
```

```text
["Apple", "Banana", "Mango"]
```

---

# 4. Practical Example with `push()`

Adding a new user:

```javascript
const users = [
    "Sandip",
    "Ram"
];

users.push("Sita");

console.log(users);
```

Output:

```text
["Sandip", "Ram", "Sita"]
```

Adding a new order:

```javascript
const orders = [];

orders.push({
    item: "Pizza",
    quantity: 2
});

console.log(orders);
```

---

# 5. `pop()`

The `pop()` method removes the **last element** from an array.

### Syntax

```javascript
array.pop();
```

Example:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits.pop();

console.log(fruits);
```

Output:

```text
["Apple", "Banana"]
```

---

# 6. `pop()` Returns the Removed Element

```javascript
const fruits = ["Apple", "Banana", "Mango"];

const removed = fruits.pop();

console.log(removed);
```

Output:

```text
Mango
```

The array is now:

```text
["Apple", "Banana"]
```

This is useful when you need to know what was removed.

---

# 7. `push()` and `pop()` Together

These methods work with the **end** of an array.

```javascript
const numbers = [10, 20];

numbers.push(30);

console.log(numbers);
```

```text
[10, 20, 30]
```

Then:

```javascript
const removed = numbers.pop();

console.log(removed);
```

```text
30
```

Final array:

```text
[10, 20]
```

---

# 8. `unshift()`

The `unshift()` method adds one or more elements to the **beginning** of an array.

### Syntax

```javascript
array.unshift(element);
```

Example:

```javascript
const fruits = ["Banana", "Mango"];

fruits.unshift("Apple");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

---

# 9. Adding Multiple Elements with `unshift()`

```javascript
const numbers = [30, 40];

numbers.unshift(10, 20);

console.log(numbers);
```

Output:

```text
[10, 20, 30, 40]
```

The elements are inserted in the order supplied.

---

# 10. `unshift()` Returns the New Length

```javascript
const fruits = ["Banana", "Mango"];

const length = fruits.unshift("Apple");

console.log(length);
```

Output:

```text
3
```

---

# 11. `shift()`

The `shift()` method removes the **first element** from an array.

### Syntax

```javascript
array.shift();
```

Example:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits.shift();

console.log(fruits);
```

Output:

```text
["Banana", "Mango"]
```

---

# 12. `shift()` Returns the Removed Element

```javascript
const fruits = ["Apple", "Banana", "Mango"];

const removed = fruits.shift();

console.log(removed);
```

Output:

```text
Apple
```

The array becomes:

```text
["Banana", "Mango"]
```

---

# 13. `unshift()` and `shift()` Together

These methods work with the **beginning** of an array.

```javascript
const numbers = [20, 30];

numbers.unshift(10);

console.log(numbers);
```

Output:

```text
[10, 20, 30]
```

Then:

```javascript
const removed = numbers.shift();

console.log(removed);
```

Output:

```text
10
```

Final array:

```text
[20, 30]
```

---

# 14. Array Method Comparison

```text
                 Beginning          End
                    │                │
                    ▼                ▼

Add             unshift()        push()
Remove          shift()          pop()
```

Remember:

```text
push()     → add at end
pop()      → remove from end

unshift()  → add at beginning
shift()    → remove from beginning
```

---

# 15. `splice()`

`splice()` is one of the most powerful array methods.

It can:

* Add elements
* Remove elements
* Replace elements

### Syntax

```javascript
array.splice(start, deleteCount, item1, item2, ...);
```

---

# 16. Removing with `splice()`

Example:

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];

fruits.splice(1, 1);

console.log(fruits);
```

Output:

```text
["Apple", "Mango", "Orange"]
```

Explanation:

```text
start = 1
deleteCount = 1
```

Index `1` contains `"Banana"`.

So `"Banana"` is removed.

---

# 17. Removing Multiple Elements

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];

fruits.splice(1, 2);

console.log(fruits);
```

Output:

```text
["Apple", "Orange"]
```

Explanation:

```text
start = 1
deleteCount = 2
```

Starting from index `1`:

```text
Banana
Mango
```

are removed.

---

# 18. `splice()` Returns Removed Elements

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango"
];

const removed = fruits.splice(1, 1);

console.log(removed);
```

Output:

```text
["Banana"]
```

Notice that `splice()` returns an **array** containing the removed elements.

---

# 19. Adding Elements with `splice()`

You can add elements without removing anything.

```javascript
const fruits = [
    "Apple",
    "Mango"
];

fruits.splice(1, 0, "Banana");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

Explanation:

```text
start = 1
deleteCount = 0
item = "Banana"
```

Nothing is deleted.

`"Banana"` is inserted at index `1`.

---

# 20. Adding Multiple Elements with `splice()`

```javascript
const fruits = [
    "Apple",
    "Orange"
];

fruits.splice(1, 0, "Banana", "Mango");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango", "Orange"]
```

---

# 21. Replacing Elements with `splice()`

`splice()` can remove and add elements at the same position.

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango"
];

fruits.splice(1, 1, "Orange");

console.log(fruits);
```

Output:

```text
["Apple", "Orange", "Mango"]
```

Explanation:

```text
Remove:
Banana

Add:
Orange
```

---

# 22. Replacing Multiple Elements

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];

fruits.splice(1, 2, "Grapes", "Pineapple");

console.log(fruits);
```

Output:

```text
["Apple", "Grapes", "Pineapple", "Orange"]
```

Two elements were removed:

```text
Banana
Mango
```

Two new elements were inserted:

```text
Grapes
Pineapple
```

---

# 23. `splice()` with Only Start Index

If `deleteCount` is omitted, `splice()` removes everything from the start index to the end.

```javascript
const numbers = [10, 20, 30, 40, 50];

numbers.splice(2);

console.log(numbers);
```

Output:

```text
[10, 20]
```

Everything from index `2` was removed.

---

# 24. Negative Index with `splice()`

`splice()` supports negative start indexes.

```javascript
const numbers = [10, 20, 30, 40];

numbers.splice(-2, 1);

console.log(numbers);
```

Output:

```text
[10, 20, 40]
```

`-2` refers to the second-last position.

---

# 25. `slice()` vs `splice()`

These two methods are often confused.

### `slice()`

* Does not modify the original array.
* Creates a new array.

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.slice(1, 3);

console.log(result);
```

Output:

```text
[20, 30]
```

Original:

```text
[10, 20, 30, 40]
```

---

### `splice()`

* Modifies the original array.
* Can add/remove/replace elements.

```javascript
const numbers = [10, 20, 30, 40];

numbers.splice(1, 2);

console.log(numbers);
```

Output:

```text
[10, 40]
```

---

# 26. `slice()` vs `splice()` Summary

| Feature           | `slice()`             | `splice()`       |
| ----------------- | --------------------- | ---------------- |
| Modifies original | No                    | Yes              |
| Returns           | New array             | Removed elements |
| Remove elements   | Creates selected copy | Yes              |
| Add elements      | No                    | Yes              |
| Replace elements  | No                    | Yes              |
| Good for copying  | Yes                   | No               |

---

# 27. Practical Example: Shopping Cart

Suppose we have:

```javascript
const cart = [
    "Laptop",
    "Mouse",
    "Keyboard"
];
```

Add a product:

```javascript
cart.push("Monitor");
```

Remove the last product:

```javascript
cart.pop();
```

Add a product at the beginning:

```javascript
cart.unshift("Laptop Bag");
```

Remove the first product:

```javascript
cart.shift();
```

Remove a specific product:

```javascript
cart.splice(1, 1);
```

---

# 28. Practical Example: Hotel Orders

Suppose:

```javascript
const orders = [
    {
        id: 1,
        item: "Pizza"
    },
    {
        id: 2,
        item: "Burger"
    },
    {
        id: 3,
        item: "Momo"
    }
];
```

Remove order with index `1`:

```javascript
orders.splice(1, 1);

console.log(orders);
```

Result:

```text
[
    {
        id: 1,
        item: "Pizza"
    },
    {
        id: 3,
        item: "Momo"
    }
]
```

---

# 29. Removing an Object by Condition

`splice()` works with indexes, so first find the index.

```javascript
const orders = [
    { id: 1, item: "Pizza" },
    { id: 2, item: "Burger" },
    { id: 3, item: "Momo" }
];

const index = orders.findIndex(order => order.id === 2);

if (index !== -1) {
    orders.splice(index, 1);
}

console.log(orders);
```

Result:

```text
[
    { id: 1, item: "Pizza" },
    { id: 3, item: "Momo" }
]
```

This pattern is very common when working with arrays of objects.

---

# 30. Queue Example

A queue follows:

```text
FIFO
First In, First Out
```

Example:

```javascript
const queue = [];

queue.push("Customer 1");
queue.push("Customer 2");
queue.push("Customer 3");

console.log(queue);
```

Remove the first customer:

```javascript
const customer = queue.shift();

console.log(customer);
```

Output:

```text
Customer 1
```

The queue now contains:

```text
["Customer 2", "Customer 3"]
```

---

# 31. Stack Example

A stack follows:

```text
LIFO
Last In, First Out
```

Example:

```javascript
const stack = [];

stack.push("Page 1");
stack.push("Page 2");
stack.push("Page 3");
```

Remove the last item:

```javascript
const page = stack.pop();

console.log(page);
```

Output:

```text
Page 3
```

The stack now contains:

```text
["Page 1", "Page 2"]
```

---

# 32. Return Values

Understanding return values is important.

### `push()`

Returns the new array length.

```javascript
const numbers = [1, 2];

console.log(numbers.push(3));
```

Output:

```text
3
```

### `pop()`

Returns the removed element.

```javascript
console.log(numbers.pop());
```

Output:

```text
3
```

### `unshift()`

Returns the new array length.

```javascript
const numbers = [2, 3];

console.log(numbers.unshift(1));
```

Output:

```text
3
```

### `shift()`

Returns the removed element.

```javascript
console.log(numbers.shift());
```

Output:

```text
1
```

### `splice()`

Returns an array containing removed elements.

```javascript
const numbers = [10, 20, 30];

console.log(numbers.splice(1, 1));
```

Output:

```text
[20]
```

---

# 33. Empty Array Behavior

### `pop()` on an empty array

```javascript
const items = [];

console.log(items.pop());
```

Output:

```text
undefined
```

### `shift()` on an empty array

```javascript
console.log(items.shift());
```

Output:

```text
undefined
```

### `splice()` on an empty array

```javascript
console.log(items.splice(0, 1));
```

Output:

```text
[]
```

---

# 34. Common Mistakes

## Mistake 1: Confusing `pop()` and `shift()`

Remember:

```text
pop()   → removes from END
shift() → removes from BEGINNING
```

---

## Mistake 2: Confusing `push()` and `unshift()`

Remember:

```text
push()    → adds to END
unshift() → adds to BEGINNING
```

---

## Mistake 3: Forgetting that `splice()` mutates

```javascript
const numbers = [1, 2, 3];

numbers.splice(1, 1);

console.log(numbers);
```

The original array has changed.

---

## Mistake 4: Confusing `splice()` and `slice()`

Remember:

```text
slice()  → does NOT modify original
splice() → modifies original
```

A simple memory trick:

```text
SPlice → changes the array
SLice  → creates a selection
```

---

## Mistake 5: Using the wrong `splice()` parameters

```javascript
array.splice(start, deleteCount);
```

For example:

```javascript
numbers.splice(2, 1);
```

means:

```text
Start at index 2
Remove 1 element
```

It does not mean "remove element number 2."

---

# 35. Best Practices

### Use `push()` for normal additions at the end

```javascript
items.push(newItem);
```

### Use `pop()` when removing from the end

```javascript
const removed = items.pop();
```

### Use `unshift()` carefully

Adding repeatedly at the beginning can be less efficient for large arrays because existing indexes may need to be shifted.

### Use `shift()` carefully for large queues

For very large queue workloads, repeatedly using `shift()` can be less efficient than maintaining an index or using another queue data structure.

### Use `splice()` when you intentionally want to mutate an array

If immutability is preferred, create a new array instead.

---

# 36. Immutable Alternatives

Instead of:

```javascript
const numbers = [10, 20, 30];

numbers.push(40);
```

You can create a new array:

```javascript
const numbers = [10, 20, 30];

const updatedNumbers = [...numbers, 40];
```

Instead of removing with `splice()`:

```javascript
const numbers = [10, 20, 30];

const updatedNumbers = numbers.filter(number => number !== 20);
```

This creates a new array rather than modifying the original.

This style is especially common in **React state management**.

---

# 37. Quick Revision

```text
ADD
│
├── push()       → end
└── unshift()    → beginning

REMOVE
│
├── pop()        → end
└── shift()      → beginning

MODIFY
│
└── splice()     → add/remove/replace

COPY / EXTRACT
│
└── slice()      → does not modify original
```

---

# 38. Method Examples

```javascript
const fruits = ["Apple", "Banana"];
```

### Add to end

```javascript
fruits.push("Mango");
```

### Remove from end

```javascript
fruits.pop();
```

### Add to beginning

```javascript
fruits.unshift("Orange");
```

### Remove from beginning

```javascript
fruits.shift();
```

### Insert

```javascript
fruits.splice(1, 0, "Mango");
```

### Remove

```javascript
fruits.splice(1, 1);
```

### Replace

```javascript
fruits.splice(1, 1, "Grapes");
```

### Copy/extract

```javascript
const copy = fruits.slice();
```

---

# 39. Key Takeaways

* `push()` adds elements to the end.
* `pop()` removes the last element.
* `unshift()` adds elements to the beginning.
* `shift()` removes the first element.
* `splice()` can add, remove, and replace elements.
* `slice()` creates a new array without modifying the original.
* `push()` and `unshift()` return the new array length.
* `pop()` and `shift()` return the removed element.
* `splice()` returns an array containing removed elements.
* These methods mutate the original array except `slice()`.
* `push()` + `shift()` can be used for a basic queue.
* `push()` + `pop()` can be used for a basic stack.
* `splice()` is useful when you know the index.
* For immutable code, spread, `filter()`, and other non-mutating approaches can create new arrays.

---
