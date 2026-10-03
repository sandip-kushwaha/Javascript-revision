# JavaScript Modules

JavaScript **modules** allow you to split code into separate files and reuse that code where needed.

Instead of keeping an entire application in one large file, modules help organize code into smaller, maintainable files.

For example:

```text
src/
├── api.js
├── auth.js
├── utils.js
└── app.js
```

Each file can contain related functionality and export what other files need.

---

# 1. Why Use Modules?

Without modules, a large application can become difficult to maintain:

```text
app.js
│
├── authentication
├── API requests
├── validation
├── calculations
├── UI logic
└── utility functions
```

With modules:

```text
src/
├── auth.js
├── api.js
├── validation.js
├── utils.js
└── app.js
```

Benefits:

* Better organization
* Code reuse
* Easier maintenance
* Less global-scope pollution
* Clear dependencies
* Easier testing
* Better scalability

---

# 2. Export and Import

JavaScript modules mainly use:

```javascript
export
```

and:

```javascript
import
```

Example:

### `math.js`

```javascript
export const add = (a, b) => {
  return a + b;
};
```

### `app.js`

```javascript
import { add } from "./math.js";

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 3. Named Export

A **named export** exports something using its specific name.

```javascript
export const apiUrl = "https://api.example.com";

export function getUsers() {
  return [];
}
```

You can import them using the same names:

```javascript
import { apiUrl, getUsers } from "./api.js";
```

---

# 4. Export at the End

You can also define the code first and export it later.

```javascript
const apiUrl = "https://api.example.com";

function getUsers() {
  return [];
}

export {
  apiUrl,
  getUsers
};
```

This is useful when you want to keep definitions together and exports at the bottom.

---

# 5. Multiple Named Exports

One file can export many values.

### `utils.js`

```javascript
export function formatCurrency(amount) {
  return `$${amount.toFixed(2)}`;
}

export function formatDate(date) {
  return date.toISOString().split("T")[0];
}

export function capitalize(value) {
  return value.charAt(0).toUpperCase() + value.slice(1);
}
```

Import:

```javascript
import {
  formatCurrency,
  formatDate,
  capitalize
} from "./utils.js";
```

---

# 6. Import Only What You Need

Suppose:

```javascript
export function createUser() {}
export function updateUser() {}
export function deleteUser() {}
```

You only need `createUser`:

```javascript
import { createUser } from "./users.js";
```

You don't have to import everything.

---

# 7. Import All Named Exports

You can import all named exports as an object-like namespace.

```javascript
import * as utils from "./utils.js";
```

Then:

```javascript
utils.capitalize("javascript");
utils.formatCurrency(250);
```

Example:

```javascript
import * as math from "./math.js";

console.log(math.add(5, 10));
console.log(math.subtract(20, 8));
```

---

# 8. Renaming an Import

You can rename an imported value using `as`.

Suppose:

```javascript
export function calculateTotal() {
  // ...
}
```

You can import it as:

```javascript
import {
  calculateTotal as getTotal
} from "./cart.js";
```

Now use:

```javascript
getTotal();
```

The original exported name remains:

```text
calculateTotal
```

Only the local imported name is different.

---

# 9. Renaming Multiple Imports

```javascript
import {
  createUser as addUser,
  deleteUser as removeUser
} from "./users.js";
```

Now:

```javascript
addUser();
removeUser();
```

---

# 10. Default Export

A module can have one **default export**.

Example:

### `logger.js`

```javascript
export default function logger(message) {
  console.log(message);
}
```

Import:

```javascript
import logger from "./logger.js";
```

Notice that default imports do **not** require `{}`.

---

# 11. Default Export Can Be Renamed

Suppose:

```javascript
export default function logger(message) {
  console.log(message);
}
```

You can import it as:

```javascript
import log from "./logger.js";
```

or:

```javascript
import writeLog from "./logger.js";
```

The local name can be different.

---

# 12. Named vs Default Import

### Named export

```javascript
export const version = "1.0";
```

Import:

```javascript
import { version } from "./config.js";
```

### Default export

```javascript
export default version;
```

Import:

```javascript
import version from "./config.js";
```

Main difference:

```text
Named export   → uses {}
Default export → does not use {}
```

---

# 13. Default + Named Exports

A module can contain one default export and multiple named exports.

### `api.js`

```javascript
export default function request(url) {
  // request logic
}

export function getUsers() {
  // ...
}

