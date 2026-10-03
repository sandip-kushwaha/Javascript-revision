# JavaScript Recursion

**Recursion** is a programming technique where a function calls itself to solve a problem.

A recursive function usually has two important parts:

```text
Base Case
    ↓
Stops the recursion

Recursive Case
    ↓
Calls the function again
```

---

# 1. Basic Recursion

Example:

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    console.log(number);

    countDown(number - 1);
}

countDown(5);
```

Output:

```text
5
4
3
2
1
```

The function keeps calling itself until:

```javascript
number === 0
```

---

# 2. Base Case

The **base case** tells the function when to stop.

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    console.log(number);

    countDown(number - 1);
}
```

Here:

```javascript
if (number === 0) {
    return;
}
```

is the base case.

Without a base case, recursion may continue indefinitely.

---

# 3. Recursive Case

The recursive case is the part that calls the function again.

```javascript
countDown(number - 1);
```

Complete structure:

```javascript
function recursiveFunction(value) {
    if (baseCondition) {
        return;
    }

    // work

    recursiveFunction(newValue);
}
```

The important requirement is that the recursive call should eventually move toward the base case.

---

# 4. How Recursion Works

Consider:

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    console.log(number);

    countDown(number - 1);
}

countDown(3);
```

Execution:

```text
countDown(3)
    ↓
countDown(2)
    ↓
countDown(1)
    ↓
countDown(0)
    ↓
return
```

Then the calls return back through the call stack.

---

# 5. Recursion and the Call Stack

Every function call is placed on the call stack.

Example:

```javascript
function one() {
    two();
}

function two() {
    three();
}

function three() {
    console.log("Hello");
}

one();
```

Conceptually:

```text
three()
two()
one()
global
```

Recursive functions use the same call stack.

Example:

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    countDown(number - 1);
}
```

The stack grows as recursive calls are made.

---

# 6. Returning from Recursion

Recursion can also return values.

Example:

```javascript
function sum(number) {
    if (number === 1) {
        return 1;
    }

    return number + sum(number - 1);
}

console.log(sum(5));
```

Calculation:

```text
sum(5)
= 5 + sum(4)

= 5 + 4 + sum(3)

= 5 + 4 + 3 + sum(2)

= 5 + 4 + 3 + 2 + sum(1)

= 5 + 4 + 3 + 2 + 1

= 15
```

Output:

```text
15
```

---

# 7. Factorial

Factorial is a classic recursion example.

Mathematically:

```text
5! = 5 × 4 × 3 × 2 × 1
```

Recursive implementation:

```javascript
function factorial(number) {
    if (number === 0 || number === 1) {
        return 1;
    }

    return number * factorial(number - 1);
}

console.log(factorial(5));
```

Output:

```text
120
```

The recursive relationship is:

```text
factorial(n)
    =
n × factorial(n - 1)
```

---

# 8. Factorial Execution

For:

```javascript
factorial(4);
```

The calls are:

```text
factorial(4)
    ↓
4 × factorial(3)
        ↓
        3 × factorial(2)
                ↓
                2 × factorial(1)
                        ↓
                        1
```

Then the results return:

```text
1
2 × 1 = 2
3 × 2 = 6
4 × 6 = 24
```

Result:

```text
24
```

---

# 9. Recursive Array Sum

Recursion can process arrays.

```javascript
function sumArray(numbers, index = 0) {
    if (index === numbers.length) {
        return 0;
    }

    return (
        numbers[index] +
        sumArray(numbers, index + 1)
    );
}

const numbers = [10, 20, 30, 40];

console.log(sumArray(numbers));
```

Output:

```text
100
```

The recursion moves through the array one index at a time.

---

# 10. Find an Array Element Recursively

```javascript
function contains(numbers, target, index = 0) {
    if (index === numbers.length) {
        return false;
    }

    if (numbers[index] === target) {
        return true;
    }

    return contains(
        numbers,
        target,
        index + 1
    );
}
```

Usage:

```javascript
const numbers = [10, 20, 30, 40];

console.log(
    contains(numbers, 30)
);
```

Output:

```text
true
```

---

# 11. Recursive String Reversal

A string can also be processed recursively.

