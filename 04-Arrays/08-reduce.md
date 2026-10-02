# JavaScript `reduce()` Method

The `reduce()` method is one of the most powerful and commonly used array methods in JavaScript.

It is used to **process all elements of an array and combine them into a single final value**.

The final value can be:

* Number
* String
* Boolean
* Object
* Array
* Any other JavaScript value

---

## 1. What is `reduce()`?

`reduce()` executes a callback function for each element of an array and keeps an **accumulator** that stores the result.

### Simple Example

```javascript
const numbers = [1, 2, 3, 4];

const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);

console.log(total);
```

Output:

```text
10
```

### How it works

```text
Initial accumulator = 0

0 + 1 = 1
1 + 2 = 3
3 + 3 = 6
6 + 4 = 10
```

Final result:

```text
10
```

---

# 2. Syntax

```javascript
array.reduce((accumulator, currentValue, currentIndex, array) => {
    // logic
}, initialValue);
```

There are four callback parameters:

| Parameter      | Description                                   |
| -------------- | --------------------------------------------- |
| `accumulator`  | Stores the result from the previous iteration |
| `currentValue` | Current array element                         |
| `currentIndex` | Current element index                         |
| `array`        | Original array                                |
| `initialValue` | Starting value of accumulator                 |

Usually, you only need:

```javascript
accumulator
currentValue
```

---

# 3. Basic Example

```javascript
const numbers = [10, 20, 30];

const result = numbers.reduce((acc, current) => {
    return acc + current;
}, 0);

console.log(result);
```

Output:

```text
60
```

---

# 4. Understanding the Accumulator

The accumulator remembers the result from the previous iteration.

```javascript
const numbers = [5, 10, 15];

const result = numbers.reduce((acc, current) => {
    console.log("Accumulator:", acc);
    console.log("Current:", current);

    return acc + current;
}, 0);
```

Conceptually:

```text
acc = 0, current = 5  → 5
acc = 5, current = 10 → 15
acc = 15, current = 15 → 30
```

Final result:

```text
30
```

---

# 5. `initialValue`

The second argument of `reduce()` is the initial value.

```javascript
const numbers = [1, 2, 3];

const result = numbers.reduce((acc, current) => {
    return acc + current;
}, 0);
```

Here:

```javascript
0
```

is the initial accumulator value.

For addition, use:

```javascript
0
```

For multiplication:

```javascript
1
```

For an object:

```javascript
{}
```

For an array:

```javascript
[]
```

---

# 6. Why `initialValue` Is Important

Consider:

```javascript
const numbers = [1, 2, 3];

const result = numbers.reduce((acc, current) => {
    return acc + current;
});
```

JavaScript uses the first array element as the initial accumulator.

Conceptually:

```text
acc = 1
current = 2

acc = 3
current = 3

acc = 6
```

This works for a non-empty array.

However, if the array is empty:

```javascript
const numbers = [];

const result = numbers.reduce((acc, current) => {
    return acc + current;
});
```

JavaScript throws:

```text
TypeError
```

Using an initial value is generally safer:

```javascript
const result = numbers.reduce((acc, current) => {
    return acc + current;
}, 0);
```

Now an empty array produces:

```text
0
```

### Best Practice

Prefer providing an explicit `initialValue`.

---

# 7. Sum of Numbers

One of the most common uses of `reduce()` is calculating a total.

```javascript
const prices = [100, 200, 300];

const total = prices.reduce((sum, price) => {
    return sum + price;
}, 0);

console.log(total);
```

Output:

```text
600
```

### Short Version

```javascript
const total = prices.reduce((sum, price) => sum + price, 0);
```

---

# 8. Product of Numbers

```javascript
const numbers = [2, 3, 4];

const product = numbers.reduce((result, number) => {
    return result * number;
}, 1);

console.log(product);
```

Output:

```text
24
```

Calculation:

```text
1 × 2 = 2
2 × 3 = 6
6 × 4 = 24
```

---

# 9. Find Maximum Value

```javascript
const numbers = [10, 45, 23, 89, 12];

const maximum = numbers.reduce((max, number) => {
    return number > max ? number : max;
}, numbers[0]);

console.log(maximum);
```

Output:

```text
89
```

For simple numeric arrays, `Math.max()` with spread can also be clearer:

