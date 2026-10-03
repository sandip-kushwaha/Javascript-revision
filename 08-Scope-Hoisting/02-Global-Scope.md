# JavaScript Global Scope

**Global scope** is the outermost scope in JavaScript.

A variable in the global scope can generally be accessed from other code within the same script or module context, depending on how it was declared.

Global scope is useful for values that genuinely need application-wide access, but too many global variables can make applications difficult to maintain.

---

# 1. What Is Global Scope?

A variable declared outside functions and blocks is in the outermost scope of a classic script.

```javascript
const appName = "Hotel Management System";

console.log(appName);
```

`appName` is available in the surrounding script because it was declared outside any function or block.

---

# 2. Global Variable Example

```javascript
const apiUrl = "https://api.example.com";

function getUsers() {
  console.log(apiUrl);
}

getUsers();
```

Output:

```text
https://api.example.com
```

`getUsers()` can access `apiUrl` because the function's scope can look outward.

---

# 3. Global Scope and Function Scope

Consider:

```javascript
const company = "Tech Corp";

function showCompany() {
  const department = "Development";

  console.log(company);
  console.log(department);
}

showCompany();
```

Inside `showCompany()`:

```text
company    → outer/global scope
department → function scope
```

But outside:

```javascript
console.log(department);
```

does not work because `department` belongs to the function scope.

---

# 4. Global Scope and Block Scope

`let` and `const` declared at the top level are available throughout their surrounding top-level scope.

```javascript
const appName = "Hotel App";

if (true) {
  console.log(appName);
}
```

Output:

```text
Hotel App
```

But a variable declared inside the block is not available outside:

```javascript
if (true) {
  const status = "active";
}

console.log(status);
```

This causes a `ReferenceError`.

---

# 5. Global `var`

In a classic browser script, a top-level `var` declaration has a special relationship with the global object.

```javascript
var appName = "Hotel App";

console.log(window.appName);
```

In a normal browser script, this can produce:

```text
Hotel App
```

This is different from top-level `let` and `const`.

---

# 6. `let` and `const` Are Not Properties of `window`

In a browser classic script:

```javascript
var a = 10;
let b = 20;
const c = 30;

console.log(window.a);
console.log(window.b);
console.log(window.c);
```

Typically:

```text
10
undefined
undefined
```

So:

```text
var   → can create a window property in classic scripts
let   → does not
const → does not
```

This is one reason top-level `var` can cause global namespace problems.

---

# 7. Global Object

JavaScript environments have a global object.

In browsers, the global object is:

```javascript
window
```

In modern JavaScript, a standard cross-environment reference is:

```javascript
globalThis
```

Example:

```javascript
console.log(globalThis);
```

`globalThis` provides a standard way to access the global object across JavaScript environments.

---

# 8. Browser Global Object

In a browser:

```javascript
console.log(globalThis === window);
```

Output:

```text
true
```

So in browsers:

```text
globalThis
   ↓
window
```

---

# 9. Global Scope in Node.js

Node.js also provides a global object.

Modern Node.js code can use:

```javascript
globalThis
```

Node.js also exposes:

```javascript
global
```

For example:

```javascript
console.log(globalThis);
```

The exact behavior of top-level variables depends on whether you're using CommonJS or ES modules.

---

# 10. Global Scope and ES Modules

ES modules have their own module scope.

Example:

### `config.js`

```javascript
const apiUrl = "/api/v1";

export {
  apiUrl
};
```

`apiUrl` is not automatically added as a browser `window` property.

Another module must import it:

```javascript
import { apiUrl } from "./config.js";

console.log(apiUrl);
```

This helps prevent accidental global variables.

---

# 11. Global Variables in Classic Scripts

Consider:

```html
<script>
  var username = "Sandip";
</script>

<script>
  console.log(username);
</script>
```

The second script can access the variable.

This happens because both classic scripts share the relevant global environment.

---

# 12. Global Variables with `let` and `const`

Consider:

```html
<script>
  let username = "Sandip";
</script>

<script>
  console.log(username);
</script>
```

Top-level `let` in a classic script can still be visible to other script code through the global lexical environment, but it does **not** become a property of `window`.

For example:

```javascript
let username = "Sandip";

console.log(username);
console.log(window.username);
```

Typically:

```text
Sandip
undefined
```

The important distinction is:

```text
Global lexical binding ≠ window property
```

---

# 13. Accidental Global Variables

One common mistake is creating a variable without declaring it.

Avoid code like:

```javascript
function createUser() {
  username = "Sandip";
}
```

Depending on the environment and strictness, this can create or attempt to create a global variable.

Instead use:

```javascript
function createUser() {
  const username = "Sandip";
}
```

Always declare variables with:

```javascript
const
```

or:

```javascript
let
```

when appropriate.

---

# 14. Strict Mode Helps

Strict mode prevents accidental assignment to undeclared variables.

```javascript
"use strict";

username = "Sandip";
```

This produces an error because `username` was never declared.

Without strict mode, older non-strict code could behave differently.

ES modules automatically use strict mode.

---

# 15. Why Global Variables Can Be Dangerous

Suppose an application contains:

```javascript
var user = "Sandip";
```

Another part of the application might accidentally use the same global name:

```javascript
var user = "Admin";
```

Now the application can have unexpected behavior.

As applications become larger, managing global variables becomes harder.

---

# 16. Global Namespace Pollution

**Global namespace pollution** means putting too many unrelated names into the global environment.

For example:

```javascript
var user;
var product;
var order;
var cart;
var settings;
var api;
var config;
var helper;
```

A large application can become difficult to understand.

Modules provide a cleaner structure.

---

# 17. Better Approach: Modules

Instead of:

```javascript
var apiUrl = "...";
var token = "...";
var user = "...";
```

