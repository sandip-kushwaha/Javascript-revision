# JavaScript HTTP Requests

**HTTP** (Hypertext Transfer Protocol) is the communication protocol commonly used between clients and servers on the web.

A JavaScript application can use HTTP requests to:

* Get data
* Create data
* Update data
* Delete data
* Send form data
* Authenticate users
* Communicate with REST APIs

Basic flow:

```text
Client
  ↓
HTTP Request
  ↓
Server
  ↓
HTTP Response
  ↓
Client
```

---

# 1. What Is an HTTP Request?

An HTTP request is a message sent by a client to a server.

For example:

```text
GET /api/users
```

The browser sends a request to the server asking for users.

The server then sends a response.

---

# 2. HTTP Request Structure

An HTTP request can contain:

```text
Request
├── Method
├── URL
├── Headers
├── Body
└── Credentials
```

Example:

```javascript
fetch("/api/users", {
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

# 3. HTTP Methods

The most common HTTP methods are:

| Method | Common Purpose        |
| ------ | --------------------- |
| GET    | Read data             |
| POST   | Create data           |
| PUT    | Replace/update data   |
| PATCH  | Partially update data |
| DELETE | Delete data           |

Example API:

```text
GET     /users
POST    /users
GET     /users/10
PATCH   /users/10
DELETE  /users/10
```

---

# 4. GET Request

`GET` is commonly used to retrieve data.

```javascript
const response = await fetch("/api/users");

const users = await response.json();

console.log(users);
```

Equivalent HTTP request:

```http
GET /api/users
```

A GET request normally does not contain a request body.

---

# 5. GET Request with Query Parameters

Query parameters are commonly used for:

* Searching
* Filtering
* Sorting
* Pagination

Example:

```text
/api/users?page=1&limit=10
```

JavaScript:

```javascript
const params = new URLSearchParams({
    page: "1",
    limit: "10"
});

const response = await fetch(`/api/users?${params}`);

const data = await response.json();
```

---

# 6. Path Parameters

Path parameters identify a specific resource.

Example:

```text
/api/users/25
```

Here:

```text
25
```

can represent the user's ID.

JavaScript:

```javascript
const userId = 25;

const response = await fetch(
    `/api/users/${userId}`
);

const user = await response.json();
```

---

# 7. Query Parameters vs Path Parameters

### Path parameter

```text
/users/25
```

Used to identify a specific resource.

### Query parameter

```text
/users?page=2&limit=10
```

Used to modify or filter a request.

Example:

```text
/users/25/orders?page=1
```

Here:

```text
25 → Path parameter
page=1 → Query parameter
```

---

# 8. POST Request

`POST` is commonly used to create a new resource.

```javascript
const response = await fetch("/api/users", {
    method: "POST",

    headers: {
        "Content-Type": "application/json"
    },

    body: JSON.stringify({
        name: "Sandip",
        email: "sandip@example.com"
    })
});

const user = await response.json();

console.log(user);
```

---

# 9. PUT Request

`PUT` is commonly used when replacing a resource representation.

```javascript
const response = await fetch("/api/users/25", {
    method: "PUT",

    headers: {
        "Content-Type": "application/json"
    },

    body: JSON.stringify({
        name: "Sandip",
        email: "sandip@example.com",
        role: "developer"
    })
});
```

The exact update semantics depend on the API design.

---

# 10. PATCH Request

`PATCH` is commonly used for partial updates.

```javascript
const response = await fetch("/api/users/25", {
    method: "PATCH",

    headers: {
        "Content-Type": "application/json"
    },

    body: JSON.stringify({
        role: "admin"
    })
});
```

Only the specified field may be changed.

---

# 11. DELETE Request

`DELETE` is used to request removal of a resource.

```javascript
const response = await fetch("/api/users/25", {
    method: "DELETE"
});

if (!response.ok) {
    throw new Error(`Delete failed: ${response.status}`);
}

console.log("Deleted");
```

A successful DELETE response may contain JSON, text, or no body depending on the API.

---

# 12. HTTP Status Codes

HTTP responses contain status codes.

Common categories:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client error
5xx → Server error
```

---

# 13. Common 2xx Status Codes

### 200 OK

Request succeeded.

```text
GET /users → 200 OK
```

### 201 Created

A resource was created.

```text
POST /users → 201 Created
```

### 202 Accepted

The request was accepted for processing, but processing may not be complete yet.

### 204 No Content

Request succeeded but there is no response body.

Common example:

```text
DELETE /users/25 → 204 No Content
```

---

# 14. Common 3xx Status Codes

### 301 Moved Permanently

The resource has permanently moved.

### 302 Found

The resource is temporarily redirected.

