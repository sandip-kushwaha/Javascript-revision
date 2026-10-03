# JavaScript Fetch API

The **Fetch API** is a modern JavaScript API used to make HTTP requests.

It allows JavaScript to communicate with servers and APIs.

For example:

```text
Browser
   ↓
JavaScript
   ↓
Fetch API
   ↓
Backend API
   ↓
Database
```

It is commonly used in:

* React applications
* Node.js applications
* REST APIs
* CRUD applications
* Login/register systems
* Fetching products, users, news, orders, etc.

---

# 1. What is Fetch API?

The Fetch API provides the `fetch()` function for making network requests.

Basic syntax:

```javascript
fetch(url);
```

Example:

```javascript
fetch("https://api.example.com/users");
```

`fetch()` returns a **Promise**.

---

# 2. Basic GET Request

```javascript
fetch("https://api.example.com/users")
    .then((response) => response.json())
    .then((data) => {
        console.log(data);
    })
    .catch((error) => {
        console.error(error);
    });
```

Flow:

```text
fetch()
   ↓
Promise
   ↓
Response
   ↓
response.json()
   ↓
JSON data
```

---

# 3. Using `async/await`

The same request can be written more clearly using `async/await`.

```javascript
async function getUsers() {
    const response = await fetch("https://api.example.com/users");

    const data = await response.json();

    console.log(data);
}

getUsers();
```

For most application code, `async/await` is easier to read.

---

# 4. What Does `fetch()` Return?

`fetch()` returns a Promise.

```javascript
const result = fetch("https://api.example.com/users");

console.log(result);
```

The Promise eventually resolves to a `Response` object.

```text
fetch()
   ↓
Promise<Response>
```

---

# 5. The Response Object

Example:

```javascript
const response = await fetch(
    "https://api.example.com/users"
);

console.log(response);
```

The `Response` object contains information about the HTTP response.

Useful properties include:

```javascript
response.ok
response.status
response.statusText
response.headers
response.url
```

---

# 6. `response.status`

`status` gives the HTTP status code.

```javascript
const response = await fetch(
    "https://api.example.com/users"
);

console.log(response.status);
```

Examples:

```text
200 → OK
201 → Created
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
500 → Internal Server Error
```

---

# 7. `response.ok`

`response.ok` is `true` when the status is in the successful HTTP range.

Example:

```javascript
const response = await fetch(
    "https://api.example.com/users"
);

if (response.ok) {
    console.log("Request successful");
}
```

Otherwise:

```javascript
if (!response.ok) {
    console.log("Request failed");
}
```

---

# 8. Important: Fetch Does Not Reject for HTTP Errors

This is an important behavior.

A `404` or `500` response normally does **not** cause `fetch()` itself to reject.

For example:

```javascript
try {
    const response = await fetch(
        "https://api.example.com/users"
    );

    console.log("Fetch completed");
} catch (error) {
    console.error("Network error:", error);
}
```

A normal HTTP `404` response may still reach:

```javascript
console.log("Fetch completed");
```

Therefore, check:

```javascript
if (!response.ok) {
    throw new Error(`HTTP error: ${response.status}`);
}
```

---

# 9. Recommended GET Pattern

```javascript
async function getUsers() {
    try {
        const response = await fetch(
            "https://api.example.com/users"
        );

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error("Failed to fetch users:", error);
    }
}
```

This handles both:

* Network/request failures
* HTTP error responses

---

# 10. Reading JSON

Most REST APIs return JSON.

Use:

```javascript
response.json();
```

Example:

```javascript
const response = await fetch(
    "https://api.example.com/users"
);

const data = await response.json();

console.log(data);
```

`response.json()` also returns a Promise.

Therefore:

```javascript
const data = await response.json();
```

---

# 11. JSON Response Example

Suppose the server returns:

```json
{
    "name": "Sandip",
    "role": "developer"
}
```

JavaScript:

```javascript
const response = await fetch(
    "https://api.example.com/user"
);

const data = await response.json();

console.log(data.name);
console.log(data.role);
```

Output:

```text
Sandip
developer
```

---

# 12. Fetching an Array

Suppose the API returns:

```json
[
    {
        "id": 1,
        "name": "Laptop"
    },
    {
        "id": 2,
        "name": "Mouse"
    }
]
```

JavaScript:

```javascript
const response = await fetch(
    "https://api.example.com/products"
);

const products = await response.json();

products.forEach((product) => {
    console.log(product.name);
});
```

---

# 13. GET Request with Query Parameters

Suppose an API supports:

```text
/api/products?category=electronics
```

You can use `URLSearchParams`.

```javascript
const params = new URLSearchParams({
    category: "electronics",
    page: "1"
});

const response = await fetch(
    `https://api.example.com/products?${params}`
);

const data = await response.json();

console.log(data);
```

Generated URL:

```text
https://api.example.com/products?category=electronics&page=1
```

---

# 14. POST Request

`fetch()` can also send data to a server.

Example:

```javascript
const response = await fetch(
    "https://api.example.com/users",
    {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            name: "Sandip",
            email: "sandip@example.com"
        })
    }
);

const data = await response.json();

console.log(data);
```

---

# 15. Understanding the POST Options

```javascript
{
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(data)
}
```

### `method`

Specifies the HTTP method:

```javascript
method: "POST"
```

### `headers`

Provides information about the request.

```javascript
headers: {
    "Content-Type": "application/json"
}
```

### `body`

Contains the data being sent.

```javascript
body: JSON.stringify(data)
```

---

# 16. Why Use `JSON.stringify()`?

JavaScript object:

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

Convert it to JSON:

```javascript
JSON.stringify(user);
```

Result:

```json
{"name":"Sandip","age":22}
```

HTTP request bodies commonly send JSON as text.

The server can then parse it back into an object.

---

# 17. PUT Request

`PUT` is commonly used to replace or update a resource.

```javascript
const response = await fetch(
    "https://api.example.com/users/10",
    {
        method: "PUT",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            name: "Sandip",
            email: "new@example.com"
        })
    }
);

const data = await response.json();

console.log(data);
```

---

# 18. PATCH Request

`PATCH` is commonly used for partial updates.

```javascript
const response = await fetch(
    "https://api.example.com/users/10",
    {
        method: "PATCH",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            name: "Sandip"
        })
    }
);

const data = await response.json();

console.log(data);
```

Here only the `name` is being changed.

---

# 19. DELETE Request

```javascript
const response = await fetch(
    "https://api.example.com/users/10",
    {
        method: "DELETE"
    }
);

if (!response.ok) {
    throw new Error(`Delete failed: ${response.status}`);
}

console.log("User deleted");
```

Some APIs return JSON after deletion:

```javascript
const data = await response.json();
```

Others may return an empty response body.

---

# 20. Fetch CRUD Example

A simple CRUD structure:

```text
GET     /users
POST    /users
GET     /users/:id
PATCH   /users/:id
DELETE  /users/:id
```

JavaScript:

```javascript
// GET
await fetch("/users");

// POST
await fetch("/users", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(user)
});

// GET ONE
await fetch("/users/10");

// PATCH
await fetch("/users/10", {
    method: "PATCH",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        name: "Updated Name"
    })
});

// DELETE
await fetch("/users/10", {
    method: "DELETE"
});
```

---

# 21. Request Headers

Headers provide additional information about a request.

Example:

```javascript
const response = await fetch("/api/users", {
    headers: {
        "Accept": "application/json",
        "Authorization": "Bearer TOKEN"
    }
});
```

Common headers:

```text
Content-Type
Accept
Authorization
Cache-Control
```

---

# 22. `Content-Type`

When sending JSON:

```javascript
headers: {
    "Content-Type": "application/json"
}
```

This tells the server:

> The request body contains JSON data.

Example:

```javascript
await fetch("/api/users", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        name: "Sandip"
    })
});
```

---

# 23. `Accept`

`Accept` tells the server what response format the client can handle.

```javascript
headers: {
    "Accept": "application/json"
}
```

Example:

```javascript
const response = await fetch("/api/users", {
    headers: {
        "Accept": "application/json"
    }
});
```

---

# 24. Authorization Header

A token can be sent using:

```javascript
headers: {
    Authorization: `Bearer ${token}`
}
```

Example:

```javascript
const response = await fetch("/api/profile", {
    headers: {
        Authorization: `Bearer ${token}`
    }
});
```

The exact authentication mechanism depends on the backend.

---

# 25. Sending Cookies

For cross-origin requests, cookies are not automatically included unless the request credentials policy allows them.

Example:

```javascript
fetch("https://api.example.com/profile", {
    credentials: "include"
});
```

This is commonly used when authentication relies on cookies.

The server must also be configured correctly for cross-origin credentials.

---

# 26. `credentials` Options

Common values include:

```javascript
credentials: "omit"
```

Do not send credentials.

```javascript
credentials: "same-origin"
```

Send credentials for same-origin requests.

```javascript
credentials: "include"
```

Send credentials even for cross-origin requests, subject to browser security and server configuration.

Example:

```javascript
const response = await fetch("/api/profile", {
    credentials: "include"
});
```

---

# 27. Form Data

For file uploads or multipart forms, `FormData` can be used.

```javascript
const formData = new FormData();

