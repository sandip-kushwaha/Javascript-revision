# JavaScript SessionStorage

`sessionStorage` is a browser Web Storage API used to store key-value data for the current browser tab or session.

It is similar to `localStorage`, but the main difference is **how long the data normally remains available**.

```text
localStorage
    → normally persists after closing the browser

sessionStorage
    → normally lasts for the current page session
```

Common uses:

* Temporary form data
* Multi-step form state
* Temporary filters
* Temporary UI settings
* Data that should not normally survive closing a tab

---

# 1. What Is SessionStorage?

Access it using:

```javascript
sessionStorage
```

Basic structure:

```text
key → value
```

Example:

```javascript
sessionStorage.setItem(
    "username",
    "Sandip"
);
```

---

# 2. Basic Methods

The main methods are:

```javascript
sessionStorage.setItem();
sessionStorage.getItem();
sessionStorage.removeItem();
sessionStorage.clear();
sessionStorage.key();
```

The API is very similar to `localStorage`.

---

# 3. `setItem()`

Store a value:

```javascript
sessionStorage.setItem(
    "name",
    "Sandip"
);
```

---

# 4. `getItem()`

Retrieve a value:

```javascript
const name =
    sessionStorage.getItem("name");

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
sessionStorage.removeItem("name");
```

After removal:

```javascript
sessionStorage.getItem("name");
```

returns:

```text
null
```

---

# 6. `clear()`

Remove all sessionStorage entries for the current page session:

```javascript
sessionStorage.clear();
```

Use this carefully because it removes every sessionStorage entry for the current origin in that session context.

---

# 7. `key()`

Get a key by numeric index:

```javascript
const key =
    sessionStorage.key(0);

console.log(key);
```

Do not depend on the returned key order for application logic.

---

# 8. `length`

Get the number of stored keys:

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
    "developer"
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

# 9. SessionStorage Stores Strings

Like `localStorage`, `sessionStorage` stores values as strings.

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

