# Browser Storage Comparison

JavaScript applications have several ways to store data in the browser.

The most common options are:

```text
localStorage
sessionStorage
Cookies
IndexedDB
```

Each storage mechanism has a different purpose.

---

# 1. Overview

```text
Browser Storage
│
├── localStorage
│   └── Persistent client-side data
│
├── sessionStorage
│   └── Temporary tab/session data
│
├── Cookies
│   └── Browser ↔ server data
│
└── IndexedDB
    └── Larger structured client-side data
```

---

# 2. localStorage

`localStorage` stores key-value data that normally remains available after:

* Page refresh
* Tab closing
* Browser closing
* Reopening the website

Example:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

Read:

```javascript
const theme =
    localStorage.getItem("theme");
```

Common uses:

```text
Theme
Language
UI preferences
Small application settings
Shopping cart data
```

Do not use it as a secure secret store.

---

# 3. sessionStorage

`sessionStorage` stores data associated with the current browsing session.

Example:

```javascript
sessionStorage.setItem(
    "checkoutStep",
    "2"
);
```

Read:

```javascript
const step =
    sessionStorage.getItem(
        "checkoutStep"
    );
```

Common uses:

```text
Temporary form data
Checkout progress
Multi-step forms
Temporary UI state
Tab-specific state
```

Refreshing the page normally does not remove it.

Closing the associated tab/window normally ends its session lifetime.

---

# 4. Cookies

Cookies are small pieces of data that can be sent automatically with matching HTTP requests.

Example:

```javascript
document.cookie =
    "theme=dark; Path=/";
```

Cookies can also be created by the server:

```text
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax
```

Common uses:

```text
Authentication sessions
Session identifiers
Small server-related preferences
Browser/server state
```

---

# 5. IndexedDB

IndexedDB is a browser database API designed for larger and more structured client-side data.

It supports storing:

```text
Objects
Arrays
Structured records
Binary data
Large datasets
```

Unlike Web Storage, IndexedDB is designed for asynchronous database-style operations.

Example conceptually:

```text
Application
    ↓
IndexedDB
    ↓
Object Store
    ↓
Records
```

Common uses:

```text
Offline applications
Large client-side datasets
Caching application data
Progressive web applications
```

---

# 6. Main Comparison

| Feature                      | localStorage           | sessionStorage         | Cookies                    | IndexedDB                  |
| ---------------------------- | ---------------------- | ---------------------- | -------------------------- | -------------------------- |
| Main purpose                 | Persistent client data | Temporary session data | Browser/server data        | Structured client database |
| Persistence                  | Long-lived             | Current session        | Configurable               | Long-lived                 |
| Survives refresh             | Yes                    | Yes                    | Yes                        | Yes                        |
| Normally survives tab close  | Yes                    | No                     | Depends                    | Yes                        |
| Automatically sent to server | No                     | No                     | Yes, when applicable       | No                         |
| JavaScript access            | Yes                    | Yes                    | Depends on `HttpOnly`      | Yes                        |
| `HttpOnly`                   | No                     | No                     | Yes                        | No                         |
| `Secure` attribute           | No                     | No                     | Yes                        | No                         |
| `SameSite`                   | No                     | No                     | Yes                        | No                         |
| Data model                   | Key-value strings      | Key-value strings      | Small text values          | Structured records         |
| Async API                    | No                     | No                     | No                         | Yes                        |
| Suitable for large data      | No                     | No                     | No                         | Yes                        |
| Good for temporary state     | Sometimes              | Yes                    | Sometimes                  | Yes                        |
| Good for authentication      | Not ideal for secrets  | Not ideal for secrets  | Common choice for sessions | No                         |

---

# 7. Persistence Comparison

```text
localStorage
    ↓
Long-term browser storage
```

```text
sessionStorage
    ↓
Current browsing session
```

```text
Cookies
    ↓
Lifetime controlled by cookie attributes
```