### 304 Not Modified

The cached representation can be reused because the resource has not changed according to the request's cache validation.

For example, browser developer tools may show:

```text
304 Not Modified
```

This is not normally an application failure.

---

# 15. Common 4xx Status Codes

### 400 Bad Request

The server cannot process the request because the request is invalid.

Example:

```text
Missing required field
Invalid JSON
Invalid parameter
```

### 401 Unauthorized

Authentication is required or the provided authentication is invalid.

### 403 Forbidden

The server understood the request but refuses to allow it.

For example, a logged-in user may not have permission for an admin-only operation.

### 404 Not Found

The requested resource or route was not found.

### 409 Conflict

The request conflicts with the current state of the resource.

Example:

```text
Email already exists
```

### 422 Unprocessable Content

The request syntax may be valid, but the submitted data fails application validation.

---

# 16. Common 5xx Status Codes

### 500 Internal Server Error

The server encountered an unexpected error.

### 501 Not Implemented

The server does not support the functionality required by the request.

### 502 Bad Gateway

A gateway or proxy received an invalid response from an upstream server.

### 503 Service Unavailable

The server is temporarily unable to handle the request.

### 504 Gateway Timeout

A gateway or proxy did not receive a timely response from an upstream server.

---

# 17. HTTP Headers

Headers provide metadata about a request or response.

Example request:

```javascript
fetch("/api/users", {
    headers: {
        "Accept": "application/json"
    }
});
```

Common request headers:

```text
Accept
Content-Type
Authorization
Cookie
User-Agent
```

Common response headers:

```text
Content-Type
Content-Length
Cache-Control
Set-Cookie
Location
```

---

# 18. `Content-Type`

`Content-Type` describes the format of the message body.

For JSON:

```javascript
headers: {
    "Content-Type": "application/json"
}
```

For HTML:

```text
text/html
```

For plain text:

```text
text/plain
```

For URL-encoded form data:

```text
application/x-www-form-urlencoded
```

For multipart forms:

```text
multipart/form-data
```

---

# 19. `Accept`

`Accept` tells the server which response formats the client can handle.

```javascript
headers: {
    Accept: "application/json"
}
```

This is different from `Content-Type`.

```text
Content-Type → format being sent
Accept       → format expected in response
```

---

# 20. Authorization Header

An API can use an authorization token.

Example:

```javascript
const response = await fetch("/api/profile", {
    headers: {
        Authorization: `Bearer ${token}`
    }
});
```

The server validates the token before returning protected data.

---

# 21. Cookies

Cookies can also be used for authentication.

For same-origin requests, browser cookie behavior is generally automatic according to the cookie and request rules.

For cross-origin Fetch requests, you may need:

```javascript
fetch("https://api.example.com/profile", {
    credentials: "include"
});
```

The server must also allow credentialed cross-origin requests appropriately.

---

# 22. Request Body

Some HTTP methods can contain a request body.

Example JSON body:

```javascript
const user = {
    name: "Sandip",
    email: "sandip@example.com"
};

fetch("/api/users", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(user)
});
```

The body contains the actual data being sent.

---

# 23. JSON Request Body

JavaScript object:

```javascript
const product = {
    name: "Laptop",
    price: 85000
};
```

Convert it to JSON:

```javascript
JSON.stringify(product);
```

Then send it:

```javascript
fetch("/api/products", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(product)
});
```

---

# 24. Response Body

The server sends a response body.

For JSON:

```javascript
const data = await response.json();
```

For text:

```javascript
const text = await response.text();
```

For binary data:

```javascript
const blob = await response.blob();
```

---

# 25. HTTP Request and Response

A simplified example:

### Request

```http
POST /api/users HTTP/1.1
Content-Type: application/json

{
    "name": "Sandip"
}
```

### Response

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": 101,
    "name": "Sandip"
}
```

---

# 26. HTTP Request Lifecycle

A typical API request works like this:

```text
1. User performs an action
        ↓
2. JavaScript creates request
        ↓
3. Browser sends HTTP request
        ↓
4. Server receives request
        ↓
5. Server validates request
        ↓
6. Server performs operation
        ↓
7. Server sends HTTP response
        ↓
8. JavaScript receives response
        ↓
9. JavaScript updates UI
```

---

# 27. Example: Login Request

Frontend:

```javascript
async function login(email, password) {
    const response = await fetch("/api/auth/login", {
        method: "POST",

        headers: {
            "Content-Type": "application/json"
        },

        credentials: "include",

        body: JSON.stringify({
            email,
            password
        })
    });

    if (!response.ok) {
        throw new Error(`Login failed: ${response.status}`);
    }

    return response.json();
}
```

The backend may:

```text
Receive credentials
       ↓