```javascript
const maximum = Math.max(...numbers);
```

---

# 10. Find Minimum Value

```javascript
const numbers = [10, 45, 23, 89, 12];

const minimum = numbers.reduce((min, number) => {
    return number < min ? number : min;
}, numbers[0]);

console.log(minimum);
```

Output:

```text
10
```

---

# 11. Calculate Average

```javascript
const marks = [70, 80, 90, 60];

const total = marks.reduce((sum, mark) => {
    return sum + mark;
}, 0);

const average = total / marks.length;

console.log(average);
```

Output:

```text
75
```

You can also do it directly:

```javascript
const average = marks.reduce((sum, mark) => {
    return sum + mark;
}, 0) / marks.length;
```

Be careful with an empty array because:

```javascript
0 / 0
```

produces:

```text
NaN
```

---

# 12. Count Values

Suppose we have:

```javascript
const numbers = [1, 2, 1, 3, 2, 1];
```

We can count how many times each number appears.

```javascript
const frequency = numbers.reduce((count, number) => {
    count[number] = (count[number] || 0) + 1;

    return count;
}, {});

console.log(frequency);
```

Output:

```javascript
{
    1: 3,
    2: 2,
    3: 1
}
```

---

# 13. Frequency of Strings

```javascript
const fruits = [
    "apple",
    "banana",
    "apple",
    "orange",
    "banana",
    "apple"
];

const frequency = fruits.reduce((count, fruit) => {
    count[fruit] = (count[fruit] || 0) + 1;

    return count;
}, {});

console.log(frequency);
```

Result:

```javascript
{
    apple: 3,
    banana: 2,
    orange: 1
}
```

---

# 14. Convert Array into Object

Suppose:

```javascript
const users = [
    { id: 1, name: "Ram" },
    { id: 2, name: "Shyam" },
    { id: 3, name: "Hari" }
];
```

We can create an object indexed by ID:

```javascript
const userMap = users.reduce((result, user) => {
    result[user.id] = user;

    return result;
}, {});

console.log(userMap);
```

Result:

```javascript
{
    1: { id: 1, name: "Ram" },
    2: { id: 2, name: "Shyam" },
    3: { id: 3, name: "Hari" }
}
```

This can be useful when you frequently need to access objects by ID.

---

# 15. Group Objects by Category

Consider hotel food items:

```javascript
const foods = [
    { name: "Pizza", category: "Fast Food" },
    { name: "Burger", category: "Fast Food" },
    { name: "Momo", category: "Nepali" },
    { name: "Dal Bhat", category: "Nepali" }
];
```

We can group them by category:

```javascript
const groupedFoods = foods.reduce((groups, food) => {
    if (!groups[food.category]) {
        groups[food.category] = [];
    }

    groups[food.category].push(food);

    return groups;
}, {});

console.log(groupedFoods);
```

Result:

```javascript
{
    "Fast Food": [
        { name: "Pizza", category: "Fast Food" },
        { name: "Burger", category: "Fast Food" }
    ],
    "Nepali": [
        { name: "Momo", category: "Nepali" },
        { name: "Dal Bhat", category: "Nepali" }
    ]
}
```

---

# 16. Shopping Cart Total

This is a common real-world use of `reduce()`.

```javascript
const cart = [
    { name: "Laptop", price: 80000, quantity: 1 },
    { name: "Mouse", price: 1500, quantity: 2 },
    { name: "Keyboard", price: 3000, quantity: 1 }
];

const total = cart.reduce((sum, item) => {
    return sum + item.price * item.quantity;
}, 0);

console.log(total);
```

Calculation:

```text
Laptop   = 80000 × 1 = 80000
Mouse    = 1500  × 2 = 3000
Keyboard = 3000  × 1 = 3000

Total = 86000
```

Output:

```text
86000
```

---

# 17. Hotel Order Total

For a hotel ordering system:

```javascript
const orderItems = [
    { name: "Momo", price: 150, quantity: 2 },
    { name: "Chowmein", price: 180, quantity: 1 },
    { name: "Coke", price: 100, quantity: 2 }
];

const total = orderItems.reduce((total, item) => {
    return total + item.price * item.quantity;
}, 0);

console.log(total);
```

Output:

```text
680
```

---

# 18. Nested Arrays with `reduce()`

Suppose:

