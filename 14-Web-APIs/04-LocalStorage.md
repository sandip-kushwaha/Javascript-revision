# JavaScript LocalStorage

**Local Storage** is a browser Web Storage API that allows a website to store data as key-value pairs in the user's browser.

Data stored in `localStorage` normally remains available even after:

* Refreshing the page
* Closing the browser
* Restarting the computer

It is commonly used for small pieces of client-side data such as:

* Theme preference
* Language preference
* UI settings
* Non-sensitive application state
* Recently selected options

---

# 1. What Is LocalStorage?

Local Storage provides:

```javascript
localStorage
```

Basic structure:

```text
key → value
```

Example:

```javascript
localStorage.setItem("theme", "dark");
```

Here:

```text
key   → theme
value → dark
```

---

# 2. Basic Methods

The most important methods are:

```javascript
localStorage.setItem();
localStorage.getItem();
localStorage.removeItem();
localStorage.clear();
```

There is also:

```javascript
localStorage.key();
```

---

# 3. `setItem()`

Use `setItem()` to store data.

```javascript
localStorage.setItem("name", "Sandip");
```

The browser stores:

```text
name → Sandip
```

---

# 4. `getItem()`

Use `getItem()` to retrieve data.

```javascript
const name = localStorage.getItem("name");

console.log(name);
```

Output:

```text
Sandip
```

---

# 5. `removeItem()`

Remove one item:

```javascript
localStorage.removeItem("name");
```

After this:

```javascript
localStorage.getItem("name");
```

returns:

```text
null
```

---

# 6. `clear()`

Remove all local storage data for the current origin:

```javascript
localStorage.clear();
```

Be careful with this method because it removes all localStorage entries belonging to that origin, not just one application key.

---

# 7. `key()`

`key()` returns the key at a particular numeric index.

```javascript
const key = localStorage.key(0);

console.log(key);
```

The order should not be relied upon for application logic.

---

# 8. LocalStorage Stores Strings

This is very important.

Even if you store a number:

```javascript
localStorage.setItem("age", 22);
```

retrieving it gives a string:

```javascript
const age = localStorage.getItem("age");

console.log(typeof age);
```

Output:

```text
string
```

The value is:

```text
"22"
```

---

# 9. Converting Stored Numbers

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

# 10. Storing Boolean Values

If you do:

```javascript
localStorage.setItem("isLoggedIn", true);
```

the stored value becomes:

```text
"true"
```

Therefore this is dangerous:

```javascript
Boolean(
    localStorage.getItem("isLoggedIn")
);
```

Because:

```javascript
Boolean("false");
```

is:

```text
true
```

Instead, compare or parse the stored representation appropriately.

Example:

```javascript
const isLoggedIn =
    localStorage.getItem("isLoggedIn") === "true";
```

---

# 11. Storing Objects

LocalStorage cannot directly store a JavaScript object as an object.

This:

```javascript
const user = {
    name: "Sandip",
    role: "developer"
};

localStorage.setItem("user", user);
```

does not store the object structure correctly.

You should convert it to JSON:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

# 12. Reading Objects

Retrieve the stored string:

```javascript
const storedUser =
    localStorage.getItem("user");
```

Convert it back:

```javascript
const user = JSON.parse(storedUser);

console.log(user.name);
```

---

# 13. Complete Object Example

```javascript
const user = {
    id: 101,
    name: "Sandip",
    role: "developer"
};

localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

Read it:

```javascript
const storedUser =
    localStorage.getItem("user");

if (storedUser) {
    const user = JSON.parse(storedUser);

    console.log(user.name);
}
```

---

# 14. Storing Arrays

Arrays also need JSON conversion.

```javascript
const skills = [
    "JavaScript",
    "React",
    "Node.js"
];

localStorage.setItem(
    "skills",
    JSON.stringify(skills)
);
```

Read:

```javascript
const skills = JSON.parse(
    localStorage.getItem("skills")
);

console.log(skills);
```

---

# 15. Safely Reading JSON

`JSON.parse()` can throw an error if the stored value is invalid.

A safer helper:

```javascript
function getJSON(key) {
    const value = localStorage.getItem(key);

    if (value === null) {
        return null;
    }

    try {
        return JSON.parse(value);
    } catch {
        return null;
    }
}
```

Usage:

```javascript
const user = getJSON("user");

console.log(user);
```

---

# 16. Default Values

You can provide a fallback when an item does not exist.

```javascript
const theme =
    localStorage.getItem("theme") ?? "light";

console.log(theme);
```

If `"theme"` does not exist:

```text
light
```

is used.

---

# 17. Theme Example

Store theme:

```javascript
function setTheme(theme) {
    localStorage.setItem("theme", theme);
}
```

Read theme:

```javascript
const theme =
    localStorage.getItem("theme") ?? "light";
