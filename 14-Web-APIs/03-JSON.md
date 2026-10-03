# JavaScript JSON

**JSON** stands for **JavaScript Object Notation**.

It is a lightweight text format commonly used to exchange data between applications.

JSON is widely used with:

* REST APIs
* Fetch API
* Node.js
* Express
* React
* Databases
* Configuration files

A common API flow is:

```text
Frontend
   ↓
HTTP Request
   ↓
Backend API
   ↓
JSON Response
   ↓
Frontend
```

---

# 1. What Is JSON?

JSON represents structured data using a text format.

Example:

```json
{
    "name": "Sandip",
    "age": 22,
    "role": "developer"
}
```

JSON looks similar to a JavaScript object, but JSON is **data represented as text**, not a JavaScript object.

---

# 2. JavaScript Object vs JSON

JavaScript object:

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

JSON:

```json
{
    "name": "Sandip",
    "age": 22
}
```

The main difference is that JSON property names must use **double quotes**.

---

# 3. JSON Data Types

JSON supports:

* String
* Number
* Boolean
* Object
* Array
* `null`

Example:

```json
{
    "name": "Sandip",
    "age": 22,
    "isStudent": true,
    "skills": ["JavaScript", "React", "Node.js"],
    "address": {
        "city": "Birgunj",
        "country": "Nepal"
    },
    "phone": null
}
```

---

# 4. JSON Strings

JSON strings must use double quotes.

Correct:

```json
{
    "name": "Sandip"
}
```

Incorrect:

```text
{
    'name': 'Sandip'
}
```

JSON does not use single quotes for strings.

---

# 5. JSON Numbers

Numbers do not use quotes.

Correct:

```json
{
    "age": 22,
    "price": 85000
}
```

If you write:

```json
{
    "age": "22"
}
```

`22` is a string, not a number.

---

# 6. JSON Boolean

JSON supports:

```json
true
```

and:

```json
false
```

Example:

```json
{
    "isActive": true,
    "isAdmin": false
}
```

Do not use:

```text
True
False
```

JSON uses lowercase:

```text
true
false
```

---

# 7. JSON `null`

`null` represents an intentional absence of a value.

Example:

```json
{
    "middleName": null
}
```

---

# 8. JSON Arrays

Arrays use square brackets:

```json
[
    "JavaScript",
    "React",
    "Node.js"
]
```

An object can contain an array:

```json
{
    "name": "Sandip",
    "skills": [
        "JavaScript",
        "React",
        "Node.js"
    ]
}
```

---

# 9. JSON Objects

Objects use curly braces:

```json
{
    "name": "Sandip",
    "role": "developer"
}
```

Objects contain key-value pairs.

```text
key → value
```

Example:

```text
name → "Sandip"
role → "developer"
```

---

# 10. Nested JSON Objects

JSON objects can contain other objects.

```json
{
    "name": "Sandip",
    "address": {
        "city": "Birgunj",
        "country": "Nepal"
    }
}
```

Accessing the equivalent JavaScript object:

```javascript
console.log(user.address.city);
```

---

# 11. JSON Arrays of Objects

This is very common in APIs.

```json
[
    {
        "id": 1,
        "name": "Laptop",
        "price": 85000
    },
    {
        "id": 2,
        "name": "Mouse",
        "price": 1200
    }
]
```

JavaScript:

```javascript
products.forEach((product) => {
    console.log(product.name);
});
```

---

# 12. `JSON.stringify()`

`JSON.stringify()` converts a JavaScript value into a JSON string.

Example:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

const json = JSON.stringify(user);

console.log(json);
```

Output:

```text
{"name":"Sandip","age":22}
```

The result is a string.

```javascript
console.log(typeof json);
```

Output:

```text
string
```

---

# 13. Why Use `JSON.stringify()`?

When sending JSON through an HTTP request, you commonly convert a JavaScript object into a JSON string.

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

---

# 14. `JSON.parse()`

`JSON.parse()` converts a valid JSON string into a JavaScript value.

Example:

```javascript
const json = '{"name":"Sandip","age":22}';

const user = JSON.parse(json);

console.log(user.name);
```

Output:

```text
Sandip
```

---

# 15. `JSON.stringify()` vs `JSON.parse()`

| Method             | Converts                       |
| ------------------ | ------------------------------ |
| `JSON.stringify()` | JavaScript value → JSON string |
| `JSON.parse()`     | JSON string → JavaScript value |

Remember:

```text
Object
  ↓
