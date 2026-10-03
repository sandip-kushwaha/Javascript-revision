# JavaScript Stack

A **Stack** is a data structure that follows the:

```text
LIFO
```

principle.

**LIFO = Last In, First Out**

The element added most recently is the first element removed.

---

# 1. What is a Stack?

Think about a stack of plates:

```text
    ┌───────┐
    │ Plate │ ← Last added
    ├───────┤
    │ Plate │
    ├───────┤
    │ Plate │
    └───────┘
```

You normally remove the top plate first.

The same idea applies to a Stack.

```text
Push → Add
Pop  → Remove
```

---

# 2. LIFO Principle

Suppose we add:

```js
push("A");
push("B");
push("C");
```

The Stack becomes:

```text
Top
 ↓
C
B
A
```

If we remove one:

```js
pop();
```

`C` is removed first.

Then:

```text
Top
 ↓
B
A
```

So:

```text
Last In → First Out
```

---

# 3. JavaScript Does Not Have a Built-in Stack Class

JavaScript does not provide a dedicated:

```js
new Stack();
```

Instead, an `Array` can easily be used as a Stack.

```js
const stack = [];
```

Use:

```text
push() → add
pop()  → remove
```

---

# 4. push()

`push()` adds an element to the top of the Stack.

```js
const stack = [];

stack.push("A");
stack.push("B");
stack.push("C");

console.log(stack);
```

Result:

```js
[
  "A",
  "B",
  "C"
]
```

The top is:

```text
C
```

---

# 5. pop()

`pop()` removes and returns the last element.

```js
const stack = [
  "A",
  "B",
  "C",
];

const item = stack.pop();

console.log(item);
// C

console.log(stack);
```

Result:

```js
[
  "A",
  "B"
]
```

Because `C` was the last element added.

---

# 6. Stack Top

With an array-based Stack, the top is usually the last element.

```js
const stack = [
  "A",
  "B",
  "C",
];

const top = stack[stack.length - 1];

console.log(top);
// C
```

You can also create a helper:

```js
function peek(stack) {
  return stack[stack.length - 1];
}
```

---

# 7. peek()

`peek()` means:

```text
Look at the top without removing it.
```

JavaScript arrays do not have a built-in `peek()` method, so we can create one.

```js
const stack = [
  "A",
  "B",
  "C",
];

function peek(stack) {
  return stack[stack.length - 1];
}

console.log(peek(stack));
// C

console.log(stack);
```

The Stack remains unchanged.

---

# 8. Checking if a Stack Is Empty

Use:

```js
stack.length === 0
```

Example:

```js
const stack = [];

console.log(stack.length === 0);
// true
```

After adding:

```js
stack.push("A");

console.log(stack.length === 0);
// false
```

Helper:

```js
function isEmpty(stack) {
  return stack.length === 0;
}
```

---

# 9. Basic Stack Operations

A Stack commonly provides:

```text
push()
    ↓
Add item

pop()
    ↓
Remove top item

peek()
    ↓
View top item

isEmpty()
    ↓
Check whether empty
```

With JavaScript arrays:

```js
stack.push(value);
stack.pop();
stack[stack.length - 1];
stack.length === 0;
```

---

# 10. Stack Example

```js
const stack = [];

stack.push("HTML");
stack.push("CSS");
stack.push("JavaScript");

console.log(stack);
```

Stack:

```text
Top
 ↓
JavaScript
CSS
HTML
```

Now:

```js
console.log(stack.pop());
```

Output:

```text
JavaScript
```

Remaining:

```text
Top
 ↓
CSS
HTML
```

---

# 11. Stack Class

For learning data structures, we can create a Stack class.

```js
class Stack {
  constructor() {
    this.items = [];
  }

  push(value) {
    this.items.push(value);
  }

  pop() {
    return this.items.pop();
  }

  peek() {
    return this.items[
      this.items.length - 1
    ];
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}
```

Usage:

```js
const stack = new Stack();

stack.push("A");
stack.push("B");
stack.push("C");

console.log(stack.peek());
// C

console.log(stack.pop());
// C

console.log(stack.size());
// 2
```

---

# 12. Stack with Error Handling

You can decide what should happen when popping an empty Stack.

Simple version:

```js
class Stack {
  constructor() {
    this.items = [];
  }

  push(value) {
    this.items.push(value);
  }

  pop() {
    if (this.isEmpty()) {
      return undefined;
    }

    return this.items.pop();
  }

  peek() {
    if (this.isEmpty()) {
      return undefined;
    }

    return this.items[
      this.items.length - 1
    ];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

---

# 13. Stack Size

For an array-based Stack:

```js
const stack = [
  "A",
  "B",
  "C",
];