```javascript
function reverseString(text) {
    if (text.length <= 1) {
        return text;
    }

    return (
        reverseString(text.slice(1)) +
        text[0]
    );
}

console.log(
    reverseString("hello")
);
```

Output:

```text
olleh
```

The base case is:

```javascript
text.length <= 1
```

---

# 12. Recursive Countdown

A simple countdown:

```javascript
function countdown(number) {
    if (number <= 0) {
        console.log("Done");
        return;
    }

    console.log(number);

    countdown(number - 1);
}

countdown(5);
```

Output:

```text
5
4
3
2
1
Done
```

---

# 13. Recursion with Objects

Recursion is useful when data contains nested objects.

Example:

```javascript
const user = {
    name: "Sandip",
    address: {
        city: "Birgunj",
        location: {
            country: "Nepal"
        }
    }
};
```

A recursive function can inspect nested values.

```javascript
function printObject(object) {
    for (const key in object) {
        const value = object[key];

        if (
            typeof value === "object" &&
            value !== null
        ) {
            printObject(value);
        } else {
            console.log(key, value);
        }
    }
}

printObject(user);
```

Output:

```text
name Sandip
city Birgunj
country Nepal
```

---

# 14. Recursion with Nested Arrays

Consider:

```javascript
const numbers = [
    1,
    [2, 3],
    [4, [5, 6]]
];
```

A recursive function can process nested arrays.

```javascript
function flattenArray(array) {
    const result = [];

    for (const item of array) {
        if (Array.isArray(item)) {
            result.push(
                ...flattenArray(item)
            );
        } else {
            result.push(item);
        }
    }

    return result;
}

console.log(
    flattenArray(numbers)
);
```

Output:

```text
[1, 2, 3, 4, 5, 6]
```

---

# 15. Tree Structures

Recursion is especially useful for tree structures.

Example:

```text
        A
       / \
      B   C
     / \
    D   E
```

Each node can contain:

```text
value
children
```

Example:

```javascript
const tree = {
    value: "A",
    children: [
        {
            value: "B",
            children: [
                {
                    value: "D",
                    children: []
                },
                {
                    value: "E",
                    children: []
                }
            ]
        },
        {
            value: "C",
            children: []
        }
    ]
};
```

A recursive traversal:

```javascript
function printTree(node) {
    console.log(node.value);

    for (const child of node.children) {
        printTree(child);
    }
}

printTree(tree);
```

Output:

```text
A
B
D
E
C
```

---

# 16. File and Folder Structures

Recursion is useful for processing nested directories.

Conceptually:

```text
project/
├── src/
│   ├── components/
│   │   ├── Header.js
│   │   └── Footer.js
│   └── pages/
│       └── Home.js
└── package.json
```

A program can recursively:

```text
Open folder
    ↓
Check each item
    ↓
If folder → process recursively
    ↓
If file → process file
```

This pattern is common in:

* File systems
* Build tools
* Search tools
* Compilers
* Project analyzers

---

# 17. Recursive Tree Search

Example:

```javascript
function findNode(node, target) {
    if (node.value === target) {
        return node;
    }

    for (const child of node.children) {
        const result = findNode(
            child,
            target
        );

        if (result) {
            return result;
        }
    }

    return null;
}
```

Usage:

```javascript
const result = findNode(
    tree,
    "E"
);

console.log(result);
```

The function searches each node and recursively explores its children.

---

# 18. Recursion vs Loop

Many recursive problems can also be solved with loops.

### Loop

```javascript
for (
    let i = 5;
    i > 0;
    i--
) {
    console.log(i);
}
```

### Recursion

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    console.log(number);

    countDown(number - 1);
}

countDown(5);
```

Both can produce:

```text
5
4
3
2
1
```

The difference is how the repetition is represented.

---

# 19. When to Use Recursion

Recursion is particularly useful when a problem naturally contains smaller versions of itself.

Common examples:

```text
Tree traversal
Folder traversal
Nested objects
Nested arrays
Graph algorithms
Divide-and-conquer algorithms
Backtracking
Parsing
Searching nested structures
```

---

# 20. When a Loop Is Simpler

Do not use recursion automatically.

For simple repetition:

```javascript
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

