# JavaScript URL API

The **URL API** provides JavaScript interfaces for creating, reading, modifying, and working with URLs.

It is useful when working with:

* API endpoints
* Query parameters
* Search and filter pages
* Pagination
* Navigation
* Redirect URLs
* File URLs
* Browser history
* React applications
* Fetch requests

The main objects are:

```text
URL
URLSearchParams
```

---

# 1. What Is a URL?

URL means:

```text
Uniform Resource Locator
```

Example:

```text
https://example.com/products?page=2&category=phone
```

A URL can contain:

```text
Protocol
Hostname
Port
Path
Query String
Hash
```

---

# 2. URL Structure

Consider:

```text
https://example.com:8080/products/123?category=phone&page=2#details
```

Breakdown:

```text
https
  ↓
Protocol

example.com
  ↓
Hostname

8080
  ↓
Port

/products/123
  ↓
Path

?category=phone&page=2
  ↓
Query String

#details
  ↓
Hash
```

---

# 3. Creating a URL Object

Use:

```javascript
const url = new URL(
    "https://example.com/products"
);
```

Now:

```javascript
console.log(url);
```

creates a `URL` object.

---

# 4. URL Properties

Example:

```javascript
const url = new URL(
    "https://example.com:8080/products/123?category=phone#details"
);
```

You can access:

```javascript
url.href;
url.protocol;
url.hostname;
url.port;
url.host;
url.origin;
url.pathname;
url.search;
url.hash;
```

---

# 5. `href`

Returns the complete URL.

```javascript
console.log(url.href);
```

Example:

```text
https://example.com:8080/products/123?category=phone#details
```

---

# 6. `protocol`

Returns the protocol.

```javascript
console.log(url.protocol);
```

Output:

```text
https:
```

Other examples:

```text
http:
https:
```

---

# 7. `hostname`

Returns the hostname.

```javascript
console.log(url.hostname);
```

Output:

```text
example.com
```

---

# 8. `port`

Returns the port.

```javascript
console.log(url.port);
```

For:

```text
https://example.com:8080
```

result:

```text
8080
```

If the default port is being used, the property may be an empty string.

---

# 9. `host`

`host` contains:

```text
hostname + port
```

Example:

```javascript
console.log(url.host);
```

Output:

```text
example.com:8080
```

---

# 10. `origin`

`origin` contains the URL's:

```text
scheme + hostname + port
```

Example:

```javascript
console.log(url.origin);
```

Output:

```text
https://example.com:8080
```

---

# 11. `pathname`

Returns the URL path.

```javascript
console.log(url.pathname);
```

Example:

```text
/products/123
```

For an API:

```text
/api/v1/users/42
```

---

# 12. `search`

Returns the query string including `?`.

Example:

```javascript
const url = new URL(
    "https://example.com/products?page=2"
);

console.log(url.search);
```

Output:

```text
?page=2
```

---

# 13. `hash`

Returns the fragment including `#`.

```javascript
const url = new URL(
    "https://example.com/docs#installation"
);

console.log(url.hash);
```

Output:

```text
#installation
```

---

# 14. Complete URL Example

```javascript
const url = new URL(
    "https://example.com:8080/products/123?category=phone&page=2#details"
);

console.log(url.href);
console.log(url.protocol);
console.log(url.hostname);
console.log(url.port);
console.log(url.pathname);
console.log(url.search);
console.log(url.hash);
```

---

# 15. Relative URLs

A relative URL can be resolved against a base URL.

```javascript
const url = new URL(
    "/products",
    "https://example.com"
);

console.log(url.href);
```

Result:

```text
https://example.com/products
```

---

# 16. Relative Path Example

```javascript
const url = new URL(
    "../images/logo.png",
    "https://example.com/products/item/"
);

console.log(url.href);
```

The `URL` constructor resolves the relative path against the base URL.

---

# 17. `URLSearchParams`

`URLSearchParams` is used to work with query parameters.

Example URL:

```text
https://example.com/products?page=2&category=phone
```

Create:

```javascript
const params = new URLSearchParams(
    "?page=2&category=phone"
);
```

---

# 18. `get()`

Get a parameter:

```javascript
const page =
    params.get("page");

console.log(page);
```

Output:

```text
2
```

Another:

```javascript
const category =
    params.get("category");

console.log(category);
```

Output:

```text
phone
```

---

# 19. Missing Parameters

If the parameter does not exist:

```javascript
const sort =
    params.get("sort");

console.log(sort);
```

Result:

```text
null
```

---

# 20. `set()`

Set or replace a parameter:

```javascript
params.set(
    "page",
    "3"
);
```

Now:

```javascript
console.log(
    params.toString()
);
```

Result:

```text
page=3&category=phone
```

---

# 21. `append()`

`append()` adds another value for the same parameter.

```javascript
params.append(
    "category",
    "laptop"
);
```

Now the query can contain:

```text
category=phone&category=laptop
```

This is useful for multi-value parameters.

---

# 22. `delete()`

Remove a parameter:

```javascript
params.delete(
    "category"
);
```

Now:

```javascript
console.log(
    params.toString()
);
```

The `category` parameter is removed.

---

# 23. `has()`

Check whether a parameter exists:

```javascript
if (params.has("page")) {
    console.log("Page exists");
}
```

Returns:

```text
true
```

or:

```text
false
```

---

# 24. `getAll()`

When a parameter has multiple values:

```javascript
const params =
    new URLSearchParams();

params.append(
    "category",
    "phone"
);

params.append(
    "category",
    "laptop"
);
```

Use:

```javascript
console.log(
    params.getAll("category")
);
```

Result:

```javascript
[
    "phone",
    "laptop"
]
```

---

# 25. `toString()`

Convert query parameters to a query string:

```javascript
const params =
    new URLSearchParams();

params.set(
    "page",
    "2"
);

params.set(
    "limit",
    "10"
);

console.log(
    params.toString()
);
```

Output:

```text
page=2&limit=10
```

---

# 26. Building a URL

Instead of manually writing:

```javascript
const url =
    "/products?page=2&limit=10";
```

you can use:

```javascript
const url =
    new URL(
        "/products",
        "https://example.com"
    );

url.searchParams.set(
    "page",
    "2"
);

url.searchParams.set(
    "limit",
    "10"
);

console.log(url.href);
```

Result:

```text
https://example.com/products?page=2&limit=10
```

---

# 27. URL Search Params from a URL

You can access query parameters directly:

```javascript
const url = new URL(
    "https://example.com/products?page=2&limit=10"
);

console.log(
    url.searchParams.get("page")
);
```

Output:

```text
2
```

---

# 28. Updating URL Parameters

Example:

```javascript
const url = new URL(
    "https://example.com/products?page=1"
);

url.searchParams.set(
    "page",
    "2"
);

console.log(url.href);
```

Result:

```text
https://example.com/products?page=2
```

---

# 29. Removing URL Parameters

```javascript
const url = new URL(
    "https://example.com/products?page=2&sort=price"
);

url.searchParams.delete(
    "sort"
);

console.log(url.href);
```

Result:

```text
https://example.com/products?page=2
```

---

# 30. URL Encoding

URLs cannot safely contain every character directly.

For example:

```text
hello world
```

may need encoding when used as a URL component.

Use:

```javascript
encodeURIComponent(
    "hello world"
);
```

Result:

```text
hello%20world
```

Decode:

```javascript
decodeURIComponent(
    "hello%20world"
);
```

Result:

```text
hello world
```

---

# 31. URLSearchParams Encoding

`URLSearchParams` automatically handles query parameter encoding.

Example:

```javascript
const params =
    new URLSearchParams();

params.set(
    "search",
    "JavaScript tutorial"
);

console.log(
    params.toString()
);
```

Result will encode the space appropriately:

```text
search=JavaScript+tutorial
```

This makes `URLSearchParams` safer and easier than manually concatenating query strings.

---

# 32. Avoid Manual Query String Construction

Instead of:

```javascript
const url =
    `/products?search=${search}&page=${page}`;
```

use:

```javascript
const params =
    new URLSearchParams();

params.set(
    "search",
    search
);

params.set(
    "page",
    String(page)
);

const url =
    `/products?${params.toString()}`;
```

This handles encoding correctly.

---

# 33. Fetch with URLSearchParams

```javascript
const params =
    new URLSearchParams();

params.set(
    "page",
    "1"
);

params.set(
    "limit",
    "10"
);

const response = await fetch(
    `/api/products?${params.toString()}`
);

const data =
    await response.json();
```

---

# 34. API Query Parameters

For a backend API:

```text
/api/v1/products?page=1&limit=10&sort=price
```

You can build it:

```javascript
const url = new URL(
    "/api/v1/products",
    "https://api.example.com"
);

url.searchParams.set(
    "page",
    "1"
);

url.searchParams.set(
    "limit",
    "10"
);

url.searchParams.set(
    "sort",
    "price"
);

console.log(url.href);
```

---

# 35. Search Example

Suppose a search page uses:

```text
/products?search=laptop
```

Read it:

```javascript
const params =
    new URLSearchParams(
        window.location.search
    );

const search =
    params.get("search");

console.log(search);
```

---

