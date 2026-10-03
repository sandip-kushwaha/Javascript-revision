# JavaScript Cookies

Cookies are small pieces of data that a website can store in the user's browser.

Unlike `localStorage` and `sessionStorage`, cookies can be automatically sent to the server with matching HTTP requests.

Cookies are commonly used for:

* Authentication sessions
* Session identifiers
* User preferences
* Remembering small pieces of state
* Server-side session management

---

# 1. What is a Cookie?

A cookie is a small name-value pair stored by the browser.

Example:

```javascript
document.cookie = "username=Sandip";
```

Read cookies:

```javascript
console.log(document.cookie);
```

Possible output:

```text
username=Sandip
```

---

# 2. Basic Cookie Structure

A cookie can contain:

```text
name=value
```

Example:

```text
username=Sandip
```

It can also have attributes:

```text
name=value; Max-Age=3600; Path=/; Secure; SameSite=Lax
```

Important attributes include:

```text
Expires
Max-Age
Domain
Path
Secure
HttpOnly
SameSite
```

---

# 3. Creating a Cookie

Basic example:

```javascript
document.cookie =
    "username=Sandip";
```

Read it:

```javascript
console.log(document.cookie);
```

---

# 4. Cookie Values Are Strings

Cookie values are represented as text.

Example:

```javascript
document.cookie =
    "age=22";
```

When reading:

```javascript
console.log(document.cookie);
```

The value is represented as:

```text
age=22
```

If your application needs structured data, you must serialize and parse it appropriately.

---

# 5. Cookie Expiration

A cookie can have an expiration date.

Example:

```javascript
document.cookie =
    "username=Sandip; Expires=Wed, 31 Dec 2026 23:59:59 GMT; Path=/";
```

After the expiration time, the browser can remove the cookie.

---

# 6. Max-Age

`Max-Age` specifies how many seconds the cookie should remain valid.

Example:

```javascript
document.cookie =
    "username=Sandip; Max-Age=3600; Path=/";
```

Here:

```text
3600 seconds = 1 hour
```

`Max-Age` is often easier to calculate than an absolute expiration date.

---

# 7. Session Cookies

If a cookie does not specify persistent expiration information, it can act as a session cookie.

Example:

```javascript
document.cookie =
    "session=abc123; Path=/";
```

Its lifetime is managed according to browser session behavior.

Do not use session-cookie lifetime as a security mechanism by itself.

---

# 8. Path Attribute

`Path` controls which URL paths can receive the cookie.

Example:

```javascript
document.cookie =
    "theme=dark; Path=/";
```

This makes the cookie available to paths under the site's root.

A narrower path can be used:

```javascript
document.cookie =
    "checkoutStep=2; Path=/checkout";
```

The cookie is then scoped to matching paths.

---

# 9. Domain Attribute

`Domain` controls which hostnames can receive the cookie.

Example:

```text
Domain=example.com
```

A cookie's domain behavior is subject to browser cookie rules and domain relationships.

Avoid setting `Domain` unnecessarily. Host-only cookies are often preferable when a cookie does not need to be shared with subdomains.

---

# 10. Secure Attribute

`Secure` tells the browser to send the cookie only over secure HTTPS connections, subject to browser rules.

Example:

```javascript
document.cookie =
    "session=abc123; Secure; Path=/";
```

For production applications, sensitive cookies should generally be protected with HTTPS.

---

# 11. HttpOnly Attribute

`HttpOnly` prevents JavaScript from reading the cookie through APIs such as:

```javascript
document.cookie
```

A server can set:

```text
Set-Cookie: session=abc123; HttpOnly; Secure
```

JavaScript cannot directly read the value.

This is especially useful for sensitive session cookies.

> `HttpOnly` cannot normally be added to a cookie using `document.cookie`. It must be set by the server through the `Set-Cookie` response header.

---

# 12. SameSite Attribute

`SameSite` controls how cookies are handled in cross-site requests.

Common values:

```text
Strict
Lax
None
```

Example:

```javascript
document.cookie =
    "session=abc123; SameSite=Lax; Secure; Path=/";
```

---

## SameSite=Strict

```text
SameSite=Strict
```

Provides stronger cross-site restrictions.

The browser generally sends the cookie only in same-site contexts.

---

## SameSite=Lax

```text
SameSite=Lax
```

Provides a balance between usability and cross-site request protection and is a common choice for many session cookies.

---

## SameSite=None

```text
SameSite=None; Secure
```

Allows the cookie to be sent in cross-site contexts when other cookie rules permit it.

