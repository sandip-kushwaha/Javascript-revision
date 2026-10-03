# JavaScript ES Modules

**ES Modules (ESM)** are JavaScript's standard system for splitting code into separate files.

Modules help you organize large applications into smaller, reusable pieces.

They are commonly used in:

* React
* Vite
* Node.js
* Express
* Frontend applications
* Backend applications

---

# 1. Why Use Modules?

Without modules, a large application can become difficult to manage.

For example:

```text
app.js
```

might contain:

```text
Users
Products
Authentication
Orders
Payments
Database
Utilities
```

As the application grows, this becomes difficult to maintain.

Modules allow us to separate these responsibilities:

```text
src/
│
├── users.js
├── products.js
├── auth.js
├── orders.js
└── utils.js
```

Each file can contain related functionality.

---

# 2. What is an ES Module?

An ES Module is a JavaScript file that can:

* Export values
* Import values
* Maintain its own scope
* Reuse functionality from other files

Example:

```javascript
// math.js

export const add = (a, b) => {
    return a + b;
};
```

Another file can import it:

```javascript
// app.js

import { add } from "./math.js";

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 3. Export and Import

The two most important module keywords are:

```javascript
export
import
```

`export` makes a value available to other modules.

`import` brings an exported value into another module.

Basic flow:

```text
math.js
   │
   │ export
   ↓
add()
   │
   │ import
   ↓
app.js
```

---

# 4. Named Export

A named export exports a specific value.

```javascript
// math.js

export const add = (a, b) => {
    return a + b;
};

export const subtract = (a, b) => {
    return a - b;
};
```

Import them:

```javascript
// app.js

import {
    add,
    subtract
} from "./math.js";
```

Use them:

```javascript
console.log(add(10, 5));
console.log(subtract(10, 5));
```

Output:

```text
15
5
```

---

# 5. Exporting Multiple Values

A module can export multiple values.

```javascript
// user.js

export const name = "Sandip";

export const age = 22;

export const role = "Developer";
```

Import:

```javascript
// app.js

import {
    name,
    age,
    role
} from "./user.js";

console.log(name);
console.log(age);
console.log(role);
```

---

# 6. Export at the Bottom

You do not always have to write `export` when declaring a value.

You can export values later:

```javascript
// math.js

const add = (a, b) => {
    return a + b;
};

const subtract = (a, b) => {
    return a - b;
};

export {
    add,
    subtract
};
```

Import:

```javascript
import {
    add,
    subtract
} from "./math.js";
```

This style can be useful when you want to clearly see all exports together.

---

# 7. Default Export

A module can have one default export.

Example:

```javascript
// User.js

class User {
    constructor(name) {
        this.name = name;
    }
}

export default User;
```

Import:

```javascript
// app.js

import User from "./User.js";

const user = new User("Sandip");

console.log(user.name);
```

Output:

```text
Sandip
```

---

# 8. Default Export Can Be Renamed

When importing a default export, the local name can be chosen by the importer.

Export:

```javascript
// User.js

export default class User {
    constructor(name) {
        this.name = name;
    }
}
```

Import:

```javascript
import Person from "./User.js";
```

This is valid because the default export does not require the same local name.

You could also write:

```javascript
import UserAccount from "./User.js";
```

The imported value is still the same default export.

---

# 9. Named Export Names Must Match

Suppose:

```javascript
// math.js

export const add = (a, b) => {
    return a + b;
};
```

The normal import is:

```javascript
import { add } from "./math.js";
```

The imported name must correspond to the exported name.

---

# 10. Renaming Named Imports

Named imports can be renamed using:

```javascript
as
```

Example:

```javascript
import {
    add as sum
} from "./math.js";
```

Now use:

```javascript
console.log(
    sum(10, 20)
);
```

The original export is still called:

```text
add
```

but the local imported name is:

```text
sum
```

---

# 11. Renaming Named Exports

You can also rename an export.

```javascript
const add = (a, b) => {
    return a + b;
};

export {
    add as sum
};
```

Now the module exports:

```text
sum
```

Import:

```javascript
import {
    sum
} from "./math.js";
```

---

# 12. Import Multiple Named Exports

Example:

```javascript
// math.js