```javascript
const numbers = [
    [1, 2],
    [3, 4],
    [5, 6]
];
```

We can flatten it using `reduce()`:

```javascript
const flattened = numbers.reduce((result, current) => {
    return result.concat(current);
}, []);

console.log(flattened);
```

Output:

```javascript
[1, 2, 3, 4, 5, 6]
```

However, for normal array flattening, `flat()` is usually clearer:

```javascript
const flattened = numbers.flat();
```

---

# 19. Remove Duplicate Values

```javascript
const numbers = [1, 2, 2, 3, 4, 4, 5];

const unique = numbers.reduce((result, number) => {
    if (!result.includes(number)) {
        result.push(number);
    }

    return result;
}, []);

console.log(unique);
```

Output:

```javascript
[1, 2, 3, 4, 5]
```

For this specific task, `Set` is usually simpler:

```javascript
const unique = [...new Set(numbers)];
```

---

# 20. Build an Object Lookup

Consider:

```javascript
const products = [
    { id: "p1", name: "Laptop" },
    { id: "p2", name: "Mouse" },
    { id: "p3", name: "Keyboard" }
];
```

Create a lookup object:

```javascript
const productLookup = products.reduce((result, product) => {
    result[product.id] = product;

    return result;
}, {});
```

Now:

```javascript
console.log(productLookup.p2);
```

Output:

```javascript
{
    id: "p2",
    name: "Mouse"
}
```

---

# 21. Using `reduce()` with Objects

`reduce()` is not limited to producing numbers.

For example:

```javascript
const users = [
    { name: "Ram", role: "admin" },
    { name: "Shyam", role: "user" },
    { name: "Hari", role: "user" }
];

const usersByRole = users.reduce((result, user) => {
    if (!result[user.role]) {
        result[user.role] = [];
    }

    result[user.role].push(user);

    return result;
}, {});
```

Result:

```javascript
{
    admin: [
        { name: "Ram", role: "admin" }
    ],
    user: [
        { name: "Shyam", role: "user" },
        { name: "Hari", role: "user" }
    ]
}
```

---

# 22. Using `reduce()` with Strings

You can also build a string:

```javascript
const words = ["JavaScript", "is", "powerful"];

const sentence = words.reduce((result, word) => {
    return result + " " + word;
}, "");

console.log(sentence.trim());
```

Output:

```text
JavaScript is powerful
```

For simple string joining, however, `join()` is usually clearer:

```javascript
const sentence = words.join(" ");
```

---

# 23. `reduce()` with `map()`

You can combine array methods.

```javascript
const numbers = [1, 2, 3, 4];

const total = numbers
    .map(number => number * 2)
    .reduce((sum, number) => sum + number, 0);

console.log(total);
```

Process:

```text
[1, 2, 3, 4]

map()
↓
[2, 4, 6, 8]

reduce()
↓
20
```

---

# 24. `reduce()` with `filter()`

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const total = numbers
    .filter(number => number % 2 === 0)
    .reduce((sum, number) => sum + number, 0);

console.log(total);
```

Process:

```text
Original:
[1, 2, 3, 4, 5, 6]

filter():
[2, 4, 6]

reduce():
12
```

---

# 25. `reduce()` Callback Parameters

You can access all callback parameters:

```javascript
const numbers = [10, 20, 30];

numbers.reduce((accumulator, currentValue, currentIndex, array) => {
    console.log(accumulator);
    console.log(currentValue);
    console.log(currentIndex);
    console.log(array);

    return accumulator + currentValue;
}, 0);
```

Parameters:

```text
accumulator
currentValue
currentIndex
array
```

---

# 26. `reduce()` vs `map()`

### `map()`

Use `map()` when you want to transform **each element**.

```javascript
const numbers = [1, 2, 3];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
```

Result:

```javascript
[2, 4, 6]
```

### `reduce()`

Use `reduce()` when you want to combine elements into a final result.

```javascript
const numbers = [1, 2, 3];

const total = numbers.reduce((sum, number) => sum + number, 0);

console.log(total);
```

Result:

```text
6
```

---

# 27. `reduce()` vs `filter()`

### `filter()`

Selects elements:

```javascript
const numbers = [1, 2, 3, 4];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
```

Result:

```javascript
[2, 4]
```

### `reduce()`

Combines elements:

```javascript
const total = numbers.reduce((sum, number) => sum + number, 0);

