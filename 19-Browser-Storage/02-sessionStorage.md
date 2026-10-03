# JavaScript sessionStorage

`sessionStorage` is a browser storage API used to store data for the current browser tab or window.

It is useful when data should remain available during a page session but should normally disappear when that tab or window is closed.

Common uses:

* Temporary form data
* Multi-step forms
* Temporary UI state
* Current-page settings
* Temporary checkout information
* Short-lived browser data

---

# 1. What is sessionStorage?

`sessionStorage` provides key-value storage in the browser.

Example:

```javascript
sessionStorage.setItem(
    "username",
    "Sandip"
);
```

Read the value:

```javascript
const username =
    sessionStorage.getItem("username");

console.log(username);
```

Output:

```text
Sandip
```

---

# 2. sessionStorage vs localStorage

The main difference is how long the data is intended to live.

| Feature            | sessionStorage       | localStorage    |
| ------------------ | -------------------- | --------------- |
| Storage type       | Browser storage      | Browser storage |
| Persistence        | Current page session | Persistent      |
| Survives refresh   | Yes                  | Yes             |
| Survives tab close | Normally no          | Yes             |
| Stores strings     | Yes                  | Yes             |
| `setItem()`        | Yes                  | Yes             |
| `getItem()`        | Yes                  | Yes             |
| `removeItem()`     | Yes                  | Yes             |
| `clear()`          | Yes                  | Yes             |

Simple rule:

```text
localStorage
    → keep data longer

sessionStorage
    → keep data for the current tab/session
```

---

# 3. Basic Syntax

The API is similar to `localStorage`.

```javascript
sessionStorage.setItem(key, value);

sessionStorage.getItem(key);

sessionStorage.removeItem(key);

sessionStorage.clear();
```

---

# 4. Store Data

Use:

```javascript
sessionStorage.setItem(
    "theme",
    "dark"
);
```

Another example:

```javascript
sessionStorage.setItem(
    "step",
    "2"
);
```

---

# 5. Read Data

Use:

```javascript
const theme =
    sessionStorage.getItem("theme");

console.log(theme);
```

Output:

```text
dark
```

If the key does not exist:

```javascript
const value =
    sessionStorage.getItem("unknown");

console.log(value);
```

Output:

```text
null
```

---

# 6. Update Data

Calling `setItem()` with the same key updates its value.

```javascript
sessionStorage.setItem(
    "step",
    "1"
);

sessionStorage.setItem(
    "step",
    "2"
);
```

Read:

```javascript
console.log(
    sessionStorage.getItem("step")
);
```

Output:

```text
2
```

---

# 7. Remove One Item

Use:

```javascript
sessionStorage.removeItem("step");
```

After removal:

```javascript
console.log(
    sessionStorage.getItem("step")
);
```

Output:

```text
null
```

---

# 8. Clear All sessionStorage

Use:

```javascript
sessionStorage.clear();
```

This removes all sessionStorage entries for the current storage area.

Use it carefully.

If you only want to remove one value:

```javascript
sessionStorage.removeItem("step");
```

is more precise.

---

# 9. Check Number of Items

Use:

```javascript
console.log(
    sessionStorage.length
);
```

Example:

```javascript
sessionStorage.setItem(
    "name",
    "Sandip"
);

sessionStorage.setItem(
    "role",
    "student"
);

console.log(
    sessionStorage.length
);
```

Output:

```text
2
```

---

# 10. Get a Key by Index

Use:

```javascript
const key =
    sessionStorage.key(0);

console.log(key);
```

The order of keys should not be relied upon for application logic.

---

# 11. sessionStorage Stores Strings

Like `localStorage`, `sessionStorage` stores values as strings.

Example:

```javascript
sessionStorage.setItem(
    "age",
    22
);
```

Read:

```javascript
const age =
    sessionStorage.getItem("age");

console.log(age);
console.log(typeof age);
```

Output:

```text
22
string
```

If you need a number:

```javascript
const age = Number(
    sessionStorage.getItem("age")
);
```

---

# 12. Storing Boolean Values

```javascript
sessionStorage.setItem(
    "isAdmin",
    true
);
```

The stored value becomes:

```text
"true"
```

Read it:

```javascript
const isAdmin =
    sessionStorage.getItem("isAdmin")
    === "true";

console.log(isAdmin);
```

Output:

```text
true
```

---

# 13. Storing Objects

Objects should be converted to JSON.

```javascript
const user = {
    name: "Sandip",
    role: "student"
};

sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

# 14. Reading Objects

```javascript
const storedUser =
    sessionStorage.getItem("user");

const user = storedUser
    ? JSON.parse(storedUser)
    : null;

console.log(user);
```

Result:

```javascript
{
    name: "Sandip",
    role: "student"
}
```

---

# 15. Storing Arrays

```javascript
const steps = [
    "personal-info",
    "address",
    "payment"
];

sessionStorage.setItem(
    "steps",
    JSON.stringify(steps)
);
```

Read:

```javascript
const storedSteps =
    sessionStorage.getItem("steps");