formData.append("name", "Sandip");
formData.append("profile", file);

const response = await fetch("/api/profile", {
    method: "POST",
    body: formData
});
```

When using `FormData`, normally **do not manually set**:

```javascript
"Content-Type": "multipart/form-data"
```

The browser needs to set the correct multipart boundary automatically.

---

# 28. Handling Errors

A good Fetch request should handle errors.

```javascript
async function getProducts() {
    try {
        const response = await fetch("/api/products");

        if (!response.ok) {
            throw new Error(
                `Request failed with status ${response.status}`
            );
        }

        const products = await response.json();

        return products;
    } catch (error) {
        console.error("Failed to load products:", error);
        throw error;
    }
}
```

---

# 29. Network Error vs HTTP Error

These are different.

### Network/request failure

For example:

* DNS failure
* Connection failure
* Request blocked by certain browser policies
* Aborted request

The Fetch Promise can reject.

```javascript
try {
    const response = await fetch("/api/products");
} catch (error) {
    console.error("Network/request error:", error);
}
```

### HTTP error

For example:

```text
404
500
403
```

Fetch can still resolve with a `Response`.

Therefore:

```javascript
if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
}
```

---

# 30. Aborting a Request

You can cancel a fetch using `AbortController`.

```javascript
const controller = new AbortController();

const response = await fetch("/api/products", {
    signal: controller.signal
});
```

Cancel it with:

```javascript
controller.abort();
```

Example:

```javascript
const controller = new AbortController();

setTimeout(() => {
    controller.abort();
}, 5000);

try {
    const response = await fetch("/api/products", {
        signal: controller.signal
    });

    const data = await response.json();

    console.log(data);
} catch (error) {
    if (error.name === "AbortError") {
        console.log("Request cancelled");
    } else {
        console.error(error);
    }
}
```

---

# 31. Loading State

In a web application, you can show a loading message while waiting.

```javascript
async function loadUsers() {
    console.log("Loading...");

    try {
        const response = await fetch("/api/users");

        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }

        const users = await response.json();

        console.log(users);
    } catch (error) {
        console.error(error);
    } finally {
        console.log("Finished");
    }
}
```

---

# 32. Reusable Fetch Function

Instead of repeating error handling everywhere, create a helper.

```javascript
async function request(url, options = {}) {
    const response = await fetch(url, options);

    if (!response.ok) {
        throw new Error(`HTTP error: ${response.status}`);
    }

    return response.json();
}
```

Now:

```javascript
const users = await request("/api/users");

console.log(users);
```

---

# 33. Reusable JSON Request Helper

```javascript
async function request(url, options = {}) {
    const response = await fetch(url, {
        ...options,
        headers: {
            "Content-Type": "application/json",
            ...options.headers
        }
    });

    if (!response.ok) {
        throw new Error(`HTTP error: ${response.status}`);
    }

    return response.json();
}
```

Usage:

```javascript
const user = await request("/api/users", {
    method: "POST",
    body: JSON.stringify({
        name: "Sandip"
    })
});
```

---

# 34. Fetch with Query Parameters

Using `URLSearchParams` is safer than manually building complex query strings.

```javascript
const params = new URLSearchParams({
    search: "javascript",
    page: "2",
    limit: "10"
});

const response = await fetch(
    `/api/news?${params.toString()}`
);

const data = await response.json();
```

---

# 35. Reading Text Instead of JSON

Not every response is JSON.

For text:

```javascript
const response = await fetch("/message.txt");

const text = await response.text();

console.log(text);
```

---

# 36. Reading a Blob

For files or other binary content:

```javascript
const response = await fetch("/image.png");

const blob = await response.blob();

console.log(blob);
```

A blob can be used with APIs such as:

```javascript
URL.createObjectURL(blob);
```

---

# 37. Checking Response Content

You can inspect the response headers:

```javascript
const response = await fetch("/api/users");

console.log(response.headers.get("content-type"));
```

Example:

```javascript
const contentType = response.headers.get("content-type");