export function getProducts() {
  // ...
}
```

Import:

```javascript
import request, {
  getUsers,
  getProducts
} from "./api.js";
```

---

# 14. File Extensions

In browser ES modules, it's generally safest to include the `.js` extension:

```javascript
import { add } from "./math.js";
```

Instead of:

```javascript
import { add } from "./math";
```

For browser-native modules, use the actual module URL/path.

---

# 15. Browser Modules

HTML must tell the browser that the JavaScript file is a module.

```html
<script type="module" src="./app.js"></script>
```

Example structure:

```text
project/
├── index.html
├── app.js
└── math.js
```

### `math.js`

```javascript
export function multiply(a, b) {
  return a * b;
}
```

### `app.js`

```javascript
import { multiply } from "./math.js";

console.log(multiply(4, 5));
```

### `index.html`

```html
<!DOCTYPE html>
<html>
<head>
  <title>Modules</title>
</head>
<body>

  <script type="module" src="./app.js"></script>

</body>
</html>
```

---

# 16. Why `type="module"` Matters

This:

```html
<script src="./app.js"></script>
```

does not enable ES module syntax.

Use:

```html
<script type="module" src="./app.js"></script>
```

Then JavaScript can use:

```javascript
import ...
```

and:

```javascript
export ...
```

---

# 17. Modules Have Their Own Scope

Variables inside a module are not automatically global.

### `config.js`

```javascript
const apiUrl = "https://api.example.com";

export {
  apiUrl
};
```

The `apiUrl` variable isn't automatically available everywhere.

Another file must explicitly import it:

```javascript
import { apiUrl } from "./config.js";
```

This helps prevent accidental global variables.

---

# 18. Module Scope Example

### `one.js`

```javascript
const message = "Hello";
```

### `two.js`

```javascript
console.log(message);
```

This does not automatically work.

`two.js` needs an export/import relationship.

### `one.js`

```javascript
export const message = "Hello";
```

### `two.js`

```javascript
import { message } from "./one.js";

console.log(message);
```

---

# 19. Reusable Configuration Module

A practical project might have:

### `config.js`

```javascript
export const API_URL =
  "https://api.example.com/api/v1";

export const API_TIMEOUT = 5000;
```

Then:

### `api.js`

```javascript
import {
  API_URL,
  API_TIMEOUT
} from "./config.js";

console.log(API_URL);
console.log(API_TIMEOUT);
```

This keeps configuration in one place.

---

# 20. Utility Module

A utility file can contain reusable functions.

### `utils.js`

```javascript
export function formatPrice(price) {
  return `Rs. ${price.toFixed(2)}`;
}

export function isValidEmail(email) {
  return email.includes("@");
}
```

Then:

```javascript
import {
  formatPrice,
  isValidEmail
} from "./utils.js";

console.log(formatPrice(1500));
console.log(isValidEmail("user@example.com"));
```

---

# 21. API Module

In a frontend application, API functions can be separated.

### `userApi.js`

```javascript
export async function getUsers() {
  const response = await fetch("/api/users");

  if (!response.ok) {
    throw new Error("Failed to fetch users");
  }

  return response.json();
}
```

Another file can use it:

```javascript
import { getUsers } from "./userApi.js";

const users = await getUsers();

console.log(users);
```

---

# 22. Module Dependencies

Modules can import other modules.

```text
app.js
  ↓
api.js
  ↓
config.js
```

For example:

### `config.js`

```javascript
export const API_URL = "/api/v1";
```

### `api.js`

```javascript
import { API_URL } from "./config.js";

export function getUsers() {
  return fetch(`${API_URL}/users`);
}
```

### `app.js`

```javascript
import { getUsers } from "./api.js";

getUsers();
```

This creates a dependency chain.

---

# 23. Re-Exporting

A module can import something and export it again.

### `utils.js`

```javascript
export function formatPrice(price) {
  return `Rs. ${price}`;
}
```

### `index.js`

```javascript
export {
  formatPrice
} from "./utils.js";
```

Now another file can import from `index.js`:

```javascript
import { formatPrice } from "./index.js";
```

This is useful for creating a central public API for a folder.

---

# 24. Re-Export Everything

You can re-export all named exports:

```javascript
export * from "./users.js";
export * from "./products.js";
export * from "./orders.js";
```

Then consumers can import from one file:

```javascript
import {
  createUser,
  getProducts,
  createOrder
} from "./index.js";
```

This pattern is commonly called a **barrel file**.

---

# 25. Dynamic Import

JavaScript also supports loading modules dynamically.

```javascript
const module = await import("./utils.js");
```

Then:

```javascript
module.formatPrice(500);
```

Unlike a normal static import:

```javascript
import { formatPrice } from "./utils.js";
```

dynamic import happens when the code reaches it.

---

# 26. Dynamic Import Example

```javascript
async function loadFeature() {
  const module = await import("./feature.js");

  module.startFeature();
}
```

This can be useful when a feature is only needed under certain conditions.

---

# 27. Modules and `async`

Top-level `await` is supported in ES modules.

For example:

```javascript
const response = await fetch("/api/users");

