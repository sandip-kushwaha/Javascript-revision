# JavaScript `for` Loop

A `for` loop is used to **repeat a block of code multiple times**.

It is especially useful when you know how many times you want to execute something or when you need to iterate through a range of values.

---

# 1. What is a `for` Loop?

Example:

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

Output:

```text
1
2
3
4
5
```

The loop repeats the code while the condition is `true`.

---

# 2. Basic Syntax

```javascript
for (initialization; condition; update) {
    // code
}
```

Example:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

There are three main parts:

```text
initialization
condition
update
```

---

# 3. Initialization

Initialization runs **once**, before the loop starts.

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

Here:

```javascript
let i = 1;
```

is the initialization.

The loop starts with:

```text
i = 1
```

---

# 4. Condition

The condition determines whether the loop should continue.

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

The condition is:

```javascript
i <= 5
```

As long as it is `true`, the loop continues.

When it becomes `false`, the loop stops.

---

# 5. Update

The update changes the loop variable after each iteration.

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

The update is:

```javascript
i++
```

This means:

```text
i = i + 1
```

---

# 6. How a `for` Loop Executes

Consider:

```javascript
for (let i = 1; i <= 3; i++) {
    console.log(i);
}
```

Execution:

```text
1. let i = 1
2. Check i <= 3
3. Execute console.log(i)
4. i++
5. Check i <= 3
6. Execute console.log(i)
7. i++
8. Check i <= 3
9. Execute console.log(i)
10. i++
11. Condition becomes false
12. Stop
```

Output:

```text
1
2
3
```

---

# 7. Counting from 0

JavaScript commonly uses zero-based indexing.

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

Output:

```text
0
1
2
3
4
```

Notice:

```text
5
```

is not printed.

Because:

```javascript
i < 5
```

becomes false when:

```text
i = 5
```

---

# 8. Counting from 1

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

Output:

```text
1
2
3
4
5
```

---

# 9. Increment by 2

You don't have to increase by exactly 1.

```javascript
for (let i = 0; i <= 10; i += 2) {
    console.log(i);
}
```

Output:

```text
0
2
4
6
8
10
```

---

# 10. Decrementing

You can also count backward.

```javascript
for (let i = 5; i >= 1; i--) {
    console.log(i);
}
```

Output:

```text
5
4
3
2
1
```

---

# 11. Decrement by 2

```javascript
for (let i = 10; i >= 0; i -= 2) {
    console.log(i);
}
```

Output:

```text
10
8
6
4
2
0
```

---

# 12. Loop Through an Array

A traditional `for` loop can access array elements using their indexes.

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

# 13. Array Indexes

Consider:

```javascript
const fruits = ["Apple", "Banana", "Mango"];
```

The indexes are:

```text
Apple  → 0
Banana → 1
Mango  → 2
```

Therefore:

```javascript
fruits[0]
fruits[1]
fruits[2]
```

Access each element using:

```javascript
for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

---

# 14. Why Use `i < array.length`?

This is the standard pattern:

```javascript
for (let i = 0; i < array.length; i++) {
    console.log(array[i]);
}
```

Suppose:

```text
array.length = 3
```

Valid indexes are:

```text
0
1
2
```

So:

```javascript
i < 3
```

is correct.

Using:

```javascript
i <= array.length
```

would attempt to access:

```text
array[3]
```

which does not exist.

---

# 15. Using `let` in Loops

Prefer `let` for the loop counter:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

The variable `i` is block-scoped.

---

# 16. Using `const` in a Loop

You can use `const` in loops such as:

```javascript
const users = ["Sandip", "Ram", "Hari"];

