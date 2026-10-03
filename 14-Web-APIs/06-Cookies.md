# JavaScript Cookies

A **cookie** is a small piece of data associated with a website that can be stored by the browser and, depending on its attributes, sent with HTTP requests to the server.

Cookies are commonly used for:

* Authentication sessions
* Login state
* User preferences
* Session identifiers
* Tracking
* Server-side state

Unlike `localStorage` and `sessionStorage`, cookies are designed to participate directly in HTTP communication.

---

# 1. What Is a Cookie?

A cookie is generally stored as:

```text
name=value
```

Example:

```text
theme=dark
```

A cookie can also have attributes:

```text
theme=dark; Path=/; Max-Age=3600
```

Common attributes include:

```text
Path
Expires
Max-Age
Domain
Secure
HttpOnly
SameSite
```

---

# 2. Creating a Cookie with JavaScript

Use:

```javascript
document.cookie = "theme=dark";
```

This creates or updates a cookie named:

```text
theme
```

with value:

```text
dark
```

---

# 3. Reading Cookies

Read cookies using:

```javascript
console.log(document.cookie);
```

You may get:

```text
theme=dark; language=en
```

Important:

JavaScript does not receive cookies as a JavaScript object.

`document.cookie` returns a string.

---

# 4. Reading a Specific Cookie

Because `document.cookie` contains multiple cookies, you usually need to parse it.

Example:

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
const theme = getCookie("theme");

console.log(theme);
```

---

# 5. Setting a Cookie with Options

Example:

```javascript
document.cookie =
    "theme=dark; Path=/";
```

`Path=/` means the cookie is available to pages under the site's root path.

---

# 6. Cookie Values

Cookie values are strings.

Example:

```javascript
document.cookie =
    "username=Sandip";
```

If you need to store special characters, encode the value.

```javascript
const value =
    encodeURIComponent("Sandip Kushwaha");

document.cookie =
    `username=${value}; Path=/`;
```

Read it with:

```javascript
const decoded =
    decodeURIComponent(value);
```

---

# 7. `encodeURIComponent()`

Use:

```javascript
encodeURIComponent(value);
```

Example:

```javascript
const value =
    encodeURIComponent("hello world");

console.log(value);
```

The space is encoded so that the value can safely be represented in a cookie.

---

# 8. `decodeURIComponent()`

Decode an encoded value:

```javascript
const value =
    decodeURIComponent(encodedValue);
```

Example:

```javascript
const encoded =
    encodeURIComponent(
        "Sandip Kushwaha"
    );

const decoded =
    decodeURIComponent(encoded);

console.log(decoded);
```

Output:

```text
Sandip Kushwaha
```

---

# 9. Cookie `Path`

Example:

```javascript
document.cookie =
    "theme=dark; Path=/";
```

This makes the cookie available throughout the site's path hierarchy.

You can also specify a narrower path:

```javascript
document.cookie =
    "cart=123; Path=/shop";
```

The cookie is then associated with the `/shop` path and its applicable subpaths.

---

# 10. Cookie `Expires`

You can specify an expiration date:

```javascript
const date = new Date();

date.setTime(
    date.getTime() + 24 * 60 * 60 * 1000
);

document.cookie =
    `theme=dark; Expires=${date.toUTCString()}; Path=/`;
```

This cookie is set to expire approximately one day later.

---

# 11. Cookie `Max-Age`

`Max-Age` specifies how many seconds the cookie should remain valid.

Example:

```javascript
document.cookie =
    "theme=dark; Max-Age=3600; Path=/";
```

This requests a lifetime of:

```text
3600 seconds
```

which is:

```text
1 hour
```

---

# 12. Session Cookies

A cookie without `Expires` or `Max-Age` is generally a session cookie.

Example:

```javascript
document.cookie =
    "temporary=true; Path=/";
```

The browser can remove a session cookie when the relevant browsing session ends.

Exact browser behavior can vary because session restoration and browser policies may affect persistence.

---

# 13. Persistent Cookies

A cookie with `Expires` or `Max-Age` is generally persistent.

Example:

```javascript
document.cookie =
    "theme=dark; Max-Age=86400; Path=/";
```

This gives it a lifetime of approximately:

```text
24 hours
```

---

# 14. Deleting a Cookie

To delete a cookie, set its expiration in the past.

```javascript
document.cookie =
    "theme=; Max-Age=0; Path=/";