```

Apply it:

```javascript
document.documentElement.dataset.theme =
    theme;
```

---

# 18. Dark Mode Example

```javascript
const savedTheme =
    localStorage.getItem("theme");

if (savedTheme === "dark") {
    document.body.classList.add("dark");
}
```

When the user changes the theme:

```javascript
function toggleTheme() {
    const isDark =
        document.body.classList.toggle("dark");

    localStorage.setItem(
        "theme",
        isDark ? "dark" : "light"
    );
}
```

This allows the preference to survive page reloads.

---

# 19. Saving User Preferences

Example:

```javascript
const settings = {
    theme: "dark",
    language: "en",
    sidebar: true
};

localStorage.setItem(
    "settings",
    JSON.stringify(settings)
);
```

Read:

```javascript
const settings = JSON.parse(
    localStorage.getItem("settings")
);
```

---

# 20. Updating Stored Objects

Suppose:

```javascript
const user = {
    name: "Sandip",
    role: "developer"
};
```

Store it:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

To update it:

```javascript
const storedUser =
    localStorage.getItem("user");

const user = storedUser
    ? JSON.parse(storedUser)
    : {};

user.role = "full-stack developer";

localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

The complete object is stored again.

---

# 21. LocalStorage Helper Functions

You can create reusable helpers.

```javascript
function setItem(key, value) {
    localStorage.setItem(
        key,
        JSON.stringify(value)
    );
}

function getItem(key) {
    const value = localStorage.getItem(key);

    return value
        ? JSON.parse(value)
        : null;
}

function removeItem(key) {
    localStorage.removeItem(key);
}
```

Usage:

```javascript
setItem("user", {
    name: "Sandip",
    role: "developer"
});
```

Read:

```javascript
const user = getItem("user");

console.log(user);
```

Remove:

```javascript
removeItem("user");
```

---

# 22. A Safer JSON Helper

For application code, parsing should be protected from malformed stored data.

```javascript
function setJSON(key, value) {
    localStorage.setItem(
        key,
        JSON.stringify(value)
    );
}

function getJSON(key) {
    const value = localStorage.getItem(key);

    if (value === null) {
        return null;
    }

    try {
        return JSON.parse(value);
    } catch (error) {
        console.error(
            `Invalid stored JSON for "${key}"`,
            error
        );

        return null;
    }
}

function removeJSON(key) {
    localStorage.removeItem(key);
}
```

---

# 23. Checking Whether a Key Exists

You can use:

```javascript
const value =
    localStorage.getItem("theme");

if (value !== null) {
    console.log("Theme exists");
}
```

Remember:

```javascript
localStorage.getItem("missing");
```

returns:

```text
null
```

---

# 24. LocalStorage Length

Use:

```javascript
localStorage.length;
```

Example:

```javascript
console.log(localStorage.length);
```

It returns the number of stored keys for the current origin.

---

# 25. Iterating Through LocalStorage

Example:

```javascript
for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i);

    const value =
        localStorage.getItem(key);

    console.log(key, value);
}
```

The ordering of keys should not be treated as meaningful.

---

# 26. LocalStorage and Browser Origin

LocalStorage is associated with a browser **origin**.

An origin is:

```text
scheme + host + port
```

For example:

```text
http://localhost:5173
```

and:

```text
http://localhost:8000
```

are different origins.

Their localStorage data is separate.

---

# 27. LocalStorage and Different Domains

For example:

```text
https://example.com
```

and:

```text
https://another.com
```

do not normally share localStorage.

Each origin has its own storage area.

---

# 28. LocalStorage Persists Across Reloads

Suppose:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

Refresh the page:

```javascript
localStorage.getItem("theme");
```

Result:

```text
dark
```

The data normally remains.

---

# 29. LocalStorage Persists After Browser Restart

Unlike normal JavaScript variables:

```javascript
let theme = "dark";
```

the variable disappears when the page is unloaded.

LocalStorage:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

normally remains available after closing and reopening the browser.

---

# 30. LocalStorage vs JavaScript Variables

### JavaScript variable

```javascript
let name = "Sandip";
```

Data exists only while the relevant JavaScript context exists.

### LocalStorage

```javascript
localStorage.setItem(
    "name",
    "Sandip"
);
```

Data persists in browser storage.

---

# 31. LocalStorage vs SessionStorage

| Feature                  | LocalStorage   | SessionStorage                |
| ------------------------ | -------------- | ----------------------------- |
| API                      | `localStorage` | `sessionStorage`              |
| Stores strings           | Yes            | Yes                           |
| Survives page reload     | Yes            | Yes                           |
| Survives browser session | Normally yes   | Normally no                   |
| Scope                    | Origin         | Origin + browser tab/session  |
| Automatic expiration     | No             | Usually when tab/session ends |

