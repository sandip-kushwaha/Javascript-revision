# JavaScript `do...while` Loop

The `do...while` loop is used to execute a block of code **at least once**, and then continue executing it as long as a condition is `true`.

The main difference from a `while` loop is:

* `while` checks the condition **before** execution.
* `do...while` checks the condition **after** execution.

---

# 1. Basic Syntax

```javascript
do {
    // code to execute
} while (condition);
```

Example:

```javascript
let count = 1;

do {
    console.log(count);

    count++;
} while (count <= 5);
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

# 2. How `do...while` Works

The execution order is:

```text
Start
  ↓
Execute code
  ↓
Update value
  ↓
Check condition
  ↓
true ─────→ Execute again
  ↓
false
  ↓
Stop
```

Example:

```javascript
let i = 1;

do {
    console.log(i);

    i++;
} while (i <= 3);
```

Execution:

```text
i = 1 → print 1
i = 2 → print 2
i = 3 → print 3
i = 4 → condition false → stop
```

---

# 3. Important Difference from `while`

Consider this example:

```javascript
let i = 10;

while (i < 5) {
    console.log(i);
}
```

Nothing is printed because the condition is checked first:

```text
10 < 5
```

is `false`.

Now:

```javascript
let i = 10;

do {
    console.log(i);
} while (i < 5);
```

Output:

```text
10
```

Why?

Because the `do` block executes **before** the condition is checked.

---

# 4. `while` vs `do...while`

| Feature                    | `while`               | `do...while`             |
| -------------------------- | --------------------- | ------------------------ |
| Condition checked          | Before execution      | After execution          |
| Minimum executions         | 0                     | 1                        |
| Guaranteed first execution | No                    | Yes                      |
| Syntax                     | `while`               | `do...while`             |
| Useful for                 | Condition-first loops | Must-run-once operations |

---

# 5. Basic Counting

```javascript
let i = 1;

do {
    console.log(i);

    i++;
} while (i <= 5);
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

# 6. Counting Backward

```javascript
let i = 5;

do {
    console.log(i);

    i--;
} while (i >= 1);
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

# 7. Increment by 2

```javascript
let i = 0;

do {
    console.log(i);

    i += 2;
} while (i <= 10);
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

# 8. Decrement by 2

```javascript
let i = 10;

do {
    console.log(i);

    i -= 2;
} while (i >= 0);
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

# 9. Condition Initially False

This is the most important example.

```javascript
let i = 10;

do {
    console.log("Hello");

    i++;
} while (i < 5);
```

Output:

```text
Hello
```

Even though:

```javascript
i < 5
```

is false, the code inside `do` executes once.

---

# 10. `do...while` with `break`

`break` immediately stops the loop.

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

When `i` becomes `3`, `break` stops the loop.

---

# 11. `do...while` with `continue`

`continue` skips the current iteration.

However, be careful with `continue` in a `do...while` loop because the condition is checked after the loop body.

Example:

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

The value `3` is skipped.

### Important

Always make sure the loop variable is updated before `continue` when necessary.

---

# 12. Multiplication Table

```javascript
let i = 1;

do {
    console.log(`5 × ${i} = ${5 * i}`);

    i++;
} while (i <= 10);
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

# 13. Sum of Numbers

Calculate the sum from `1` to `5`.

```javascript
let i = 1;
let sum = 0;

do {
    sum += i;

    i++;
} while (i <= 5);

console.log(sum);
```

Output:

```text
15
```

---

# 14. Even Numbers

```javascript
let i = 1;

do {
    if (i % 2 === 0) {
        console.log(i);
    }

    i++;
} while (i <= 10);
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

# 15. Odd Numbers

```javascript
let i = 1;

do {
    if (i % 2 !== 0) {
        console.log(i);
    }

    i++;
} while (i <= 10);
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

# 16. Arrays with `do...while`

You can use a `do...while` loop to process an array.

```javascript
const fruits = ["Apple", "Banana", "Mango"];

let i = 0;

do {
    console.log(fruits[i]);

    i++;
} while (i < fruits.length);
```

Output:

```text
Apple
Banana
Mango
```

### Important Edge Case

Because `do...while` executes once before checking the condition, an empty array requires extra care.

For example:

```javascript
const fruits = [];

let i = 0;

do {
    console.log(fruits[i]);

    i++;
} while (i < fruits.length);
```

This prints:

```text
undefined
```

For arrays where zero iterations may be appropriate, a `while` loop or `for...of` may be more suitable.

---

# 17. String with `do...while`

```javascript
const text = "JavaScript";

let i = 0;

do {
    console.log(text[i]);

    i++;
} while (i < text.length);
```

Output:

```text
J
a
v
a
S
c
r
i
p
t
```

---

# 18. User Input Example

A common use case is repeatedly asking for input until the user provides an acceptable value.

```javascript
let answer;

do {
    answer = prompt("Enter yes or no:");
} while (answer !== "yes" && answer !== "no");

console.log(`You entered: ${answer}`);
```

The user gets at least one opportunity to provide input.

> `prompt()` is available in browsers, not by default in Node.js.

---

# 19. Menu Example

A menu system is a classic use case for `do...while`.

```javascript
let choice;

do {
    console.log("1. View Menu");
    console.log("2. Place Order");
    console.log("3. Exit");

    choice = prompt("Enter your choice:");
} while (choice !== "3");

console.log("Application closed.");
```

The menu appears at least once.

---

# 20. Hotel Management Example

Imagine a hotel ordering system with a menu:

```javascript
let choice;

do {
    console.log("===== HOTEL MENU =====");
    console.log("1. View Food");
    console.log("2. View Tables");
    console.log("3. Place Order");
    console.log("4. Exit");

    choice = prompt("Select an option:");
} while (choice !== "4");

console.log("Thank you.");
```

This demonstrates why `do...while` can be useful for menu-driven applications.

---

# 21. Login Attempt Example

Suppose a user must enter a password at least once.

```javascript
let password;

do {
    password = prompt("Enter password:");
} while (password !== "1234");

console.log("Login successful");
```

The user must enter the password at least once.

> In a real application, passwords should never be hard-coded or handled this way. This is only a loop example.

---

# 22. Retry Logic

Conceptually, `do...while` can represent an operation that must happen once and may need to be repeated.

```javascript
let success = false;

do {
    console.log("Trying operation...");

    // operation would happen here

    success = true;
} while (!success);

console.log("Operation completed");
```

For real asynchronous retry logic, use Promises and `async/await` rather than blocking JavaScript execution.

---

# 23. Nested `do...while`

A `do...while` loop can be nested.

```javascript
let i = 1;

do {
    let j = 1;

    do {
        console.log(`i = ${i}, j = ${j}`);

        j++;
    } while (j <= 3);

    i++;
} while (i <= 3);
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

---

# 24. Infinite `do...while` Loop

Be careful when the condition never becomes false.

```javascript
let i = 1;

do {
    console.log(i);
} while (i <= 5);
```

This is an infinite loop because `i` never changes.

### Correct

```javascript
let i = 1;

do {
    console.log(i);

    i++;
} while (i <= 5);
```

---

# 25. Common Infinite Loop Mistake

### Wrong

```javascript
let count = 1;

do {
    console.log(count);

} while (count <= 10);
```

`count` never changes.

### Correct

```javascript
let count = 1;

do {
    console.log(count);

    count++;
} while (count <= 10);
```

---

# 26. `do...while` vs `while` Example

### `while`

```javascript
let number = 10;

while (number < 5) {
    console.log("while");
}
```

Output:

```text
Nothing
```

### `do...while`

```javascript
let number = 10;

do {
    console.log("do...while");
} while (number < 5);
```

Output:

```text
do...while
```

### Why?

`while`:

```text
Check → Execute
```

`do...while`:

```text
Execute → Check
```

---

# 27. `do...while` Syntax Detail

Notice the semicolon at the end:

```javascript
do {
    // code
} while (condition);
```

The semicolon after `while (condition)` is part of the syntax.

---

# 28. When Should You Use `do...while`?

Use `do...while` when the operation should happen **at least once**.

Common examples:

* Menus
* User input
* Validation
* Retry operations
* Interactive programs
* Repeated choices

Example:

```javascript
let choice;

do {
    choice = prompt("Choose an option:");
} while (choice !== "exit");
```

---

# 29. When Should You NOT Use `do...while`?

If zero executions are valid, a `while` loop is often clearer.

For example:

```javascript
const numbers = [];

let i = 0;

while (i < numbers.length) {
    console.log(numbers[i]);

    i++;
}
```

This correctly executes zero times for an empty array.

With `do...while`, the body executes once even when the array is empty.

---

# 30. `for` vs `while` vs `do...while`

| Loop         | Minimum Executions | Condition |
| ------------ | -----------------: | --------- |
| `for`        |                  0 | Before    |
| `while`      |                  0 | Before    |
| `do...while` |                  1 | After     |

### Example

```javascript
// for
for (let i = 0; i < 0; i++) {
    console.log(i);
}
```

```javascript
// while
let i = 0;

while (i < 0) {
    console.log(i);
}
```

Both execute zero times.

But:

```javascript
// do...while
let j = 0;

do {
    console.log(j);
} while (j < 0);
```

prints:

```text
0
```

---

# 31. Common Mistakes

## Mistake 1: Forgetting the Update

```javascript
let i = 1;

do {
    console.log(i);
} while (i <= 5);
```

This creates an infinite loop.

### Fix

```javascript
let i = 1;

do {
    console.log(i);

    i++;
} while (i <= 5);
```

---

## Mistake 2: Expecting Zero Executions

```javascript
let i = 10;

do {
    console.log(i);
} while (i < 5);
```

This still prints:

```text
10
```

because the body always executes once.

---

## Mistake 3: Forgetting the Semicolon

Use:

```javascript
do {
    // code
} while (condition);
```

not:

```javascript
do {
    // code
} while (condition)
```

# 32. Quick Revision

### Basic Syntax

```javascript
do {
    // code
} while (condition);
```

### Counting

```javascript
let i = 1;

do {
    console.log(i);

    i++;
} while (i <= 5);
```

### `break`

```javascript
do {
    if (condition) {
        break;
    }
} while (condition);
```

### `continue`

```javascript
do {
    // update when necessary

    if (condition) {
        continue;
    }
} while (condition);
```

### Important Rule

```text
while:
    Check → Execute

do...while:
    Execute → Check
```

---

# 33. Key Takeaways

* `do...while` executes the body **at least once**.
* The condition is checked **after** execution.
* It is different from `while`.
* `while` can execute zero times.
* `do...while` always executes at least once.
* `break` stops the loop.
* `continue` skips the current iteration.
* Always make sure the loop can eventually stop.
* `do...while` is useful for menus and user input.
* Be careful when using it with empty arrays or collections.
* A `do...while` loop can be nested.
* The syntax ends with a semicolon:

  ```javascript
  } while (condition);
  ```

---
