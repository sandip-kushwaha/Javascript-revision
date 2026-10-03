# JavaScript localStorage

`localStorage` is a browser API used to store data that remains available even after the browser tab or browser is closed.

It is commonly used for:

* Theme preferences
* Language preferences
* Shopping cart data
* UI settings
* Non-sensitive application preferences

> `localStorage` stores data as **strings**.

---

# 1. What is localStorage?

`localStorage` is part of the browser's Web Storage API.

Basic example:

```javascript
localStorage.setItem("username", "Sandip");
```

Read the value:

```javascript
const username = localStorage.getItem("username");

console.log(username);
```

Output:

```text
Sandip
```

---

# 2. localStorage Persistence

Unlike temporary JavaScript variables, `localStorage` data normally remains after:

* Page refresh
* Tab closing
* Browser closing
* Opening the website again

Example:

```javascript
localStorage.setItem("theme", "dark");
```

Later:

```javascript
const theme = localStorage.getItem("theme");

console.log(theme);
```

Output:

```text
dark
```

---

# 3. Storing Data

Use:

```javascript
localStorage.setItem(key, value);
```

Example:

```javascript
localStorage.setItem("username", "Sandip");
localStorage.setItem("theme", "dark");
localStorage.setItem("language", "en");
```

---

# 4. Reading Data

Use:

```javascript
localStorage.getItem(key);
```

Example:

```javascript
const username = localStorage.getItem("username");

console.log(username);
```

If the key does not exist:

```javascript
const value = localStorage.getItem("unknown");

console.log(value);
```

Output:

```text
null
```

---

# 5. Updating Data

Calling `setItem()` with an existing key replaces its value.

```javascript
localStorage.setItem("theme", "light");

localStorage.setItem("theme", "dark");
```

Now:

```javascript
console.log(
    localStorage.getItem("theme")
);
```

Output:

```text
dark
```

---

# 6. Removing One Item

Use:

```javascript
localStorage.removeItem(key);
```

Example:

```javascript
localStorage.setItem("username", "Sandip");

localStorage.removeItem("username");
```

Now:

```javascript
console.log(
    localStorage.getItem("username")
);
```

Output:

```text
null
```

---

# 7. Clearing localStorage

To remove all data stored by the current website:

```javascript
localStorage.clear();
```

Be careful:

```javascript
localStorage.clear();
```

removes all localStorage entries belonging to that origin.

---

# 8. Checking Number of Items

Use:

```javascript
localStorage.length;
```

Example:

```javascript
localStorage.setItem("name", "Sandip");
localStorage.setItem("theme", "dark");

console.log(localStorage.length);
```

Output:

```text
2
```

---

# 9. Getting a Key by Index

Use:

```javascript
localStorage.key(index);
```

Example:

```javascript
const key = localStorage.key(0);

console.log(key);
```

The order should not be relied upon for application logic.

---

# 10. localStorage Only Stores Strings

This is very important.

Suppose:

```javascript
const age = 22;

localStorage.setItem("age", age);
```

When reading:

```javascript
const age = localStorage.getItem("age");

console.log(age);
console.log(typeof age);
```

Output:

```text
22
string
```

The stored value is returned as a string.

---

# 11. Storing Numbers

If you store a number:

```javascript
localStorage.setItem("age", 22);
```

Read it:

```javascript
const age = localStorage.getItem("age");

console.log(age);
```

It is:

```text
"22"
```

If you need a number:

```javascript
const age = Number(
    localStorage.getItem("age")
);
```

Now:

```javascript
console.log(typeof age);
```

Output:

```text
number
```

---

# 12. Storing Boolean Values

Consider:

```javascript
const isLoggedIn = true;

localStorage.setItem(
    "isLoggedIn",
    isLoggedIn
);
```

When reading:

```javascript
const value =
    localStorage.getItem("isLoggedIn");

console.log(value);
```

Result:

```text
"true"
```

This is a string, not a Boolean.

Convert it carefully:

```javascript
const isLoggedIn =
    localStorage.getItem("isLoggedIn") === "true";

console.log(isLoggedIn);
```

Result:

```text
true
```

---

# 13. Storing Objects

You cannot directly store an object and expect it to remain an object.

Avoid:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