for (const user of users) {
    console.log(user);
}
```

This is a `for...of` loop, which will be covered separately.

For a traditional counter-based loop, use:

```javascript
let i
```

because the counter changes.

---

# 17. `break`

`break` immediately stops the loop.

Example:

```javascript
for (let i = 1; i <= 10; i++) {
    if (i === 5) {
        break;
    }

    console.log(i);
}
```

Output:

```text
1
2
3
4
```

When:

```text
i === 5
```

becomes true, the loop stops.

---

# 18. `continue`

`continue` skips the current iteration and moves to the next iteration.

Example:

```javascript
for (let i = 1; i <= 5; i++) {
    if (i === 3) {
        continue;
    }

    console.log(i);
}
```

Output:

```text
1
2
4
5
```

The number `3` is skipped.

---

# 19. `break` vs `continue`

| Statement  | Behavior                    |
| ---------- | --------------------------- |
| `break`    | Stops the entire loop       |
| `continue` | Skips the current iteration |

Example:

```javascript
break;
```

means:

```text
Stop loop completely
```

While:

```javascript
continue;
```

means:

```text
Skip this iteration
Continue with the next one
```

---

# 20. Sum of Numbers

A `for` loop can be used to calculate a total.

```javascript
let sum = 0;

for (let i = 1; i <= 5; i++) {
    sum += i;
}

console.log(sum);
```

Output:

```text
15
```

Because:

```text
1 + 2 + 3 + 4 + 5 = 15
```

---

# 21. Product of Numbers

```javascript
let product = 1;

for (let i = 1; i <= 5; i++) {
    product *= i;
}

console.log(product);
```

Output:

```text
120
```

Because:

```text
1 × 2 × 3 × 4 × 5 = 120
```

---

# 22. Multiplication Table

```javascript
const number = 5;

for (let i = 1; i <= 10; i++) {
    console.log(`${number} × ${i} = ${number * i}`);
}
```

Output:

```text
5 × 1 = 5
5 × 2 = 10
5 × 3 = 15
5 × 4 = 20
5 × 5 = 25
5 × 6 = 30
5 × 7 = 35
5 × 8 = 40
5 × 9 = 45
5 × 10 = 50
```

---

# 23. Even Numbers

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        console.log(i);
    }
}
```

Output:

```text
2
4
6
8
10
```

---

# 24. Odd Numbers

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 !== 0) {
        console.log(i);
    }
}
```

Output:

```text
1
3
5
7
9
```

---

# 25. Sum of Even Numbers

```javascript
let sum = 0;

for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        sum += i;
    }
}

console.log(sum);
```

Output:

```text
30
```

Because:

```text
2 + 4 + 6 + 8 + 10 = 30
```

---

# 26. Find an Element

```javascript
const users = ["Ram", "Sandip", "Hari"];

for (let i = 0; i < users.length; i++) {
    if (users[i] === "Sandip") {
        console.log("User found");
        break;
    }
}
```

Output:

```text
User found
```

Using `break` prevents unnecessary iterations after the user is found.

---

# 27. Search with Index

```javascript
const users = ["Ram", "Sandip", "Hari"];

let foundIndex = -1;

for (let i = 0; i < users.length; i++) {
    if (users[i] === "Sandip") {
        foundIndex = i;
        break;
    }
}

console.log(foundIndex);
```

Output:

```text
1
```

If the value is not found:

```text
-1
```

can indicate that no matching index was found.

---

# 28. Count Matching Values

```javascript
const numbers = [10, 20, 10, 30, 10];

let count = 0;

for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] === 10) {
        count++;
    }
}

console.log(count);
```

Output:

```text
3
```

---

# 29. Find the Largest Number

```javascript
const numbers = [10, 25, 7, 40, 15];

let largest = numbers[0];

for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > largest) {
        largest = numbers[i];
    }
}

console.log(largest);
```

Output:

```text
40
```

---

# 30. Find the Smallest Number

```javascript
const numbers = [10, 25, 7, 40, 15];

let smallest = numbers[0];

for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] < smallest) {
        smallest = numbers[i];
    }
}

console.log(smallest);
```

Output:

```text
7
```

---

# 31. Reverse a String

```javascript
const text = "JavaScript";
let reversed = "";