JSON.stringify()
  ↓
JSON string
```

And:

```text
JSON string
  ↓
JSON.parse()
  ↓
JavaScript value
```

---

# 16. Parsing API Response

Fetch provides methods such as:

```javascript
response.json()
```

Example:

```javascript
const response = await fetch("/api/users");

const users = await response.json();

console.log(users);
```

`response.json()` reads the response body and parses JSON.

---

# 17. Sending JSON with Fetch

```javascript
const user = {
    name: "Sandip",
    email: "sandip@example.com"
};

const response = await fetch("/api/users", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify(user)
});
```

The important part is:

```javascript
body: JSON.stringify(user)
```

---

# 18. JSON Parsing Errors

Invalid JSON can cause `JSON.parse()` to throw an error.

Example:

```javascript
const data = '{"name":"Sandip"';

JSON.parse(data);
```

The JSON is incomplete.

Use `try...catch` when parsing data that may be invalid:

```javascript
try {
    const data = JSON.parse(input);

    console.log(data);
} catch (error) {
    console.error("Invalid JSON:", error);
}
```

---

# 19. JSON.stringify() with Arrays

```javascript
const skills = [
    "JavaScript",
    "React",
    "Node.js"
];

const json = JSON.stringify(skills);

console.log(json);
```

Output:

```json
["JavaScript","React","Node.js"]
```

---

# 20. JSON.parse() with Arrays

```javascript
const json = '["JavaScript","React","Node.js"]';

const skills = JSON.parse(json);

console.log(skills[0]);
```

Output:

```text
JavaScript
```

---

# 21. Formatting JSON

By default:

```javascript
const user = {
    name: "Sandip",
    age: 22
};

console.log(JSON.stringify(user));
```

Output:

```text
{"name":"Sandip","age":22}
```

You can format it using the third argument:

```javascript
console.log(
    JSON.stringify(user, null, 2)
);
```

Output:

```json
{
  "name": "Sandip",
  "age": 22
}
```

`2` means two spaces for indentation.

---

# 22. JSON.stringify() with Replacer

`JSON.stringify()` can accept a replacer.

Example:

```javascript
const user = {
    name: "Sandip",
    age: 22,
    password: "secret"
};

const json = JSON.stringify(
    user,
    ["name", "age"]
);

console.log(json);
```

Output:

```json
{"name":"Sandip","age":22}
```

The `password` property is excluded.

---

# 23. JSON.stringify() with a Function Replacer

You can also provide a function.

```javascript
const user = {
    name: "Sandip",
    age: 22
};

const json = JSON.stringify(
    user,
    (key, value) => {
        if (key === "age") {
            return undefined;
        }

        return value;
    }
);

console.log(json);
```

The `age` property is omitted.

---

# 24. JSON.stringify() and Undefined

Consider:

```javascript
const user = {
    name: "Sandip",
    age: undefined
};

console.log(JSON.stringify(user));
```

Result:

```json
{
    "name": "Sandip"
}
```

An object property whose value is `undefined` is omitted.

For arrays, `undefined` elements are represented as `null`:

```javascript
const values = [1, undefined, 3];

console.log(JSON.stringify(values));
```

Result:

```json
[1,null,3]
```

---

# 25. JSON.stringify() and Functions

Functions are not represented in JSON.

```javascript
const user = {
    name: "Sandip",
    greet() {
        console.log("Hello");
    }
};

console.log(JSON.stringify(user));
```

The function property is omitted.

---

# 26. JSON and Date

JavaScript `Date` objects are converted to strings by `JSON.stringify()`.

```javascript
const data = {
    createdAt: new Date()
};

console.log(JSON.stringify(data));
```

The date is represented as an ISO-style string.

Example:

```text
2026-10-02T07:25:00.000Z
```

When parsed again:

```javascript
const data = JSON.parse(json);
```

the date value is a **string**, not automatically a JavaScript `Date` object.

You can create a Date manually:

```javascript
const date = new Date(data.createdAt);
```

---

# 27. JSON and BigInt

`BigInt` cannot normally be directly serialized using `JSON.stringify()`.

Example:

```javascript
const data = {
    value: 123n
};