localStorage.setItem("user", user);
```

Instead, convert it to JSON:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

# 14. Reading an Object

Use `JSON.parse()` when retrieving JSON data.

```javascript
const user = {
    name: "Sandip",
    age: 22
};

localStorage.setItem(
    "user",
    JSON.stringify(user)
);

const storedUser = JSON.parse(
    localStorage.getItem("user")
);

console.log(storedUser.name);
```

Output:

```text
Sandip
```

---

# 15. Storing Arrays

Arrays also need JSON conversion.

```javascript
const users = [
    "Sandip",
    "Ram",
    "Hari"
];

localStorage.setItem(
    "users",
    JSON.stringify(users)
);
```

Read:

```javascript
const users = JSON.parse(
    localStorage.getItem("users")
);

console.log(users);
```

Result:

```javascript
["Sandip", "Ram", "Hari"]
```

---

# 16. Updating an Object

Suppose localStorage contains:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

Read it:

```javascript
const storedUser = JSON.parse(
    localStorage.getItem("user")
);
```

Update:

```javascript
storedUser.age = 23;
```

Store it again:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(storedUser)
);
```

---

# 17. Safe JSON Parsing

If the key does not exist:

```javascript
localStorage.getItem("user");
```

returns:

```text
null
```

Avoid blindly parsing unknown data.

A common pattern is:

```javascript
const storedUser =
    localStorage.getItem("user");

const user = storedUser
    ? JSON.parse(storedUser)
    : null;
```

Now:

```javascript
console.log(user);
```

will be:

```text
null
```

if the item does not exist.

---

# 18. Example — Theme

Store the selected theme:

```javascript
function setTheme(theme) {
    localStorage.setItem(
        "theme",
        theme
    );
}
```

Use:

```javascript
setTheme("dark");
```

Read:

```javascript
const theme =
    localStorage.getItem("theme");

console.log(theme);
```

---

# 19. Example — Theme on Page Load

```javascript
const theme =
    localStorage.getItem("theme");

if (theme === "dark") {
    document.body.classList.add("dark");
}
```

This allows a user's theme preference to survive a page refresh.

---

# 20. Example — Save Theme

```javascript
const themeButton =
    document.querySelector("#themeButton");

themeButton.addEventListener("click", () => {
    localStorage.setItem(
        "theme",
        "dark"
    );
});
```

---

# 21. Example — Shopping Cart

Suppose:

```javascript
const cart = [
    {
        id: 1,
        name: "Burger",
        price: 250,
        quantity: 2
    },
    {
        id: 2,
        name: "Pizza",
        price: 500,
        quantity: 1
    }
];
```

Store it:

```javascript
localStorage.setItem(
    "cart",
    JSON.stringify(cart)
);
```

Read it:

```javascript
const storedCart =
    localStorage.getItem("cart");

const cartData = storedCart
    ? JSON.parse(storedCart)
    : [];

console.log(cartData);
```

---

# 22. Example — Add Item to Cart

```javascript
function addToCart(product) {
    const storedCart =
        localStorage.getItem("cart");

    const cart = storedCart
        ? JSON.parse(storedCart)
        : [];

    cart.push(product);

    localStorage.setItem(
        "cart",
        JSON.stringify(cart)
    );
}
```

Example:

```javascript
addToCart({
    id: 1,
    name: "Burger",
    price: 250
});
```

---

# 23. Example — Remove Cart

```javascript
function clearCart() {
    localStorage.removeItem("cart");
}
```

This removes only the cart instead of deleting all application storage.

---

# 24. Checking Whether a Key Exists

There is no separate `hasItem()` method.

You can use:

```javascript
const value =
    localStorage.getItem("theme");

if (value !== null) {
    console.log("Theme exists");
}
```

For example:

```javascript
if (
    localStorage.getItem("username") !== null
) {
    console.log("Username exists");
}
```

---

# 25. Iterating Through localStorage

You can inspect all keys:

```javascript
for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i);
    const value = localStorage.getItem(key);

    console.log(key, value);
}
```

Remember that key ordering should not be treated as meaningful.

---

# 26. localStorage and Same-Origin Policy

`localStorage` is separated by origin.

An origin is based on:

```text
scheme
+
host
+
port
```

For example:

```text
https://example.com
```

has different storage from:

```text
http://example.com
```

and potentially different storage from:

```text
https://api.example.com
```

Storage is not automatically shared across different origins.

---

# 27. localStorage in Multiple Tabs

