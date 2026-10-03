# JavaScript Named Export

A **named export** allows a JavaScript module to export multiple values by their specific names.

Named exports are useful when a file contains several related functions, variables, classes, or constants.

Basic syntax:

```javascript
export const name = "Sandip";
```

Import using curly braces:

```javascript
import { name } from "./user.js";
```

---

# 1. Basic Named Export

```javascript
export const name = "Sandip";
```

Import:

```javascript
import { name } from "./user.js";

console.log(name);
```

Output:

```text
Sandip
```

The exported name and imported name match:

```text
export name
     ↓
import { name }
```

---

# 2. Named Export Function

```javascript
export function add(a, b) {
  return a + b;
}
```

Import:

```javascript
import { add } from "./math.js";

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 3. Named Export Arrow Function

```javascript
export const multiply = (a, b) => {
  return a * b;
};
```

Import:

```javascript
import { multiply } from "./math.js";

console.log(multiply(5, 4));
```

Output:

```text
20
```

---

# 4. Named Export Multiple Values

A module can have many named exports.

```javascript
export const name = "Sandip";

export const age = 22;

export const role = "developer";
```

Import:

```javascript
import {
  name,
  age,
  role,
} from "./user.js";
```

Use:

```javascript
console.log(name);
console.log(age);
console.log(role);
```

---

# 5. Named Export Multiple Functions

```javascript
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

export function multiply(a, b) {
  return a * b;
}
```

Import:

```javascript
import {
  add,
  subtract,
  multiply,
} from "./math.js";
```

Use:

```javascript
console.log(add(10, 5));

console.log(subtract(10, 5));