spread across global scripts, use modules.

### `config.js`

```javascript
export const API_URL = "/api/v1";
```

### `auth.js`

```javascript
export function login() {
  // login logic
}
```

### `app.js`

```javascript
import { API_URL } from "./config.js";
import { login } from "./auth.js";
```

Now dependencies are explicit.

---

# 18. Global Constants

Some applications have values that are logically shared across many modules.

For example:

```javascript
export const APP_NAME = "Hotel Management System";
export const API_VERSION = "v1";
```

These can be imported wherever required.

This is generally better than putting everything on the global object.

---

# 19. Global Functions

Avoid creating unnecessary global functions like:

```javascript
function showMessage() {
  console.log("Hello");
}
```

If many scripts use the same name, conflicts can occur.

Instead, put reusable functions in modules:

```javascript
export function showMessage() {
  console.log("Hello");
}
```

Then:

```javascript
import { showMessage } from "./utils.js";
```

---

# 20. Global Object vs Global Scope

These concepts are related but not identical.

### Global scope

The outermost lexical environment where top-level bindings can exist.

### Global object

An object representing the environment's global object.

In browsers:

```javascript
window
```

and:

```javascript
globalThis
```

refer to the same global object.

But not every global binding is necessarily a property of that object.

---

# 21. Example

```javascript
var a = 10;
let b = 20;
const c = 30;

console.log(a);
console.log(b);
console.log(c);
```

All three variables can be used in their appropriate top-level scope.

But in a browser classic script:

```javascript
console.log(window.a);
console.log(window.b);
console.log(window.c);
```

typically gives:

```text
10
undefined
undefined
```

because only the `var` binding becomes a property of the global object in this situation.

---

# 22. Global Scope in a Function

A function can access global variables:

```javascript
const hotelName = "Grand Hotel";

function displayHotel() {
  console.log(hotelName);
}

displayHotel();
```

Output:

```text
Grand Hotel
```

The function searches its own scope first.

If the variable isn't there, JavaScript searches outward.

---

# 23. Local Variable Shadows Global Variable

```javascript
const role = "admin";

function showRole() {
  const role = "waiter";

  console.log(role);
}

showRole();

console.log(role);
```

Output:

```text
waiter
admin
```

The function's local variable takes priority inside the function.

---

# 24. Accessing the Global Variable

If a local variable shadows a global property, browser code can sometimes access the global object explicitly.

Example:

```javascript
var role = "admin";

function showRole() {
  var role = "waiter";

  console.log(role);
  console.log(globalThis.role);
}

showRole();
```

Output in a classic browser script:

```text
waiter
admin
```

However, relying on global-object properties this way is usually unnecessary in modern application code. Modules and explicit imports are cleaner.

---

# 25. Global Scope and Security

Global variables should not be used for sensitive information.

Avoid putting secrets such as:

```javascript
const databasePassword = "...";
const privateApiKey = "...";
```

into browser-side global code.

Anything sent to browser JavaScript can generally be inspected by the user.

For server-side applications, sensitive values should normally be kept in environment variables or secure secret-management systems rather than exposed as browser globals.

---

# 26. Global Scope in a Frontend Application

A frontend application might have:

```text
src/
├── app.js
├── config.js
├── auth.js
├── api.js
└── utils.js
```

Instead of global variables:

```javascript
window.api = ...
window.auth = ...
window.utils = ...
```

prefer modules:

```javascript
import { api } from "./api.js";
import { login } from "./auth.js";
```

This makes dependencies clear.

---

# 27. Practical Example

Suppose a hotel application needs a common API URL.

### `config.js`

```javascript
export const API_URL =
  "https://example.com/api/v1";
```

### `userApi.js`

```javascript
import { API_URL } from "./config.js";

export async function getUsers() {
  const response = await fetch(`${API_URL}/users`);

  return response.json();
}
```

### `orderApi.js`

```javascript
import { API_URL } from "./config.js";

export async function getOrders() {
  const response = await fetch(`${API_URL}/orders`);

  return response.json();
}
```

The API URL is shared without creating a global `window.API_URL`.

---

# 28. Global Scope Best Practices

### Prefer local scope

Keep variables close to where they are used.

### Prefer `const`

Use:

```javascript
const
```

when reassignment isn't required.

### Use `let` when necessary

Use:

```javascript
let
```

when the binding needs to change.

### Avoid unnecessary `var`

Modern JavaScript generally favors `let` and `const`.

### Use modules

Modules provide clear boundaries between pieces of code.

### Avoid accidental globals

Always declare variables.

### Don't store secrets in frontend globals

Frontend code is accessible to the client.

---

# 29. Quick Comparison

| Concept         | Meaning                                                |
| --------------- | ------------------------------------------------------ |
| Global Scope    | Outermost scope                                        |
| Global Object   | Environment's global object                            |
| `globalThis`    | Standard reference to global object                    |
| `window`        | Browser global object                                  |
| `global`        | Node.js global object                                  |
| Module Scope    | Scope belonging to an ES module                        |
| Global Variable | A variable available from the outer/global environment |

---

# 30. Key Takeaways

* Global scope is the outermost scope.
* Functions can access variables from outer/global scopes.
* Inner variables can shadow global variables.
* `var`, `let`, and `const` behave differently at the top level.
* In browser classic scripts, top-level `var` can become a `window` property.
* Top-level `let` and `const` do not become `window` properties.
* `globalThis` provides a standard way to access the global object.
* ES modules have their own module scope.
* Avoid unnecessary global variables.
* Modules are usually a better way to share functionality.
* Never treat browser global variables as a secure place for secrets.
* Understanding global scope makes function scope, block scope, modules, and closures easier to understand.

---