Validate user
       ↓
Check password
       ↓
Create authentication state
       ↓
Send response
```

---

# 28. Example: CRUD API

A typical user API could look like:

```text
GET     /api/users
GET     /api/users/10
POST    /api/users
PATCH   /api/users/10
DELETE  /api/users/10
```

JavaScript:

```javascript
// Get all
const users = await fetch("/api/users");

// Get one
const user = await fetch("/api/users/10");

// Create
await fetch("/api/users", {
    method: "POST"
});

// Update
await fetch("/api/users/10", {
    method: "PATCH"
});

// Delete
await fetch("/api/users/10", {
    method: "DELETE"
});
```

---

# 29. Handling HTTP Errors

A reusable helper:

```javascript
async function request(url, options = {}) {
    const response = await fetch(url, options);

    if (!response.ok) {
        throw new Error(
            `HTTP ${response.status}: ${response.statusText}`
        );
    }

    return response;
}
```

Usage:

```javascript
const response = await request("/api/users");

const users = await response.json();
```

---

# 30. HTTP Method Is Not Security

Changing:

```text
GET
```

to:

```text
POST
```

does not automatically make an API secure.

Security requires appropriate measures such as:

* Authentication
* Authorization
* HTTPS
* Input validation
* Secure cookies
* CSRF protection where applicable
* Rate limiting
* Proper CORS configuration
* Secure server-side handling

---

# 31. HTTPS

HTTP can be transported over TLS using **HTTPS**.

Example:

```text
http://example.com
```

versus:

```text
https://example.com
```

HTTPS helps protect data while it travels between the client and server.

For production applications, sensitive traffic should use HTTPS.

---

# 32. HTTP vs HTTPS

| Feature                    | HTTP                  | HTTPS                     |
| -------------------------- | --------------------- | ------------------------- |
| Encryption                 | No TLS encryption     | TLS encryption            |
| Data protection in transit | No                    | Yes                       |
| Authentication of server   | No TLS authentication | Yes, through certificates |
| Typical production use     | Limited               | Standard                  |

---

# 33. CORS

**CORS** means:

> Cross-Origin Resource Sharing

Suppose:

```text
Frontend:
http://localhost:5173
```

Backend:

```text
http://localhost:8000
```

These are different origins.

A browser may block JavaScript from reading the response unless the server provides appropriate CORS permission.

Example server configuration concept:

```text
Allow origin:
http://localhost:5173
```

---

# 34. Same-Origin Policy

Browsers enforce the **Same-Origin Policy** as an important security boundary.

An origin consists of:

```text
scheme + host + port
```

Example:

```text
http://localhost:5173
```

has:

```text
scheme → http
host   → localhost
port   → 5173
```

Changing the port creates a different origin.

Therefore:

```text
http://localhost:5173
```

and:

```text
http://localhost:8000
```

are different origins.

---

# 35. Request Headers vs Response Headers

### Request headers

Sent from client to server:

```text
Client
  ↓
Request Headers
  ↓
Server
```

Examples:

```text
Authorization
Content-Type
Accept
```

### Response headers

Sent from server to client:

```text
Server
  ↓
Response Headers
  ↓
Client
```

Examples:

```text
Content-Type
Cache-Control
Set-Cookie
Location
```

---

# 36. HTTP Status Checking with Fetch

A good pattern:

```javascript
async function getUsers() {
    const response = await fetch("/api/users");

    if (!response.ok) {
        throw new Error(
            `Request failed with status ${response.status}`
        );
    }

    return response.json();
}
```

This makes HTTP failure handling explicit.

---

# 37. Multiple Requests

Independent requests can sometimes run concurrently with `Promise.all()`.

```javascript
const [usersResponse, productsResponse] =
    await Promise.all([
        fetch("/api/users"),
        fetch("/api/products")
    ]);

if (!usersResponse.ok || !productsResponse.ok) {
    throw new Error("One or more requests failed");
}

const users = await usersResponse.json();
const products = await productsResponse.json();
```

This can reduce total waiting time when the requests do not depend on each other.

---

# 38. Sequential Requests

Sometimes one request depends on another.

```javascript
const userResponse = await fetch("/api/user");

if (!userResponse.ok) {
    throw new Error("Failed to get user");
}

const user = await userResponse.json();

const ordersResponse = await fetch(
    `/api/users/${user.id}/orders`
);

if (!ordersResponse.ok) {
    throw new Error("Failed to get orders");
}