JSON.stringify(data);
```

This throws an error.

Convert it to an appropriate representation first:

```javascript
const data = {
    value: "123"
};
```

The correct representation depends on the API's requirements.

---

# 28. JSON and `NaN`

JSON does not have a separate `NaN` value.

When stringified:

```javascript
const data = {
    value: NaN
};

console.log(JSON.stringify(data));
```

It becomes:

```json
{
    "value": null
}
```

The same JSON limitation applies to `Infinity` and `-Infinity`.

---

# 29. JSON Object Property Names

JSON object property names must be strings.

Correct:

```json
{
    "name": "Sandip"
}
```

They must use double quotes.

JavaScript allows unquoted property names in many object literals:

```javascript
const user = {
    name: "Sandip"
};
```

But that syntax is not valid JSON.

---

# 30. JSON Does Not Support Comments

This is invalid JSON:

```json
{
    "name": "Sandip",
    // User name
    "age": 22
}
```

Standard JSON does not support comments.

---

# 31. JSON Does Not Support Trailing Commas

Invalid:

```json
{
    "name": "Sandip",
    "age": 22,
}
```

Correct:

```json
{
    "name": "Sandip",
    "age": 22
}
```

---

# 32. JSON File

JSON is also commonly stored in `.json` files.

Example:

```text
package.json
```

Example content:

```json
{
    "name": "my-project",
    "version": "1.0.0",
    "description": "JavaScript project"
}
```

---

# 33. Reading JSON in JavaScript

In a browser application, JSON can be loaded using Fetch:

```javascript
const response = await fetch("./data.json");

const data = await response.json();

console.log(data);
```

---

# 34. JSON in Node.js

Node.js applications commonly work with JSON files and JSON APIs.

For example, `package.json` contains project metadata:

```json
{
    "name": "hotel-management",
    "version": "1.0.0"
}
```

Node.js also provides APIs for reading and writing files containing JSON.

---

# 35. JSON in REST APIs

A REST API commonly returns:

```json
{
    "success": true,
    "data": {
        "id": 101,
        "name": "Sandip"
    }
}
```

The frontend can process it:

```javascript
const response = await fetch("/api/user");

const result = await response.json();

console.log(result.data.name);
```

---

# 36. API Response with Array

A backend may return:

```json
{
    "success": true,
    "data": [
        {
            "id": 1,
            "name": "Laptop"
        },
        {
            "id": 2,
            "name": "Mouse"
        }
    ]
}
```

JavaScript:

```javascript
const response = await fetch("/api/products");

const result = await response.json();

result.data.forEach((product) => {
    console.log(product.name);
});
```

---

# 37. JSON Response with Pagination

A common API response can look like:

```json
{
    "success": true,
    "data": [
        {
            "id": 1,
            "title": "News One"
        }
    ],
    "pagination": {
        "page": 1,
        "limit": 10,
        "total": 50,
        "totalPages": 5
    }
}
```

JavaScript:

```javascript
const response = await fetch("/api/news?page=1&limit=10");

const result = await response.json();

console.log(result.data);
console.log(result.pagination.totalPages);
```

---

# 38. JSON and LocalStorage

`localStorage` stores strings.

Therefore, objects need JSON conversion.

Store:

```javascript
const user = {
    name: "Sandip",
    role: "developer"
};

localStorage.setItem(
    "user",
    JSON.stringify(user)
);
```

Read:

```javascript
const user = JSON.parse(
    localStorage.getItem("user")
);

console.log(user.name);
```

---

# 39. Handling Missing LocalStorage Data

This can return `null`:

```javascript
localStorage.getItem("user");
```

Therefore:

```javascript
const storedUser = localStorage.getItem("user");

const user = storedUser
    ? JSON.parse(storedUser)
    : null;
```

---

# 40. JSON and Deep Copy

For simple JSON-compatible data, this pattern can create a deep copy:

```javascript
const copy = JSON.parse(
    JSON.stringify(original)
);
```

Example:

```javascript
const user = {
    name: "Sandip",
    address: {
        city: "Birgunj"
    }
};