console.log(typeof age);
```

Output:

```text
string
```

The stored value is:

```text
"22"
```

---

# 10. Storing Numbers

Convert the stored string back to a number:

```javascript
const age = Number(
    sessionStorage.getItem("age")
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

# 11. Storing Boolean Values

This:

```javascript
sessionStorage.setItem(
    "isActive",
    true
);
```

stores:

```text
"true"
```

Read it:

```javascript
const isActive =
    sessionStorage.getItem("isActive") === "true";
```

---

# 12. Storing Objects

Objects should be converted to JSON.

```javascript
const user = {
    name: "Sandip",
    role: "developer"
};

sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

# 13. Reading Objects

```javascript
const storedUser =
    sessionStorage.getItem("user");

if (storedUser) {
    const user =
        JSON.parse(storedUser);

    console.log(user.name);
}
```

---

# 14. Storing Arrays

```javascript
const steps = [
    "personal",
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
const steps = JSON.parse(
    sessionStorage.getItem("steps")
);
```

---

# 15. SessionStorage and Page Reload

A normal page reload does not usually remove sessionStorage.

For example:

```javascript
sessionStorage.setItem(
    "step",
    "2"
);
```

After refreshing the page:

```javascript
console.log(
    sessionStorage.getItem("step")
);
```

normally still gives:

```text
2
```

This makes it useful for temporary state that should survive reloads.

---

# 16. SessionStorage and Closing the Tab

A page session normally ends when the tab or window is closed.

Therefore:

```javascript
sessionStorage.setItem(
    "temporaryData",
    "hello"
);
```

normally does not remain available after the browser page session ends.

However, browser behavior can vary in some session restoration scenarios.

---

# 17. SessionStorage and Browser Tabs

SessionStorage is associated with a particular browsing context.

For example:

```text
Tab A
    ↓
sessionStorage

Tab B
    ↓
sessionStorage
```

The two tabs should not be treated as sharing the same sessionStorage data.

This makes sessionStorage useful when different tabs should maintain independent temporary state.

---

# 18. LocalStorage vs SessionStorage

| Feature          | LocalStorage             | SessionStorage            |
| ---------------- | ------------------------ | ------------------------- |
| API              | `localStorage`           | `sessionStorage`          |
| Stores strings   | Yes                      | Yes                       |
| Page reload      | Persists                 | Persists                  |
| Browser restart  | Normally persists        | Normally does not         |
| Typical lifetime | Persistent until removed | Current page session      |
| Scope            | Origin                   | Origin + browsing context |
| `setItem()`      | Yes                      | Yes                       |
| `getItem()`      | Yes                      | Yes                       |
| `removeItem()`   | Yes                      | Yes                       |
| `clear()`        | Yes                      | Yes                       |
| JSON support     | Manual                   | Manual                    |

Simple rule:

```text
localStorage
    → keep data longer

sessionStorage
    → keep data temporarily
```

---

# 19. SessionStorage vs JavaScript Variables

A normal variable:

```javascript
let currentStep = 2;
```

exists only inside the relevant JavaScript execution context.

SessionStorage:

```javascript
sessionStorage.setItem(
    "currentStep",
    "2"
);
```

can survive a page reload during the same page session.

---

# 20. Multi-Step Form Example

Imagine a registration form with:

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

Read it:

```javascript
const step =
    Number(
        sessionStorage.getItem(
            "registrationStep"
        )
    ) || 1;
```

Now a page reload can restore the current step.

---

# 21. Temporary Form Data

You can temporarily store non-sensitive form information:

```javascript
const formData = {
    firstName: "Sandip",
    city: "Birgunj"
};

sessionStorage.setItem(
    "formData",
    JSON.stringify(formData)
);
```

Read:

```javascript
const stored =
    sessionStorage.getItem("formData");

if (stored) {
    const formData =
        JSON.parse(stored);

    console.log(formData.firstName);
}
```

Do not use browser storage for highly sensitive information such as passwords.

---

# 22. Temporary Filters

Suppose a product page has:

```text
Category
Price
Sort
```

Store the current filter:

```javascript
const filters = {
    category: "electronics",
    sort: "price-low"
};

sessionStorage.setItem(
    "productFilters",
    JSON.stringify(filters)
);
```

Read:

```javascript
const stored =
    sessionStorage.getItem(
        "productFilters"
    );

const filters = stored
    ? JSON.parse(stored)
    : null;
```

---

# 23. SessionStorage Helper

You can create a small helper:

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
        sessionStorage.removeItem(key);
    }
};
```

Usage:

```javascript
sessionStore.set(
    "filters",
    {
        category: "laptop",
        sort: "price"
    }
);
```

Read:

```javascript
const filters =
    sessionStore.get("filters");

console.log(filters);
```

Remove:

```javascript
sessionStore.remove("filters");
```

---

# 24. SessionStorage in React

A common use case is preserving temporary UI state.

```jsx
import { useState } from "react";

function Checkout() {
    const [step, setStep] = useState(() => {
        return Number(
            sessionStorage.getItem(
                "checkoutStep"
            )
        ) || 1;
    });

    function nextStep() {
        const next = step + 1;

        setStep(next);

        sessionStorage.setItem(
            "checkoutStep",
            String(next)
        );
    }

    return (
        <div>
            <p>Step: {step}</p>

            <button onClick={nextStep}>
                Next
            </button>
        </div>
    );
}
```

---

# 25. SessionStorage and JSON

The storage API itself only stores strings.

Therefore:

```javascript
sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

and:

```javascript
const user = JSON.parse(
    sessionStorage.getItem("user")
);
```

are common patterns.

Remember:

```text
JavaScript Object
      ↓
JSON.stringify()
      ↓
String
      ↓
sessionStorage
      ↓
String
      ↓
JSON.parse()
      ↓
JavaScript Object
```

---

# 26. Checking for Missing Data

`getItem()` returns `null` if the key does not exist.

```javascript
const value =
    sessionStorage.getItem("username");

if (value === null) {
    console.log("No username stored");
}
```

This is better than assuming a value always exists.

---

# 27. Iterating Through SessionStorage

```javascript
for (
    let i = 0;
    i < sessionStorage.length;
    i++
) {
    const key =
        sessionStorage.key(i);

    const value =
        sessionStorage.getItem(key);

    console.log(key, value);
}
```

The key order should not be relied upon.

---

# 28. SessionStorage and Origin

SessionStorage is also associated with an origin.

An origin consists of:

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

Their storage is separate.

---

# 29. Security Considerations

SessionStorage is accessible to JavaScript.

For example:

```javascript
sessionStorage.getItem(
    "someData"
);
```

Therefore, do not assume sessionStorage is a secure secret store.

Avoid storing:

```text
Passwords
Private keys
Highly sensitive data
Long-lived authentication secrets
```

An XSS vulnerability can potentially expose data accessible to JavaScript.

---

# 30. SessionStorage and Authentication

Do not assume that using sessionStorage automatically makes authentication secure.

For example:

```javascript
sessionStorage.setItem(
    "token",
    token
);
```

makes the token accessible to JavaScript.

Authentication systems should carefully consider secure cookie-based approaches and other protections appropriate to the application.

---

# 31. SessionStorage and Cookies

SessionStorage and cookies have different purposes.

### SessionStorage

```text
Browser-side temporary storage
```

### Cookies

```text
Small pieces of browser data
that can also participate in
HTTP request handling
```

Cookies can have security attributes such as:

```text
HttpOnly
Secure
SameSite
```

SessionStorage does not provide equivalent cookie attributes.

---

# 32. SessionStorage Is Not a Database

Do not use sessionStorage as a replacement for:

```text
MongoDB
PostgreSQL
MySQL
Redis
```

It is client-side browser storage.

For larger structured client-side data, consider IndexedDB.

---

# 33. SessionStorage vs URL Parameters

Temporary state can sometimes be represented in the URL.

Example:

```text
/products?category=phone
```

Advantages:

* Shareable
* Bookmarkable
* Visible in URL

SessionStorage:

```text
Temporary browser-side state
```

Choose based on whether the state should be shareable and represented as part of navigation.

---

# 34. SessionStorage vs React State

React state:

```javascript
const [step, setStep] =
    useState(1);
```

is useful for active UI rendering.

SessionStorage:

```javascript
sessionStorage.setItem(
    "step",
    "1"
);
```

can preserve temporary state across page reloads during the page session.

They can be used together.

---

# 35. Example: Search State

```javascript
const searchState = {
    query: "laptop",
    page: 2
};

sessionStorage.setItem(
    "searchState",
    JSON.stringify(searchState)
);
```

Read:

```javascript
const stored =
    sessionStorage.getItem(
        "searchState"
    );

if (stored) {
    const searchState =
        JSON.parse(stored);

    console.log(searchState.query);
}
```

---

# 36. Example: Checkout Step

Store:

```javascript
sessionStorage.setItem(
    "checkoutStep",
    "3"
);
```

Read:

```javascript
const step =
    Number(
        sessionStorage.getItem(
            "checkoutStep"
        )
    ) || 1;

console.log(step);
```

Clear when checkout is finished:

```javascript
sessionStorage.removeItem(
    "checkoutStep"
);
```

---

# 37. Example: Temporary UI Preference

```javascript
sessionStorage.setItem(
    "sidebar",
    "collapsed"
);
```

Read:

```javascript
const sidebar =
    sessionStorage.getItem(
        "sidebar"
    );

if (sidebar === "collapsed") {
    console.log("Sidebar is collapsed");
}
```

---

# 38. Storage Errors

Storage operations can fail in some environments.

Use `try...catch` when appropriate:

```javascript
try {
    sessionStorage.setItem(
        "data",
        "hello"
    );
} catch (error) {
    console.error(
        "Unable to use sessionStorage:",
        error
    );
}
```

Possible reasons include browser privacy settings or storage restrictions.

---

# 39. Common Mistakes

## Mistake 1: Expecting an object

Wrong:

```javascript
sessionStorage.setItem(
    "user",
    user
);
```

Correct:

```javascript
sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

## Mistake 2: Forgetting `JSON.parse()`

Wrong:

```javascript
const user =
    sessionStorage.getItem("user");

console.log(user.name);
```

Correct:

```javascript
const user = JSON.parse(
    sessionStorage.getItem("user")
);

console.log(user.name);
```

For production code, handle missing or invalid JSON.

---

## Mistake 3: Assuming data lasts forever

SessionStorage is intended for a page session.

If data must persist longer, consider:

```text
localStorage
```

or a server-side persistence mechanism.

---

## Mistake 4: Storing passwords

Never use sessionStorage as a password storage mechanism.

---

# 40. LocalStorage vs SessionStorage Example

### LocalStorage

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

Use when the preference should normally persist.

### SessionStorage

```javascript
sessionStorage.setItem(
    "checkoutStep",
    "2"
);
```

Use when the information is temporary for the current browsing session.

---

# 41. When to Use SessionStorage

Good examples:

```text
Multi-step form progress
Temporary search state
Temporary filters
Checkout step
Temporary UI state
Unsaved non-sensitive form data
```

Avoid using it for:

```text
Passwords
Private keys
Highly sensitive secrets
Large datasets
Permanent application data
```

---

# 42. Key Takeaways

* `sessionStorage` is part of the Web Storage API.
* It stores key-value pairs.
* Values are stored as strings.
* Use JSON for objects and arrays.
* `getItem()` returns `null` when a key does not exist.
* `setItem()` stores data.
* `removeItem()` removes one item.
* `clear()` removes all sessionStorage entries for the current origin and session context.
* Page reloads normally preserve sessionStorage.
* Closing the page session normally removes sessionStorage.
* SessionStorage is associated with the current browsing context.
* Different tabs should be treated as having separate sessionStorage.
* SessionStorage is not a database.
* SessionStorage is accessible to JavaScript.
* Do not store passwords or highly sensitive secrets.
* Use localStorage when data should normally persist longer.
* Use sessionStorage for temporary browser-side state.

---

# Quick Cheat Sheet

```javascript
// Store
sessionStorage.setItem(
    "name",
    "Sandip"
);

// Read
const name =
    sessionStorage.getItem("name");

// Remove one
sessionStorage.removeItem("name");

// Remove all
sessionStorage.clear();

// Store object
sessionStorage.setItem(
    "user",
    JSON.stringify(user)
);

// Read object
const user = JSON.parse(
    sessionStorage.getItem("user")
);

// Number
const age = Number(
    sessionStorage.getItem("age")
);

// Boolean
const active =
    sessionStorage.getItem("active") === "true";

// Number of keys
sessionStorage.length;

// Get key by index
sessionStorage.key(0);
```

---