const orders = await ordersResponse.json();
```

Here the second request needs the user's ID.

---

# 39. Request Timeout

Fetch does not provide a simple `timeout` option like some HTTP client libraries.

A common approach is `AbortController`.

```javascript
async function fetchWithTimeout(url, timeout = 5000) {
    const controller = new AbortController();

    const timer = setTimeout(() => {
        controller.abort();
    }, timeout);

    try {
        return await fetch(url, {
            signal: controller.signal
        });
    } finally {
        clearTimeout(timer);
    }
}
```

Usage:

```javascript
try {
    const response = await fetchWithTimeout(
        "/api/users",
        5000
    );

    const data = await response.json();

    console.log(data);
} catch (error) {
    console.error(error);
}
```

---

# 40. HTTP Request in a Full-Stack Application

For a typical React + Express application:

```text
React Frontend
      ↓
fetch()
      ↓
HTTP Request
      ↓
Express Route
      ↓
Controller
      ↓
Database
      ↓
Controller
      ↓
HTTP Response
      ↓
React Frontend
```

Example:

```javascript
const response = await fetch(
    "http://localhost:8000/api/v1/users"
);
```

Express might handle:

```javascript
app.get("/api/v1/users", getUsers);
```

---

# 41. Request Methods in REST APIs

A common REST-style mapping is:

```text
GET     → Read
POST    → Create
PUT     → Replace
PATCH   → Partial update
DELETE  → Delete
```

Example:

```text
GET     /products
GET     /products/10

POST    /products

PUT     /products/10
PATCH   /products/10

DELETE  /products/10
```

The exact API semantics depend on how the server is designed.

---

# 42. Idempotent Requests

An operation is **idempotent** when repeating the same request has the same intended effect as making it once.

Commonly considered idempotent:

```text
GET
PUT
DELETE
```

`POST` is generally not assumed to be idempotent.

For example, repeatedly sending:

```http
POST /orders
```

may create multiple orders.

API designers can use idempotency keys when they need safe retry behavior for operations such as payments or order creation.

---

# 43. Safe HTTP Methods

HTTP methods commonly considered **safe** are:

```text
GET
HEAD
OPTIONS
```

A safe method is intended not to request a state-changing action on the server.

This does not mean the request has absolutely no side effects at the infrastructure level.

---

# 44. Request Body and GET

Avoid putting sensitive information in a GET URL.

For example, avoid:

```text
/login?password=123456
```

URLs can appear in:

* Browser history
* Logs
* Analytics
* Referrer information
* Monitoring systems

Use an appropriate HTTPS request body and authentication design instead.

---

# 45. HTTP Request Best Practices

### Check HTTP status

```javascript
if (!response.ok) {
    throw new Error("Request failed");
}
```

### Handle errors

```javascript
try {
    // request
} catch (error) {
    // handle error
}
```

### Use HTTPS

Especially for authentication and sensitive data.

### Validate server responses

Do not blindly trust external data.

### Avoid sensitive data in URLs

Use appropriate request bodies or secure authentication mechanisms.

### Use appropriate HTTP methods

Make the API's intent clear.

### Keep API URLs organized

For example:

```text
/api/v1/users
/api/v1/products
/api/v1/orders
```

---

# 46. Complete Example

```javascript
async function createProduct(productData) {
    try {
        const response = await fetch(
            "/api/v1/products",
            {
                method: "POST",

                headers: {
                    "Content-Type": "application/json",
                    "Accept": "application/json"
                },

                body: JSON.stringify(productData)
            }
        );

        if (!response.ok) {
            throw new Error(
                `HTTP ${response.status}`
            );
        }

        const product = await response.json();

        console.log("Created:", product);

        return product;
    } catch (error) {
        console.error(
            "Product creation failed:",
            error
        );

        throw error;
    }
}
```

Usage:

```javascript
await createProduct({
    name: "Laptop",
    price: 85000
});
```

---

# 47. Key Takeaways

* HTTP allows clients and servers to communicate.
* A request contains information such as method, URL, headers, and sometimes a body.
* `GET` retrieves data.
* `POST` commonly creates data.
* `PUT` commonly replaces a resource.
* `PATCH` commonly performs a partial update.
* `DELETE` requests resource deletion.
* Status codes describe the result of a request.
* `2xx` generally indicates success.
* `4xx` generally indicates a client/request problem.
* `5xx` generally indicates a server-side problem.
* Headers provide metadata.
* `Content-Type` describes the request body format.
* `Accept` describes acceptable response formats.
* Path parameters identify resources.
* Query parameters filter or modify requests.
* HTTPS protects HTTP traffic with TLS.
* CORS controls browser access to cross-origin responses.
* Fetch does not automatically reject because of HTTP `4xx` or `5xx` status codes.
* Always check `response.ok` when appropriate.
* Use `AbortController` when you need cancellation or time limits.

---
