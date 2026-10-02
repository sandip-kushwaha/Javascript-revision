# JavaScript Array Basics

An **array** is a data structure used to store multiple values in a single variable.

Instead of creating separate variables:

```javascript
const food1 = "Pizza";
const food2 = "Burger";
const food3 = "Momo";
```

We can use an array:

```javascript
const foods = ["Pizza", "Burger", "Momo"];
```

Arrays are one of the most commonly used data structures in JavaScript.

---

# 1. What is an Array?

An array is an ordered collection of values.

```javascript
const fruits = ["Apple", "Banana", "Mango"];
```

The array contains three elements:

```text
Apple
Banana
Mango
```

Each element has a position called an **index**.

```text
Index:     0         1         2
          ↓         ↓         ↓
        Apple     Banana    Mango
```

JavaScript arrays use **zero-based indexing**.

That means the first element is at index `0`.

---

# 2. Creating an Array

The simplest way is using square brackets:

```javascript
const fruits = ["Apple", "Banana", "Mango"];
```

Another example:

```javascript
const numbers = [10, 20, 30, 40];
```

Empty array:

```javascript
const items = [];
```

---

# 3. Accessing Array Elements

Use the index:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

console.log(fruits[0]);
```

Output:

```text
Apple
```

Second element:

```javascript
console.log(fruits[1]);
```

Output:

```text
Banana
```

Third element:

```javascript
console.log(fruits[2]);
```

Output:

```text
Mango
```

---

# 4. Array Index

Consider:

```javascript
const languages = ["JavaScript", "Python", "C++", "Java"];
```

The indexes are:

```text
Index:       0            1         2        3
             ↓            ↓         ↓        ↓
Value:   JavaScript     Python     C++      Java
```

Therefore:

```javascript
console.log(languages[0]); // JavaScript
console.log(languages[1]); // Python
console.log(languages[2]); // C++
console.log(languages[3]); // Java
```

---

# 5. Changing an Array Element

Arrays declared with `const` can still have their elements changed.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits[1] = "Orange";

console.log(fruits);
```

Output:

```text
["Apple", "Orange", "Mango"]
```

Important:

```javascript
const fruits = ["Apple", "Banana"];
```

`const` prevents reassignment of the variable:

```javascript
fruits = ["Mango", "Orange"]; // Error
```

But changing an element is allowed:

```javascript
fruits[0] = "Mango";
```

---

# 6. Array Length

The `length` property tells us how many elements an array contains.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

console.log(fruits.length);
```

Output:

```text
3
```

Another example:

```javascript
const numbers = [10, 20, 30, 40, 50];

console.log(numbers.length);
```

Output:

```text
5
```

---

# 7. Last Element

Because arrays start at index `0`, the last element is:

```javascript
array.length - 1
```

Example:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

console.log(fruits[fruits.length - 1]);
```

Output:

```text
Mango
```

Modern JavaScript also provides:

```javascript
console.log(fruits.at(-1));
```

Output:

```text
Mango
```

---

# 8. Array Can Store Different Data Types

JavaScript arrays can contain different types of values.

```javascript
const data = [
    "Sandip",
    22,
    true,
    null,
    undefined
];
```

You can also have objects and functions:

```javascript
const items = [
    "JavaScript",
    100,
    { name: "Sandip" },
    () => console.log("Hello")
];
```

Although mixed arrays are possible, keeping related data together usually makes code easier to understand.

---

# 9. Arrays Can Contain Objects

This is extremely common in real applications.

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

Access the first object:

```javascript
console.log(users[0]);
```

Output:

```text
{ name: "Sandip", age: 22 }
```

Access a property:

```javascript
console.log(users[0].name);
```

Output:

```text
Sandip
```

---

# 10. Arrays Can Contain Arrays

Arrays can also contain other arrays.

This is called a **nested array**.

```javascript
const numbers = [
    [1, 2, 3],
    [4, 5, 6]
];
```

Access the first nested array:

```javascript
console.log(numbers[0]);
```

