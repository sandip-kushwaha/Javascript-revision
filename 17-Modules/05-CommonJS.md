# JavaScript CommonJS

**CommonJS (CJS)** is a JavaScript module system traditionally used by Node.js.

Before ES Modules became widely adopted, CommonJS was the standard module format for many Node.js applications.

The two main CommonJS keywords are:

```text
require()
module.exports
```

Basic example:

```javascript
const math = require("./math");

console.log(math.add(10, 20));
```

Export:

```javascript
module.exports = {
  add,
};
```

---

# 1. CommonJS vs ES Modules

JavaScript has two major module systems:

```text
CommonJS
    ↓
require()
module.exports

ES Modules
    ↓
import
export
```

Example CommonJS:

```javascript
const express = require("express");
```

Example ES Modules:

```javascript
import express from "express";
```

---

# 2. Basic CommonJS Export

Create a file:

```text
math.js
```

Code:

```javascript
function add(a, b) {
  return a + b;
}

module.exports = {
  add,
};
```

Another file:

```text
app.js
```

Import:

```javascript
const math = require("./math");

console.log(math.add(10, 20));
```

Output:

```text
30
```

---

# 3. `module.exports`

`module.exports` defines what a CommonJS module makes available to other files.

Example:

```javascript
const name = "Sandip";

module.exports = name;
```

Import:

```javascript
const name = require("./user");

console.log(name);
```

Output:

```text
Sandip
```

---

# 4. Export an Object

You can export multiple values as an object.

```javascript
const name = "Sandip";

const age = 22;

const role = "developer";

module.exports = {
  name,
  age,
  role,
};
```

Import:

```javascript
const user = require("./user");

console.log(user.name);
console.log(user.age);
console.log(user.role);
```

---

# 5. Export Multiple Functions

```javascript
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

function multiply(a, b) {
  return a * b;
}

module.exports = {
  add,
  subtract,
  multiply,
};
```

Import:

```javascript
const {
  add,
  subtract,
  multiply,
} = require("./math");
```

Use:

```javascript
console.log(add(10, 5));

console.log(subtract(10, 5));

console.log(multiply(10, 5));
```

---

# 6. Destructuring with `require()`

Because CommonJS exports are often objects, you can use destructuring.

Example:

```javascript
module.exports = {
  add,
  subtract,
};
```

Import:

```javascript
const {
  add,
  subtract,
} = require("./math");
```

This is similar to named imports in ES Modules:

```javascript
import {
  add,
  subtract,
} from "./math.js";
```

The syntax is different because CommonJS and ES Modules are different module systems.

---

# 7. Export a Single Function

You can export one function directly.

```javascript
function greet(name) {
  return `Hello ${name}`;
}

module.exports = greet;
```

Import:

```javascript
const greet = require("./greet");

console.log(
  greet("Sandip")
);
```

Output:

```text
Hello Sandip
```

---

# 8. Export a Class

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello ${this.name}`);
  }
}

module.exports = User;
```

Import:

```javascript
const User = require("./User");

const user = new User("Sandip");

user.greet();
```

---

# 9. Export an Object with Methods

```javascript
const userService = {
  createUser() {
    console.log("Creating user");
  },

  getUser() {
    console.log("Getting user");
  },

  deleteUser() {
    console.log("Deleting user");
  },
};

module.exports = userService;
```

Import:

```javascript
const userService = require("./user.service");

userService.createUser();

userService.getUser();
```

---

# 10. `exports` Shortcut

CommonJS also provides:

```javascript
exports
```

For example:

```javascript
exports.add = (a, b) => {
  return a + b;
};

exports.subtract = (a, b) => {
  return a - b;
};
```

Import:

```javascript
const {
  add,
  subtract,
} = require("./math");
```

---

# 11. `exports` vs `module.exports`

Initially:

```text
exports
   ↓
module.exports
```

So this works:

```javascript
exports.add = add;
```

But this can break the connection:

```javascript
exports = add;
```

Because you are reassigning the local `exports` variable rather than changing `module.exports`.

For clarity, many developers prefer:

```javascript
module.exports = {
  add,
};
```

---

# 12. Important Difference

This works:

```javascript
exports.add = add;
```

This also works:

```javascript
module.exports.add = add;
```