```

The `Path` should match the path used when the cookie was created.

If the cookie also used a specific `Domain`, that needs to match as well.

---

# 15. Cookie `Secure`

The `Secure` attribute tells the browser to send the cookie only over secure HTTPS connections.

Example:

```text
theme=dark; Secure
```

For production applications, sensitive cookies should generally be protected with HTTPS.

---

# 16. Cookie `HttpOnly`

`HttpOnly` prevents JavaScript from reading the cookie through:

```javascript
document.cookie
```

For example:

```text
sessionId=abc123; HttpOnly
```

JavaScript cannot access the value directly.

This is important for server-managed authentication cookies.

---

# 17. JavaScript Cannot Create HttpOnly Cookies

This does **not** work:

```javascript
document.cookie =
    "token=abc123; HttpOnly";
```

`HttpOnly` is a server-controlled cookie attribute.

The server can send:

```http
Set-Cookie: token=abc123; HttpOnly; Secure
```

The browser then stores the cookie without exposing it to JavaScript.

---

# 18. Cookie `SameSite`

`SameSite` controls when cookies can be sent in cross-site request situations.

Common values:

```text
Strict
Lax
None
```

---

# 19. SameSite=Strict

Example:

```text
session=abc123; SameSite=Strict
```

This provides the strictest same-site behavior.

The browser generally restricts sending the cookie in cross-site contexts.

---

# 20. SameSite=Lax

Example:

```text
session=abc123; SameSite=Lax
```

`Lax` allows some cross-site navigation scenarios while restricting many cross-site request contexts.

It is a common default-style choice for many session cookies.

---

# 21. SameSite=None

Example:

```text
session=abc123; SameSite=None; Secure
```

`SameSite=None` allows the cookie to be sent in cross-site contexts when browser requirements are satisfied.

Modern browsers generally require:

```text
SameSite=None
Secure
```

together.

---

# 22. Cookie Example

A server might send:

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

This means:

```text
sessionId
    → cookie name

abc123
    → cookie value

HttpOnly
    → JavaScript cannot read it

Secure
    → HTTPS only

SameSite=Lax
    → controls cross-site sending

Path=/
    → available throughout the site
```

---

# 23. Cookies and HTTP Requests

One major difference between cookies and localStorage:

```text
localStorage
    → not automatically attached to HTTP requests

Cookies
    → can be automatically included with matching requests
```

For example:

```text
Browser
   ↓
HTTP Request
   ↓
Cookie: sessionId=abc123
   ↓
Server
```

The browser controls whether the cookie is included based on its attributes and request context.

---

# 24. `document.cookie` vs HTTP Cookies

JavaScript:

```javascript
document.cookie
```

allows JavaScript to read cookies that are not `HttpOnly` and are otherwise accessible to the current document.

The browser also manages cookies received from the server through:

```http
Set-Cookie
```

Example:

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure
```

That cookie can be sent with applicable requests without being exposed through `document.cookie`.

---

# 25. Cookies and Authentication

Cookies are commonly used for authentication sessions.

A typical flow:

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
6. Browser sends cookie with applicable requests
        ↓
7. Server authenticates the request
```

Example response header:

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

---

# 26. Cookie-Based Authentication

A secure session cookie might look conceptually like:

```text
sessionId=randomValue
```

with:

```text
HttpOnly
Secure
SameSite=Lax
Path=/
```

The actual security configuration depends on the application's architecture and deployment environment.

---

# 27. Cookies with Fetch

For same-origin requests, cookies are generally handled by the browser according to normal cookie rules.

For cross-origin requests where credentials are intended, Fetch can use:

```javascript
fetch(
    "https://api.example.com/user",
    {
        credentials: "include"
    }
);
```

The server must also allow credentialed cross-origin requests through an appropriate CORS configuration.

---

# 28. Cookies with Axios

With Axios:

```javascript
axios.get(
    "https://api.example.com/user",
    {
        withCredentials: true
    }
);
```

For a frontend and backend on different origins, the backend must be configured correctly for credentialed CORS.

---

# 29. Cookie and CORS

Suppose:

```text
Frontend
http://localhost:5173
```

and:

```text
Backend
http://localhost:8000
```

are different origins.

For credentialed requests, the server must explicitly allow the requesting origin and credentials.

Conceptually:

```text
Access-Control-Allow-Origin:
http://localhost:5173