Both are part of the Web Storage API.

---

# 32. LocalStorage vs Cookies

| Feature                               | LocalStorage                       | Cookies                                 |
| ------------------------------------- | ---------------------------------- | --------------------------------------- |
| JavaScript access                     | Yes                                | Depends on `HttpOnly`                   |
| Automatically sent with HTTP requests | No                                 | Yes, when applicable                    |
| Storage size                          | Larger than typical cookie storage | Smaller                                 |
| Main purpose                          | Client-side storage                | Cookies, sessions, server communication |
| `HttpOnly` support                    | No                                 | Yes                                     |
| `Secure` attribute                    | No                                 | Yes                                     |

LocalStorage is therefore not a direct replacement for secure authentication cookies.

---

# 33. LocalStorage and Authentication

Avoid storing highly sensitive authentication information in localStorage unless you fully understand the security trade-offs.

For example:

```javascript
localStorage.setItem(
    "accessToken",
    token
);
```

This token is accessible to JavaScript running on the page.

If an attacker successfully executes malicious JavaScript through an XSS vulnerability, browser-accessible storage can potentially be exposed.

For authentication systems, `HttpOnly` cookies can provide protections that JavaScript-accessible storage cannot.

---

# 34. LocalStorage Is Not a Database

LocalStorage is designed for relatively small client-side storage.

It is not a replacement for:

* MongoDB
* PostgreSQL
* MySQL
* Redis
* IndexedDB for larger structured browser storage

Do not store your application's entire database in localStorage.

---

# 35. Storage Limits

Browsers impose storage limits.

The exact limit depends on:

* Browser
* Storage type
* Available device storage
* Browser policies

Do not assume an unlimited amount of storage is available.

For large browser-side datasets, consider alternatives such as IndexedDB.

---

# 36. Handling Storage Errors

Storage operations can fail in some environments.

For example:

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

Possible causes include:

* Storage restrictions
* Browser privacy settings
* Storage quota limitations
* Security policies

---

# 37. LocalStorage and React

A common React pattern is reading an initial preference:

```javascript
const [theme, setTheme] = useState(() => {
    return (
        localStorage.getItem("theme") ??
        "light"
    );
});
```

When the theme changes:

```javascript
useEffect(() => {
    localStorage.setItem("theme", theme);
}, [theme]);
```

This keeps the React state and localStorage synchronized.

---

# 38. React Example

```jsx
import { useEffect, useState } from "react";

function Theme() {
    const [theme, setTheme] = useState(() => {
        return (
            localStorage.getItem("theme") ??
            "light"
        );
    });

    useEffect(() => {
        localStorage.setItem("theme", theme);
    }, [theme]);

    return (
        <button
            onClick={() => {
                setTheme(
                    theme === "light"
                        ? "dark"
                        : "light"
                );
            }}
        >
            {theme}
        </button>
    );
}
```

---

# 39. LocalStorage and API Data

You can temporarily cache some API data:

```javascript
async function getProducts() {
    const cached =
        localStorage.getItem("products");

    if (cached) {
        return JSON.parse(cached);
    }

    const response =
        await fetch("/api/products");

    if (!response.ok) {
        throw new Error("Failed to load products");
    }

    const products =
        await response.json();

    localStorage.setItem(
        "products",
        JSON.stringify(products)
    );

    return products;
}
```

However, this simple cache can become stale.

For more advanced caching, dedicated caching strategies or libraries may be more appropriate.

---

# 40. Cache Expiration

LocalStorage does not automatically expire an item.

You can store an expiration timestamp yourself.

```javascript
const data = {
    value: {
        theme: "dark"
    },
    expiresAt:
        Date.now() + 60 * 60 * 1000
};

localStorage.setItem(
    "settings",
    JSON.stringify(data)
);
```

Read:

```javascript
const stored =
    localStorage.getItem("settings");

if (stored) {
    const data = JSON.parse(stored);

    if (Date.now() < data.expiresAt) {
        console.log(data.value);
    } else {
        localStorage.removeItem("settings");
    }
}
```

---

# 41. LocalStorage Event

The `storage` event can notify another document when storage changes.

Example:

```javascript
window.addEventListener(
    "storage",
    (event) => {
        console.log("Key:", event.key);
        console.log("Old:", event.oldValue);
        console.log("New:", event.newValue);
    }
);
```

Important:

The `storage` event is generally fired in **other same-origin documents**, such as another tab, not in the same document that made the change.

---

# 42. Storage Event Example

Suppose two tabs are open:

```text
Tab A
Tab B
```