Output:

```text
[1, 2, 3]
```

Access a value inside it:

```javascript
console.log(numbers[0][1]);
```

Output:

```text
2
```

---

# 11. Two-Dimensional Arrays

A two-dimensional array can represent rows and columns.

```javascript
const matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];
```

Structure:

```text
        Column
        0  1  2

Row 0   1  2  3
Row 1   4  5  6
Row 2   7  8  9
```

Access:

```javascript
console.log(matrix[1][2]);
```

Output:

```text
6
```

---

# 12. Array Constructor

You can also create an array using `Array()`.

```javascript
const fruits = new Array("Apple", "Banana", "Mango");

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

However, the array literal syntax is usually simpler:

```javascript
const fruits = ["Apple", "Banana", "Mango"];
```

---

# 13. Important `Array()` Behavior

Be careful with:

```javascript
const numbers = new Array(5);
```

This creates an array with length `5`, not an array containing the number `5`.

```javascript
console.log(numbers.length);
```

Output:

```text
5
```

Compare:

```javascript
const a = new Array(5);
const b = [5];

console.log(a.length); // 5
console.log(b.length); // 1
```

---

# 14. Array.isArray()

To check whether a value is an array, use:

```javascript
Array.isArray()
```

Example:

```javascript
const fruits = ["Apple", "Banana"];

console.log(Array.isArray(fruits));
```

Output:

```text
true
```

For an object:

```javascript
const user = {
    name: "Sandip"
};

console.log(Array.isArray(user));
```

Output:

```text
false
```

---

# 15. Why Not Use `typeof`?

You might try:

```javascript
const fruits = ["Apple", "Banana"];

console.log(typeof fruits);
```

Output:

```text
object
```

Arrays are technically objects in JavaScript.

Therefore:

```javascript
typeof []
```

returns:

```text
"object"
```

Use:

```javascript
Array.isArray([])
```

instead.

---

# 16. Checking Array Length

```javascript
const users = ["Sandip", "Ram", "Sita"];

if (users.length > 0) {
    console.log("Users available");
}
```

Output:

```text
Users available
```

To check an empty array:

```javascript
const users = [];

if (users.length === 0) {
    console.log("No users");
}
```

---

# 17. Looping Through an Array

You can use a traditional `for` loop.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

Output:

```text
Apple
Banana
Mango
```

---

# 18. Using `for...of`

`for...of` directly gives you each array value.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

for (const fruit of fruits) {
    console.log(fruit);
}
```

Output:

```text
Apple
Banana
Mango
```

This is often easier to read when you don't need the index.

---

# 19. Using `forEach()`

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits.forEach(fruit => {
    console.log(fruit);
});
```

Output:

```text
Apple
Banana
Mango
```

`forEach()` uses a callback function.

---

# 20. Getting Both Value and Index

`forEach()` provides the index as the second callback parameter.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

fruits.forEach((fruit, index) => {
    console.log(index, fruit);
});
```

Output:

```text
0 Apple
1 Banana
2 Mango
```

---

# 21. Array Destructuring

You can extract array values into variables.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

const [first, second, third] = fruits;

console.log(first);
console.log(second);
console.log(third);
```

Output:

```text
Apple
Banana
Mango
```

This is called **array destructuring**.

A complete explanation will be covered later in:

```text
04-Arrays/11-Array-Destructuring.md
```

---

# 22. Skipping Array Elements

You can skip elements while destructuring.

```javascript
const numbers = [10, 20, 30];

const [first, , third] = numbers;

console.log(first);
console.log(third);
```

Output:

```text
10
30
```

The empty position skips `20`.

---

# 23. Rest with Arrays

You can collect remaining values using `...`.

```javascript
const numbers = [10, 20, 30, 40];

const [first, ...remaining] = numbers;