console.log(multiply(10, 5));
```

---

# 6. Export at the Bottom

You do not have to put `export` directly before every declaration.

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

Import:

```javascript
import {
  name,
  age,
  greet,
} from "./user.js";
```

This style can make the public exports of a file easy to see in one place.

---

# 7. Named Export a Class

```javascript
export class User {
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
import { User } from "./User.js";

const user = new User("Sandip");

user.greet();
```

---

# 8. Named Export an Object

```javascript
export const user = {
  name: "Sandip",
  age: 22,
};
```

Import:

```javascript
import { user } from "./user.js";

console.log(user.name);
```

---

# 9. Named Export an Array

```javascript
export const users = [
  "Sandip",
  "Ram",
  "Shyam",
];
```

Import:

```javascript
import { users } from "./users.js";

console.log(users);
```

---

# 10. Named Export Constants

A common use of named exports is sharing application constants.

```javascript
export const PORT = 8000;

export const API_VERSION = "v1";

export const MAX_FILE_SIZE = 5 * 1024 * 1024;
```

Import:

```javascript
import {
  PORT,
  API_VERSION,
  MAX_FILE_SIZE,
} from "./config.js";
```

---

# 11. Named Import

Named exports must normally be imported using curly braces.

Example:

```javascript
export const add = (a, b) => a + b;
```

Correct:

```javascript
import { add } from "./math.js";
```

Incorrect:

```javascript
import add from "./math.js";
```

The second form expects a default export.

---

# 12. Import Multiple Named Exports

```javascript
import {
  add,
  subtract,
  multiply,
  divide,
} from "./math.js";
```

This allows one module to use several exports from another module.

---

# 13. Import Only One Named Export

Suppose:

```javascript
export const add = (a, b) => a + b;

export const subtract = (a, b) => a - b;

export const multiply = (a, b) => a * b;
```

You can import only what you need:

```javascript
import { add } from "./math.js";
```

The other named exports do not need to be imported.

---

# 14. Named Import Aliasing

You can rename a named import with `as`.

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

# 15. Multiple Import Aliases

```javascript
import {
  add as sum,
  subtract as difference,
  multiply as product,
} from "./math.js";
```

Use:

```javascript
console.log(sum(10, 5));

console.log(difference(10, 5));

console.log(product(10, 5));
```

---

# 16. Export Aliasing

You can also rename a value during export.

```javascript
const username = "Sandip";

export {
  username as name,
};
```

Another module imports:

```javascript
import { name } from "./user.js";
```

The internal variable is:

```text
username
```

The public export is:

```text
name
```

---

# 17. Named Export with Alias

Another example:

```javascript
const calculateTotal = (price, quantity) => {
  return price * quantity;
};

export {
  calculateTotal as getTotal,
};
```

Import:

```javascript
import {
  getTotal,
} from "./cart.js";
```

Use:

```javascript
console.log(
  getTotal(100, 3)
);
```

---

# 18. Named Export vs Default Export

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
Named
  → uses { }

Default
  → no { }
```

---

# 19. Multiple Named Exports vs One Default

Named exports:

```javascript
export const add = () => {};

export const subtract = () => {};

export const multiply = () => {};
```

This is useful because the module exposes several related utilities.

A default export is more appropriate when one main value represents the module:

```javascript
export default User;
```

---

# 20. Named Exports in Utility Files

Utility files commonly contain several named functions.

Example:

```javascript
export function formatPrice(price) {
  return `$${price}`;
}

export function formatName(name) {
  return name.trim();
}

export function capitalize(text) {
  return text.charAt(0).toUpperCase() +
    text.slice(1);
}
```

Import:

```javascript
import {
  formatPrice,
  formatName,
  capitalize,
} from "./utils.js";
```

---

# 21. Named Exports in React

Named exports are useful when a file contains multiple reusable components or helper values.

Example:

```jsx
export function PrimaryButton() {
  return <button>Primary</button>;
}

export function SecondaryButton() {
  return <button>Secondary</button>;
}
```

Import:

```jsx
import {
  PrimaryButton,
  SecondaryButton,
} from "./Buttons.jsx";
```

Use:

```jsx
function App() {
  return (
    <>
      <PrimaryButton />
      <SecondaryButton />
    </>
  );
}
```

---

# 22. Named Exports in React Utilities

Example:

```javascript
export function formatDate(date) {
  return new Date(date)
    .toLocaleDateString();
}

export function formatCurrency(amount) {
  return `$${amount.toFixed(2)}`;
}
```

Import:

```javascript
import {
  formatDate,
  formatCurrency,
} from "./formatters.js";
```

---

# 23. Named Exports in Node.js

Example:

```javascript
export const createUser = async (data) => {
  // create user
};

export const getUser = async (id) => {
  // get user
};

export const deleteUser = async (id) => {
  // delete user
};
```

Import:

```javascript
import {
  createUser,
  getUser,
  deleteUser,
} from "./user.service.js";
```

This pattern works well for service modules containing multiple related operations.

---

# 24. Named Exports in Express Controllers

```javascript
export const getUsers = async (req, res) => {
  res.json({
    message: "Users",
  });
};

export const createUser = async (req, res) => {
  res.status(201).json({
    message: "User created",
  });
};
```

Import:

```javascript
import {
  getUsers,
  createUser,
} from "./user.controller.js";
```

Routes:

```javascript
router.get(
  "/users",
  getUsers
);

router.post(
  "/users",
  createUser
);
```

---

# 25. Named Exports for Constants

A configuration file can expose multiple constants:

```javascript
export const COOKIE_NAME = "accessToken";

export const ACCESS_TOKEN_EXPIRY = "15m";

export const REFRESH_TOKEN_EXPIRY = "7d";
```

Import:

```javascript
import {
  COOKIE_NAME,
  ACCESS_TOKEN_EXPIRY,
  REFRESH_TOKEN_EXPIRY,
} from "./config.js";
```

---

# 26. Namespace Import

All named exports can be collected under a namespace.

Suppose:

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
console.log(
  math.add(10, 5)
);

console.log(
  math.subtract(10, 5)
);
```

The namespace provides access to the module's exported bindings.

---

# 27. Named Re-Export

A module can re-export a named value from another module.

Suppose:

```javascript
// math.js

export const add = (a, b) => a + b;
```

Another file:

```javascript
// index.js

export {
  add,
} from "./math.js";
```

Then:

```javascript
import { add } from "./index.js";
```

---

# 28. Re-Export with Alias

```javascript
export {
  add as sum,
} from "./math.js";
```

Import:

```javascript
import { sum } from "./index.js";
```

This allows the central module to expose the function under a different public name.

---

# 29. Re-Export Multiple Named Values

```javascript
export {
  add,
  subtract,
  multiply,
} from "./math.js";
```

Then:

```javascript
import {
  add,
  subtract,
  multiply,
} from "./index.js";
```

---

# 30. `export *`

You can re-export all named exports:

```javascript
export * from "./math.js";
```

For example:

```javascript
// math.js

export const add = () => {};
export const subtract = () => {};
export const multiply = () => {};
```

Then:

```javascript
// index.js

export * from "./math.js";
```

Now:

```javascript
import {
  add,
  subtract,
  multiply,
} from "./index.js";
```

Note:

```text
export *
```

does not re-export the default export.

---

# 31. Barrel File with Named Exports

Suppose:

```text
utils/
├── format.js
├── validation.js
├── calculation.js
└── index.js
```

`format.js`:

```javascript
export function formatPrice(price) {
  return `$${price}`;
}
```

`validation.js`:

```javascript
export function isValidEmail(email) {
  return email.includes("@");
}
```

`calculation.js`:

```javascript
export function calculateTotal(price, quantity) {
  return price * quantity;
}
```

`index.js`:

```javascript
export {
  formatPrice,
} from "./format.js";

export {
  isValidEmail,
} from "./validation.js";

export {
  calculateTotal,
} from "./calculation.js";
```

Now:

```javascript
import {
  formatPrice,
  isValidEmail,
  calculateTotal,
} from "./utils/index.js";
```

---

# 32. Named Export and Live Bindings

ES Modules export bindings rather than simply copying values.

Example:

```javascript
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

console.log(count);

increment();

console.log(count);
```

The imported binding reflects the value maintained by the exporting module.

The importing module cannot reassign the imported binding itself.

---

# 33. Named Export with `let`

You can export a mutable binding:

```javascript
export let counter = 0;

export function increase() {
  counter++;
}
```

The module controls how the value changes.

This is different from allowing another module to directly assign:

```javascript
counter = 100;
```

Imported bindings are read-only from the importing module.

---

# 34. Named Export with `const`

```javascript
export const API_URL =
  "https://example.com/api";
```

Import:

```javascript
import {
  API_URL,
} from "./config.js";
```

This is common for constants that should not be reassigned.

---

# 35. Named Export with `function`

```javascript
export function login(email, password) {
  // authentication logic
}
```

Import:

```javascript
import { login } from "./auth.js";
```

Functions are frequently named exports in service and utility files.

---

# 36. Named Export with `class`

```javascript
export class User {
  constructor(name) {
    this.name = name;
  }
}
```

Import:

```javascript
import { User } from "./User.js";
```

Create an instance:

```javascript
const user = new User("Sandip");
```

---

# 37. Common Mistake: Missing Braces

If the file contains:

```javascript
export const user = {};
```

Correct:

```javascript
import { user } from "./user.js";
```

Incorrect:

```javascript
import user from "./user.js";
```

The incorrect version expects a default export.

---

# 38. Common Mistake: Wrong Export Name

Suppose:

```javascript
export const getUsers = () => {};
```

This is incorrect:

```javascript
import { fetchUsers } from "./user.js";
```

because the module exports:

```text
getUsers
```

not:

```text
fetchUsers
```

Use:

```javascript
import { getUsers } from "./user.js";
```

Or explicitly rename it:

```javascript
import {
  getUsers as fetchUsers,
} from "./user.js";
```

---

# 39. Common Mistake: Default vs Named

Suppose:

```javascript
export const User = {};
```

Incorrect:

```javascript
import User from "./User.js";
```

Correct:

```javascript
import { User } from "./User.js";
```

If the module instead has:

```javascript
export default User;
```

then:

```javascript
import User from "./User.js";
```

is correct.

---

# 40. Named Export Comparison

| Syntax                          | Meaning                          |
| ------------------------------- | -------------------------------- |
| `export const x = 10`           | Export `x` immediately           |
| `export function x() {}`        | Export function `x`              |
| `export class X {}`             | Export class `X`                 |
| `export { x }`                  | Export an existing value         |
| `export { x as y }`             | Export `x` using public name `y` |
| `import { x }`                  | Import named export `x`          |
| `import { x as y }`             | Import `x` locally as `y`        |
| `import * as utils`             | Import module namespace          |
| `export { x } from "./file.js"` | Re-export named `x`              |
| `export * from "./file.js"`     | Re-export all named exports      |

---

# 41. Named vs Default Export

```text
NAMED EXPORT
─────────────

export const add = () => {};