export const add = (a, b) => a + b;

export const subtract = (a, b) => a - b;

export const multiply = (a, b) => a * b;

export const divide = (a, b) => a / b;
```

Import:

```javascript
import {
    add,
    subtract,
    multiply,
    divide
} from "./math.js";
```

Use:

```javascript
console.log(add(10, 5));
console.log(subtract(10, 5));
console.log(multiply(10, 5));
console.log(divide(10, 5));
```

---

# 13. Import Everything

You can import all named exports as a namespace object.

```javascript
import * as math from "./math.js";
```

Now:

```javascript
console.log(
    math.add(10, 5)
);

console.log(
    math.multiply(10, 5)
);
```

The imported object contains the module's named exports.

---

# 14. Namespace Import

Consider:

```javascript
// math.js

export const add = (a, b) => a + b;

export const subtract = (a, b) => a - b;
```

Import:

```javascript
import * as math from "./math.js";
```

Now:

```javascript
math.add(10, 5);

math.subtract(10, 5);
```

This can be useful when a module contains many related functions.

---

# 15. Default + Named Exports

A module can have:

* One default export
* Multiple named exports

Example:

```javascript
// User.js

export default class User {
    constructor(name) {
        this.name = name;
    }
}

export const role = "user";

export const active = true;
```

Import:

```javascript
import User, {
    role,
    active
} from "./User.js";
```

Use:

```javascript
const user = new User("Sandip");

console.log(user.name);
console.log(role);
console.log(active);
```

---

# 16. One Default Export per Module

A module cannot have multiple default exports.

Invalid:

```javascript
export default User;

export default Product;
```

A module can have only one default export.

However, it can have many named exports:

```javascript
export const user = {};
export const product = {};
export const order = {};
```

---

# 17. Importing for Side Effects

Sometimes a module does not need to export anything.

You may import it only to execute its code.

Example:

```javascript
import "./setup.js";
```

The module is loaded and executed.

This can be useful for:

* Initialization
* Polyfills
* Global configuration
* CSS imports in bundlers
* Application setup

---

# 18. Module Scope

Every ES module has its own scope.

Example:

```javascript
// first.js

const message = "Hello";
```

This variable is not automatically available in:

```javascript
// second.js
```

You need to export and import it.

```javascript
// first.js

export const message = "Hello";
```

Then:

```javascript
// second.js

import { message } from "./first.js";

console.log(message);
```

---

# 19. Modules Avoid Global Variables

Without modules, variables can accidentally share global scope.

Modules provide separate scopes.

Example:

```javascript
// user.js

const name = "Sandip";

export {
    name
};
```

Another module can have:

```javascript
// admin.js

const name = "Admin";
```

These variables do not conflict simply because they have the same name.

---

# 20. Module File Structure

A simple application might look like:

```text
src/
│
├── app.js
│
├── math/
│   └── math.js
│
├── users/
│   └── user.js
│
└── utils/
    └── format.js
```

Example:

```javascript
// math/math.js

export const add = (a, b) => a + b;
```

Then:

```javascript
// app.js

import { add } from "./math/math.js";

console.log(add(5, 10));
```

---

# 21. Relative Paths

Modules commonly use relative paths.

Current directory:

```text
.
```

Parent directory:

```text
..
```

Example:

```javascript
import { add } from "./math.js";
```

Means:

```text
Current directory
    ↓
math.js
```

Example:

```javascript
import { add } from "../math.js";
```

Means:

```text
Parent directory
    ↓
math.js
```

---

# 22. File Extensions

In browser-based native ES Modules, explicit file extensions are commonly required.

Example:

```javascript
import { add } from "./math.js";
```

rather than:

```javascript
import { add } from "./math";
```

Bundlers such as Vite can resolve imports according to their configuration and ecosystem conventions, but explicit extensions are useful to understand when working with native browser modules and Node.js ESM.

---

# 23. ES Modules in HTML

To use an ES module directly in a browser:

```html
<script
    type="module"
    src="./app.js">
