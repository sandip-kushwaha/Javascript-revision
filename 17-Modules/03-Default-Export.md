# JavaScript Default Export

A **default export** is used when a JavaScript module has one primary value, function, class, or object that it wants to make available to other modules.

The main syntax is:

```javascript
export default value;
```

Then import it without curly braces:

```javascript
import value from "./file.js";
```

---

# 1. Basic Default Export

```javascript
const name = "Sandip";

export default name;
```

Import:

```javascript
import name from "./user.js";

console.log(name);
```

Output:

```text
Sandip
```

---

# 2. Default Export a Function

You can export a function directly:

```javascript
export default function greet() {
  console.log("Hello Sandip");
}
```

Import:

```javascript
import greet from "./greet.js";

greet();
```

Output:

```text
Hello Sandip
```

---

# 3. Default Export an Arrow Function

```javascript
const greet = () => {
  console.log("Hello Sandip");
};

export default greet;
```

Import:

```javascript
import greet from "./greet.js";

greet();
```

You can also write:

```javascript
export default () => {
  console.log("Hello Sandip");
};
```

---

# 4. Default Export a Class

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello ${this.name}`);
  }
}

export default User;
```

Import:

```javascript
import User from "./User.js";

const user = new User("Sandip");

user.greet();
```

---

# 5. Default Export an Object

```javascript
const user = {
  name: "Sandip",
  age: 22,
  role: "developer",
};

export default user;
```

Import:

```javascript
import user from "./user.js";

console.log(user.name);
console.log(user.role);
```

---

# 6. Default Export an Array

```javascript
const users = [
  "Sandip",
  "Ram",
  "Shyam",
];

export default users;
```

Import:

```javascript
import users from "./users.js";

console.log(users);
```

---

# 7. Default Export a Value Directly

You do not always need to create a variable first.

```javascript
export default "Hello World";
```

Import:

```javascript
import message from "./message.js";

console.log(message);
```

Another example:

```javascript
export default 100;
```

Import:

```javascript
import price from "./price.js";

console.log(price);
```

---

# 8. Default Export a Function Directly

```javascript
export default function add(a, b) {
  return a + b;
}
```

Import:

```javascript
import add from "./math.js";

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 9. Default Export Function Name

A default-exported function can have a name:

```javascript
export default function greet() {
  console.log("Hello");
}
```

The importer chooses its local name:

```javascript
import greet from "./greet.js";
```

The importing module can technically choose another local name:

```javascript
import sayHello from "./greet.js";
```

Both refer to the same default export.

For readability, use a meaningful and consistent name.

---

# 10. Default Import Does Not Use Curly Braces

Correct:

```javascript
import User from "./User.js";
```

Incorrect for a default export:

```javascript
import { User } from "./User.js";
```

The curly braces indicate a **named import**.

Remember:

```text
Default export
      ↓
import User from "./User.js"

Named export
      ↓
import { User } from "./User.js"
```

---

# 11. One Default Export Per Module

A module can have only one default export.

Correct:

```javascript
export default User;
```

You cannot have:

```javascript
export default User;
export default Product;
```

in the same module.

If you need multiple exported values, use named exports:

```javascript
export {
  User,
  Product,
};
```

---

# 12. Default + Named Exports

A module can have one default export together with multiple named exports.

```javascript
const User = {
  name: "Sandip",
};

const role = "developer";

function login() {
  console.log("Login");
}

export default User;

export {
  role,
  login,
};
```

Import:

```javascript
import User, {
  role,
  login,
} from "./user.js";
```

Usage:

```javascript
console.log(User.name);

console.log(role);

login();
```

---

# 13. Default Export vs Named Export

### Default

```javascript
export default User;
```

Import:

```javascript
import User from "./User.js";
```

### Named

```javascript
export { User };
```

Import:

```javascript
import { User } from "./User.js";
```

The key syntax difference is:

```text
Default → no { }
Named   → uses { }
```

---

# 14. Default Export in React

Default exports are commonly used for React components.

Example:

```jsx
function Header() {
  return (
    <header>
      My Website
    </header>
  );
}

export default Header;
```

Import:

```jsx
import Header from "./Header.jsx";
```

Use:

```jsx
function App() {
  return (
    <div>
      <Header />
    </div>
  );
}

