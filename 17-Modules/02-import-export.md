# JavaScript Import and Export

`import` and `export` are used to share code between JavaScript modules.

They allow you to organize large applications into multiple files instead of putting everything into one file.

Example:

```text
project/
├── math.js
├── user.js
└── app.js
```

You can export functions from `math.js` and import them into `app.js`.

---

# 1. Named Export

A **named export** allows you to export one or more values by name.

```javascript
export const name = "Sandip";

export const age = 22;
```

You can also export functions:

```javascript
export function add(a, b) {
  return a + b;
}
```

---

# 2. Named Import

Named exports are imported using `{ }`.

Suppose `math.js` contains:

```javascript
export const add = (a, b) => {
  return a + b;
};
```

Import it:

```javascript
import { add } from "./math.js";
```

Use it:

```javascript
console.log(add(10, 20));
```

Output:

```text
30
```

---

# 3. Export Multiple Values

You can export multiple values from one module.

```javascript
export const name = "Sandip";

export const age = 22;

export function greet() {
  console.log("Hello");
}
```

Import them:

```javascript
import {
  name,
  age,
  greet,
} from "./user.js";
```

Use them:

```javascript
console.log(name);
console.log(age);

greet();
```

---

# 4. Export at the Bottom

Instead of adding `export` before every declaration, you can export them together.

```javascript
const name = "Sandip";

const age = 22;

function greet() {
  console.log("Hello");
}

export {
  name,
  age,
  greet,
};
```

This is useful when a file contains many declarations.

---

# 5. Import Only What You Need

Suppose:

```javascript
export const add = (a, b) => a + b;

export const subtract = (a, b) => a - b;

export const multiply = (a, b) => a * b;
```

You can import only `add`:

```javascript
import { add } from "./math.js";
```

You don't need to import everything.

---

# 6. Import Multiple Named Exports

```javascript
import {
  add,
  subtract,
  multiply,
} from "./math.js";
```

Then:

```javascript
console.log(add(10, 5));
console.log(subtract(10, 5));
console.log(multiply(10, 5));
```

---

# 7. Aliasing Named Imports

You can rename an imported value using `as`.

Example:

```javascript
import {
  add as sum,
} from "./math.js";
```

Now use:

```javascript
console.log(sum(10, 20));
```

The original exported name is:

```text
add
```

The local name is:

```text
sum
```

---

# 8. Aliasing Multiple Imports

```javascript
import {
  add as sum,
  subtract as difference,
  multiply as product,
} from "./math.js";
```

Usage:

```javascript
console.log(sum(10, 5));

console.log(difference(10, 5));

console.log(product(10, 5));
```

---

# 9. Aliasing Exports

You can also rename values when exporting them.

```javascript
const username = "Sandip";

export {
  username as name,
};
```

Now another file can import:

```javascript
import { name } from "./user.js";
```

---

# 10. Default Export

A module can have one default export.

```javascript
const user = {
  name: "Sandip",
  age: 22,
};

export default user;
```

Import it without `{ }`:

```javascript
import user from "./user.js";
```

Use it:

```javascript
console.log(user.name);
```

---

# 11. Default Export Function

You can directly export a function as the default export.

```javascript
export default function greet() {
  console.log("Hello Sandip");
}
```

Import:

```javascript
import greet from "./greet.js";
```

Use:

```javascript
greet();
```

---

# 12. Default Export Class

```javascript
export default class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello ${this.name}`);
  }
}
```

Import:

```javascript
import User from "./User.js";
```

Create an object:

```javascript
const user = new User("Sandip");

user.greet();
```

---

# 13. Default Import Can Be Renamed

Suppose:

```javascript
export default function greet() {
  console.log("Hello");
}
```

You can import it as:

```javascript
import sayHello from "./greet.js";
```

This works because default imports choose their local name.

You could technically write:

```javascript
import hello from "./greet.js";
```

But keeping the imported name meaningful makes code easier to understand.

---

# 14. Named vs Default Import

### Named Export

```javascript
export const add = () => {};
```

Import:

```javascript
import { add } from "./math.js";
```

### Default Export

```javascript
export default add;
```

Import:

```javascript
import add from "./math.js";
```

Main difference:

```text
Named export
    ↓
Uses { }

Default export
    ↓