Pages from the same origin can access the same localStorage data.

For example:

```text
Tab 1
https://example.com

Tab 2
https://example.com
```

Both can access the same origin's localStorage.

---

# 28. The `storage` Event

The browser provides a `storage` event for changes to Web Storage.

Example:

```javascript
window.addEventListener(
    "storage",
    (event) => {
        console.log(event.key);
        console.log(event.oldValue);
        console.log(event.newValue);
    }
);
```

Important:

> A `storage` event normally fires in other same-origin documents, not in the document that made the change.

This can be useful for synchronizing state between browser tabs.

---

# 29. Storage Event Example

Suppose Tab A executes:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

Tab B can receive:

```javascript
window.addEventListener(
    "storage",
    (event) => {
        if (event.key === "theme") {
            console.log(
                "Theme changed:",
                event.newValue
            );
        }
    }
);
```

This can help another tab react to the change.

---

# 30. localStorage vs Variables

Normal variable:

```javascript
let theme = "dark";
```

The value exists only while the JavaScript context is alive.

localStorage:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

The value can remain available across page loads.

---

# 31. localStorage vs Cookies

| Feature                               | localStorage                           | Cookies                           |
| ------------------------------------- | -------------------------------------- | --------------------------------- |
| Main purpose                          | Client-side storage                    | Browser/server data               |
| Sent automatically with HTTP requests | No                                     | Yes, when applicable              |
| JavaScript access                     | Yes                                    | Depends on `HttpOnly`             |
| Typical size                          | Larger than cookies, browser-dependent | Smaller                           |
| Persistence                           | Until removed or cleared               | Depends on cookie attributes      |
| Best for                              | Preferences, UI data                   | Session-related/server-aware data |

For authentication, sensitive tokens should not be placed in localStorage simply because it is convenient. JavaScript-accessible storage can be exposed if your page suffers an XSS vulnerability. Secure, `HttpOnly` cookies are often preferred for sensitive authentication material when appropriate for the application's architecture.

---

# 32. localStorage and Security

Do **not** treat localStorage as a secure secret store.

Avoid storing sensitive information such as:

```text
Passwords
Private keys
Highly sensitive personal data
Long-lived authentication secrets
```

Why?

JavaScript running on the page can access localStorage:

```javascript
localStorage.getItem("token");
```

If an attacker executes malicious JavaScript through an XSS vulnerability, that code may be able to read stored values.

For sensitive authentication data, consider secure cookie-based designs using appropriate cookie attributes such as:

```text
HttpOnly
Secure
SameSite
```

The correct authentication architecture depends on the application and threat model.

---

# 33. localStorage and Node.js

`localStorage` is a browser Web API.

This works in a browser:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

A normal Node.js backend does not provide browser `localStorage`.

For Node.js applications, use server-side storage mechanisms such as:

```text
Database
Files
Redis
Environment variables
```

depending on the type of data.

---

# 34. Storage Size

`localStorage` has a browser-defined storage limit.

Do not design an application around an assumption that every browser provides exactly the same capacity.

It is intended for relatively small client-side data, not large databases or files.

For large browser-side datasets, consider technologies such as:

```text
IndexedDB
Cache API
```

depending on the use case.

---

# 35. localStorage Is Synchronous

Operations such as:

```javascript
localStorage.setItem(...);
localStorage.getItem(...);
```

are synchronous.

For small amounts of data this is usually fine.

However, avoid repeatedly reading or writing large amounts of data during performance-sensitive operations.

---

# 36. Handling Storage Errors

Storage operations can fail in some situations, including storage quota or browser policy restrictions.

You can handle failures:

```javascript
try {
    localStorage.setItem(
        "theme",
        "dark"
    );
} catch (error) {
    console.error(
        "Unable to save data:",
        error
    );
}
```

For example, a quota-related failure can result in a `QuotaExceededError`.

---

# 37. Creating a Storage Helper

Instead of repeatedly writing the same code:

```javascript
const storage = {
    set(key, value) {
        localStorage.setItem(
            key,
            JSON.stringify(value)
        );
    },

    get(key) {
        const value =
            localStorage.getItem(key);

        return value
            ? JSON.parse(value)
            : null;
    },

    remove(key) {
        localStorage.removeItem(key);
    },

    clear() {
        localStorage.clear();
    }
};
```