But:

```javascript
exports = {
  add,
};
```

does not replace what `require()` receives.

If you want to replace the entire exported value, use:

```javascript
module.exports = {
  add,
};
```

---

# 13. CommonJS Import with `require()`

Basic syntax:

```javascript
const module = require("./module");
```

Package example:

```javascript
const express = require("express");
```

Node.js built-in module:

```javascript
const path = require("path");
```

Another example:

```javascript
const fs = require("fs");
```

---

# 14. Relative Paths

CommonJS can import local files using relative paths.

Current directory:

```javascript
const math = require("./math");
```

Parent directory:

```javascript
const user = require("../user");
```

So:

```text
./   → current directory
../  → parent directory
```

---

# 15. Importing a Directory

CommonJS can resolve certain directory imports according to Node.js module resolution rules.

For example:

```text
utils/
├── index.js
└── format.js
```

You can write:

```javascript
const utils = require("./utils");
```

Node.js can resolve the directory's entry module according to its resolution rules.

An explicit path is often clearer:

```javascript
const utils = require("./utils/index.js");
```

---

# 16. CommonJS and Node.js

CommonJS has historically been strongly associated with Node.js.

Example:

```javascript
const http = require("http");

const server = http.createServer(
  (req, res) => {
    res.end("Hello");
  }
);

server.listen(8000);
```

This is a traditional CommonJS Node.js program.

---

# 17. CommonJS with Express

Traditional Express application:

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.send("Hello World");
});

app.listen(8000);
```

Modern Node.js applications can also use ES Modules:

```javascript
import express from "express";

const app = express();
```

Both styles are used in real projects.

---

# 18. CommonJS Controller Example

`user.controller.js`:

```javascript
const getUsers = async (req, res) => {
  res.json({
    message: "Users",
  });
};

const createUser = async (req, res) => {
  res.status(201).json({
    message: "User created",
  });
};

module.exports = {
  getUsers,
  createUser,
};
```

Import in routes:

```javascript
const {
  getUsers,
  createUser,
} = require("./user.controller");
```

Use:

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

# 19. CommonJS Middleware Example

`auth.middleware.js`:

```javascript
const authMiddleware = (req, res, next) => {
  console.log("Checking authentication");

  next();
};

module.exports = authMiddleware;
```

Import:

```javascript
const authMiddleware =
  require("./auth.middleware");
```

Use:

```javascript
app.use(
  authMiddleware
);
```

---

# 20. CommonJS Configuration

You can export configuration values:

```javascript
const PORT = 8000;

const API_VERSION = "v1";

module.exports = {
  PORT,
  API_VERSION,
};
```

Import:

```javascript
const {
  PORT,
  API_VERSION,
} = require("./config");
```

---

# 21. CommonJS Utility Module

`utils.js`:

```javascript
function formatPrice(price) {
  return `$${price.toFixed(2)}`;
}

function capitalize(text) {
  return (
    text.charAt(0).toUpperCase() +
    text.slice(1)
  );
}

module.exports = {
  formatPrice,
  capitalize,
};
```

Import:

```javascript
const {
  formatPrice,
  capitalize,
} = require("./utils");
```

---

# 22. CommonJS Mongoose Model

Example:

```javascript
const mongoose = require("mongoose");

const userSchema =
  new mongoose.Schema({
    name: {
      type: String,
      required: true,
    },

    email: {
      type: String,
      required: true,
    },
  });

const User =
  mongoose.model("User", userSchema);

module.exports = User;
```

Import:

```javascript
const User =
  require("./user.model");
```

---

# 23. CommonJS vs ES Module Syntax

| Task                | CommonJS                 | ES Modules                          |
| ------------------- | ------------------------ | ----------------------------------- |
| Import              | `require()`              | `import`                            |
| Export              | `module.exports`         | `export`                            |
| Default-like export | `module.exports = value` | `export default value`              |
| Multiple exports    | Object                   | Named exports                       |
| File extension      | Often omitted            | Usually explicit in native Node ESM |
| Common Node usage   | Traditional              | Modern                              |

---

# 24. Export Comparison

### CommonJS

```javascript
module.exports = {
  add,
  subtract,
};
```

Import:

```javascript
const {
  add,
  subtract,
} = require("./math");
```

### ES Modules

```javascript
export {
  add,
  subtract,
};
```

Import:

```javascript
import {
  add,
  subtract,
} from "./math.js";
```

---

# 25. Single Export Comparison

### CommonJS

```javascript
module.exports = User;
```

Import:

```javascript
const User =
  require("./User");