Access-Control-Allow-Credentials:
true
```

A wildcard:

```text
Access-Control-Allow-Origin: *
```

cannot be used for credentialed CORS requests.

---

# 30. Cookies vs LocalStorage

| Feature                      | Cookies              | LocalStorage                                |
| ---------------------------- | -------------------- | ------------------------------------------- |
| JavaScript access            | Yes, unless HttpOnly | Yes                                         |
| HttpOnly available           | Yes                  | No                                          |
| Secure attribute             | Yes                  | No                                          |
| SameSite                     | Yes                  | No                                          |
| Automatically sent with HTTP | Yes, when applicable | No                                          |
| Storage size                 | Small                | Larger                                      |
| Common authentication use    | Yes                  | Possible, but different security trade-offs |
| Web Storage API              | No                   | Yes                                         |

---

# 31. Cookies vs SessionStorage

| Feature                  | Cookies                           | SessionStorage       |
| ------------------------ | --------------------------------- | -------------------- |
| HTTP request integration | Yes                               | No                   |
| JavaScript access        | Depends on HttpOnly               | Yes                  |
| HttpOnly                 | Yes                               | No                   |
| Secure                   | Yes                               | No                   |
| SameSite                 | Yes                               | No                   |
| Temporary storage        | Possible                          | Yes                  |
| Main use                 | Sessions, preferences, HTTP state | Temporary page state |

---

# 32. Cookie Parsing

Suppose:

```javascript
console.log(document.cookie);
```

returns:

```text
theme=dark; language=en; user=Sandip
```

You can parse it:

```javascript
const cookies =
    document.cookie.split("; ");

console.log(cookies);
```

Result:

```javascript
[
    "theme=dark",
    "language=en",
    "user=Sandip"
]
```

---

# 33. Better Cookie Getter

A reusable function:

```javascript
function getCookie(name) {
    const cookies =
        document.cookie.split("; ");

    for (const cookie of cookies) {
        const index = cookie.indexOf("=");

        if (index === -1) {
            continue;
        }

        const key =
            cookie.slice(0, index);

        const value =
            cookie.slice(index + 1);

        if (key === name) {
            return decodeURIComponent(value);
        }
    }

    return null;
}
```

Usage:

```javascript
const theme =
    getCookie("theme");