for (let i = text.length - 1; i >= 0; i--) {
    reversed += text[i];
}

console.log(reversed);
```

Output:

```text
tpircSavaJ
```

---

# 32. Count Characters

```javascript
const text = "JavaScript";

let count = 0;

for (let i = 0; i < text.length; i++) {
    count++;
}

console.log(count);
```

Output:

```text
10
```

---

# 33. Count Vowels

```javascript
const text = "javascript";
let count = 0;

for (let i = 0; i < text.length; i++) {
    if ("aeiou".includes(text[i])) {
        count++;
    }
}

console.log(count);
```

Output:

```text
3
```

The vowels are:

```text
a
a
i
```

---

# 34. Nested `for` Loops

A loop inside another loop is called a **nested loop**.

Example:

```javascript
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        console.log(i, j);
    }
}
```

Output:

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

The inner loop completes all its iterations for each iteration of the outer loop.

---

# 35. Multiplication Table Grid

```javascript
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 5; j++) {
        console.log(`${i} × ${j} = ${i * j}`);
    }
}
```

This produces multiplication results for:

```text
1 × 1 ... 1 × 5
2 × 1 ... 2 × 5
3 × 1 ... 3 × 5
```

---

# 36. Nested Loop with Arrays

```javascript
const categories = [
    ["Food", "Drinks"],
    ["Pizza", "Burger"],
    ["Tea", "Coffee"]
];

for (let i = 0; i < categories.length; i++) {
    for (let j = 0; j < categories[i].length; j++) {
        console.log(categories[i][j]);
    }
}
```

Output:

```text
Food
Drinks
Pizza
Burger
Tea
Coffee
```

---

# 37. Infinite Loop

Be careful when the loop condition never becomes false.

Example:

```javascript
for (let i = 0; i < 10;) {
    console.log(i);
}
```

This creates an infinite loop because `i` never changes.

Correct:

```javascript
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

---

# 38. Common Infinite Loop Mistake

Incorrect:

```javascript
for (let i = 0; i < 5; i--) {
    console.log(i);
}
```

The condition:

```text
i < 5
```

continues to remain true as `i` becomes smaller.

Correct:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

---

# 39. Omitting Parts of a `for` Loop

JavaScript allows you to omit parts of the `for` statement.

For example:

```javascript
let i = 0;

for (; i < 5; i++) {
    console.log(i);
}
```

The initialization is outside the loop.

You can also write:

```javascript
let i = 0;

for (;;) {
    if (i >= 5) {
        break;
    }

    console.log(i);
    i++;
}
```

This is valid but generally less readable than a normal `for` loop.

---

# 40. Multiple Variables

You can initialize multiple variables.

```javascript
for (let i = 0, j = 10; i < 5; i++, j--) {
    console.log(i, j);
}
```

Output:

```text
0 10
1 9
2 8
3 7
4 6
```

---

# 41. Practical Hotel Example — Tables

Suppose:

```javascript
const tables = [
    { number: 1, status: "available" },
    { number: 2, status: "occupied" },
    { number: 3, status: "available" }
];
```

Find available tables:

```javascript
for (let i = 0; i < tables.length; i++) {
    if (tables[i].status === "available") {
        console.log(`Table ${tables[i].number} is available`);
    }
}
```

Output:

```text
Table 1 is available
Table 3 is available
```

---

# 42. Practical Hotel Example — Total Bill

```javascript
const orders = [
    { name: "Pizza", price: 500, quantity: 2 },
    { name: "Coffee", price: 150, quantity: 3 },
    { name: "Burger", price: 350, quantity: 1 }
];

let total = 0;

for (let i = 0; i < orders.length; i++) {
    total += orders[i].price * orders[i].quantity;
}

console.log(total);
```

Output:

```text
1850
```

Calculation:

```text
500 × 2 = 1000
150 × 3 = 450
350 × 1 = 350

Total = 1800
```