const copy = JSON.parse(
    JSON.stringify(user)
);
```

However, this approach has limitations.

It does not correctly preserve values such as:

* `Date`
* `Map`
* `Set`
* `BigInt`
* `undefined`
* Functions
* `NaN` and Infinity in their original form

For general deep cloning, modern JavaScript also provides:

```javascript
structuredClone(value);
```

---

# 41. JSON Security

Never assume JSON received from an external source is trustworthy.

Example:

```javascript
const response = await fetch("/api/data");

const data = await response.json();
```

The data should still be validated before being used in sensitive operations.

Also avoid using:

```javascript
eval()
```

to parse JSON.

Use:

```javascript
JSON.parse()
```

instead.

---

# 42. JSON vs JavaScript Object

| Feature       | JavaScript Object     | JSON                   |
| ------------- | --------------------- | ---------------------- |
| Purpose       | Program data          | Data exchange/storage  |
| String quotes | Single/double allowed | Double quotes          |
| Functions     | Can contain           | Not supported          |
| `undefined`   | Supported             | Not supported          |
| Comments      | Possible in JS source | Not supported          |
| `Date`        | Supported             | Represented as string  |
| `BigInt`      | Supported             | Not directly supported |
| Methods       | Can contain           | Not supported          |

---

# 43. JSON.stringify() Flow

```text
JavaScript Object
       ↓
JSON.stringify()
       ↓
JSON String
       ↓
HTTP / Storage / File
```

Example:

```javascript
const user = {
    name: "Sandip"
};

const json = JSON.stringify(user);
```

---

# 44. JSON.parse() Flow

```text
JSON String
    ↓
JSON.parse()
    ↓
JavaScript Object
```

Example:

```javascript
const json = '{"name":"Sandip"}';

const user = JSON.parse(json);
```

---

# 45. Complete API Example

Suppose the server returns:

```json
{
    "success": true,
    "user": {
        "id": 101,
        "name": "Sandip",
        "role": "developer"
    }
}
```

Fetch it:

```javascript
async function getUser() {
    const response = await fetch("/api/user");

    if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
    }

    const result = await response.json();

    console.log(result.success);
    console.log(result.user.name);
    console.log(result.user.role);
}
```

---

# 46. Complete POST Example

```javascript
async function createUser(userData) {
    const response = await fetch("/api/users", {
        method: "POST",

        headers: {
            "Content-Type": "application/json",
            "Accept": "application/json"
        },

        body: JSON.stringify(userData)
    });

    if (!response.ok) {
        throw new Error(`HTTP ${response.status}`);
    }

    return response.json();
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

# 47. Common JSON Mistakes

### Mistake 1: Single quotes

Wrong:

```json
{
    'name': 'Sandip'
}
```

Correct:

```json
{
    "name": "Sandip"
}
```

---

### Mistake 2: Trailing comma

Wrong:

```json
{
    "name": "Sandip",
}
```

Correct:

```json
{
    "name": "Sandip"
}
```

---

### Mistake 3: Comments

Wrong:

```json
{
    "name": "Sandip",
    // name
    "age": 22
}
```

JSON does not support comments.

---

### Mistake 4: Treating JSON as an object

This is a string:

```javascript
const json = '{"name":"Sandip"}';
```

To access the property:

```javascript
const user = JSON.parse(json);

console.log(user.name);
```

---

### Mistake 5: Forgetting `JSON.stringify()`

When sending JSON:

```javascript
body: JSON.stringify(user)
```

not:

```javascript
body: user
```

unless the API or body type specifically expects something else.

---

# 48. Key Takeaways

* JSON means **JavaScript Object Notation**.
* JSON is a text-based data format.
* JSON is commonly used for API communication.
* JSON supports strings, numbers, booleans, objects, arrays, and `null`.
* JSON strings use double quotes.
* JSON does not support comments.
* JSON does not support trailing commas.
* `JSON.stringify()` converts JavaScript values into JSON strings.
* `JSON.parse()` converts JSON strings into JavaScript values.
* `response.json()` reads and parses a JSON response body.
* JSON does not support functions or `undefined` as data values.
* `Date` values are serialized as strings.
* `BigInt` cannot normally be directly serialized as JSON.
* JSON is commonly used with Fetch API and REST APIs.
* JSON can also be stored in `localStorage`, but `localStorage` stores strings.
* Never use `eval()` to parse JSON.
* Validate external JSON data before trusting it in sensitive application logic.

---