if (contentType?.includes("application/json")) {
    const data = await response.json();

    console.log(data);
}
```

---

# 38. Fetch and CORS

**CORS** stands for:

> Cross-Origin Resource Sharing

Suppose your frontend runs on:

```text
http://localhost:5173
```

and your backend runs on:

```text
http://localhost:8000
```

These are different origins.

The backend must provide appropriate CORS headers for the browser to allow the frontend to access the response.

Frontend:

```javascript
fetch("http://localhost:8000/api/users");
```

Backend CORS configuration determines whether the browser permits the response to be accessed by the frontend.

---

# 39. Fetch in a React Application

Example:

```javascript
import { useEffect, useState } from "react";

function Users() {
    const [users, setUsers] = useState([]);

    useEffect(() => {
        async function loadUsers() {
            const response = await fetch("/api/users");

            if (!response.ok) {
                throw new Error("Failed to load users");
            }

            const data = await response.json();

            setUsers(data);
        }

        loadUsers();
    }, []);

    return (
        <div>
            {users.map((user) => (
                <p key={user.id}>{user.name}</p>
            ))}
        </div>
    );
}
```

In larger applications, API calls are often separated into service/API files.

---

# 40. Fetch with Cookies in a Full-Stack Application

If authentication uses HTTP cookies:

```javascript
const response = await fetch(
    "http://localhost:8000/api/v1/auth/current-user",
    {
        credentials: "include"
    }
);
```

The backend must also allow credentialed CORS requests.

For example, a backend may need to allow the specific frontend origin rather than using a wildcard origin.

---

# 41. Fetch and Authentication

There are two common patterns.

### Token in Authorization header

```javascript
fetch("/api/profile", {
    headers: {
        Authorization: `Bearer ${token}`
    }
});
```

### Authentication using cookies

```javascript
fetch("/api/profile", {
    credentials: "include"
});
```

The correct approach depends on the backend architecture and security requirements.

---

# 42. Fetch Request Structure

A useful mental model:

```javascript
fetch(url, {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(data),
    credentials: "include"
});
```

Think of it as:

```text
URL
 ↓
Method
 ↓
Headers
 ↓
Body
 ↓
Credentials
 ↓
Server
 ↓
Response
```

---

# 43. Complete Example

```javascript
async function createUser(userData) {
    try {
        const response = await fetch(
            "https://api.example.com/users",
            {
                method: "POST",

                headers: {
                    "Content-Type": "application/json",
                    "Accept": "application/json"
                },

                body: JSON.stringify(userData)
            }
        );

        if (!response.ok) {
            throw new Error(
                `Request failed: ${response.status}`
            );
        }

        const data = await response.json();

        return data;
    } catch (error) {
        console.error("Create user failed:", error);
        throw error;
    }
}
```

Usage:

```javascript
const user = await createUser({
    name: "Sandip",
    email: "sandip@example.com"
});

console.log(user);
```

---

# 44. Important Fetch Rules

Remember these:

```text
fetch() returns a Promise
```

```text
fetch() resolves to a Response
```

```text
response.json() returns a Promise
```

```text
HTTP 404/500 does not automatically reject fetch()
```

Therefore:

```javascript
if (!response.ok) {
    throw new Error(`HTTP ${response.status}`);
}
```

For JSON:

```javascript
const data = await response.json();
```

For cookies:

```javascript
credentials: "include"
```

For cancellation:

```javascript
const controller = new AbortController();
```

---

# 45. Common Fetch Pattern

For GET requests:

```javascript
async function getData() {
    try {
        const response = await fetch("/api/data");

        if (!response.ok) {
            throw new Error(`HTTP ${response.status}`);
        }

        const data = await response.json();

        return data;
    } catch (error) {
        console.error(error);
        throw error;
    }
}
```

For POST requests:

```javascript
async function createData(data) {
    const response = await fetch("/api/data", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(data)
    });

    if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
    }

    return response.json();
}
```

---

# 46. Key Takeaways

* `fetch()` is used to make HTTP requests.
* It returns a Promise.
* The Promise resolves to a `Response`.
* Use `response.json()` to read JSON.
* Use `response.ok` to check whether the HTTP status indicates success.
* HTTP errors such as `404` and `500` do not normally reject `fetch()` by themselves.
* Use `GET` to retrieve data.
* Use `POST` to create/send data.
* Use `PUT` for full replacement-style updates.
* Use `PATCH` for partial updates.
* Use `DELETE` to remove resources.
* Use `JSON.stringify()` when sending JSON.
* Use `credentials: "include"` when appropriate for cookie-based cross-origin requests.
* Use `AbortController` to cancel requests.
* Use `FormData` for multipart form/file uploads.
* CORS is controlled by the server and enforced by browsers.
* Always handle both request failures and unsuccessful HTTP responses.

---