const stepsData = storedSteps
    ? JSON.parse(storedSteps)
    : [];

console.log(stepsData);
```

---

# 16. Practical Example — Multi-Step Form

Suppose a registration form has multiple steps:

```text
Step 1 → Personal Information
Step 2 → Address
Step 3 → Confirmation
```

Store the current step:

```javascript
sessionStorage.setItem(
    "registrationStep",
    "2"
);
```

When the page loads:

```javascript
const step =
    sessionStorage.getItem(
        "registrationStep"
    );

console.log(step);
```

The application can restore the current step during the same session.

---

# 17. Practical Example — Temporary Form Data

Suppose:

```javascript
const formData = {
    firstName: "Sandip",
    lastName: "Kushwaha",
    city: "Birgunj"
};
```

Store it:

```javascript
sessionStorage.setItem(
    "formData",
    JSON.stringify(formData)
);
```

Read it later:

```javascript
const storedData =
    sessionStorage.getItem("formData");

const data = storedData
    ? JSON.parse(storedData)
    : null;
```

This can help preserve temporary form information during navigation or refreshes.

---

# 18. Practical Example — Checkout Step

```javascript
function saveCheckoutStep(step) {
    sessionStorage.setItem(
        "checkoutStep",
        String(step)
    );
}
```

Use:

```javascript
saveCheckoutStep(2);
```

Read:

```javascript
const step = Number(
    sessionStorage.getItem(
        "checkoutStep"
    )
);

console.log(step);
```

Output:

```text
2
```

---

# 19. Tab-Specific Storage

One important difference from `localStorage` is that `sessionStorage` is associated with a particular top-level browsing context, such as a browser tab.

For example:

```text
Tab A
example.com
    ↓
sessionStorage

Tab B
example.com
    ↓
different sessionStorage
```

So two tabs of the same website generally do not use the same sessionStorage area.

This makes sessionStorage useful for temporary state that should remain isolated between tabs.

---

# 20. Page Refresh

Refreshing the page normally does **not** remove sessionStorage.

Example:

```javascript
sessionStorage.setItem(
    "page",
    "dashboard"
);
```

After refreshing:

```javascript
console.log(
    sessionStorage.getItem("page")
);
```

The value can still be available.

---

# 21. Closing the Tab

When the browsing session associated with a tab/window ends, its sessionStorage is normally cleared.

Therefore:

```text
Open tab
   ↓
sessionStorage available
   ↓
Refresh
   ↓
sessionStorage remains
   ↓
Close tab
   ↓
sessionStorage normally ends
```

Browser behavior around restoring closed/crashed sessions can have implementation-specific details, so do not use sessionStorage as a security boundary.

---

# 22. sessionStorage and Cookies

| Feature                               | sessionStorage                         | Cookies                          |
| ------------------------------------- | -------------------------------------- | -------------------------------- |
| Browser storage                       | Yes                                    | Yes                              |
| Sent automatically with HTTP requests | No                                     | Yes, when applicable             |
| JavaScript access                     | Yes                                    | Depends on `HttpOnly`            |
| Typical purpose                       | Temporary client-side state            | Client/server state              |
| Size                                  | Larger than cookies, browser-dependent | Smaller                          |
| Current-tab use case                  | Strong                                 | Not specifically designed for it |

---

# 23. sessionStorage and Security

`sessionStorage` should not be treated as a secure storage mechanism.

JavaScript running on the page can read it:

```javascript
sessionStorage.getItem("data");
```

Therefore, do not store highly sensitive secrets simply because the storage disappears when the tab closes.

For sensitive authentication data, use an authentication architecture designed around appropriate security controls, such as secure cookies where suitable.

---

# 24. sessionStorage and Node.js

`sessionStorage` is a browser Web API.

This works in browser JavaScript:

```javascript
sessionStorage.setItem(
    "step",
    "2"
);
```

A normal Node.js server does not provide the browser's sessionStorage API.

For server-side session management, applications commonly use:

```text
Cookies
Databases
Redis
Server-side session stores
```

depending on the architecture.

---

# 25. Storage Events

Web Storage changes can trigger the `storage` event in other relevant documents.

Example:

```javascript
window.addEventListener(
    "storage",
    (event) => {
        console.log(event.key);
        console.log(event.newValue);
    }
);
```

However, `sessionStorage` has different lifetime and browsing-context behavior from `localStorage`, so it should not be treated as a general cross-tab synchronization mechanism.

---

# 26. Handling Storage Errors

Storage operations can fail because of browser restrictions, quota conditions, or other environment-specific policies.

Use:

```javascript
try {
    sessionStorage.setItem(
        "step",
        "2"
    );
} catch (error) {
    console.error(
        "Unable to save session data:",
        error
    );
}
```

This prevents a storage failure from unexpectedly breaking application logic.

---

# 27. Creating a Storage Helper

You can create a small helper for JSON data:

```javascript
const sessionStore = {
    set(key, value) {
        sessionStorage.setItem(
            key,
            JSON.stringify(value)
        );
    },

    get(key) {
        const value =
            sessionStorage.getItem(key);

        return value
            ? JSON.parse(value)
            : null;
    },

    remove(key) {
        sessionStorage.removeItem(key);
    },

    clear() {
        sessionStorage.clear();
    }
};
```

Usage:

```javascript
sessionStore.set(
    "user",
    {
        name: "Sandip",
        role: "student"
    }
);
```

Read:

```javascript
const user =
    sessionStore.get("user");