console.log(first);
console.log(remaining);
```

Output:

```text
10
[20, 30, 40]
```

This is called the **rest syntax**.

---

# 24. Copying an Array with Spread

The spread operator can create a shallow copy.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

const copiedFruits = [...fruits];

console.log(copiedFruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

The two arrays are different array objects.

```javascript
console.log(fruits === copiedFruits);
```

Output:

```text
false
```

---

# 25. Combining Arrays

The spread operator can combine arrays.

```javascript
const frontend = ["HTML", "CSS", "JavaScript"];

const backend = ["Node.js", "MongoDB"];

const skills = [...frontend, ...backend];

console.log(skills);
```

Output:

```text
[
    "HTML",
    "CSS",
    "JavaScript",
    "Node.js",
    "MongoDB"
]
```

---

# 26. Adding Elements by Index

You can add or replace an element at a specific index.

```javascript
const fruits = ["Apple", "Banana"];

fruits[2] = "Mango";

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

Be careful when assigning a far-away index:

```javascript
const numbers = [10, 20];

numbers[5] = 60;

console.log(numbers);
```

The array becomes sparse, with empty slots between the existing elements and index `5`.

---

# 27. Sparse Arrays

A sparse array has missing elements.

```javascript
const numbers = [];

numbers[2] = 30;

console.log(numbers.length);
```

Output:

```text
3
```

But indexes `0` and `1` do not contain actual values.

For normal application code, avoid creating sparse arrays unintentionally.

---

# 28. Array References

Arrays are objects, so variables hold references to array objects.

```javascript
const fruits = ["Apple", "Banana"];

const anotherFruits = fruits;

anotherFruits[0] = "Mango";

console.log(fruits);
```

Output:

```text
["Mango", "Banana"]
```

Both variables refer to the same array.

---

# 29. Array Reference vs Copy

This does **not** create a new array:

```javascript
const a = [1, 2, 3];

const b = a;
```

This creates a shallow copy:

```javascript
const a = [1, 2, 3];

const b = [...a];
```

Now:

```javascript
b[0] = 100;

console.log(a);
console.log(b);
```

Output:

```text
[1, 2, 3]
[100, 2, 3]
```

---

# 30. Comparing Arrays

Two separate arrays are not equal just because their contents are the same.

```javascript
const a = [1, 2, 3];
const b = [1, 2, 3];

console.log(a === b);
```

Output:

```text
false
```

They are different array objects.

But:

```javascript
const a = [1, 2, 3];
const b = a;

console.log(a === b);
```

Output:

```text
true
```

Both variables reference the same array.

---

# 31. Practical Example: Hotel Food Menu

A simple food menu can be represented as an array:

```javascript
const menu = [
    "Chicken Momo",
    "Pizza",
    "Burger",
    "Chowmein",
    "Fried Rice"
];
```

Display the menu:

```javascript
menu.forEach((food, index) => {
    console.log(`${index + 1}. ${food}`);
});
```

Output:

```text
1. Chicken Momo
2. Pizza
3. Burger
4. Chowmein
5. Fried Rice
```

---

# 32. Practical Example: Hotel Tables

```javascript
const tables = [
    {
        tableNumber: "T-01",
        capacity: 2
    },
    {
        tableNumber: "T-02",
        capacity: 4
    },
    {
        tableNumber: "T-03",
        capacity: 6
    }
];
```

Access the first table:

```javascript
console.log(tables[0]);
```

Access its number:

```javascript
console.log(tables[0].tableNumber);
```

Output:

```text
T-01
```

---

# 33. Practical Example: Order Items

```javascript
const orders = [
    {
        item: "Pizza",
        quantity: 2,
        price: 500
    },
    {
        item: "Momo",
        quantity: 3,
        price: 250
    }
];
```

Access the second order:

```javascript
console.log(orders[1]);
```

Access quantity:

```javascript
console.log(orders[1].quantity);
```

Output:

```text
3
```

---

# 34. Nested Arrays in Real Applications

A shopping cart could contain products:

```javascript
const cart = [
    ["Pizza", 2],
    ["Burger", 1],
    ["Momo", 3]
];
```

Access:

```javascript
console.log(cart[0][0]);
```

Output:

```text
Pizza
```

And:

```javascript
console.log(cart[0][1]);
```

Output:

```text
2
```

In real applications, arrays of objects are often easier to understand:

```javascript
const cart = [
    {
        product: "Pizza",
        quantity: 2
    },
    {
        product: "Burger",
        quantity: 1
    }
];
```

---

# 35. Important Array Properties

The most important basic property is:

```javascript
array.length
```

Example:

```javascript
const numbers = [10, 20, 30];

console.log(numbers.length);
```

Output:

```text
3
```

Most array operations are performed using methods, which will be covered in the next files.

---

# 36. Common Mistakes

## Mistake 1: Forgetting zero-based indexing

Wrong assumption:

```text
First element → index 1
```

Correct:

```text
First element → index 0
```

---

## Mistake 2: Accessing an invalid index

```javascript
const fruits = ["Apple", "Banana"];

console.log(fruits[5]);
```

Output:

```text
undefined
```

JavaScript does not automatically throw an error for a normal out-of-range index access.

---

## Mistake 3: Using `typeof` to detect arrays

Avoid:

```javascript
typeof value === "array"
```

There is no `"array"` result from `typeof`.

Use:

```javascript
Array.isArray(value)
```

---

## Mistake 4: Accidentally sharing an array reference

```javascript
const original = [1, 2, 3];

const copy = original;
```

`copy` is not an independent copy.

Use:

```javascript
const copy = [...original];
```

for a shallow copy.

---

## Mistake 5: Confusing `length` with the last index

For:

```javascript
const numbers = [10, 20, 30];
```

Length:

```text
3
```

Last index:

```text
2
```

So:

```javascript
numbers[numbers.length - 1]
```

gets the last element.

---

# 37. Best Practices

### 1. Use `const` by default

```javascript
const users = [];
```

If you need to reassign the entire array, use `let`.

```javascript
let users = [];

users = ["Sandip", "Ram"];
```

---

### 2. Use descriptive names

Good:

```javascript
const users = [];
const products = [];
const orders = [];
const menuItems = [];
```

Avoid unclear names:

```javascript
const x = [];
const data1 = [];
```

when the purpose is not obvious.

---

### 3. Keep related data together

Good:

```javascript
const users = [
    {
        name: "Sandip",
        age: 22
    }
];
```

This is easier to work with than many unrelated variables.

---

### 4. Use `Array.isArray()`

When you need to verify an array:

```javascript
if (Array.isArray(data)) {
    console.log("Data is an array");
}
```

---

### 5. Avoid unnecessary mutation

Prefer creating a new array when appropriate:

```javascript
const updatedUsers = [...users, newUser];
```

rather than changing the original array unnecessarily.

---

# 38. Quick Revision

```text
Array
 │
 ├── Stores multiple values
 │
 ├── Zero-based index
 │
 ├── First index → 0
 │
 ├── Last index → length - 1
 │
 ├── length → number of elements
 │
 ├── Array.isArray() → checks array
 │
 ├── Can contain objects
 │
 ├── Can contain nested arrays
 │
 └── Supports many useful methods
```

Example:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

console.log(fruits[0]);                 // Apple
console.log(fruits.length);             // 3
console.log(fruits[fruits.length - 1]); // Mango
```

---

# 39. Key Takeaways

* An array stores multiple values.
* Arrays use zero-based indexing.
* The first element is at index `0`.
* The last index is `length - 1`.
* Use `array.length` to get the array length.
* Arrays can contain different data types.
* Arrays can contain objects and other arrays.
* Use `Array.isArray()` to check whether a value is an array.
* `typeof []` returns `"object"`.
* Arrays are objects and are handled by reference.
* Assigning one array variable to another copies the reference, not the array.
* Use `[...array]` for a shallow copy.
* `for...of` is useful for iterating over values.
* `forEach()` is useful for executing an action for each element.
* Arrays are heavily used in frontend and backend applications.

---