```

### ES Modules

```javascript
export default User;
```

Import:

```javascript
import User from "./User.js";
```

These patterns are conceptually similar but belong to different module systems.

---

# 26. CommonJS Caching

Node.js caches loaded CommonJS modules.

For example:

```javascript
const config =
  require("./config");
```

If another module requires the same resolved module, Node.js can reuse the cached module rather than evaluating the file again.

This makes module-level state shared within the process for that module identity.

---

# 27. Module Execution

When a CommonJS module is loaded, its top-level code is executed.

Example:

```javascript
console.log(
  "Module loaded"
);

module.exports = {
  name: "Sandip",
};
```

When another file runs:

```javascript
require("./user");
```

the top-level `console.log()` executes as the module is loaded.

---

# 28. CommonJS `__dirname`

CommonJS modules traditionally provide:

```javascript
__dirname
```

which represents the directory of the current module.

Example:

```javascript
console.log(__dirname);
```

This can be useful when working with file paths.

---

# 29. CommonJS `__filename`

CommonJS also provides:

```javascript
__filename
```

which represents the resolved filename of the current module.

Example:

```javascript
console.log(__filename);
```

Together:

```text
__dirname
    → current module directory

__filename
    → current module filename
```

These CommonJS globals are not provided in the same way inside native ES Modules.

---

# 30. CommonJS `require()` is Runtime-Based

A CommonJS import is expressed as a function call:

```javascript
const math = require("./math");
```

This is different from static ES Module syntax:

```javascript
import math from "./math.js";
```

CommonJS therefore fits naturally with code that uses runtime `require()` calls.

For example:

```javascript
const moduleName = "./math";

const math = require(moduleName);
```

The exact resolution behavior depends on the Node.js module system and runtime context.

---

# 31. Conditional Require

CommonJS can be used conditionally:

```javascript
if (process.env.NODE_ENV === "development") {
  const debug = require("./debug");
  
  debug();
}
```

This style is possible because `require()` is a runtime operation.

For modern applications, dynamic `import()` is often used when working with ES Modules.

---

# 32. Mixing CommonJS and ES Modules

Avoid casually mixing:

```javascript
require()
```

and:

```javascript
import
```

in the same module.

For example, this is not generally valid as a normal CommonJS file:

```javascript
const express = require("express");

import userRouter from "./user.routes.js";
```

Choose the module system appropriate for the project and configure the runtime correctly.

---

# 33. Node.js Module Configuration

Node.js can determine the module system from project configuration and file extensions.

A package can explicitly use ES Modules with:

```json
{
  "type": "module"
}
```

Then `.js` files are treated as ES Modules by default.

Without that configuration, `.js` files in a typical Node.js package are commonly treated as CommonJS.

Node.js also supports explicit extensions such as:

```text
.mjs
.cjs
```

Generally:

```text
.mjs → ES Module
.cjs → CommonJS
```

---

# 34. `.cjs` Files

If you want to explicitly mark a file as CommonJS:

```text
server.cjs
```

Example:

```javascript
const express = require("express");

const app = express();

app.listen(8000);
```

The `.cjs` extension tells Node.js to treat the file as CommonJS.

---

# 35. `.mjs` Files

If you want to explicitly mark a file as an ES Module:

```text
server.mjs
```

Example:

```javascript
import express from "express";

const app = express();

app.listen(8000);
```

The `.mjs` extension tells Node.js to treat the file as an ES Module.

---

# 36. CommonJS Project Structure

A traditional Node.js project might look like:

```text
project/
├── package.json
├── server.js
└── src/
    ├── app.js
    ├── routes/
    │   └── user.routes.js
    ├── controllers/
    │   └── user.controller.js
    ├── models/
    │   └── user.model.js
    └── utils/
        └── response.js