console.log(total);
```

Result:

```text
10
```

---

# 28. `reduce()` vs `forEach()`

### `forEach()`

Used mainly for side effects:

```javascript
const numbers = [1, 2, 3];

numbers.forEach(number => {
    console.log(number);
});
```

`forEach()` does not return a new accumulated result.

### `reduce()`

Used to create a final result:

```javascript
const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);
```

---

# 29. `reduce()` vs `find()`

`find()` returns the first matching element:

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.find(number => number > 20);

console.log(result);
```

Output:

```text
30
```

`reduce()` processes the entire array to build one final result.

---

# 30. `reduce()` vs `some()` and `every()`

### `some()`

Checks whether **at least one** element satisfies a condition.

```javascript
const result = numbers.some(number => number > 30);
```

### `every()`

Checks whether **all** elements satisfy a condition.

```javascript
const result = numbers.every(number => number > 0);
```

### `reduce()`

Builds a final accumulated result.

```javascript
const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);
```

---

# 31. `reduceRight()`

JavaScript also provides:

```javascript
reduceRight()
```

It works like `reduce()`, but processes elements from **right to left**.

Example:

```javascript
const words = ["JavaScript", "is", "powerful"];

const result = words.reduceRight((text, word) => {
    return text + " " + word;
}, "");

console.log(result.trim());
```

Output:

```text
powerful is JavaScript
```

---

# 32. Async Operations with `reduce()`

`reduce()` itself does not automatically wait for asynchronous operations.

For example:

```javascript
const result = items.reduce(async (acc, item) => {
    // asynchronous operation
}, Promise.resolve([]));
```

Here the accumulator becomes a Promise.

If sequential async processing is actually required, you may explicitly await the previous accumulator:

```javascript
const result = await items.reduce(async (promise, item) => {
    const results = await promise;

    const value = await processItem(item);

    results.push(value);

    return results;
}, Promise.resolve([]));
```

However, if operations can safely run independently, `Promise.all()` is often clearer and faster:

```javascript
const results = await Promise.all(
    items.map(item => processItem(item))
);
```

### Important

Do not use `reduce()` for asynchronous code simply because it is possible.

Choose the approach that matches the required execution order.

---

# 33. Mutation with `reduce()`

Consider:

```javascript
const users = [
    { name: "Ram" },
    { name: "Shyam" }
];
```

This mutates the accumulator object:

```javascript
const result = users.reduce((acc, user) => {
    acc[user.name] = user;
    return acc;
}, {});
```

This is a common and valid pattern because the accumulator is a newly created object.

However, avoid unnecessarily mutating the original input objects:

```javascript
const result = users.reduce((acc, user) => {
    user.active = true;
    acc.push(user);
    return acc;
}, []);
```

Prefer creating a new object when transformation is needed:

```javascript
const result = users.reduce((acc, user) => {
    acc.push({
        ...user,
        active: true
    });

    return acc;
}, []);
```

---

# 34. Common Mistakes

## Mistake 1: Forgetting `return`

Wrong:

```javascript
const total = numbers.reduce((sum, number) => {
    sum + number;
}, 0);
```

The callback returns `undefined`.

Correct:

```javascript
const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);
```

Or:

```javascript
const total = numbers.reduce((sum, number) => sum + number, 0);
```

---

## Mistake 2: Wrong Initial Value

For addition:

```javascript
reduce((sum, number) => sum + number, 0);
```

For multiplication:

```javascript
reduce((result, number) => result * number, 1);
```

Using the wrong initial value can produce incorrect results.

---

## Mistake 3: Forgetting Empty Arrays

Without an initial value:

```javascript
[].reduce((a, b) => a + b);
```

throws a `TypeError`.

Use:

```javascript
[].reduce((a, b) => a + b, 0);
```

---

## Mistake 4: Using `reduce()` Everywhere

`reduce()` is powerful, but it can make simple code harder to understand.

For example:

```javascript
const doubled = numbers.reduce((result, number) => {
    result.push(number * 2);
    return result;
}, []);
```

This works.

But `map()` communicates the intention more clearly:

```javascript
const doubled = numbers.map(number => number * 2);
```

### Best Practice

Choose the array method that clearly describes the operation.