```text
IndexedDB
    ↓
Persistent browser database
```

---

# 8. Data Type Comparison

## localStorage

Stores strings:

```javascript
localStorage.setItem(
    "age",
    22
);
```

Read:

```javascript
const age =
    localStorage.getItem("age");

console.log(typeof age);
```

Result:

```text
string
```

Objects need JSON serialization:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

---

## sessionStorage

Also stores strings:

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
```

Result:

```text
string
```

---

## Cookies

Cookies contain textual name-value data and cookie attributes.

Example:

```text
theme=dark
```

---

## IndexedDB

IndexedDB can store structured JavaScript data rather than requiring everything to be converted into one string.

---

# 9. Server Communication

One of the biggest differences is whether data is automatically included in HTTP requests.

### localStorage

```text
Browser
   │
   │ Request
   ▼
Server

localStorage
   │
   └── Not automatically sent
```

### sessionStorage

```text
Browser
   │
   │ Request
   ▼
Server

sessionStorage
   │
   └── Not automatically sent
```

### Cookies

```text
Browser
   │
   │ Request + matching Cookie
   ▼
Server
```

### IndexedDB

```text
Browser
   │
   │ Request
   ▼
Server

IndexedDB
   │
   └── Not automatically sent
```

---

# 10. Authentication

For many web applications, authentication is implemented using server-managed sessions or tokens stored in cookies.

Example:

```text
Login
  ↓
Server verifies credentials
  ↓
Server creates session
  ↓
HttpOnly + Secure cookie
  ↓
Browser
  ↓
Future requests
  ↓
Server validates session
```

A sensitive authentication value stored in localStorage or sessionStorage is directly accessible to JavaScript, which can increase exposure if an XSS vulnerability exists.

---

# 11. localStorage for Preferences

Good example:

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

Why?

```text
Theme preference
      ↓
Should remain after reopening
      ↓
localStorage
```

---

# 12. sessionStorage for Temporary State

Example:

```javascript
sessionStorage.setItem(
    "currentStep",
    "2"
);
```

Why?

```text
Checkout step
      ↓
Needed temporarily
      ↓
Current tab/session
      ↓
sessionStorage
```

---

# 13. Cookies for Sessions

Example server response:

```text
Set-Cookie:
sessionId=abc123;
HttpOnly;
Secure;
SameSite=Lax;
Path=/
```

Why?

```text
Authentication session
       ↓
Browser ↔ Server
       ↓
Cookie
```

---

# 14. IndexedDB for Larger Client Data

Suppose an offline application needs to store:

```text
Thousands of records
Images
Structured objects
Cached application data
```

Using many localStorage entries may become inconvenient.

IndexedDB is designed for this type of client-side storage.

---

# 15. Storage Size

Storage limits vary by browser and environment.

Do not design your application around a single exact storage size unless you have verified the target browser/environment.

General idea:

```text
Cookies
    → very small

localStorage
    → small client-side storage

sessionStorage
    → small temporary storage

IndexedDB
    → much more suitable for larger datasets