Does not use { }
```

---

# 15. Default and Named Exports Together

A module can have:

```text
1 default export
+
multiple named exports
```

Example:

```javascript
const user = {
  name: "Sandip",
};

const role = "developer";

function greet() {
  console.log("Hello");
}

export default user;

export {
  role,
  greet,
};
```

Import:

```javascript
import user, {
  role,
  greet,
} from "./user.js";
```

Usage:

```javascript
console.log(user.name);

console.log(role);

greet();
```

---

# 16. Namespace Import

You can import all exports under one namespace.

Example:

```javascript
export const add = (a, b) => a + b;

export const subtract = (a, b) => a - b;
```

Import:

```javascript
import * as math from "./math.js";
```

Use:

```javascript
console.log(math.add(10, 5));

console.log(math.subtract(10, 5));
```

The namespace object groups the module's exports.

---

# 17. Namespace Import with Default Export

Suppose:

```javascript
export default function greet() {
  console.log("Hello");
}

export const name = "Sandip";
```

Import:

```javascript
import * as module from "./user.js";
```

Access the default export:

```javascript
module.default();
```

Access named exports:

```javascript
console.log(module.name);
```

For normal code, a direct default import is usually clearer:

```javascript
import greet, {
  name,
} from "./user.js";
```

---

# 18. Side-Effect Import

Sometimes you want to execute a module without importing a particular value.

Example:

```javascript
import "./setup.js";
```

The module is loaded and evaluated for its side effects.

Common examples:

```javascript
import "./styles.css";
```

or:

```javascript
import "./initialize.js";
```

This pattern is common in frontend applications.

---

# 19. Re-Exporting

A module can export something that comes from another module.

Suppose:

```text
math.js
```

contains:

```javascript
export const add = (a, b) => a + b;
```

Another file can re-export it:

```javascript
export {
  add,
} from "./math.js";
```

Now another module can import from the re-exporting file.

---

# 20. Re-Export Multiple Values

```javascript
export {
  add,
  subtract,
  multiply,
} from "./math.js";
```

This avoids importing and then exporting separately.

Instead of:

```javascript
import {
  add,
  subtract,
} from "./math.js";

export {
  add,
  subtract,
};
```

you can write:

```javascript
export {
  add,
  subtract,
} from "./math.js";
```

---

# 21. Re-Export with Alias

You can rename a value while re-exporting.

```javascript
export {
  add as sum,
} from "./math.js";
```

Now another file can use:

```javascript
import { sum } from "./index.js";
```

---

# 22. Re-Export Default Export

Suppose:

```javascript
// User.js

export default class User {
  constructor(name) {
    this.name = name;
  }
}
```

You can re-export the default:

```javascript
export {
  default,
} from "./User.js";
```

Another file can then import:

```javascript
import User from "./index.js";
```

---

# 23. Rename a Default Export During Re-Export

A common pattern is:

```javascript
export {
  default as User,
} from "./User.js";
```

Then:

```javascript
import { User } from "./index.js";
```

This is useful when creating a central export file.

---

# 24. `export *`

You can re-export all named exports from another module.

```javascript
export * from "./math.js";
```

If `math.js` contains:

```javascript
export const add = () => {};

export const subtract = () => {};
```

then both can be imported from the re-exporting module:

```javascript
import {
  add,
  subtract,
} from "./index.js";
```

`export *` does not re-export the default export.

---

# 25. Barrel File

A **barrel file** is a central module that re-exports values from multiple modules.

Example:

```text
components/
├── Button.jsx
├── Card.jsx
├── Modal.jsx
└── index.js
```

`index.js`:

```javascript
export {
  default as Button,
} from "./Button.jsx";

export {
  default as Card,
} from "./Card.jsx";

export {
  default as Modal,
} from "./Modal.jsx";
```

Now instead of:

```javascript
import Button from "./components/Button.jsx";

import Card from "./components/Card.jsx";