---

# 35. Best Practices

### 1. Provide an initial value

```javascript
numbers.reduce((sum, number) => sum + number, 0);
```

### 2. Use meaningful accumulator names

Instead of:

```javascript
arr.reduce((a, b) => a + b, 0);
```

Prefer:

```javascript
arr.reduce((total, price) => total + price, 0);
```

### 3. Keep the reducer focused

A reducer should ideally perform one clear accumulation task.

### 4. Use simpler methods when appropriate

Use:

```text
map()      → transform
filter()   → select
find()     → find one
some()     → at least one
every()    → all
forEach()  → side effects
reduce()   → accumulate
```

### 5. Avoid unnecessary mutation

Be careful when changing objects from the original array.

---

# 36. Real-World Uses of `reduce()`

`reduce()` is commonly useful for:

* Calculating totals
* Shopping carts
* Order totals
* Calculating averages
* Counting items
* Creating frequency maps
* Grouping data
* Building lookup objects
* Converting arrays into objects
* Flattening arrays
* Removing duplicates
* Combining data
* Calculating statistics
* Data transformation

For example, in a hotel management system:

```javascript
const orderItems = [
    { name: "Momo", price: 150, quantity: 2 },
    { name: "Pizza", price: 500, quantity: 1 },
    { name: "Coke", price: 100, quantity: 2 }
];

const totalAmount = orderItems.reduce(
    (total, item) => total + item.price * item.quantity,
    0
);

console.log(totalAmount);
```

Output:

```text
1000
```

---

# 37. Quick Comparison

| Method          | Main Purpose                  | Returns               |
| --------------- | ----------------------------- | --------------------- |
| `map()`         | Transform every element       | New array             |
| `filter()`      | Select elements               | New array             |
| `find()`        | Find first match              | Element / `undefined` |
| `findIndex()`   | Find first matching index     | Number                |
| `some()`        | Check if at least one matches | Boolean               |
| `every()`       | Check if all match            | Boolean               |
| `forEach()`     | Perform side effects          | `undefined`           |
| `reduce()`      | Accumulate into one result    | Any value             |
| `reduceRight()` | Accumulate right-to-left      | Any value             |

---

# 38. Quick Revision

```javascript
const numbers = [1, 2, 3, 4];

const total = numbers.reduce(
    (accumulator, currentValue) => {
        return accumulator + currentValue;
    },
    0
);

console.log(total);
```

Remember:

```text
reduce()
   ↓
process each element
   ↓
update accumulator
   ↓
continue
   ↓
return final accumulator
```

---

# 39. `reduce()` Cheat Sheet

### Sum

```javascript
numbers.reduce((sum, number) => sum + number, 0);
```

### Product

```javascript
numbers.reduce((result, number) => result * number, 1);
```

### Maximum

```javascript
numbers.reduce(
    (max, number) => Math.max(max, number),
    -Infinity
);
```

### Minimum

```javascript
numbers.reduce(
    (min, number) => Math.min(min, number),
    Infinity
);
```

### Frequency

```javascript
items.reduce((count, item) => {
    count[item] = (count[item] || 0) + 1;
    return count;
}, {});
```

### Grouping

```javascript
items.reduce((groups, item) => {
    const key = item.category;

    if (!groups[key]) {
        groups[key] = [];
    }

    groups[key].push(item);

    return groups;
}, {});
```

### Object Lookup

```javascript
items.reduce((result, item) => {
    result[item.id] = item;
    return result;
}, {});
```

---

# 40. Key Takeaways

* `reduce()` processes an entire array and produces one accumulated result.
* The accumulator stores the result between iterations.
* `currentValue` represents the current array element.
* `initialValue` defines the starting accumulator value.
* Providing an initial value is generally recommended.
* `reduce()` can return numbers, objects, arrays, strings, or other values.
* It is useful for totals, grouping, counting, lookup objects, and data transformation.
* `map()` is usually better for transformation.
* `filter()` is usually better for selection.
* `forEach()` is usually better for side effects.
* `find()` is better for finding one matching element.
* `some()` and `every()` are better for boolean checks.
* `reduce()` does not automatically handle asynchronous operations.
* `reduceRight()` processes elements from right to left.
* Avoid using `reduce()` when another array method expresses the intent more clearly.

---