Modern browsers require `Secure` when using:

```text
SameSite=None
```

---

# 13. Cookie Security Example

A server-side session cookie might be configured approximately as:

```text
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

This combines:

```text
HttpOnly
    → JavaScript cannot read it

Secure
    → HTTPS only

SameSite=Lax
    → limits cross-site sending

Path=/
    → available throughout the site
```

Exact cookie settings should match the application's authentication and deployment architecture.

---

# 14. Reading Cookies with JavaScript

JavaScript can read cookies that are accessible to the current document.

```javascript
console.log(document.cookie);
```

Example result:

```text
username=Sandip; theme=dark
```

However, `HttpOnly` cookies are not exposed through `document.cookie`.

---

# 15. Reading a Specific Cookie

`document.cookie` returns all JavaScript-accessible cookies as one string.

Example:

```javascript
console.log(document.cookie);
```

Possible result:

```text
username=Sandip; theme=dark; language=en
```

You can parse the string:

```javascript
function getCookie(name) {
    const cookies =
        document.cookie.split("; ");

    for (const cookie of cookies) {
        const [key, value] =
            cookie.split("=");

        if (key === name) {
            return decodeURIComponent(value);
        }
    }

    return null;
}
```

Usage:

```javascript
const username =
    getCookie("username");

console.log(username);
```

---

# 16. Setting a Cookie Helper

You can create a reusable function:

```javascript
function setCookie(
    name,
    value,
    maxAge
) {
    document.cookie =
        `${encodeURIComponent(name)}=${encodeURIComponent(value)}; Max-Age=${maxAge}; Path=/`;
}
```

Usage:

```javascript
setCookie(
    "theme",
    "dark",
    3600
);
```

---

# 17. Deleting a Cookie

To remove a cookie, set its expiration in the past or use:

```text
Max-Age=0
```

Example:

```javascript
document.cookie =
    "theme=; Max-Age=0; Path=/";
```

The attributes used when deleting should match the cookie's relevant scope, especially its `Path` and `Domain` if one was originally specified.

---

# 18. Updating a Cookie

To update a cookie, set the same cookie name with a new value and matching scope.

```javascript
document.cookie =
    "theme=light; Path=/";
```

Later:

```javascript
document.cookie =
    "theme=dark; Path=/";
```

The cookie value is updated.

---

# 19. Cookie Encoding

Cookie values may need encoding when they contain characters that are not appropriate for the cookie format.

Use:

```javascript
encodeURIComponent(value);
```

Example:

```javascript
const value =
    encodeURIComponent(
        "Hello World"
    );

document.cookie =
    `message=${value}; Path=/`;
```

Read it with:

```javascript
decodeURIComponent(value);
```

---

# 20. Storing JSON in Cookies

Cookies can technically contain serialized JSON, but cookies are small and are sent with matching HTTP requests.

Example:

```javascript
const preferences = {
    theme: "dark",
    language: "en"
};

document.cookie =
    `preferences=${encodeURIComponent(
        JSON.stringify(preferences)
    )}; Path=/`;
```

Read and parse:

```javascript
const raw =
    getCookie("preferences");

const preferences = raw
    ? JSON.parse(raw)
    : null;
```

For larger client-side data, use storage designed for that purpose instead of cookies.

---

# 21. Cookies and HTTP Requests

One major difference from Web Storage is that matching cookies can be included automatically in HTTP requests.

Conceptually:

```text
Browser
   │
   │ Cookie
   ▼
Server
```

For example:

```text
Cookie: sessionId=abc123
```

The server can use the cookie to identify a session.

---

# 22. Set-Cookie Response Header

Servers can create cookies using the HTTP response header:

```text
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

The browser stores the cookie.

Later, matching requests can include:

```text
Cookie: sessionId=abc123
```

This is a common pattern for server-managed sessions.

---

# 23. Cookie Request Flow

A typical authentication flow can look like:

```text
1. User logs in
        ↓
2. Server verifies credentials
        ↓
3. Server creates session/token
        ↓
4. Server sends Set-Cookie
        ↓
5. Browser stores cookie
        ↓
6. Browser sends matching cookie
   with future requests
        ↓
7. Server validates session/token
```

---

# 24. Cookies with Fetch

When making cross-origin requests, cookie behavior depends on the request and cookie configuration.

For example:

```javascript
fetch(
    "https://api.example.com/user",
    {
        credentials: "include"
    }
);
```

`credentials: "include"` tells `fetch()` to include credentials according to the browser's cookie and CORS rules.

