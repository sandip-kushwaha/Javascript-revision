# JavaScript `while` Loop

The `while` loop is used to **repeat a block of code as long as a condition is `true`**.

It is especially useful when you **do not know exactly how many times** the loop should run.

---

## 1. What is a `while` Loop?

A `while` loop checks the condition **before** executing the loop body.

### Basic Syntax

```javascript
while (condition) {
    // code to execute
}
```

### Example

```javascript
let count = 1;

while (count <= 5) {
    console.log(count);

    count++;
}
```

### Output

```text
1
2
3
4
5
```

### How it works

```text
count = 1
   ↓
count <= 5 ?
   ↓
 true
   ↓
execute code
   ↓
count++
   ↓
check condition again
```

When `count` becomes `6`:

```javascript
6 <= 5
```

is `false`, so the loop stops.

---

# 2. Important Parts of a `while` Loop

A `while` loop normally has three important parts:

```javascript
let count = 1;       // Initialization

while (count <= 5) { // Condition

    console.log(count);

    count++;         // Update
}
```

| Part           | Purpose                                           |
| -------------- | ------------------------------------------------- |
| Initialization | Starting value                                    |
| Condition      | Determines whether loop continues                 |
| Update         | Changes the value so the loop can eventually stop |

---

# 3. Simple Counting Example

```javascript
let i = 1;

while (i <= 10) {
    console.log(i);
    i++;
}
```

Output:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# 4. Counting Backward

A `while` loop can also count downward.

```javascript
let i = 5;

while (i >= 1) {
    console.log(i);
    i--;
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

# 5. Increment by More Than 1

You can increase the value by any amount.

```javascript
let i = 0;