console.log(stack.length);
// 3
```

In a Stack class:

```js
size() {
  return this.items.length;
}
```

---

# 14. Stack Underflow

**Underflow** occurs when you try to remove an item from an empty Stack.

Example:

```js
const stack = [];

console.log(stack.pop());
```

For an empty JavaScript array, `pop()` returns:

```text
undefined
```

In a custom Stack implementation, you can choose to:

* Return `undefined`
* Return `null`
* Throw an error

For example:

```js
pop() {
  if (this.isEmpty()) {
    throw new Error("Stack is empty");
  }

  return this.items.pop();
}
```

---

# 15. Stack Overflow

In a fixed-size Stack, **overflow** occurs when trying to add an element beyond its capacity.

JavaScript arrays are dynamically sized, so a normal array-based Stack does not have a fixed capacity.

You can implement a capacity manually:

```js
class Stack {
  constructor(limit) {
    this.items = [];
    this.limit = limit;
  }

  push(value) {
    if (this.items.length >= this.limit) {
      throw new Error("Stack overflow");
    }

    this.items.push(value);
  }
}
```

Example:

```js
const stack = new Stack(2);

stack.push("A");
stack.push("B");

// stack.push("C");
// Error
```

---

# 16. Practical Example: Browser History

A Stack-like structure can help explain navigation history.

Suppose:

```text
Home
 ↓
Products
 ↓
Details
```

The most recent page is:

```text
Details
```

Going back removes the most recent navigation state.

Conceptually:

```js
historyStack.pop();
```

Real browsers use the History API and more complex mechanisms, but the Stack model helps understand the basic LIFO idea.

---

# 17. Practical Example: Undo

Undo functionality can be modeled using a Stack.

Suppose a user performs:

```text
Type "Hello"
Type " World"
Delete text
```

Each action can be stored:

```js
const undoStack = [];

undoStack.push("Type Hello");
undoStack.push("Type World");
undoStack.push("Delete text");
```

When the user clicks Undo:

```js
const lastAction = undoStack.pop();

console.log(lastAction);
// Delete text
```

The most recent action is undone first.

---

# 18. Practical Example: Function Calls

The JavaScript runtime uses a **call stack** to keep track of active function calls.

Example:

```js
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

When `three()` finishes:

```text
two()
one()
global
```

Then:

```text
one()
global
```

The Call Stack follows the LIFO principle.

---

# 19. Practical Example: Parentheses Checking

A Stack is useful for checking balanced parentheses.

Example:

```text
()
```

Balanced.

```text
(())
```

Balanced.

```text
(()
```

Not balanced.

One simple approach:

```js
function isBalanced(expression) {
  const stack = [];

  for (const char of expression) {
    if (char === "(") {
      stack.push(char);
    }

    if (char === ")") {
      if (stack.length === 0) {
        return false;
      }

      stack.pop();
    }
  }

  return stack.length === 0;
}
```

Example:

```js
console.log(
  isBalanced("(())")
);
// true

console.log(
  isBalanced("(()")
);
// false
```

---

# 20. Balanced Brackets

The same concept can be extended to:

```text
()
[]
{}
```

Example:

```js
function isBalanced(expression) {
  const stack = [];

  const pairs = {
    ")": "(",
    "]": "[",
    "}": "{",
  };

  for (const char of expression) {
    if (
      char === "(" ||
      char === "[" ||
      char === "{"
    ) {
      stack.push(char);
      continue;
    }

    if (
      char === ")" ||
      char === "]" ||
      char === "}"
    ) {
      const top = stack.pop();

      if (top !== pairs[char]) {
        return false;
      }
    }
  }

  return stack.length === 0;
}
```

Example:

```js
console.log(
  isBalanced("{[()]}")
);
// true

console.log(
  isBalanced("{[(]}")
);
// false
```

---

# 21. Stack Reversal

A Stack can be used to reverse values.

```js
const stack = [];

const word = "HELLO";

for (const char of word) {
  stack.push(char);
}

let reversed = "";

while (stack.length > 0) {
  reversed += stack.pop();
}

console.log(reversed);
// OLLEH
```

The last character added is removed first.

---

# 22. Stack and Recursion

Recursion naturally uses the JavaScript Call Stack.

Example:

```js
function countdown(number) {
  if (number === 0) {
    return;
  }

  console.log(number);

  countdown(number - 1);
}

countdown(3);
```

Conceptually:

```text
countdown(3)
countdown(2)
countdown(1)
countdown(0)
```