import Modal from "./components/Modal.jsx";
```

you can write:

```javascript
import {
  Button,
  Card,
  Modal,
} from "./components/index.js";
```

Depending on your project setup, you may also import from the directory:

```javascript
import {
  Button,
  Card,
  Modal,
} from "./components";
```

Bundler and runtime resolution rules determine whether directory imports work.

---

# 26. Import Paths

Common import paths include:

```javascript
import { add } from "./math.js";
```

Current directory:

```text
./
```

Parent directory:

```javascript
import User from "../User.js";
```

Parent directory:

```text
../
```

Package/module:

```javascript
import express from "express";
```

So:

```text
./file.js     → current directory
../file.js    → parent directory
package-name  → package/module resolution
```

---

# 27. File Extensions

In native browser ES Modules, relative imports are resolved as URLs.

Usually write:

```javascript
import { add } from "./math.js";
```

In Node.js ESM, relative imports generally require the file extension:

```javascript
import { add } from "./math.js";
```

Bundlers such as Vite can provide more flexible resolution:

```javascript
import { add } from "./math";
```

The exact behavior depends on the environment and configuration.

---

# 28. Common Import Error

Suppose the module exports:

```javascript
export const add = () => {};
```

Incorrect:

```javascript
import add from "./math.js";
```

Why?

Because `add` is a named export, not a default export.

Correct:

```javascript
import { add } from "./math.js";
```

---

# 29. Another Common Error

Suppose:

```javascript
export default function greet() {}
```

Incorrect:

```javascript
import { greet } from "./greet.js";
```

Correct:

```javascript
import greet from "./greet.js";
```

The default export does not use braces.

---

# 30. Named and Default Syntax Comparison

| Export                             | Import                                            |
| ---------------------------------- | ------------------------------------------------- |
| `export const add = ...`           | `import { add } from "./math.js"`                 |
| `export function add() {}`         | `import { add } from "./math.js"`                 |
| `export default add`               | `import add from "./math.js"`                     |
| `export default function add() {}` | `import add from "./math.js"`                     |
| `export { add as sum }`            | `import { sum } from "./math.js"`                 |
| `export * from "./math.js"`        | Import named exports from the re-exporting module |

---

# 31. React Example

Suppose:

```text
src/
├── components/
│   ├── Header.jsx
│   └── Button.jsx
└── App.jsx
```

`Header.jsx`:

```jsx
export default function Header() {
  return <header>My App</header>;
}
```

`Button.jsx`:

```jsx
export default function Button() {
  return <button>Click</button>;
}
```

`App.jsx`:

```jsx
import Header from "./components/Header.jsx";

import Button from "./components/Button.jsx";

function App() {
  return (
    <>
      <Header />
      <Button />
    </>
  );
}

export default App;
```

---

# 32. React Named Export Example

`utils.js`:

```javascript
export function formatPrice(price) {
  return `$${price}`;
}

export function formatName(name) {
  return name.trim();
}
```

Component:

```jsx
import {
  formatPrice,
  formatName,
} from "./utils.js";
```

Use:

```jsx
const price = formatPrice(500);

const name = formatName(" Sandip ");
```

---

# 33. Node.js Example

`math.js`:

```javascript
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

`app.js`:

```javascript
import {
  add,
  subtract,
} from "./math.js";

console.log(add(10, 5));

console.log(subtract(10, 5));
```

If using Node.js ESM, configure the project appropriately, for example with:

```json
{
  "type": "module"
}
```

---

# 34. Express Example

`user.controller.js`:

```javascript
export const getUsers = async (req, res) => {
  res.json({
    message: "Users",
  });
};
```

`user.routes.js`:

```javascript
import express from "express";

import {
  getUsers,
} from "./user.controller.js";

const router = express.Router();

router.get(
  "/users",
  getUsers
);

export default router;
```

`app.js`:

```javascript
import express from "express";

import userRouter from "./user.routes.js";

const app = express();

app.use(
  "/api",
  userRouter
);

export default app;
```

This keeps routes, controllers, and application setup in separate modules.

---

# 35. Dynamic Import

Static imports are normally written at the top level:

```javascript
import { add } from "./math.js";
```

For dynamic loading, use:

```javascript
const module = await import("./math.js");
```

The result is a Promise that resolves to the module namespace object.

Example:

```javascript
async function loadMath() {
  const math = await import("./math.js");

  console.log(
    math.add(10, 20)
  );
}

loadMath();
```

Dynamic imports are useful when code should be loaded only when needed.

Common use cases:

```text
Lazy loading
Large features
Conditional functionality
Code splitting
```

---

# 36. Static vs Dynamic Import