while (i <= 10) {
    console.log(i);
    i += 2;
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

# 6. Decrement by More Than 1

```javascript
let i = 10;

while (i >= 0) {
    console.log(i);
    i -= 2;
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

# 7. `while` Loop with Arrays

You can use a `while` loop to access array elements.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

let i = 0;

while (i < fruits.length) {
    console.log(fruits[i]);

    i++;
}
```

Output:

```text
Apple
Banana
Mango
```

### Why use `i < fruits.length`?

Suppose:

```javascript
fruits.length
```

is:

```text
3
```

Valid indexes are:

```text
0
1
2
```

Therefore:

```javascript
i < fruits.length
```

is safer than:

```javascript
i <= fruits.length
```

---

# 8. Sum of Numbers

Calculate the sum from `1` to `5`.

```javascript
let i = 1;
let sum = 0;

while (i <= 5) {
    sum += i;

    i++;
}

console.log(sum);
```

Output:

```text
15
```

Calculation:

```text
1 + 2 + 3 + 4 + 5 = 15
```

---

# 9. Product of Numbers

Calculate the product from `1` to `5`.

```javascript
let i = 1;
let product = 1;

while (i <= 5) {
    product *= i;

    i++;
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

# 10. Even Numbers

```javascript
let i = 1;

while (i <= 10) {
    if (i % 2 === 0) {
        console.log(i);
    }

    i++;
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

# 11. Odd Numbers

```javascript
let i = 1;

while (i <= 10) {
    if (i % 2 !== 0) {
        console.log(i);
    }

    i++;
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

# 12. `break` with `while`

`break` immediately stops the loop.

```javascript
let i = 1;

while (i <= 10) {
    if (i === 6) {
        break;
    }

    console.log(i);

    i++;
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

When:

```javascript
i === 6
```

becomes `true`, `break` stops the loop.

---

# 13. `continue` with `while`

`continue` skips the current iteration.

```javascript
let i = 0;

while (i < 10) {
    i++;

    if (i === 5) {
        continue;
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
6
7
8
9
10
```

The number `5` is skipped.

> **Important:** When using `continue` in a `while` loop, make sure the loop variable is updated before `continue`, otherwise you can accidentally create an infinite loop.

---

# 14. Finding a Number

```javascript
const numbers = [10, 20, 30, 40, 50];

let i = 0;
let found = false;

while (i < numbers.length) {
    if (numbers[i] === 30) {
        found = true;
        break;
    }

    i++;
}

console.log(found);
```

Output:

```text
true
```

---

# 15. Counting Elements

Count how many numbers are greater than `10`.

```javascript
const numbers = [5, 15, 20, 8, 30];

let i = 0;
let count = 0;

while (i < numbers.length) {
    if (numbers[i] > 10) {
        count++;
    }

    i++;
}

console.log(count);
```

Output:

```text
3
```

The matching numbers are:

```text
15
20
30
```

---

# 16. Finding the Largest Number

```javascript
const numbers = [10, 45, 23, 78, 12];

let i = 1;
let largest = numbers[0];

while (i < numbers.length) {
    if (numbers[i] > largest) {
        largest = numbers[i];
    }

    i++;
}

console.log(largest);
```

Output:

```text
78
```

---

# 17. Finding the Smallest Number

```javascript
const numbers = [10, 45, 23, 78, 12];

let i = 1;
let smallest = numbers[0];

while (i < numbers.length) {
    if (numbers[i] < smallest) {
        smallest = numbers[i];
    }

    i++;
}

console.log(smallest);
```

Output:

```text
10
```

---

# 18. Reverse an Array Using `while`

```javascript
const numbers = [10, 20, 30, 40, 50];

let i = numbers.length - 1;

while (i >= 0) {
    console.log(numbers[i]);

    i--;
}
```

Output:

```text
50
40
30
20
10
```

---

# 19. Loop Through a String

Strings can also be accessed using indexes.

```javascript
const name = "Sandip";

let i = 0;

while (i < name.length) {
    console.log(name[i]);

    i++;
}
```

Output:

```text
S
a
n
d
i
p
```

---

# 20. Count Vowels

```javascript
const text = "javascript";

let i = 0;
let count = 0;

while (i < text.length) {
    const char = text[i];

    if ("aeiou".includes(char)) {
        count++;
    }

    i++;
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

# 21. Multiplication Table

Print the multiplication table of `5`.

```javascript
let i = 1;

while (i <= 10) {
    console.log(`5 × ${i} = ${5 * i}`);

    i++;
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

# 22. Nested `while` Loops

A `while` loop can be placed inside another `while` loop.

```javascript
let i = 1;

while (i <= 3) {
    let j = 1;

    while (j <= 3) {
        console.log(`i = ${i}, j = ${j}`);

        j++;
    }

    i++;
}
```

Output:

```text
i = 1, j = 1
i = 1, j = 2
i = 1, j = 3
i = 2, j = 1
i = 2, j = 2
i = 2, j = 3
i = 3, j = 1
i = 3, j = 2
i = 3, j = 3
```

Nested loops are commonly used for:

* Patterns
* Matrices
* Tables
* Grids
* Comparing elements

---

# 23. Infinite `while` Loop

If the condition never becomes `false`, the loop continues forever.

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
}
```

This is an **infinite loop** because `i` never changes.

The condition:

```javascript
i <= 5
```

always remains:

```text
true
```

### Correct version

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);

    i++;
}
```

---

# 24. Common Infinite Loop Mistake

### Wrong

```javascript
let count = 1;

while (count <= 10) {
    console.log(count);
}
```

### Correct

```javascript
let count = 1;

while (count <= 10) {
    console.log(count);

    count++;
}
```

Always make sure something inside the loop can eventually make the condition `false`.

---

# 25. `while` vs `for`

Both can perform repetition.

### `for`

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

### `while`

```javascript
let i = 0;

while (i < 5) {
    console.log(i);

    i++;
}
```

Both produce:

```text
0
1
2
3
4
```

---

# 26. When Should You Use `while`?

Use `while` when the number of iterations is not necessarily known beforehand.

For example:

```javascript
let password = "";

while (password !== "1234") {
    // ask for password
}
```

The loop can continue until the required condition is satisfied.

For a known number of repetitions, a `for` loop is often clearer:

```javascript
for (let i = 1; i <= 10; i++) {
    console.log(i);
}
```

---

# 27. `while` Loop with User Input

In a browser:

```javascript
let answer = "";

while (answer !== "yes") {
    answer = prompt("Type yes to continue:");
}

console.log("Continuing...");
```

The loop continues until the user enters:

```text
yes
```

> `prompt()` is a browser API and is not available by default in Node.js.

---

# 28. Hotel Management Example

Suppose a hotel has several tables and you want to check them one by one.

```javascript
const tables = [
    { tableNumber: 1, status: "available" },
    { tableNumber: 2, status: "occupied" },
    { tableNumber: 3, status: "available" },
    { tableNumber: 4, status: "occupied" }
];

let i = 0;

while (i < tables.length) {
    if (tables[i].status === "available") {
        console.log(`Table ${tables[i].tableNumber} is available`);
    }

    i++;
}
```

Output:

```text
Table 1 is available
Table 3 is available
```

---

# 29. Backend Example

Suppose an application has users:

```javascript
const users = [
    { name: "Ram", isActive: true },
    { name: "Shyam", isActive: false },
    { name: "Hari", isActive: true }
];

let i = 0;

while (i < users.length) {
    if (users[i].isActive) {
        console.log(`${users[i].name} is active`);
    }

    i++;
}
```

Output:

```text
Ram is active
Hari is active
```

This kind of logic is useful for understanding backend data processing, although methods such as `filter()` are often more expressive for production code.

---

# 30. `while` with `true`

You can intentionally create a loop with:

```javascript
while (true) {
    // code
}
```

Then use `break` to stop it.

Example:

```javascript
let count = 1;

while (true) {
    console.log(count);

    if (count === 5) {
        break;
    }

    count++;
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

This pattern is useful when the stopping condition is naturally checked inside the loop.

---

# 31. `while` Loop vs `do...while`

### `while`

The condition is checked **before** execution.

```javascript
let i = 10;

while (i < 5) {
    console.log(i);
}
```

Output:

```text
Nothing
```

The condition is already `false`.

### `do...while`

The code executes **at least once**.

```javascript
let i = 10;

do {
    console.log(i);

    i++;
} while (i < 5);
```

Output:

```text
10
```

The difference is:

```text
while
  ↓
check condition
  ↓
execute if true
```

versus:

```text
do...while
  ↓
execute
  ↓
check condition
```

---

# 32. Common Mistakes

## Mistake 1: Forgetting the Update

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
}
```

This creates an infinite loop.

### Fix

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
    i++;
}
```

---

## Mistake 2: Wrong Condition

```javascript
let i = 1;

while (i >= 5) {
    console.log(i);

    i++;
}
```

The loop never executes because:

```text
1 >= 5
```

is `false`.

---

## Mistake 3: Wrong Direction

```javascript
let i = 5;

while (i >= 1) {
    console.log(i);

    i++;
}
```

`i` increases instead of decreasing, so the condition never becomes false.

### Correct

```javascript
let i = 5;

while (i >= 1) {
    console.log(i);

    i--;
}
```

---

## Mistake 4: Incorrect Array Boundary

### Wrong

```javascript
const numbers = [10, 20, 30];

let i = 0;

while (i <= numbers.length) {
    console.log(numbers[i]);

    i++;
}
```

This eventually accesses:

```javascript
numbers[3]
```

which is:

```text
undefined
```

### Correct

```javascript
while (i < numbers.length) {
    console.log(numbers[i]);

    i++;
}
```

---

# 33. `while` Loop Complexity

For:

```javascript
let i = 0;

while (i < n) {
    console.log(i);

    i++;
}
```

The loop runs approximately `n` times.

### Time Complexity

```text
O(n)
```

Nested loop:

```javascript
let i = 0;

while (i < n) {
    let j = 0;

    while (j < n) {
        console.log(i, j);

        j++;
    }

    i++;
}
```

Time complexity:

```text
O(n²)
```

---

# 34. Quick Comparison

| Loop         | Condition Check       | Best Use                           |
| ------------ | --------------------- | ---------------------------------- |
| `for`        | Before each iteration | Known number of iterations         |
| `while`      | Before each iteration | Unknown/condition-based iterations |
| `do...while` | After each iteration  | Must execute at least once         |
| `for...of`   | Iterates values       | Arrays/iterables                   |
| `for...in`   | Iterates keys         | Object properties                  |

---

# 35. Real-World Examples

`while` loops can be useful for:

* Waiting for a condition
* Processing data until a condition is met
* Searching until an item is found
* Retry-style logic
* Reading items until there are no more items
* Menu systems
* Game loops
* Algorithmic problems

In asynchronous JavaScript, however, do **not** use a synchronous `while` loop to repeatedly wait for a Promise or timer. That can block the JavaScript thread.

---

# 36. Important Rule

A `while` loop should usually have this structure:

```javascript
initialization;

while (condition) {
    // work

    update;
}
```

Example:

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);

    i++;
}
```

Remember:

```text
Initialize
    ↓
Check
    ↓
Execute
    ↓
Update
    ↓
Check again
```

---

# 40. Key Takeaways

* `while` repeats code while a condition is `true`.
* The condition is checked **before** each iteration.
* A `while` loop can execute **zero times**.
* Always make sure the loop can eventually stop.
* Update the loop variable when necessary.
* `break` stops the loop.
* `continue` skips the current iteration.
* `while` is useful for condition-based repetition.
* `for` is often clearer when the number of iterations is known.
* `do...while` always executes at least once.
* Array indexes usually use:

  ```javascript
  i < array.length
  ```
* A simple loop is usually `O(n)`.
* Nested loops can be `O(n²)`.
* Avoid blocking synchronous loops when working with asynchronous operations.

---