```

---

# 34. Better Cookie Setter

```javascript
function setCookie(
    name,
    value,
    maxAge
) {
    document.cookie =
        `${encodeURIComponent(name)}=` +
        `${encodeURIComponent(value)}; ` +
        `Max-Age=${maxAge}; ` +
        `Path=/`;
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

This creates a cookie with a lifetime of approximately one hour.

---

# 35. Cookie Deletion Helper

```javascript
function deleteCookie(name) {
    document.cookie =
        `${encodeURIComponent(name)}=` +
        `Max-Age=0; Path=/`;
}
```

Usage:

```javascript
deleteCookie("theme");
```

The path and domain must match the cookie being deleted where applicable.

---

# 36. Cookie Security Flags

For sensitive server-managed cookies, commonly considered attributes include:

```text
HttpOnly
Secure
SameSite
Path
```

Example:

```text
sessionId=abc123;
HttpOnly;
Secure;
SameSite=Lax;
Path=/
```

Remember:

```text
HttpOnly → protects against JavaScript reading the cookie
Secure   → HTTPS transport
SameSite → cross-site request behavior
Path     → URL path scope
```

---

# 37. Cookie Domain

A cookie can optionally specify a domain.

Example:

```text
Domain=example.com
```

This affects which hosts can receive the cookie.

Domain configuration should be used carefully because broader cookie scope can expose the cookie to more subdomains.

---

# 38. Host-Only Cookies

If a cookie is set without a `Domain` attribute, it is generally restricted to the host that set it.

This is often preferable when a cookie does not need to be shared with other subdomains.

---

# 39. Cookie Prefixes

Modern browsers support cookie name prefixes that impose additional requirements.

Examples:

```text
__Secure-
__Host-
```

For example:

```text
__Host-session=abc123
```

`__Host-` cookies have stricter requirements, including:

```text
Secure
Path=/
No Domain attribute
```

These prefixes can help enforce safer cookie configurations when supported by the browser.

---

# 40. Cookie Size

Cookies are intended for relatively small pieces of data.

Do not store large application data inside cookies.

For larger browser-side data, consider:

```text
localStorage
sessionStorage
IndexedDB
```

depending on the use case.

---

# 41. Cookie Performance

Cookies can affect network requests because applicable cookies may be sent automatically with requests.

Therefore, avoid putting large unnecessary values into cookies.

A common pattern is:

```text
Cookie
    ↓
Small session identifier
    ↓
Server
    ↓
Session data
```

rather than storing large application objects in cookies.

---

# 42. Cookies and CSRF

Because cookies can be automatically sent with requests, applications using cookie-based authentication should consider **CSRF protection**.

Common defenses include:

```text
SameSite cookie configuration
CSRF tokens
Origin/Referer validation
Appropriate server-side request checks
```

The correct approach depends on the application's architecture.

---

# 43. Cookies and XSS

`HttpOnly` prevents JavaScript from reading the cookie directly:

```text
document.cookie
    ↓
HttpOnly cookie
    ↓
Not accessible
```

However, `HttpOnly` does **not** make an application immune to XSS.

Malicious JavaScript may still attempt to perform actions as the authenticated user through the application's normal browser context.

Therefore, XSS prevention remains important.

---

# 44. Cookies Are Not Automatically Secure

This:

```javascript
document.cookie =
    "token=abc123";
```

does not automatically mean the cookie is secure.

For sensitive cookies, consider appropriate server-side attributes such as:

```text
HttpOnly
Secure
SameSite
```

and use HTTPS.

---

# 45. Cookie Expiration

Cookies can use:

```text
Expires
```

or:

```text
Max-Age
```

Example:

```text
session=abc123; Max-Age=3600
```

means approximately:

```text
3600 seconds
```

of lifetime.

`Max-Age=0` or a negative value can be used to remove a cookie.

---

# 46. Practical Theme Cookie

For a non-sensitive preference:

```javascript
function saveTheme(theme) {
    document.cookie =
        `theme=${encodeURIComponent(theme)}; ` +
        `Max-Age=2592000; ` +
        `Path=/`;
}
```

This stores the theme for approximately:

```text
30 days
```

Read:

```javascript
const theme =
    getCookie("theme") ?? "light";
```

---

# 47. Practical Language Cookie

```javascript
function saveLanguage(language) {
    document.cookie =
        `language=${encodeURIComponent(language)}; ` +
        `Max-Age=2592000; ` +
        `Path=/`;
}
```

Read:

```javascript
const language =
    getCookie("language") ?? "en";
```

---

# 48. Server-Set Cookie Example

A backend can send:

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

The browser stores the cookie.

For later matching requests, the browser can send:

```http
Cookie: sessionId=abc123
```

The JavaScript application does not need direct access to the session ID when the cookie is `HttpOnly`.

---

# 49. Cookie Authentication in a Full-Stack App

A common architecture:

```text
React Frontend
      ↓
POST /auth/login
      ↓
Express Backend
      ↓
Verify credentials
      ↓
Create session/token
      ↓
Set HttpOnly Cookie
      ↓
Browser stores cookie
      ↓
React requests protected API
      ↓
Browser sends cookie
      ↓
Express verifies cookie
      ↓
Return protected data
```

This pattern is commonly used for web authentication.

---

# 50. Key Takeaways

* Cookies are small pieces of browser-managed data.
* Cookies can participate in HTTP requests.
* `document.cookie` can read non-HttpOnly cookies accessible to the current document.
* `HttpOnly` cookies cannot be read through JavaScript.
* `Secure` restricts sending to secure HTTPS connections.
* `SameSite` controls cross-site cookie behavior.
* `Path` controls URL path scope.
* `Domain` controls host scope.
* `Expires` and `Max-Age` control lifetime.
* Cookies are commonly used for authentication sessions.
* Cookies are automatically sent with applicable requests.
* Cookie-based authentication requires appropriate CORS configuration when cross-origin requests are involved.
* Cookie-based authentication should consider CSRF protections.
* `HttpOnly` helps reduce direct cookie theft through JavaScript but does not eliminate XSS risks.
* Cookies are not suitable for storing large application data.
* Never store passwords in cookies.
* Sensitive authentication cookies should be carefully configured and normally used with HTTPS.

---

# Quick Cheat Sheet

```javascript
// Set
document.cookie =
    "theme=dark; Path=/";

// Read all accessible cookies
console.log(document.cookie);

// Encode
const value =
    encodeURIComponent("Sandip Kushwaha");

// Decode
const decoded =
    decodeURIComponent(value);

// One-hour cookie
document.cookie =
    "theme=dark; Max-Age=3600; Path=/";

// Delete
document.cookie =
    "theme=; Max-Age=0; Path=/";
```

Server-side example:

```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Lax; Path=/
```

---

## Cookie Security Summary

```text
HttpOnly
    ↓
JavaScript cannot read the cookie

Secure
    ↓
Cookie sent only over HTTPS

SameSite
    ↓
Controls cross-site cookie sending

Path
    ↓
Controls URL path scope

Domain
    ↓
Controls host scope

Max-Age / Expires
    ↓
Controls cookie lifetime
```

---