export default App;
```

---

# 15. Default Export Component Directly

You can also write:

```jsx
export default function Header() {
  return (
    <header>
      My Website
    </header>
  );
}
```

Import:

```jsx
import Header from "./Header.jsx";
```

This is a common React pattern.

---

# 16. React Page Example

Suppose:

```text
src/
├── pages/
│   ├── Home.jsx
│   ├── Login.jsx
│   └── Dashboard.jsx
└── App.jsx
```

`Home.jsx`:

```jsx
export default function Home() {
  return <h1>Home Page</h1>;
}
```

`Login.jsx`:

```jsx
export default function Login() {
  return <h1>Login Page</h1>;
}
```

`Dashboard.jsx`:

```jsx
export default function Dashboard() {
  return <h1>Dashboard</h1>;
}
```

Import:

```jsx
import Home from "./pages/Home.jsx";
import Login from "./pages/Login.jsx";
import Dashboard from "./pages/Dashboard.jsx";
```

Each file has one primary component, so default exports work naturally.

---

# 17. Default Export in Express

A router is often exported as the default value.

Example:

```javascript
import express from "express";

const router = express.Router();

router.get("/users", (req, res) => {
  res.json({
    message: "Users",
  });
});

export default router;
```

Import:

```javascript
import userRouter from "./user.routes.js";
```

Then:

```javascript
app.use(
  "/api",
  userRouter
);
```

---

# 18. Default Export Controllers

You can export a controller as the default value:

```javascript
const userController = {
  getUsers(req, res) {
    res.json({
      message: "Users",
    });
  },

  createUser(req, res) {
    res.json({
      message: "User created",
    });
  },
};

export default userController;
```

Import:

```javascript
import userController from "./user.controller.js";
```

Use:

```javascript
router.get(
  "/users",
  userController.getUsers
);
```

---

# 19. Default Export Model

Example with Mongoose:

```javascript
import mongoose from "mongoose";

const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
  },

  email: {
    type: String,
    required: true,
  },
});

const User = mongoose.model(
  "User",
  userSchema
);

export default User;
```

Import:

```javascript
import User from "./user.model.js";
```

This pattern is common in Node.js and Express applications.

---

# 20. Default Export Utility

Suppose you have one main utility function:

```javascript
function generateToken(userId) {
  return `token-${userId}`;
}

export default generateToken;
```

Import:

```javascript
import generateToken from "./generateToken.js";
```

Use:

```javascript
const token = generateToken("123");
```

---

# 21. Default Export from an Index File

Suppose:

```text
components/
├── Button.jsx
├── Header.jsx
└── index.js
```

`Button.jsx`:

```jsx
export default function Button() {
  return <button>Click</button>;
}
```

`Header.jsx`:

```jsx
export default function Header() {
  return <header>Header</header>;
}
```

`index.js`:

```javascript
export {
  default as Button,
} from "./Button.jsx";

export {
  default as Header,
} from "./Header.jsx";
```

Now:

```javascript
import {
  Button,
  Header,
} from "./components/index.js";
```

---

# 22. Re-Export a Default Value

Suppose `User.js` contains:

```javascript
export default User;
```

Another file can re-export it:

```javascript
export {
  default,
} from "./User.js";
```

Then:

```javascript
import User from "./index.js";
```

---

# 23. Rename Default Export During Re-Export

A useful pattern is:

```javascript
export {
  default as User,
} from "./User.js";
```

Now:

```javascript
import { User } from "./index.js";
```

This turns a default export from another file into a named export from the central file.

---

# 24. Default Export and Aliasing

Default imports do not require `as`.

For example:

```javascript
import User from "./User.js";
```

You can choose another local name directly:

```javascript
import Account from "./User.js";
```

There is no need for:

```javascript
import User as Account from "./User.js";
```

That syntax is invalid.

---

# 25. Common Mistake: Curly Braces

Suppose:

```javascript
export default function login() {
  console.log("Login");
}
```

Correct:

```javascript
import login from "./login.js";
```

Wrong:

```javascript
import { login } from "./login.js";
```

The second syntax searches for a named export called `login`, but the module has a default export.

---

# 26. Common Mistake: Multiple Defaults

Wrong:

```javascript
export default User;

export default Product;
```

Correct:

```javascript
export default User;