        ↓

import { add } from "./math.js";
```

```text
DEFAULT EXPORT
───────────────

export default add;

        ↓

import add from "./math.js";
```

The visual difference is important:

```text
Named   → { }
Default → no { }
```

---

# 42. Practical Full Example

### `user.js`

```javascript
export const userName = "Sandip";

export const userRole = "developer";

export function greetUser() {
  return `Hello ${userName}`;
}

export function isAdmin(role) {
  return role === "admin";
}
```

### `app.js`

```javascript
import {
  userName,
  userRole,
  greetUser,
  isAdmin,
} from "./user.js";

console.log(userName);

console.log(userRole);

console.log(greetUser());

console.log(
  isAdmin(userRole)
);
```

Output:

```text
Sandip
developer
Hello Sandip
false
```

---

# 43. Recommended Usage

Use named exports when:

```text
One module
   ↓
Multiple related values
```

For example:

```text
math.js
├── add
├── subtract
└── multiply
```

or:

```text
user.service.js
├── createUser
├── getUser
├── updateUser
└── deleteUser
```

Named exports make the available functions explicit.

---

# 44. Key Takeaways

* Named exports are identified by their export names.
* Named imports use curly braces.
* A module can have many named exports.
* Functions, classes, objects, arrays, and constants can be named exports.
* Named imports can be renamed with `as`.
* Named exports can also be renamed during export.
* `export *` re-exports named exports, not the default export.
* Named exports are useful for utility, service, controller, and configuration modules.
* Imported bindings cannot be reassigned by the importing module.
* Named exports work alongside a module's single default export.
* Use meaningful names for public exports.
* Keep related named exports together in focused modules.