console.log(user);
```

---

# 28. React Example

`sessionStorage` can be used for temporary React state.

Example:

```jsx
const [step, setStep] = useState(() => {
    const storedStep =
        sessionStorage.getItem(
            "checkoutStep"
        );

    return storedStep
        ? Number(storedStep)
        : 1;
});
```

Save changes:

```jsx
useEffect(() => {
    sessionStorage.setItem(
        "checkoutStep",
        String(step)
    );
}, [step]);
```

Now the current step can survive a refresh during the session.

---

# 29. localStorage vs sessionStorage Example

### Persistent theme

Use `localStorage`:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

A user may want the theme to remain after reopening the browser.

### Temporary checkout step

Use `sessionStorage`:

```javascript
sessionStorage.setItem(
    "checkoutStep",
    "2"
);
```

The application may only need this information during the current tab session.

---

# 30. Choosing the Right Storage

Use `localStorage` when:

```text
Data should persist longer
        ↓
User preferences
Theme
Language
Non-sensitive settings
```

Use `sessionStorage` when:

```text
Data is temporary
        ↓
Current tab/session
Multi-step form
Temporary UI state
Checkout progress
```

Use cookies when:

```text
Browser ↔ Server communication
        ↓
Session identifiers
Authentication architecture
Server-related state
```

Use IndexedDB when:

```text
More structured/larger client-side data
        ↓
Offline applications
Large browser datasets
Complex client-side storage
```

---

# 31. Common Mistakes

## Mistake 1 — Expecting numbers to remain numbers

```javascript
sessionStorage.setItem(
    "age",
    22
);

const age =
    sessionStorage.getItem("age");

console.log(typeof age);
```

Result:

```text
string
```

Convert it when necessary:

```javascript
const age = Number(
    sessionStorage.getItem("age")
);
```

---

## Mistake 2 — Storing objects directly

Avoid:

```javascript
sessionStorage.setItem(
    "user",
    user
);
```

Use:

```javascript
sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

## Mistake 3 — Parsing missing values blindly

Avoid:

```javascript
const user = JSON.parse(
    sessionStorage.getItem("user")
);
```

Prefer:

```javascript
const storedUser =
    sessionStorage.getItem("user");

const user = storedUser
    ? JSON.parse(storedUser)
    : null;
```

---

## Mistake 4 — Using sessionStorage as a security boundary

Do not assume that closing a tab makes sensitive data safe.

JavaScript running in the page can access:

```javascript
sessionStorage
```

Use appropriate security controls for sensitive information.

---

# 32. Quick Cheat Sheet

```javascript
// Store
sessionStorage.setItem(
    "username",
    "Sandip"
);

// Read
sessionStorage.getItem(
    "username"
);

// Update
sessionStorage.setItem(
    "username",
    "Ram"
);

// Remove one
sessionStorage.removeItem(
    "username"
);

// Remove all
sessionStorage.clear();

// Number of entries
sessionStorage.length;

// Get key by index
sessionStorage.key(0);
```

---

## Objects and Arrays

```javascript
// Store object
sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);

// Read object
const user = JSON.parse(
    sessionStorage.getItem("user")
);

// Store array
sessionStorage.setItem(
    "items",
    JSON.stringify(items)
);

// Read array
const items = JSON.parse(
    sessionStorage.getItem("items")
);
```

---

# 33. Storage Comparison

```text
Browser Storage
│
├── localStorage
│   ├── Persistent
│   ├── String values
│   └── Same-origin storage
│
├── sessionStorage
│   ├── Temporary
│   ├── String values
│   └── Associated with a browsing session/tab
│
└── Cookies
    ├── Small data
    ├── Can be sent with HTTP requests
    └── Can use security attributes
```

---

# Key Takeaways

* `sessionStorage` stores temporary browser-side data.
* It uses the same basic API as `localStorage`.
* Use `setItem()` to store or update data.
* Use `getItem()` to read data.
* Use `removeItem()` to remove one item.
* Use `clear()` to remove all entries in the storage area.
* `sessionStorage` stores values as strings.
* Use `JSON.stringify()` for objects and arrays.
* Use `JSON.parse()` when reading stored JSON.
* Refreshing a page normally does not remove sessionStorage.
* Closing the associated tab/window normally ends the sessionStorage lifetime.
* Same-origin tabs should not be treated as sharing one common sessionStorage area.
* `sessionStorage` is not a secure secret store.
* It is useful for temporary forms, checkout steps, and tab-specific UI state.
* Use `localStorage` when data should persist longer.
* Use cookies or another appropriate architecture for server-side sessions and sensitive authentication data.