```

Example dependency flow:

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

---

# 37. CommonJS with `package.json`

A traditional CommonJS project can use:

```json
{
  "name": "my-app",
  "version": "1.0.0"
}
```

If the package does not declare:

```json
{
  "type": "module"
}
```

then `.js` files are commonly treated as CommonJS under Node.js's default package behavior.

---

# 38. CommonJS with Third-Party Packages

Example:

```javascript
const express = require("express");
```

Another package:

```javascript
const bcrypt = require("bcrypt");
```

Another:

```javascript
const mongoose = require("mongoose");
```

Node.js resolves packages from:

```text
node_modules/
```

according to its module resolution rules.

---

# 39. CommonJS Error Example

Suppose:

```javascript
module.exports = {
  add,
};
```

but you write:

```javascript
const add =
  require("./math");
```

Then `add` receives the exported object:

```javascript
{
  add: [Function]
}
```

To destructure the function:

```javascript
const {
  add,
} = require("./math");
```

Or:

```javascript
const math =
  require("./math");

math.add(10, 20);
```

---

# 40. CommonJS Best Practices

### Keep one clear export style

Prefer either:

```javascript
module.exports = {
  add,
  subtract,
};
```

or:

```javascript
exports.add = add;
exports.subtract = subtract;
```

Do not unnecessarily mix patterns.

### Prefer `module.exports` when replacing the whole export

```javascript
module.exports = User;
```

### Keep modules focused

A module should have a clear responsibility.

### Avoid unnecessary circular dependencies

They can make initialization and module state harder to understand.

### Use a consistent module system

If your project uses ES Modules, use:

```javascript
import
export
```

If it uses CommonJS, use:

```javascript
require
module.exports
```

unless there is a deliberate interoperability reason.

---

# 41. CommonJS Quick Cheat Sheet

### Import a package

```javascript
const express = require("express");
```

### Import a local module

```javascript
const math = require("./math");
```

### Export one value

```javascript
module.exports = User;
```

### Export multiple values

```javascript
module.exports = {
  add,
  subtract,
};
```

### Import multiple values

```javascript
const {
  add,
  subtract,
} = require("./math");
```

### Export with `exports`

```javascript
exports.add = add;
```

### Current directory

```javascript
__dirname
```

### Current file

```javascript
__filename
```

### Explicit CommonJS file

```text
.cjs
```

---

# 42. CommonJS vs ES Modules — Practical View

```text
CommonJS
│
├── require()
├── module.exports
├── exports
├── __dirname
├── __filename
└── Traditional Node.js projects
```

```text
ES Modules
│
├── import
├── export
├── export default
├── Dynamic import()
└── Modern JavaScript applications
```

For a modern Node.js/Express application, choose one module system deliberately and configure the project consistently.

---

# 43. Final Example

## CommonJS

`math.js`:

```javascript
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = {
  add,
  subtract,
};
```

`app.js`:

```javascript
const {
  add,
  subtract,
} = require("./math");

console.log(
  add(20, 10)
);

console.log(
  subtract(20, 10)
);
```

Output:

```text
30
10
```

---

# 44. CommonJS to ES Modules

### CommonJS

```javascript
const User =
  require("./User");

module.exports = User;
```

### ES Modules

```javascript
import User from "./User.js";

export default User;
```

Multiple exports:

### CommonJS

```javascript
module.exports = {
  createUser,
  getUser,
  deleteUser,
};
```

### ES Modules

```javascript
export {
  createUser,
  getUser,
  deleteUser,
};
```

---

# Key Takeaways

* CommonJS is a JavaScript module system traditionally associated with Node.js.
* `require()` imports a CommonJS module.
* `module.exports` defines the module's exported value.
* `exports` is a convenient reference for adding properties to `module.exports`.
* `exports = ...` does not replace `module.exports`.
* Multiple values are commonly exported as an object.
* CommonJS supports exporting functions, classes, objects, arrays, and other values.
* `__dirname` represents the current module's directory in CommonJS.
* `__filename` represents the current module's filename.
* `.cjs` explicitly identifies a CommonJS file.
* `.mjs` explicitly identifies an ES Module.
* Node.js supports both CommonJS and ES Modules.
* Use a consistent module system throughout a project whenever practical.
* Modern Node.js projects commonly use ES Modules, while CommonJS remains important for existing Node.js applications and packages.
* Understanding CommonJS is especially useful when working with older Node.js projects and packages.