Tab A:

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
            console.log(event.newValue);
        }
    }
);
```

This can be useful for synchronizing simple UI preferences between tabs.

---

# 43. LocalStorage and Security

Do not store secrets casually.

Avoid storing:

```text
Passwords
Private encryption keys
Highly sensitive personal data
Long-lived authentication secrets
```

Remember:

```text
localStorage
    ↓
Accessible through JavaScript
```

Therefore, protecting the application against XSS is important.

---

# 44. LocalStorage and XSS

Suppose an application contains:

```javascript
localStorage.setItem(
    "token",
    token
);
```

If malicious JavaScript executes in the same origin, it may be able to read:

```javascript
localStorage.getItem("token");
```

This is one reason sensitive authentication data is often handled using appropriately configured cookies instead.

---

# 45. LocalStorage Naming

Use descriptive keys.

Instead of:

```javascript
localStorage.setItem(
    "x",
    "dark"
);
```

prefer:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

For larger applications, namespacing can help:

```javascript
localStorage.setItem(
    "myapp:theme",
    "dark"
);
```

---

# 46. Removing Application Data

Remove one key:

```javascript
localStorage.removeItem(
    "myapp:theme"
);
```

Remove application keys individually when possible.

Avoid blindly using:

```javascript
localStorage.clear();
```

because it removes all localStorage entries for the current origin, including entries your application may not own.

---

# 47. Practical Settings Example

```javascript
const settings = {
    theme: "dark",
    language: "en",
    notifications: true
};

try {
    localStorage.setItem(
        "myapp:settings",
        JSON.stringify(settings)
    );
} catch (error) {
    console.error("Could not save settings:", error);
}
```

Read:

```javascript
const stored =
    localStorage.getItem("myapp:settings");

if (stored) {
    try {
        const settings = JSON.parse(stored);

        console.log(settings.theme);
        console.log(settings.language);
    } catch (error) {
        console.error("Invalid settings:", error);
    }
}
```

---

# 48. Common Mistakes

## Mistake 1: Expecting objects to remain objects

Wrong:

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

## Mistake 2: Forgetting JSON.parse()

Wrong:

```javascript
const user =
    localStorage.getItem("user");

console.log(user.name);
```

Correct:

```javascript
const user = JSON.parse(
    localStorage.getItem("user")
);

console.log(user.name);
```

For production code, also handle the possibility that the key is missing or the stored JSON is invalid.

---

## Mistake 3: Treating `"false"` as false

This:

```javascript
Boolean("false");
```

returns:

```text
true
```

Use:

```javascript
const value =
    localStorage.getItem("isActive");

const isActive = value === "true";
```

---

## Mistake 4: Storing passwords

Do not use localStorage as a password store.

---

## Mistake 5: Using `clear()` carelessly

```javascript
localStorage.clear();
```

removes every localStorage entry for the current origin.

---

# 49. Useful LocalStorage Helper

A practical helper:

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

        if (value === null) {
            return null;
        }

        try {
            return JSON.parse(value);
        } catch {
            return null;
        }
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
    role: "developer"
});
```

Read:

```javascript
const user = storage.get("user");

console.log(user);
```

Remove:

```javascript
storage.remove("user");
```

---

# 50. Key Takeaways

* `localStorage` is a browser Web Storage API.
* It stores data as key-value pairs.
* Values are stored as strings.
* Use `JSON.stringify()` for objects and arrays.
* Use `JSON.parse()` when reading stored JSON.
* `getItem()` returns `null` when the key does not exist.
* `setItem()` stores a value.
* `removeItem()` removes one key.
* `clear()` removes all localStorage entries for the current origin.
* LocalStorage normally survives page reloads and browser restarts.
* LocalStorage is scoped by origin.
* LocalStorage is not a database.
* Storage limits exist.
* LocalStorage is accessible to JavaScript.
* Do not store passwords or other highly sensitive secrets in localStorage.
* `storage` events can help synchronize storage changes across documents.
* Use `AbortController`, Fetch, or other APIs separately for network operations; localStorage itself is only client-side storage.
* For large structured browser-side data, consider IndexedDB.

---

## Quick Cheat Sheet

```javascript
// Store
localStorage.setItem("theme", "dark");

// Read
const theme =
    localStorage.getItem("theme");

// Remove one
localStorage.removeItem("theme");

// Remove all
localStorage.clear();

// Store object
localStorage.setItem(
    "user",
    JSON.stringify(user)
);

// Read object
const user = JSON.parse(
    localStorage.getItem("user")
);

// Number
const age = Number(
    localStorage.getItem("age")
);

// Boolean
const active =
    localStorage.getItem("active") === "true";

// Number of keys
localStorage.length;

// Get key by index
localStorage.key(0);
```

---