> Note: The code above actually calculates `1800`, not `1850`.

Correct output:

```text
1800
```

---

# 43. Practical Backend Example — Users

```javascript
const users = [
    { name: "Sandip", role: "admin" },
    { name: "Ram", role: "waiter" },
    { name: "Hari", role: "kitchen" }
];

for (let i = 0; i < users.length; i++) {
    console.log(
        `${users[i].name} - ${users[i].role}`
    );
}
```

Output:

```text
Sandip - admin
Ram - waiter
Hari - kitchen
```

---

# 44. Loop Through Object Properties

A traditional `for` loop does not directly iterate over object properties.

You can first get the keys:

```javascript
const user = {
    name: "Sandip",
    role: "admin",
    active: true
};

const keys = Object.keys(user);

for (let i = 0; i < keys.length; i++) {
    const key = keys[i];

    console.log(key, user[key]);
}
```

Output:

```text
name Sandip
role admin
active true
```

`for...in` is another option and will be covered separately.

---

# 45. `for` vs `for...of`

Traditional `for`:

```javascript
const fruits = ["Apple", "Banana", "Mango"];

for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

`for...of`:

```javascript
for (const fruit of fruits) {
    console.log(fruit);
}
```

The traditional `for` loop is useful when you need the index or precise control over initialization, condition, and update.

---

# 46. `for` vs `forEach`

Traditional `for`:

```javascript
for (let i = 0; i < numbers.length; i++) {
    console.log(numbers[i]);
}
```

`forEach`:

```javascript
numbers.forEach((number) => {
    console.log(number);
});
```

A traditional `for` loop supports:

```javascript
break;
continue;
```

`forEach()` does not provide the same direct loop-control behavior.

---

# 47. Common Mistake — Off-by-One Error

Consider:

```javascript
const numbers = [10, 20, 30];

for (let i = 0; i <= numbers.length; i++) {
    console.log(numbers[i]);
}
```

The valid indexes are:

```text
0
1
2
```

But the loop also reaches:

```text
3
```

So:

```javascript
numbers[3]
```

is:

```text
undefined
```

Correct:

```javascript
for (let i = 0; i < numbers.length; i++) {
    console.log(numbers[i]);
}
```

---

# 48. Best Practices

### 1. Use meaningful loop variables

For simple loops:

```javascript
for (let i = 0; i < 10; i++) {
}
```

is common.

For nested loops:

```javascript
for (let row = 0; row < rows.length; row++) {
    for (let column = 0; column < rows[row].length; column++) {
    }
}
```

can be clearer.

### 2. Avoid unnecessary nested loops

Nested loops can become expensive for large datasets.

### 3. Be careful with loop boundaries

Prefer:

```javascript
i < array.length
```

when iterating through indexes.

### 4. Avoid accidental infinite loops

Make sure the update eventually causes the condition to become false.

### 5. Use `break` when searching

Once you find what you need, stop the loop when appropriate.

---

# 49. Time Complexity

A single loop that processes `n` items generally has:

```text
O(n)
```

time complexity.

Example:

```javascript
for (let i = 0; i < n; i++) {
    console.log(i);
}
```

A nested loop where each loop runs approximately `n` times generally has:

```text
O(n²)
```

time complexity.

Example:

```javascript
for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
        console.log(i, j);
    }
}
```
---

# Key Takeaways

* A `for` loop repeats code while a condition is true.
* It has three main parts: initialization, condition, and update.
* `i++` increments by one.
* `i--` decrements by one.
* Use `i < array.length` for normal index-based array iteration.
* `break` stops the entire loop.
* `continue` skips the current iteration.
* Nested loops contain one loop inside another.
* Be careful about off-by-one errors.
* Make sure loop conditions eventually become false.
* A normal loop over `n` items is generally `O(n)`.
* Two nested loops over `n` items are generally `O(n²)`.
* Traditional `for` loops are useful when you need precise control over indexes and iteration.