```

For large client-side applications, IndexedDB is generally more appropriate than Web Storage.

---

# 16. Synchronous vs Asynchronous

This distinction is important.

### localStorage

```javascript
localStorage.getItem("user");
```

Synchronous.

### sessionStorage

```javascript
sessionStorage.getItem("user");
```

Synchronous.

### IndexedDB

Designed around asynchronous database operations.

This makes IndexedDB more suitable for larger datasets and operations that should not block the main JavaScript execution path.

---

# 17. Security Comparison

| Storage        | JavaScript can access? | HttpOnly available? | Main security concern                 |
| -------------- | ---------------------- | ------------------- | ------------------------------------- |
| localStorage   | Yes                    | No                  | XSS can expose stored values          |
| sessionStorage | Yes                    | No                  | XSS can expose stored values          |
| Cookies        | Depends                | Yes                 | CSRF/XSS/session theft considerations |
| IndexedDB      | Yes                    | No                  | XSS can access stored data            |

Important:

> No browser storage mechanism should be treated as a completely secure secret vault.

Security depends on:

```text
Authentication design
XSS protection
CSRF protection
HTTPS
Cookie configuration
Server-side validation
Access control
```

---

# 18. Cookies and HttpOnly

One major advantage of cookies for sensitive session identifiers is:

```text
HttpOnly
```

Example:

```text
Set-Cookie:
sessionId=abc123;
HttpOnly;
Secure;
SameSite=Lax;
Path=/
```

JavaScript cannot normally read the cookie:

```javascript
document.cookie
```

will not expose the HttpOnly value.

However, HttpOnly does not prevent all consequences of XSS. Malicious JavaScript can still potentially make authenticated requests from the victim's browser.

---

# 19. Same-Origin Behavior

Browser storage is subject to origin rules.

An origin is based on:

```text
Scheme
Host
Port
```

For example:

```text
https://example.com
```

is a different origin from:

```text
http://example.com
```

Storage is not automatically shared between different origins.

---

# 20. Storage Scope

### localStorage

Associated with an origin.

```text
Origin
   ↓
localStorage
```

### sessionStorage

Associated with an origin and browsing session/context.

```text
Origin
   ↓
Tab / browsing context
   ↓
sessionStorage
```

### Cookies

Cookie scope can be affected by:

```text
Domain
Path
Secure
SameSite
```

### IndexedDB

IndexedDB databases are associated with an origin.

---

# 21. Choosing Storage

Use this decision guide:

```text
Need persistent small client data?
            │
            └── Yes
                 ↓
            localStorage
```

```text
Need temporary tab/session data?
            │
            └── Yes
                 ↓
            sessionStorage
```

```text
Need browser ↔ server session data?
            │
            └── Yes
                 ↓
              Cookies
```

```text
Need larger structured client data?
            │
            └── Yes
                 ↓
             IndexedDB
```

---

# 22. Example — Theme

```javascript
localStorage.setItem(
    "theme",
    "dark"
);
```

Best fit:

```text
localStorage
```

because the preference can persist.

---

# 23. Example — Multi-Step Form

```javascript
sessionStorage.setItem(
    "formStep",
    "3"
);
```

Best fit:

```text
sessionStorage
```

because the information is temporary.

---

# 24. Example — Authentication Session

Server:

```javascript
res.cookie(
    "sessionId",
    sessionId,
    {
        httpOnly: true,
        secure: true,
        sameSite: "lax",
        path: "/"
    }
);
```

Best fit:

```text
Cookie
```

because the browser can send it with matching requests and the server can manage the session.

---

# 25. Example — Offline Application

Suppose an application needs to work without an internet connection.

It may need to store:

```text
Products
Orders
Cached API data
User-generated records
Images
```

For larger structured client-side storage:

```text
IndexedDB
```

is generally more appropriate than localStorage.

---

# 26. Browser Storage Architecture

A typical application might use multiple mechanisms:

```text
                Web Application
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
 localStorage    sessionStorage     Cookies
        │              │              │
        │              │              └── Authentication
        │              └── Temporary state
        └── Preferences
                       │
                       ▼
                   IndexedDB
                       │
                       └── Larger client data
```

Using multiple storage mechanisms is normal when each one has a different purpose.

---

# 27. Example — React Application

A React application might use:

```text
localStorage
    → theme

sessionStorage
    → current checkout step

Cookie
    → authentication session

IndexedDB
    → offline cached data
```

This separation keeps each type of data in a storage mechanism appropriate to its role.

---

# 28. Example — Full-Stack Application

For a React + Node.js application:

```text
React Frontend
       │
       ├── localStorage
       │      └── theme
       │
       ├── sessionStorage
       │      └── temporary form state
       │
       └── Cookie
              └── authentication session
                       │
                       ▼
                  Node.js API
                       │
                       ▼
                    Database