The server must also be configured correctly for credentialed cross-origin requests.

---

# 25. Cookies and CORS

Suppose:

```text
Frontend:
https://app.example.com

Backend:
https://api.example.com
```

If cookies are involved, the frontend and backend must use compatible:

```text
CORS configuration
Cookie attributes
Credential settings
```

For example:

```javascript
fetch(
    "https://api.example.com/user",
    {
        credentials: "include"
    }
);
```

The backend must explicitly allow the requesting origin and credentials where required.

A wildcard:

```text
Access-Control-Allow-Origin: *
```

cannot be used for credentialed browser requests.

---

# 26. Cookies in Express

In an Express backend, cookies can be set with:

```javascript
res.cookie(
    "sessionId",
    sessionId,
    {
        httpOnly: true,
        secure: true,
        sameSite: "lax",
        maxAge: 60 * 60 * 1000
    }
);
```

This creates a cookie with a one-hour lifetime.

---

# 27. Reading Cookies in Express

With the `cookie-parser` middleware:

```javascript
import cookieParser from "cookie-parser";

app.use(cookieParser());
```

Then:

```javascript
app.get(
    "/profile",
    (req, res) => {
        console.log(
            req.cookies.sessionId
        );

        res.json({
            message: "Profile"
        });
    }
);
```

---

# 28. Clearing Cookies in Express

Use:

```javascript
res.clearCookie(
    "sessionId"
);
```

The cookie scope should be configured consistently with how the original cookie was created.

---

# 29. Cookies for Authentication

A common architecture is:

```text
Login
  ↓
Server verifies credentials
  ↓
Server creates session/token
  ↓
HttpOnly Secure cookie
  ↓
Browser
  ↓
Future requests
  ↓
Server validates cookie
```

This can prevent JavaScript from directly reading the authentication cookie when `HttpOnly` is used.

---

# 30. Cookies vs localStorage for Authentication

| Feature                                        | Cookie                  | localStorage          |
| ---------------------------------------------- | ----------------------- | --------------------- |
| Automatically sent with matching HTTP requests | Yes                     | No                    |
| JavaScript access                              | Depends on `HttpOnly`   | Yes                   |
| Can use `HttpOnly`                             | Yes                     | No                    |
| Can use `Secure`                               | Yes                     | No                    |
| Can use `SameSite`                             | Yes                     | No                    |
| Suitable for server-managed sessions           | Yes                     | Not directly          |
| XSS exposure of stored value                   | Reduced with `HttpOnly` | JavaScript-accessible |

Neither storage mechanism automatically makes an application secure. Authentication systems also need protections against issues such as XSS and CSRF, depending on the architecture.

---

# 31. Cookies and CSRF

Cookies can be automatically included with requests, which is useful for authentication but also creates CSRF considerations.

Common defenses include:

```text
SameSite cookies
CSRF tokens
Origin checking
Referer checking where appropriate
```

The appropriate defense depends on the application's architecture.

---

# 32. Cookie Size

Cookies are designed for small amounts of data.

Do not use cookies as a replacement for:

```text
Database
localStorage
IndexedDB
Large JSON objects
Files
```

Cookies also have the additional cost that matching cookies can be sent with HTTP requests.

---

# 33. Cookie Scope

Cookie behavior depends on attributes such as:

```text
Domain
Path
Secure
SameSite
```

A cookie intended only for a specific part of an application can use a narrower `Path`.

For example:

```text
Path=/admin
```

can restrict the cookie to matching paths.

---

# 34. Common Cookie Mistakes

## Mistake 1 — Storing passwords

Never store passwords in cookies.

```text
❌ password=123456
```

Passwords should be securely handled by the authentication system.

---

## Mistake 2 — Storing sensitive data without protection

Avoid putting sensitive information in a JavaScript-readable cookie when it does not need to be accessible to JavaScript.

Consider:

```text
HttpOnly
Secure
SameSite
```

where appropriate.

---

## Mistake 3 — Forgetting HTTPS

Sensitive cookies should generally use:

```text
Secure
```

in production HTTPS environments.

---

## Mistake 4 — Assuming HttpOnly prevents every attack

`HttpOnly` prevents JavaScript from directly reading the cookie value, but it does not eliminate all consequences of an XSS vulnerability.

An attacker-controlled script may still be able to perform actions using the victim's authenticated browser context.

XSS prevention remains important.

---

## Mistake 5 — Incorrect CORS configuration

When using cookies across origins, make sure:

```text
Frontend credentials
        +
Backend CORS
        +
Cookie attributes
```