# 36. `window.location`

The browser provides the current URL through:

```javascript
window.location
```

Useful properties:

```javascript
window.location.href;
window.location.origin;
window.location.protocol;
window.location.hostname;
window.location.port;
window.location.pathname;
window.location.search;
window.location.hash;
```

---

# 37. Current URL Example

If the current page is:

```text
https://example.com/products?page=2#details
```

then:

```javascript
console.log(
    window.location.pathname
);
```

returns:

```text
/products
```

And:

```javascript
console.log(
    window.location.search
);
```

returns:

```text
?page=2
```

And:

```javascript
console.log(
    window.location.hash
);
```

returns:

```text
#details
```

---

# 38. Create URL from Current Page

You can create a URL object from the current page:

```javascript
const url =
    new URL(window.location.href);

console.log(url);
```

Now you can safely modify it:

```javascript
url.searchParams.set(
    "page",
    "2"
);
```

---

# 39. Updating the Browser URL

You can change the current page URL using:

```javascript
window.history.pushState(
    {},
    "",
    url
);
```

Example:

```javascript
const url =
    new URL(window.location.href);

url.searchParams.set(
    "page",
    "2"
);

window.history.pushState(
    {},
    "",
    url
);
```

This changes the URL without performing a normal page reload.

---

# 40. `replaceState()`

Use:

```javascript
window.history.replaceState(
    {},
    "",
    url
);
```

Difference:

```text
pushState()
    → creates a new history entry

replaceState()
    → replaces the current history entry
```

---

# 41. Browser Navigation

Normal navigation:

```javascript
window.location.href =
    "/dashboard";
```

or:

```javascript
window.location.assign(
    "/dashboard"
);
```

Reload current page:

```javascript
window.location.reload();
```

---

# 42. `URL` vs `URLSearchParams`

### URL

Used for the complete URL:

```javascript
const url = new URL(
    "https://example.com/products?page=2"
);
```

### URLSearchParams

Used mainly for query parameters:

```javascript
const params =
    new URLSearchParams();

params.set(
    "page",
    "2"
);
```

Simple rule:

```text
URL
    → complete URL

URLSearchParams
    → query string parameters
```

---

# 43. URLSearchParams from an Object

You can initialize it from an object:

```javascript
const params =
    new URLSearchParams({
        page: "1",
        limit: "10",
        sort: "price"
    });

console.log(
    params.toString()
);
```

Result:

```text
page=1&limit=10&sort=price
```

---

# 44. URLSearchParams from an Array

You can also use entries:

```javascript
const params =
    new URLSearchParams([
        ["page", "1"],
        ["limit", "10"],
        ["sort", "price"]
    ]);
```

---

# 45. Iterating Parameters

```javascript
const params =
    new URLSearchParams(
        "page=1&limit=10"
    );

for (const [
    key,
    value
] of params) {
    console.log(key, value);
}
```

Output:

```text
page 1
limit 10
```

---

# 46. `keys()`

```javascript
for (const key of params.keys()) {
    console.log(key);
}
```

---

# 47. `values()`

```javascript
for (const value of params.values()) {
    console.log(value);
}
```

---

# 48. `entries()`

```javascript
for (const [
    key,
    value
] of params.entries()) {
    console.log(
        key,
        value
    );
}
```

---

# 49. Sorting Query Parameters

`URLSearchParams` provides:

```javascript
params.sort();
```

Example:

```javascript
const params =
    new URLSearchParams(
        "z=3&a=1&m=2"
    );

params.sort();

console.log(
    params.toString()
);
```

The parameter names are sorted.

---

# 50. Practical Search URL

A product search might use:

```text
/products?search=laptop&category=electronics&page=2&limit=20
```

Build it:

```javascript
const params =
    new URLSearchParams();

params.set(
    "search",
    "laptop"
);

params.set(
    "category",
    "electronics"
);

params.set(
    "page",
    "2"
);

params.set(
    "limit",
    "20"
);

const url =
    `/products?${params.toString()}`;

console.log(url);
```

---

# 51. Practical API URL

```javascript
function buildProductsURL({
    page = 1,
    limit = 10,
    search = "",
    category = ""
}) {
    const params =
        new URLSearchParams();

    params.set(
        "page",
        String(page)
    );

    params.set(
        "limit",
        String(limit)
    );

    if (search) {
        params.set(
            "search",
            search
        );
    }

    if (category) {
        params.set(
            "category",
            category
        );
    }

    return `/api/products?${params}`;
}
```

Usage:

```javascript
const url =
    buildProductsURL({
        page: 2,
        limit: 20,
        search: "laptop",
        category: "electronics"
    });

console.log(url);
```