```

For larger offline frontend data:

```text
React
  ↓
IndexedDB
```

can be added when needed.

---

# 29. Common Mistakes

## Mistake 1 — Using localStorage for passwords

Never store:

```text
password
```

in localStorage.

---

## Mistake 2 — Assuming sessionStorage is secure

This is incorrect:

```text
sessionStorage disappears later
        ↓
therefore it is secure
```

Security and lifetime are different concepts.

---

## Mistake 3 — Storing large data in cookies

Cookies are sent with matching requests and have small size limits.

Do not use them as a database.

---

## Mistake 4 — Using localStorage as a database

Avoid storing a huge application dataset as one JSON string:

```javascript
localStorage.setItem(
    "hugeDatabase",
    JSON.stringify(data)
);
```

For larger structured data, consider IndexedDB.

---

## Mistake 5 — Ignoring XSS

JavaScript can access:

```text
localStorage
sessionStorage
IndexedDB
```

Therefore, protecting the application against XSS is critical.

---

# 30. Practical Storage Strategy

For a modern full-stack application, a reasonable starting point is:

```text
Theme / language
        ↓
localStorage

Temporary UI state
        ↓
sessionStorage

Authentication session
        ↓
Secure cookie

Large offline data
        ↓
IndexedDB

Permanent application data
        ↓
Server database
```

This is not a universal rule. The correct choice depends on the data, security requirements, and application architecture.

---

# 31. Quick Comparison Table

| Requirement                     | Recommended starting point |
| ------------------------------- | -------------------------- |
| Theme preference                | `localStorage`             |
| Language preference             | `localStorage`             |
| Temporary form state            | `sessionStorage`           |
| Current checkout step           | `sessionStorage`           |
| Server-managed login session    | Secure cookie              |
| Small server-related preference | Cookie                     |
| Large offline dataset           | IndexedDB                  |
| Permanent application records   | Database                   |

---

# 32. Quick Cheat Sheet

```text
localStorage
    → persistent client-side storage
    → string values
    → synchronous
    → JavaScript accessible

sessionStorage
    → temporary session/tab storage
    → string values
    → synchronous
    → JavaScript accessible

Cookies
    → browser/server communication
    → automatically sent with matching requests
    → can be HttpOnly
    → can use Secure and SameSite

IndexedDB
    → structured browser database
    → larger client-side datasets
    → asynchronous API
```

---

# 33. Final Decision Tree

```text
What type of data do you have?
             │
             ▼
      Small preference?
         │         │
        Yes        No
         │          │
         ▼          ▼
   localStorage   Temporary?
                     │
                 ┌───┴───┐
                Yes      No
                 │        │
                 ▼        ▼
          sessionStorage  Server
                            │
                            ▼
                         Cookie
                            │
                            ▼
                     Large client data?
                            │
                           Yes
                            │
                            ▼
                        IndexedDB
```

---

# Key Takeaways

* `localStorage` is useful for persistent, small client-side data.
* `sessionStorage` is useful for temporary data associated with a browsing session/tab.
* Cookies are useful when the browser needs to communicate state to a server.
* Cookies can use `HttpOnly`, `Secure`, and `SameSite`.
* IndexedDB is designed for larger and more structured browser-side data.
* `localStorage` and `sessionStorage` store strings.
* Web Storage APIs are synchronous.
* IndexedDB uses an asynchronous database-style API.
* Cookies can automatically accompany matching HTTP requests.
* JavaScript cannot normally read an `HttpOnly` cookie.
* Do not store passwords or sensitive secrets in JavaScript-accessible browser storage.
* Storage lifetime does not equal storage security.
* XSS protection is important when using any JavaScript-accessible storage.
* CSRF protections may be important when using cookie-based authentication.
* Choose storage based on persistence, size, server communication, data structure, and security requirements.