| Static Import                      | Dynamic Import               |
| ---------------------------------- | ---------------------------- |
| `import x from "./x.js"`           | `import("./x.js")`           |
| Statically declared                | Loaded dynamically           |
| Usually top-level                  | Can be used inside functions |
| Module dependency known statically | Can be loaded conditionally  |
| Common application code            | Useful for lazy loading      |

---

# 37. Importing the Same Module Multiple Times

Suppose:

```javascript
import { add } from "./math.js";
```

and another file also imports:

```javascript
import { add } from "./math.js";
```

The module is treated as the same module based on its resolved module identity.

You do not get a completely separate module instance simply because two files import it.

This is useful for shared configuration and module-level state.

---

# 38. Import Bindings Are Read-Only

Suppose:

```javascript
// counter.js

export let count = 0;

export function increment() {
  count++;
}
```

Another module:

```javascript
import {
  count,
  increment,
} from "./counter.js";
```

You cannot reassign the imported binding:

```javascript
count = 10;
```

That causes an error.

But the exporting module can update its own binding:

```javascript
increment();
```

Then:

```javascript
console.log(count);
```

can observe the updated exported value.

---

# 39. Circular Dependencies

A circular dependency occurs when modules depend on each other.

Example:

```text
A.js
 ↓
B.js
 ↓
A.js
```

Example:

```javascript
// A.js
import { valueB } from "./B.js";

export const valueA = 10;
```

```javascript
// B.js
import { valueA } from "./A.js";

export const valueB = 20;
```

Circular dependencies can make initialization difficult to understand.

Prefer a dependency structure that avoids unnecessary cycles.

---

# 40. Recommended Project Structure

For a backend application:

```text
src/
├── controllers/
│   ├── user.controller.js
│   └── food.controller.js
│
├── routes/
│   ├── user.routes.js
│   └── food.routes.js
│
├── models/
│   ├── user.model.js
│   └── food.model.js
│
├── middleware/
│   └── auth.middleware.js
│
├── utils/
│   └── response.js
│
├── app.js
└── server.js
```

Example flow:

```text
server.js
    ↓
app.js
    ↓
routes
    ↓
controllers
    ↓
models
```

Each module has a focused responsibility.

---

# 41. Best Practices

### Use named exports for multiple related utilities

```javascript
export {
  add,
  subtract,
  multiply,
};
```

### Use default exports when a module has one primary thing

```javascript
export default User;
```

### Keep imports organized

```javascript
import express from "express";

import {
  getUsers,
  createUser,
} from "./user.controller.js";
```

### Use meaningful aliases

Prefer:

```javascript
import {
  formatPrice as formatCurrency,
} from "./utils.js";
```

over unclear names.

### Avoid unnecessary `export *`

Explicit exports make the public API of a module easier to understand.

### Keep modules focused

Avoid creating one huge file containing unrelated functions, classes, routes, and utilities.

---

# 42. Quick Syntax Cheat Sheet

## Named Export

```javascript
export const name = "Sandip";
```

## Named Import

```javascript
import { name } from "./user.js";
```

## Named Export List

```javascript
export {
  name,
  age,
};
```

## Named Import Alias

```javascript
import {
  name as username,
} from "./user.js";
```

## Default Export

```javascript
export default User;
```

## Default Import

```javascript
import User from "./User.js";
```

## Default + Named Import

```javascript
import User, {
  role,
  login,
} from "./user.js";
```

## Namespace Import

```javascript
import * as utils from "./utils.js";
```

## Side-Effect Import

```javascript
import "./setup.js";
```

## Re-Export

```javascript
export {
  add,
} from "./math.js";
```

## Re-Export Everything

```javascript
export * from "./math.js";
```

## Re-Export Default as Named

```javascript
export {
  default as User,
} from "./User.js";
```

## Dynamic Import

```javascript
const module = await import("./module.js");
```

---

# 43. Final Concept

Think of modules like separate rooms in an application:

```text
math.js
    │
    ├── add
    ├── subtract
    └── multiply
          │
          ↓
      export
          │
          ↓
       app.js
          │
          └── import
```

The basic relationship is:

```text
export
   ↓
makes a value available
   ↓
import
   ↓
uses that value in another module
```

For named exports:

```text
export name
    ↓
import { name }
```

For default exports:

```text
export default value
    ↓
import value
```

For re-exporting:

```text
module A
   ↓
module B
   ↓
module C
```

This module system is fundamental to modern JavaScript, React, Node.js, and Express applications.