</script>
```

Example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Modules</title>
</head>

<body>

    <script
        type="module"
        src="./app.js">
    </script>

</body>
</html>
```

The `type="module"` attribute tells the browser to treat the script as an ES module.

---

# 24. Browser Module Example

`math.js`:

```javascript
export const add = (a, b) => {
    return a + b;
};
```

`app.js`:

```javascript
import { add } from "./math.js";

console.log(
    add(10, 20)
);
```

HTML:

```html
<script
    type="module"
    src="./app.js">
</script>
```

Flow:

```text
index.html
    ↓
app.js
    ↓
import math.js
    ↓
add()
```

---

# 25. Modules in Node.js

Node.js supports ES Modules.

Example:

```javascript
// math.js

export const add = (a, b) => {
    return a + b;
};
```

Import:

```javascript
// app.js

import { add } from "./math.js";

console.log(add(10, 20));
```

Node.js needs to know that the project uses ES Modules.

One common approach is:

```json
{
    "type": "module"
}
```

in `package.json`.

---

# 26. `package.json` with ES Modules

Example:

```json
{
    "name": "my-app",
    "version": "1.0.0",
    "type": "module"
}
```

Now `.js` files in that package are treated as ES Modules.

This is common in modern Node.js applications.

---

# 27. ES Modules in React

React projects commonly use ES Modules.

Example:

```javascript
// Button.jsx

export default function Button() {
    return (
        <button>
            Click
        </button>
    );
}
```

Import:

```javascript
// App.jsx

import Button from "./Button.jsx";

function App() {
    return (
        <div>
            <Button />
        </div>
    );
}

export default App;
```

React applications rely heavily on module imports and exports.

---

# 28. Modules and React Components

A component can be exported:

```javascript
export default function Header() {
    return <header>Header</header>;
}
```

Then imported:

```javascript
import Header from "./Header.jsx";
```

This allows components to be organized into separate files.

Example:

```text
components/
│
├── Header.jsx
├── Navbar.jsx
├── Footer.jsx
└── Button.jsx
```

---

# 29. Modules in Express

Express applications also commonly use modules.

Example:

```javascript
// user.controller.js

export const getUsers = async (req, res) => {
    res.json({
        message: "Users"
    });
};
```

Route:

```javascript
// user.routes.js

import express from "express";

import {
    getUsers
} from "./user.controller.js";

const router = express.Router();

router.get(
    "/users",
    getUsers
);

export default router;
```

Application:

```javascript
// app.js

import userRoutes from "./user.routes.js";

app.use(
    "/api/users",
    userRoutes
);
```

This separates:

```text
Routes
Controllers
Application
```

---

# 30. Modules Improve Separation of Concerns

A good project can separate responsibilities:

```text
src/
│
├── controllers/
├── routes/
├── models/
├── middleware/
├── services/
├── utils/
└── app.js
```

Each module has a focused responsibility.

For example:

```text
Controller
    ↓
Business Logic

Route
    ↓
URL + HTTP Method

Model
    ↓
Database Structure

Middleware
    ↓
Request Processing
```

---

# 31. Live Bindings

ES Module imports are **live bindings**.

Example:

```javascript
// counter.js

export let count = 0;

export function increment() {
    count++;
}
```

Another module:

```javascript
// app.js

import {
    count,
    increment
} from "./counter.js";

console.log(count);

increment();

console.log(count);
```

Output:

```text
0
1
```

The imported `count` reflects the current exported binding.

---

# 32. Imported Bindings Are Read-Only

Although imports are live bindings, the importing module cannot reassign the imported binding directly.

Example:

```javascript
import {
    count
} from "./counter.js";
```

This is not valid:

```javascript
count = 100;
```

The module that owns the export controls that binding.

---

# 33. Circular Dependencies

Modules can depend on each other.

Example:

```text
A.js
 ↓
B.js
 ↓
A.js
```

This is called a **circular dependency**.

Small circular dependencies can sometimes work because ES Modules have defined linking and evaluation behavior, but they can make code harder to understand and can produce initialization problems.

Prefer a dependency structure that keeps modules easy to reason about.

---

# 34. Module Loading

A simplified module process is:

```text
Source Code
    ↓
Parse
    ↓
Resolve Imports
    ↓
Link Modules
    ↓
Evaluate Modules
    ↓
Execute Code
```

For example:

```text
app.js
  │
  ├── imports user.js
  │
  └── imports math.js
```

The JavaScript runtime resolves these dependencies before executing the module graph.

---

# 35. Module Caching

A module is generally evaluated once per module graph/environment and its exports are reused by later imports.

Example:

```javascript
// config.js

console.log("Config loaded");

export const config = {
    appName: "My App"
};
```

If several modules import it:

```javascript
import { config } from "./config.js";
```

the module is not normally re-executed from scratch for every import.

This allows modules to share state through their exported bindings.

---

# 36. Module Dependency Graph

Consider:

```text
app.js
 │
 ├── user.js
 │    └── database.js
 │
 └── product.js
      └── database.js
```

The application has a module dependency graph.

```text
app
├── user
│   └── database
└── product
    └── database
```

The same module can be shared by multiple modules.

---

# 37. Static Imports

Normal imports are static.

Example:

```javascript
import {
    add
} from "./math.js";
```

The module dependency can be identified before normal runtime execution.

This makes static imports useful for:

* Dependency analysis
* Bundling
* Tree shaking
* Code organization

---

# 38. Dynamic Import

JavaScript also supports dynamic imports:

```javascript
import("./math.js");
```

Dynamic import returns a Promise.

Example:

```javascript
const module =
    await import("./math.js");

console.log(
    module.add(10, 20)
);
```

This can be useful when a module should be loaded only when needed.

---

# 39. Dynamic Import with `.then()`

Instead of `await`:

```javascript
import("./math.js")
    .then((module) => {
        console.log(
            module.add(10, 20)
        );
    })
    .catch((error) => {
        console.error(error);
    });
```

The returned Promise resolves to the module namespace object.

---

# 40. Dynamic Import Use Cases

Dynamic imports are useful for:

```text
Lazy loading
Code splitting
Large features
Optional functionality
Route-based loading
Performance optimization
```

Example:

```javascript
async function openEditor() {
    const editor =
        await import("./editor.js");

    editor.start();
}
```

The editor module can be loaded only when required.

---

# 41. Static vs Dynamic Import

| Static Import                | Dynamic Import            |
| ---------------------------- | ------------------------- |
| `import x from "./x.js"`     | `import("./x.js")`        |
| Dependency known statically  | Loaded dynamically        |
| Does not return a Promise    | Returns a Promise         |
| Common application imports   | Useful for lazy loading   |
| Easy for bundlers to analyze | Useful for code splitting |

---

# 42. Re-Exporting

A module can re-export values from another module.

Example:

```javascript
// math.js

export const add = (a, b) => a + b;
```

Another module:

```javascript
// index.js

export {
    add
} from "./math.js";
```

Then:

```javascript
// app.js

import {
    add
} from "./index.js";
```

This creates a central export point.

---

# 43. Re-Export Everything

You can re-export all named exports:

```javascript
export * from "./math.js";
```

Now consumers can import the exports from the current module.

Example:

```text
math.js
   ↓
index.js
   ↓
app.js
```

This pattern is often used for module "barrel" files.

---

# 44. Re-Export with Renaming

Example:

```javascript
export {
    add as sum
} from "./math.js";
```

Now consumers can use:

```javascript
import {
    sum
} from "./index.js";
```

---

# 45. Default Re-Export

A default export can also be re-exported.

Example:

```javascript
export {
    default
} from "./User.js";
```

Then:

```javascript
import User from "./index.js";
```

A default export can also be given another name while re-exporting:

```javascript
export {
    default as User
} from "./User.js";
```

---

# 46. Barrel Files

A barrel file is a central module that re-exports functionality.

Example:

```text
components/
│
├── Button.jsx
├── Header.jsx
├── Footer.jsx
└── index.js
```

`index.js`:

```javascript
export { default as Button }
    from "./Button.jsx";

export { default as Header }
    from "./Header.jsx";

export { default as Footer }
    from "./Footer.jsx";
```

Now:

```javascript
import {
    Button,
    Header,
    Footer
} from "./components/index.js";
```