Usage:

```javascript
storage.set("user", {
    name: "Sandip",
    age: 22
});
```

Read:

```javascript
const user =
    storage.get("user");

console.log(user);
```

---

# 38. Better Storage Key Names

Use descriptive keys.

Instead of:

```javascript
localStorage.setItem(
    "data",
    "dark"
);
```

Prefer:

```javascript
localStorage.setItem(
    "app:theme",
    "dark"
);
```

For larger applications:

```text
app:theme
app:cart
app:user
app:language
app:settings
```

Clear key names reduce collisions and make debugging easier.

---

# 39. React Example

In React, you can initialize state from localStorage:

```jsx
const [theme, setTheme] = useState(() => {
    return (
        localStorage.getItem("theme")
        || "light"
    );
});
```

When the theme changes:

```jsx
useEffect(() => {
    localStorage.setItem(
        "theme",
        theme
    );
}, [theme]);
```

This allows the preference to survive page reloads.

---

# 40. Common Mistakes

### Mistake 1 — Expecting numbers to remain numbers

```javascript
localStorage.setItem("age", 22);

const age =
    localStorage.getItem("age");

console.log(typeof age);
```

Result:

```text
string
```

Convert it when necessary.

---

### Mistake 2 — Storing objects directly

Avoid:

```javascript
localStorage.setItem(
    "user",
    user
);
```

Use:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

### Mistake 3 — Parsing missing data blindly

Avoid:

```javascript
const user = JSON.parse(
    localStorage.getItem("user")
);
```

Use:

```javascript
const storedUser =
    localStorage.getItem("user");

const user = storedUser
    ? JSON.parse(storedUser)
    : null;
```

---

### Mistake 4 — Using `clear()` unnecessarily

Avoid:

```javascript
localStorage.clear();
```

when you only need to remove one item.

Prefer:

```javascript
localStorage.removeItem("cart");
```

---

### Mistake 5 — Storing secrets

Do not assume localStorage is protected from JavaScript running in the page.

Sensitive authentication material requires a security-aware storage strategy.

---

# 41. Quick Cheat Sheet

```javascript
// Store
localStorage.setItem(
    "username",
    "Sandip"
);

// Read
localStorage.getItem(
    "username"
);

// Update
localStorage.setItem(
    "username",
    "Ram"
);

// Remove one
localStorage.removeItem(
    "username"
);

// Remove everything for this origin
localStorage.clear();

// Number of entries
localStorage.length;

// Get key by index
localStorage.key(0);
```

---

## Objects and Arrays

```javascript
// Store object
localStorage.setItem(
    "user",
    JSON.stringify(user)
);

// Read object
const user = JSON.parse(
    localStorage.getItem("user")
);

// Store array
localStorage.setItem(
    "cart",
    JSON.stringify(cart)
);

// Read array
const cart = JSON.parse(
    localStorage.getItem("cart")
);
```

---

# 42. localStorage Summary

```text
localStorage
│
├── setItem()
│   └── Store / update data
│
├── getItem()
│   └── Read data
│
├── removeItem()
│   └── Remove one item
│
├── clear()
│   └── Remove all items for the origin
│
├── key()
│   └── Get a key by index
│
└── length
    └── Number of stored entries
```

### Remember

```text
localStorage
    ↓
Browser storage
    ↓
Persistent across page loads
    ↓
String values
    ↓
JSON.stringify()
    ↓
Objects / Arrays
    ↓
JSON.parse()
    ↓
Do not store secrets
```

---

# Key Takeaways

* `localStorage` stores small amounts of client-side data.
* Data normally survives page refreshes and browser restarts.
* Values are stored as strings.
* Use `setItem()` to store or update data.
* Use `getItem()` to read data.
* Use `removeItem()` to remove one entry.
* Use `clear()` to remove all entries for the current origin.
* Use `JSON.stringify()` for objects and arrays.
* Use `JSON.parse()` when reading stored JSON.
* Storage is separated by origin.
* Same-origin tabs can access the same storage.
* The `storage` event can notify other same-origin documents about changes.
* `localStorage` is synchronous.
* Storage capacity is browser-dependent and limited.
* Do not use localStorage as a secure secret store.
* For sensitive authentication data, secure `HttpOnly` cookie designs may be more appropriate.
* `localStorage` is a browser API and is not normally available in Node.js.