const users = await response.json();

console.log(users);
```

This can work directly inside an ES module.

In traditional non-module scripts, top-level `await` is not available in the same way.

---

# 28. Modules in Node.js

Node.js supports JavaScript modules.

For ES modules, a project can use:

```json
{
  "type": "module"
}
```

in `package.json`.

Then:

```javascript
import express from "express";
```

and:

```javascript
export default app;
```

can be used.

Without `"type": "module"`, Node.js commonly treats `.js` files as CommonJS unless configured otherwise.

---

# 29. ES Modules vs CommonJS

JavaScript has two major module systems you'll encounter:

### ES Modules

```javascript
import express from "express";

export default app;
```

### CommonJS

```javascript
const express = require("express");

module.exports = app;
```

ES Modules are the standard module system defined by modern JavaScript.

CommonJS remains widely used in Node.js projects and older codebases.

---

# 30. Module File Structure

A practical application could look like:

```text
src/
├── app.js
├── config/
│   └── config.js
├── services/
│   ├── userService.js
│   └── orderService.js
├── utils/
│   ├── format.js
│   └── validation.js
└── api/
    ├── userApi.js
    └── orderApi.js
```

For example:

```text
app.js
   ↓
services/userService.js
   ↓
api/userApi.js
   ↓
config/config.js
```

Each module has a specific responsibility.

---

# 31. Common Import/Export Errors

## Wrong: Missing braces for named export

If you have:

```javascript
export const API_URL = "/api";
```

Use:

```javascript
import { API_URL } from "./config.js";
```

Not:

```javascript
import API_URL from "./config.js";
```

---

## Wrong: Using braces for default export

If you have:

```javascript
export default function connect() {}
```

Use:

```javascript
import connect from "./database.js";
```

Not:

```javascript
import { connect } from "./database.js";
```

---

# 32. Relative Paths Matter

Suppose:

```text
src/
├── app.js
└── utils/
    └── format.js
```

From `app.js`:

```javascript
import { formatPrice } from "./utils/format.js";
```

From inside `utils/format.js`, to import something from `app.js`:

```javascript
import { something } from "../app.js";
```

Path meaning:

```text
./   current directory
../  parent directory
```

---

# 33. Modules Are Not the Same as Files

A JavaScript file becomes an ES module when it is treated as a module.

For browsers:

```html
<script type="module">
```

or:

```html
<script type="module" src="./app.js"></script>
```

For Node.js, module behavior depends on project configuration and file extensions.

So:

```text
File ≠ automatically an ES module in every environment
```

---

# 34. Key Differences

| Feature           | Named Export              | Default Export         |
| ----------------- | ------------------------- | ---------------------- |
| Syntax            | `export { value }`        | `export default value` |
| Import            | `import { value }`        | `import value`         |
| Number per module | Multiple                  | One                    |
| Import name       | Must match unless renamed | Can choose local name  |
| Braces            | Required                  | Not used               |

---

# 35. Best Practices

### 1. Keep modules focused

Instead of:

```text
everything.js
```

prefer:

```text
auth.js
api.js
validation.js
format.js
```

### 2. Use meaningful names

```javascript
import { validateEmail } from "./validation.js";
```

is clearer than:

```javascript
import { x } from "./utils.js";
```

### 3. Avoid unnecessary exports

Only export functionality that other modules actually need.

### 4. Keep dependencies understandable

Avoid creating unnecessary circular dependencies.

### 5. Use consistent module style

In a project, prefer a consistent module system rather than mixing styles without a reason.

---

# 36. Quick Reference

### Named export

```javascript
export const value = 100;
```

### Named import

```javascript
import { value } from "./file.js";
```

### Default export

```javascript
export default function start() {}
```

### Default import

```javascript
import start from "./file.js";
```

### Rename import

```javascript
import {
  calculateTotal as total
} from "./cart.js";
```

### Import everything

```javascript
import * as utils from "./utils.js";
```

### Re-export

```javascript
export { formatPrice } from "./format.js";
```

### Dynamic import

```javascript
const module = await import("./feature.js");
```

### Browser module

```html
<script type="module" src="./app.js"></script>
```

---

# 37. Key Takeaways

* Modules divide JavaScript code into separate reusable files.
* `export` makes values available to other modules.
* `import` brings exported values into another module.
* Named exports use `{}` when imported.
* Default exports do not use `{}`.
* A module can have multiple named exports but only one default export.
* `as` allows imported names to be renamed.
* `import * as name` creates a namespace object.
* Modules have their own scope.
* Modules help organize large applications.
* ES Modules work in browsers and modern Node.js environments.
* Dynamic imports allow modules to be loaded when needed.
* Re-exporting can create a central entry point for related modules.

---