---

# 52. URL API in React

React applications commonly read query parameters.

Example:

```javascript
const params =
    new URLSearchParams(
        window.location.search
    );

const page =
    params.get("page") ?? "1";

const search =
    params.get("search") ?? "";
```

This can be used to initialize:

```text
Search state
Pagination
Filters
Sorting
Tabs
```

---

# 53. URL API in Node.js

Node.js also provides the standard `URL` API.

Example:

```javascript
const url = new URL(
    "https://example.com/api/users?page=2"
);

console.log(
    url.searchParams.get("page")
);
```

Output:

```text
2
```

This is useful when processing:

* API URLs
* Request URLs
* Redirect URLs
* Query parameters

---

# 54. URL API with Express

Express applications commonly receive query parameters through:

```javascript
req.query
```

For example:

```text
GET /api/products?page=2&limit=10
```

Then:

```javascript
console.log(req.query);
```

may produce:

```javascript
{
    page: "2",
    limit: "10"
}
```

The URL API is useful when you need to construct or manipulate URLs before making requests.

---

# 55. URL API with Fetch

```javascript
const url = new URL(
    "/api/products",
    window.location.origin
);

url.searchParams.set(
    "page",
    "1"
);

url.searchParams.set(
    "limit",
    "10"
);

const response =
    await fetch(url);
```

This keeps URL construction structured.

---

# 56. URL Fragments

A fragment begins with:

```text
#
```

Example:

```text
/docs#installation
```

Read:

```javascript
const url =
    new URL(
        "https://example.com/docs#installation"
    );

console.log(url.hash);
```

Output:

```text
#installation
```

Fragments are generally handled by the browser and are not included in the HTTP request sent to the server.

---

# 57. Hash Navigation

Example:

```javascript
window.location.hash =
    "contact";
```

This changes the URL to something like:

```text
#contact
```

It can be used for page sections.

---

# 58. URL Validation

The `URL` constructor can help validate whether a string can be parsed as a URL.

```javascript
function isValidURL(value) {
    try {
        new URL(value);
        return true;
    } catch {
        return false;
    }
}
```

Usage:

```javascript
console.log(
    isValidURL("https://example.com")
);
```

Output:

```text
true
```

---

# 59. Absolute URL Validation

If you specifically require an HTTPS URL:

```javascript
function isHTTPSURL(value) {
    try {
        const url =
            new URL(value);

        return url.protocol === "https:";
    } catch {
        return false;
    }
}
```

This checks the URL format and protocol, not whether the website actually exists.

---

# 60. Key Takeaways

* `URL` represents a complete URL.
* `URLSearchParams` works with query parameters.
* `url.href` gives the complete URL.
* `url.protocol` gives the protocol.
* `url.hostname` gives the hostname.
* `url.port` gives the port.
* `url.origin` gives scheme + host + port.
* `url.pathname` gives the path.
* `url.search` gives the query string.
* `url.hash` gives the fragment.
* `url.searchParams` provides a `URLSearchParams` object.
* `get()` reads a parameter.
* `set()` creates or replaces a parameter.
* `append()` adds another value.
* `delete()` removes a parameter.
* `has()` checks whether a parameter exists.
* `getAll()` gets multiple values.
* `toString()` creates a query string.
* `URLSearchParams` handles query parameter encoding.
* Avoid manually concatenating unescaped query parameters.
* `pushState()` adds a browser history entry.
* `replaceState()` replaces the current history entry.
* URL fragments are not normally sent to the server in HTTP requests.
* The URL API works in both browsers and modern JavaScript runtimes such as Node.js.

---

# Quick Cheat Sheet

```javascript
// Create URL
const url = new URL(
    "https://example.com/products?page=2"
);

// URL properties
url.href;
url.protocol;
url.hostname;
url.port;
url.host;
url.origin;
url.pathname;
url.search;
url.hash;

// Query parameter
url.searchParams.get("page");

// Set parameter
url.searchParams.set(
    "page",
    "3"
);

// Add parameter
url.searchParams.append(
    "category",
    "phone"
);

// Delete parameter
url.searchParams.delete(
    "category"
);

// Check parameter
url.searchParams.has("page");

// Get multiple values
url.searchParams.getAll("category");

// Convert query to string
url.searchParams.toString();

// Current URL
new URL(window.location.href);

// Current query parameters
new URLSearchParams(
    window.location.search
);
```

---

## URL Flow

```text
URL
 │
 ├── Protocol
 │
 ├── Hostname
 │
 ├── Port
 │
 ├── Pathname
 │
 ├── Search
 │    │
 │    └── URLSearchParams
 │
 └── Hash
```

---