are configured consistently.

---

# 35. Cookie Example — Theme Preference

A simple preference can be stored:

```javascript
document.cookie =
    "theme=dark; Max-Age=2592000; Path=/";
```

Read:

```javascript
const theme =
    getCookie("theme");

console.log(theme);
```

This cookie can remain for approximately 30 days.

---

# 36. Cookie Example — Session

A server can create:

```text
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

The browser stores the cookie.

The client JavaScript does not need to read the session ID.

Future matching requests can automatically include it.

---

# 37. Cookie Example — Logout

Server-side logout can clear the authentication cookie:

```javascript
res.clearCookie(
    "sessionId"
);

res.status(200).json({
    message: "Logged out"
});
```

The browser then removes the cookie according to the cookie's matching scope.

---

# 38. localStorage vs sessionStorage vs Cookies

| Feature                      | localStorage | sessionStorage               | Cookies               |
| ---------------------------- | ------------ | ---------------------------- | --------------------- |
| Persistent                   | Yes          | Usually only current session | Depends on expiration |
| Survives refresh             | Yes          | Yes                          | Yes                   |
| Normally survives tab close  | Yes          | No                           | Depends               |
| Stores strings               | Yes          | Yes                          | Text values           |
| Automatically sent to server | No           | No                           | Yes, when applicable  |
| JavaScript access            | Yes          | Yes                          | Depends on HttpOnly   |
| HttpOnly                     | No           | No                           | Yes                   |
| Secure attribute             | No           | No                           | Yes                   |
| SameSite                     | No           | No                           | Yes                   |
| Best for                     | Preferences  | Temporary tab state          | Server-aware sessions |

---

# 39. When Should You Use Cookies?

Use cookies when:

```text
Browser ↔ Server communication
```

is important.

Typical examples:

```text
Authentication sessions
Session identifiers
Small server-related preferences
Security-related browser state
```

---

# 40. When Should You Not Use Cookies?

Avoid cookies for:

```text
Large datasets
Large JSON objects
Files
Application databases
Passwords
Sensitive data that does not need to be sent to the server
```

Use a more appropriate storage mechanism.

---

# 41. Cookie Security Checklist

For a sensitive session cookie, consider:

```text
[✓] HTTPS
[✓] Secure
[✓] HttpOnly
[✓] Appropriate SameSite
[✓] Appropriate Path
[✓] Minimal Domain scope
[✓] Short appropriate lifetime
[✓] Server-side session validation
[✓] CSRF protection when needed
[✓] XSS protection
```

The exact configuration should match your application's architecture.

---

# 42. Quick Cheat Sheet

### Browser JavaScript

```javascript
// Set
document.cookie =
    "theme=dark; Path=/";

// Read
console.log(
    document.cookie
);

// Delete
document.cookie =
    "theme=; Max-Age=0; Path=/";
```

### Server

```javascript
res.cookie(
    "sessionId",
    sessionId,
    {
        httpOnly: true,
        secure: true,
        sameSite: "lax",
        maxAge: 60 * 60 * 1000
    }
);
```

### Fetch

```javascript
fetch(
    "/api/user",
    {
        credentials: "include"
    }
);
```

---

# 43. Cookie Structure

```text
Cookie
│
├── Name
│   └── sessionId
│
├── Value
│   └── abc123
│
├── Lifetime
│   ├── Expires
│   └── Max-Age
│
├── Scope
│   ├── Domain
│   └── Path
│
└── Security
    ├── Secure
    ├── HttpOnly
    └── SameSite
```

---

# Key Takeaways

* Cookies are small pieces of browser data.
* Cookies can be automatically sent with matching HTTP requests.
* `document.cookie` can read JavaScript-accessible cookies.
* `HttpOnly` cookies cannot normally be read through JavaScript.
* `Secure` restricts cookie transmission to secure connections.
* `SameSite` controls important cross-site cookie behavior.
* `Path` and `Domain` control cookie scope.
* `Max-Age` and `Expires` control cookie lifetime.
* Cookies are useful for server-managed authentication sessions.
* Cookies are small and should not be used for large application data.
* Cookie-based authentication still requires XSS and CSRF protections appropriate to the architecture.
* For sensitive authentication cookies, `HttpOnly`, `Secure`, and an appropriate `SameSite` policy are commonly important.
* `localStorage` and `sessionStorage` are client-side storage APIs and are not automatically sent with HTTP requests.
* Cookie configuration should be designed together with your frontend, backend, CORS, and authentication architecture.
