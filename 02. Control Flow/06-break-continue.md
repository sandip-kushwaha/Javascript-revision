# JavaScript `break` and `continue`

JavaScript provides two important statements for controlling loops:

* `break`
* `continue`

They allow you to change the normal flow of a loop.

```text
break     → completely stops the loop
continue  → skips the current iteration
```

---

# 1. `break`

The `break` statement immediately terminates the nearest loop or `switch` statement.

### Syntax

```javascript
break;
```

### Example

```javascript
for (let i = 1; i <= 10; i++) {
    console.log(i);

    if (i === 5) {
        break;
    }
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

When `i` becomes `5`, `break` stops the loop.

---

# 2. `break` with `while`

```javascript
let i = 1;

while (i <= 10) {
    console.log(i);

    if (i === 5) {
        break;
    }

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

---

# 3. `break` with `do...while`

```javascript
let i = 1;

do {
    console.log(i);

    if (i === 3) {
        break;
    }

    i++;
} while (i <= 10);
```

Output:

```text
1
2
3
```

---

# 4. `break` with `switch`

`break` is also commonly used inside `switch`.

```javascript
const day = 2;

switch (day) {
    case 1:
        console.log("Sunday");
        break;

    case 2:
        console.log("Monday");
        break;

    case 3:
        console.log("Tuesday");
        break;

    default:
        console.log("Invalid day");
}
```

Output:

```text
Monday
```

Without `break`, execution can continue into the next `case`.

---

# 5. Searching with `break`

One of the most common uses of `break` is stopping a search once the required item is found.

```javascript
const numbers = [10, 20, 30, 40, 50];

let found = false;

for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] === 30) {
        found = true;
        break;
    }
}

console.log(found);
```

Output:

```text
true
```

There is no need to continue searching after `30` has been found.

---

# 6. Searching an Array

```javascript
const users = [
    "Ram",
    "Shyam",
    "Hari",
    "Sita"
];

for (let i = 0; i < users.length; i++) {
    if (users[i] === "Hari") {
        console.log("User found");
        break;
    }
}
```

Output:

```text
User found
```

---

# 7. Finding the First Matching Item

```javascript
const numbers = [5, 12, 8, 20, 3];

let firstLargeNumber;

for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] > 10) {
        firstLargeNumber = numbers[i];
        break;
    }
}

console.log(firstLargeNumber);
```

Output:

```text
12
```

The loop stops at the first number greater than `10`.

---

# 8. `break` in Nested Loops

A normal `break` stops only the **nearest enclosing loop**.

```javascript
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        console.log(i, j);

        if (j === 2) {
            break;
        }
    }
}
```

Output:

```text
1 1
1 2
2 1
2 2
3 1
3 2
```

The inner loop stops when `j === 2`, but the outer loop continues.

---

# 9. Breaking Both Nested Loops

A normal `break` cannot directly stop multiple nested loops.

One approach is to use a flag:

```javascript
let found = false;

for (let i = 0; i < 3 && !found; i++) {
    for (let j = 0; j < 3; j++) {
        if (i === 1 && j === 2) {
            found = true;
            break;
        }

        console.log(i, j);
    }
}
```

The outer loop checks the flag and also stops.

---

# 10. Labeled `break`

JavaScript also supports labeled statements.

A label can allow `break` to exit an outer loop directly.

```javascript
outerLoop:
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        if (i === 2 && j === 2) {
            break outerLoop;
        }

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
```

When:

```javascript
i === 2 && j === 2
```

becomes true, `break outerLoop` exits the labeled outer loop.

> Labeled statements are valid JavaScript, but ordinary flags, functions, or better algorithm design are often easier to maintain.

---

# 11. `continue`

The `continue` statement skips the current iteration and moves to the next iteration of the loop.

### Syntax

```javascript
continue;
```

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

The value `3` is skipped.

---

# 12. `continue` with `while`

```javascript
let i = 0;

while (i < 5) {
    i++;

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

Notice that `i++` happens before `continue`.

This is important because the loop still needs to make progress.

---

# 13. `continue` with `do...while`

```javascript
let i = 0;

do {
    i++;

    if (i === 3) {
        continue;
    }

    console.log(i);
} while (i < 5);
```

Output:

```text
1
2
4
5
```

---

# 14. Print Only Even Numbers

`continue` can skip unwanted values.

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 !== 0) {
        continue;
    }

    console.log(i);
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

The odd numbers are skipped.

---

# 15. Print Only Odd Numbers

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        continue;
    }

    console.log(i);
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

# 16. Skip Invalid Values

Suppose an array contains some invalid values:

```javascript
const numbers = [10, -5, 20, -3, 30];

for (const number of numbers) {
    if (number < 0) {
        continue;
    }

    console.log(number);
}
```

Output:

```text
10
20
30
```

The negative values are ignored.

---

# 17. Skip Inactive Users

A practical backend-style example:

```javascript
const users = [
    { name: "Ram", isActive: true },
    { name: "Shyam", isActive: false },
    { name: "Hari", isActive: true }
];

for (const user of users) {
    if (!user.isActive) {
        continue;
    }

    console.log(`Processing ${user.name}`);
}
```

Output:

```text
Processing Ram
Processing Hari
```

The inactive user is skipped.

---

# 18. Hotel Management Example

Suppose some tables are unavailable.

```javascript
const tables = [
    { number: 1, status: "available" },
    { number: 2, status: "occupied" },
    { number: 3, status: "maintenance" },
    { number: 4, status: "available" }
];

for (const table of tables) {
    if (table.status !== "available") {
        continue;
    }

    console.log(`Table ${table.number} is available`);
}
```

Output:

```text
Table 1 is available
Table 4 is available
```

---

# 19. `break` vs `continue`

| Feature                 | `break`             | `continue`         |
| ----------------------- | ------------------- | ------------------ |
| Stops loop              | Yes                 | No                 |
| Skips current iteration | Yes, by ending loop | Yes                |
| Next iteration runs     | No                  | Yes                |
| Common use              | Stop searching      | Skip unwanted data |

### Example

`break`:

```javascript
for (let i = 1; i <= 5; i++) {
    if (i === 3) {
        break;
    }

    console.log(i);
}
```

Output:

```text
1
2
```

`continue`:

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

---

# 20. `break` vs `return`

These are different.

### `break`

Stops the loop but continues executing the function after the loop.

```javascript
function test() {
    for (let i = 1; i <= 5; i++) {
        if (i === 3) {
            break;
        }

        console.log(i);
    }

    console.log("Function continues");
}

test();
```

Output:

```text
1
2
Function continues
```

### `return`

Exits the entire function.

```javascript
function test() {
    for (let i = 1; i <= 5; i++) {
        if (i === 3) {
            return;
        }

        console.log(i);
    }

    console.log("This will not execute");
}

test();
```

Output:

```text
1
2
```

---

# 21. `continue` vs `return`

`continue` skips one loop iteration:

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

`return` exits the entire function:

```javascript
function test() {
    for (let i = 1; i <= 5; i++) {
        if (i === 3) {
            return;
        }

        console.log(i);
    }
}

test();
```

Output:

```text
1
2
```

---

# 22. `break` with `for...of`

```javascript
const fruits = ["Apple", "Banana", "Mango", "Orange"];

for (const fruit of fruits) {
    console.log(fruit);

    if (fruit === "Mango") {
        break;
    }
}
```

Output:

```text
Apple
Banana
Mango
```

---

# 23. `continue` with `for...of`

```javascript
const fruits = ["Apple", "Banana", "Mango", "Orange"];

for (const fruit of fruits) {
    if (fruit === "Mango") {
        continue;
    }

    console.log(fruit);
}
```

Output:

```text
Apple
Banana
Orange
```

---

# 24. `break` with `for...in`

```javascript
const user = {
    name: "Sandip",
    age: 22,
    role: "developer"
};

for (const key in user) {
    console.log(key);

    if (key === "age") {
        break;
    }
}
```

The loop stops when the specified