This can make imports cleaner.

---

# 47. Module Best Practices

Prefer modules with a clear responsibility.

Good:

```text
auth.js
user.js
product.js
database.js
validation.js
```

Avoid putting unrelated functionality into one huge module.

Prefer:

```javascript
export const createUser = ...;
export const updateUser = ...;
```

instead of making every file contain unrelated application logic.

---

# 48. Named vs Default Export

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
export default User;
```

Import:

```javascript
import User from "./User.js";
```

Comparison:

| Named Export                        | Default Export                     |
| ----------------------------------- | ---------------------------------- |
| Can have many per module            | One per module                     |
| Usually imported with `{}`          | No `{}` required                   |
| Import name normally matches export | Importer chooses local name        |
| Good for multiple related values    | Often useful for one primary value |

---

# 49. ES Modules vs Single Large File

Without modules:

```text
app.js
│
├── users
├── products
├── orders
├── authentication
├── utilities
└── database
```

With modules:

```text
src/
│
├── users.js
├── products.js
├── orders.js
├── auth.js
├── utils.js
└── database.js
```

Advantages:

* Better organization
* Reusability
* Easier maintenance
* Better separation of concerns
* Easier testing
* Dependency management
* Smaller focused files

---

# 50. ES Module Quick Cheat Sheet

```javascript
// Named export
export const add = (a, b) => a + b;

// Named import
import { add } from "./math.js";

// Rename named import
import {
    add as sum
} from "./math.js";

// Default export
export default User;

// Default import
import User from "./User.js";

// Multiple named imports
import {
    add,
    subtract
} from "./math.js";

// Namespace import
import * as math from "./math.js";

// Side-effect import
import "./setup.js";

// Dynamic import
const module =
    await import("./math.js");

// Re-export
export {
    add
} from "./math.js";

// Re-export everything
export * from "./math.js";

// Re-export default
export {
    default as User
} from "./User.js";
```

---

# Module Structure

```text
JavaScript Module
        │
        ├── Export
        │   ├── Named Export
        │   └── Default Export
        │
        ├── Import
        │   ├── Named Import
        │   ├── Default Import
        │   ├── Namespace Import
        │   └── Side-Effect Import
        │
        ├── Dynamic Import
        │
        └── Re-Export
            ├── Named
            ├── Default
            └── All
```

---

# ES Modules in Full-Stack Development

For a React + Node.js + Express application, modules commonly organize the project like this:

```text
project/
│
├── frontend/
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── hooks/
│       ├── context/
│       ├── api/
│       └── utils/
│
└── backend/
    └── src/
        ├── controllers/
        ├── routes/
        ├── models/
        ├── middleware/
        ├── services/
        ├── utils/
        └── app.js
```

The module system allows each part of the application to import only what it needs.

---

# Key Takeaways

* ES Modules provide JavaScript's standard module system.
* `export` makes values available to other modules.
* `import` uses exported values.
* Named exports allow multiple exports from one module.
* A module can have only one default export.
* Default imports can use a different local name.
* Named imports can be renamed with `as`.
* `import * as name` creates a namespace object.
* Modules have their own scope.
* ES Modules help prevent unnecessary global variables.
* Browser modules use `type="module"`.
* Node.js supports ES Modules.
* React applications heavily use ES Modules.
* Express applications can use ES Modules to organize backend code.
* Dynamic `import()` returns a Promise.
* Dynamic imports are useful for lazy loading and code splitting.
* Modules can re-export values from other modules.
* Barrel files provide a central export point.
* ES Modules use live bindings.
* Imported bindings cannot be directly reassigned by the importing module.
* Good modules usually have a focused responsibility.

---

# ES Modules Roadmap

```text
ES Modules
    │
    ├── export
    │   ├── Named
    │   └── Default
    │
    ├── import
    │   ├── Named
    │   ├── Default
    │   ├── Namespace
    │   └── Side Effect
    │
    ├── Module Scope
    │
    ├── Module Dependency Graph
    │
    ├── Dynamic Import
    │
    ├── Re-Export
    │
    └── Barrel Files
```

---