export {
  Product,
};
```

Then:

```javascript
import User, {
  Product,
} from "./models.js";
```

---

# 27. Common Mistake: Mixing Import Styles

Suppose:

```javascript
export default User;

export const role = "admin";
```

Correct:

```javascript
import User, {
  role,
} from "./user.js";
```

Do not write:

```javascript
import {
  User,
  role,
} from "./user.js";
```

`User` is the default export, while `role` is named.

---

# 28. When to Use Default Export

Default exports work well when a module represents one primary thing.

Examples:

```text
One React component
One Mongoose model
One Express router
One main utility
One configuration object
One class
```

Examples:

```javascript
export default User;
```

```javascript
export default router;
```

```javascript
export default App;
```

---

# 29. When Named Exports Are Useful

Named exports work well when a module provides multiple related values.

Example:

```javascript
export const add = (a, b) => a + b;

export const subtract = (a, b) => a - b;

export const multiply = (a, b) => a * b;
```

Import:

```javascript
import {
  add,
  subtract,
  multiply,
} from "./math.js";
```

---

# 30. Default Export Decision

A simple way to structure modules:

```text
One main thing
      ↓
Default export

Multiple related things
      ↓
Named exports
```

For example:

```text
User.js
    ↓
User class
    ↓
default export
```

While:

```text
math.js
    ↓
add
subtract
multiply
    ↓
named exports
```

This is a convention rather than a language requirement.

---

# 31. Default Export with React Components

A common component structure:

```text
components/
├── Navbar.jsx
├── Sidebar.jsx
├── Footer.jsx
└── Button.jsx
```

`Navbar.jsx`:

```jsx
export default function Navbar() {
  return (
    <nav>
      Navbar
    </nav>
  );
}
```

`Sidebar.jsx`:

```jsx
export default function Sidebar() {
  return (
    <aside>
      Sidebar
    </aside>
  );
}
```

`Footer.jsx`:

```jsx
export default function Footer() {
  return (
    <footer>
      Footer
    </footer>
  );
}
```

Import:

```jsx
import Navbar from "./components/Navbar.jsx";
import Sidebar from "./components/Sidebar.jsx";
import Footer from "./components/Footer.jsx";
```

---

# 32. Default Export with Backend Controllers

Example:

```javascript
const authController = {
  login(req, res) {
    res.json({
      message: "Login",
    });
  },

  logout(req, res) {
    res.json({
      message: "Logout",
    });
  },
};

export default authController;
```

Import:

```javascript
import authController from "./auth.controller.js";
```

Use:

```javascript
router.post(
  "/login",
  authController.login
);

router.post(
  "/logout",
  authController.logout
);
```

---

# 33. Default Export Summary

```text
Default Export
      │
      ├── One default export per module
      │
      ├── Imported without { }
      │
      ├── Importer chooses local name
      │
      ├── Useful for one primary value
      │
      └── Common in React components,
          Express routers, and models
```

---

# 34. Quick Cheat Sheet

### Export Value

```javascript
export default user;
```

### Import Value

```javascript
import user from "./user.js";
```

### Export Function

```javascript
export default function greet() {}
```

### Import Function

```javascript
import greet from "./greet.js";
```

### Export Class

```javascript
export default class User {}
```

### Import Class

```javascript
import User from "./User.js";
```

### Export Object

```javascript
export default {
  name: "Sandip",
};
```

### Export Array

```javascript
export default [
  "React",
  "Node.js",
];
```

### Default + Named

```javascript
export default User;

export const role = "admin";
```

Import:

```javascript
import User, {
  role,
} from "./user.js";
```

### Re-export Default as Named

```javascript
export {
  default as User,
} from "./User.js";
```

---

# 35. Key Takeaways

* A module can have only one default export.
* Default exports are imported without curly braces.
* The importer chooses the local name of a default import.
* Functions, classes, objects, arrays, and primitive values can be default exports.
* React components commonly use default exports.
* Express routers and Mongoose models commonly use default exports.
* A default export can exist alongside multiple named exports.
* Default imports do not use `as` for renaming.
* `export { default as Name }` is useful for re-exporting a default value as a named export.
* Use default exports when a module has one clear primary value.
* Use named exports when a module exposes multiple related values.