A loop is usually easier to read than recursive code.

Use recursion when the problem structure benefits from it.

---

# 21. Infinite Recursion

Incorrect recursion can continue forever.

Example:

```javascript
function test() {
    test();
}

test();
```

There is no base case.

Eventually JavaScript throws an error similar to:

```text
RangeError: Maximum call stack size exceeded
```

---

# 22. Recursion Must Move Toward the Base Case

Bad:

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    countDown(number);
}
```

The value never changes.

Better:

```javascript
function countDown(number) {
    if (number === 0) {
        return;
    }

    countDown(number - 1);
}
```

Now each call moves closer to:

```text
0
```

---

# 23. Recursive Function Structure

A useful pattern is:

```javascript
function recursiveFunction(value) {
    // 1. Base case
    if (condition) {
        return result;
    }

    // 2. Process current value
    const result = process(value);

    // 3. Recursive call
    return recursiveFunction(
        smallerValue
    );
}
```

Think:

```text
Base case
    ↓
Current work
    ↓
Smaller problem
    ↓
Recursive call
```

---

# 24. Recursion and Memory

Each recursive call creates a new stack frame.

For example:

```javascript
function count(number) {
    if (number === 0) {
        return;
    }

    count(number - 1);
}
```

Calling:

```javascript
count(3);
```

creates calls similar to:

```text
count(3)
count(2)
count(1)
count(0)
```

These calls occupy stack space until they return.

Deep recursion can therefore consume significant memory.

---

# 25. Stack Overflow

If recursion becomes too deep:

```javascript
function infinite(number) {
    return infinite(number + 1);
}
```

the call stack eventually becomes full.

JavaScript then throws:

```text
RangeError:
Maximum call stack size exceeded
```

The exact recursion limit depends on the JavaScript engine and environment.

---

# 26. Tail Recursion

A tail-recursive function performs the recursive call as its final operation.

Example:

```javascript
function countDown(
    number
) {
    if (number === 0) {
        return;
    }

    console.log(number);

    return countDown(
        number - 1
    );
}
```

The recursive call is the final operation.

However, JavaScript engines generally do **not** provide reliable proper tail-call optimization in common environments, so tail recursion should not be assumed to avoid stack growth.

---

# 27. Recursion with Fibonacci

The Fibonacci sequence is commonly defined as:

```text
0
1
1
2
3
5
8
13
21
...
```

A simple recursive implementation:

```javascript
function fibonacci(number) {
    if (number <= 1) {
        return number;
    }

    return (
        fibonacci(number - 1) +
        fibonacci(number - 2)
    );
}

console.log(
    fibonacci(6)
);
```

Output:

```text
8
```

This demonstrates recursion, but this direct implementation becomes inefficient for larger inputs because it repeats many calculations.

---

# 28. Recursive Binary Search

Recursion can also be used for searching sorted arrays.

```javascript
function binarySearch(
    numbers,
    target,
    left = 0,
    right = numbers.length - 1
) {
    if (left > right) {
        return -1;
    }

    const middle =
        Math.floor(
            (left + right) / 2
        );

    if (numbers[middle] === target) {
        return middle;
    }

    if (target < numbers[middle]) {
        return binarySearch(
            numbers,
            target,
            left,
            middle - 1
        );
    }

    return binarySearch(
        numbers,
        target,
        middle + 1,
        right
    );
}
```

Example:

```javascript
const numbers = [
    10, 20, 30, 40, 50
];

console.log(
    binarySearch(numbers, 40)
);
```

Output:

```text
3
```

The search space becomes smaller after every recursive call.

---

# 29. Recursion and Divide and Conquer

Some algorithms repeatedly divide a problem into smaller problems.

General structure:

```text
Large Problem
      ↓
Split
 ┌────┴────┐
Small    Small
Problem  Problem
   ↓        ↓
Solve    Solve
   └────┬───┘
        ↓
     Combine