As each function returns, the previous call resumes.

---

# 23. Stack and DFS

Depth-First Search (**DFS**) commonly uses a Stack.

For example, when traversing a graph:

```text
A
├── B
│   ├── D
│   └── E
└── C
```

A DFS can use:

```js
const stack = ["A"];
```

Then repeatedly:

```text
1. Remove top
2. Process node
3. Add neighboring nodes
```

This allows the search to go deeper before exploring other branches.

---

# 24. Stack Complexity

For a typical array-based Stack where operations happen at the end:

| Operation   | Typical Complexity |
| ----------- | -----------------: |
| `push()`    |     O(1) amortized |
| `pop()`     |               O(1) |
| `peek()`    |               O(1) |
| `isEmpty()` |               O(1) |
| `size`      |               O(1) |

These are typical complexities for the operations shown.

---

# 25. Stack vs Queue

A Stack uses:

```text
LIFO
Last In → First Out
```

A Queue uses:

```text
FIFO
First In → First Out
```

Example Stack:

```text
A
B
C ← first removed
```

Example Queue:

```text
A ← first removed
B
C
```

Common Stack uses:

```text
Undo
Redo
Call stack
DFS
Expression evaluation
Parentheses matching
Backtracking
```

Common Queue uses:

```text
Task processing
Print queues
Request queues
BFS
Message processing
```

---

# 26. Stack vs Array

An Array is a general-purpose collection.

```js
const items = [
  "A",
  "B",
  "C",
];
```

A Stack is a **behavior/pattern** that restricts access to LIFO operations.

You can use an array to implement that behavior:

```js
items.push("D");
items.pop();
```

So:

```text
Array
→ general collection

Stack
→ LIFO data structure
```

---

# 27. Stack Implementation with Private Field

Modern JavaScript can use private class fields:

```js
class Stack {
  #items = [];

  push(value) {
    this.#items.push(value);
  }

  pop() {
    return this.#items.pop();
  }

  peek() {
    return this.#items[
      this.#items.length - 1
    ];
  }

  isEmpty() {
    return this.#items.length === 0;
  }
}
```

The internal array cannot be accessed directly from outside the class.

---

# 28. Stack Using Linked Nodes

A Stack does not have to use an array.

It can also be implemented using linked nodes.

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

Stack:

```js
class Stack {
  constructor() {
    this.top = null;
  }

  push(value) {
    const node = new Node(value);

    node.next = this.top;
    this.top = node;
  }

  pop() {
    if (!this.top) {
      return undefined;
    }

    const value = this.top.value;

    this.top = this.top.next;

    return value;
  }

  peek() {
    return this.top?.value;
  }
}
```

This implementation demonstrates the Stack concept without relying on an array.

---

# 29. Array Stack vs Linked Stack

| Feature        | Array Stack         | Linked Stack              |
| -------------- | ------------------- | ------------------------- |
| Storage        | Array               | Nodes                     |
| Implementation | Simpler             | More complex              |
| Push           | End of array        | New top node              |
| Pop            | End of array        | Top node                  |
| Random access  | Possible internally | Not typical               |
| Memory         | Array storage       | Node objects + references |
| Learning       | Easier              | Useful for DS concepts    |

For most JavaScript application code, an array is usually the simplest way to implement a Stack.

---

# 30. Quick Cheat Sheet

```js
const stack = [];

// Push
stack.push("A");
stack.push("B");
stack.push("C");

// Peek
const top =
  stack[stack.length - 1];

// Pop
const item = stack.pop();

// Is empty
const empty =
  stack.length === 0;

// Size
const size =
  stack.length;
```

The sequence:

```text
push A
push B
push C

Stack:
C ← top
B
A

pop()
↓
C removed

Stack:
B ← top
A
```

---

# 31. Key Takeaways

* A Stack follows **LIFO — Last In, First Out**.
* `push()` adds an item to the top.
* `pop()` removes the top item.
* `peek()` views the top without removing it.
* JavaScript arrays can easily implement Stacks.
* `stack.length === 0` checks whether a Stack is empty.
* The JavaScript Call Stack follows the Stack concept.
* Stacks are useful for undo operations, DFS, backtracking, and bracket matching.
* Stack overflow and underflow are common data-structure concepts.
* A Stack can be implemented using arrays or linked nodes.

### Remember

```text
STACK

        TOP
         ↓
       ┌───┐
       │ C │ ← Last In
       ├───┤
       │ B │
       ├───┤
       │ A │ ← First In
       └───┘

pop()
  ↓
Remove C

LIFO
Last In → First Out
```