```

Examples include:

```text
Merge Sort
Quick Sort
Binary Search
```

Recursion is commonly used to represent this structure.

---

# 30. Recursion in React

React applications can contain recursive components when rendering nested data.

Example:

```jsx
function TreeNode({ node }) {
    return (
        <li>
            {node.value}

            {node.children.length > 0 && (
                <ul>
                    {node.children.map(
                        (child) => (
                            <TreeNode
                                key={child.value}
                                node={child}
                            />
                        )
                    )}
                </ul>
            )}
        </li>
    );
}
```

This is useful for:

```text
File explorers
Nested comments
Category trees
Menus
Organization structures
```

---

# 31. Practical Example — Nested Categories

Consider:

```javascript
const categories = [
    {
        name: "Electronics",
        children: [
            {
                name: "Phones",
                children: []
            },
            {
                name: "Laptops",
                children: []
            }
        ]
    },
    {
        name: "Food",
        children: []
    }
];
```

Recursive rendering can process every category:

```javascript
function printCategories(categories) {
    for (const category of categories) {
        console.log(category.name);

        if (category.children.length > 0) {
            printCategories(
                category.children
            );
        }
    }
}

printCategories(categories);
```

Output:

```text
Electronics
Phones
Laptops
Food
```

---

# 32. Recursion Checklist

When writing a recursive function, ask:

```text
1. What is the base case?
2. What is the recursive case?
3. Does each call move toward the base case?
4. What value should be returned?
5. How much stack space can it use?
```

A good recursive function should have a clear stopping condition.

---

# 33. Common Recursive Patterns

### Countdown

```javascript
function count(n) {
    if (n === 0) return;

    console.log(n);

    count(n - 1);
}
```

### Accumulation

```javascript
function sum(n) {
    if (n === 0) return 0;

    return n + sum(n - 1);
}
```

### Tree Traversal

```javascript
function traverse(node) {
    console.log(node.value);

    for (const child of node.children) {
        traverse(child);
    }
}
```

### Nested Data

```javascript
function process(items) {
    for (const item of items) {
        if (item.children) {
            process(item.children);
        }
    }
}
```

---

# 34. Recursion Advantages

Recursion can make some problems easier to express.

Advantages:

* Natural for tree structures.
* Useful for nested data.
* Useful for divide-and-conquer algorithms.
* Can make traversal code easier to understand.
* Useful for backtracking algorithms.
* Closely matches mathematical definitions.

---

# 35. Recursion Disadvantages

Recursion also has costs:

* Uses call stack memory.
* Deep recursion can cause stack overflow.
* Sometimes slower than an iterative solution.
* Can be harder to debug.
* Repeated recursive calculations can be inefficient.
* A missing or incorrect base case can cause infinite recursion.

---

# 36. Recursion vs Iteration

| Recursion                            | Iteration                               |
| ------------------------------------ | --------------------------------------- |
| Function calls itself                | Loop repeats code                       |
| Uses call stack                      | Usually uses less stack memory          |
| Natural for trees                    | Simple repetition is often easier       |
| Can be elegant for nested structures | Often easier to optimize                |
| Deep recursion can overflow stack    | Loops generally avoid call-stack growth |

---

# 37. Key Takeaways

* Recursion means a function calls itself.
* Every recursive function needs a stopping condition.
* The stopping condition is called the **base case**.
* The part that calls the function again is the **recursive case**.
* Recursive calls use the JavaScript call stack.
* Each recursive call should move toward the base case.
* Missing or incorrect base cases can cause infinite recursion.
* Deep recursion can cause a stack overflow.
* Recursion is especially useful for trees and nested structures.
* Loops are often simpler for straightforward repetition.
* Tail recursion should not be assumed to eliminate stack usage in JavaScript.
* Recursive algorithms are common in searching, sorting, traversal, and backtracking.

---

# Quick Cheat Sheet

```text
Recursion
    ↓
Function calls itself
    ↓
Base Case
    ↓
Stops recursion

Recursive Case
    ↓
Calls function again
    ↓
Moves toward Base Case
```

Basic pattern:

```javascript
function recursiveFunction(value) {
    if (baseCondition) {
        return result;
    }

    return recursiveFunction(
        smallerValue
    );
}
```

Remember:

```text
Base Case
→ Stop

Recursive Case
→ Continue

Smaller Problem
→ Move toward the Base Case
```

---
