# JavaScript Template Literals

**Template literals** are a modern way to create strings in JavaScript.

They use **backticks**:

```javascript
const message = `Hello JavaScript`;
```

Template literals are useful for:

* Embedding variables
* Creating dynamic strings
* Multi-line text
* Building URLs
* Creating messages
* Generating HTML strings
* Formatting data

---

# 1. Basic Syntax

Normal string:

```javascript
const message = "Hello JavaScript";
```

Template literal:

```javascript
const message = `Hello JavaScript`;
```

The important difference is the use of:

```text
`
```

instead of:

```text
" "
' '
```

---

# 2. Variable Interpolation

Template literals allow variables to be inserted directly using:

```javascript
${variable}
```

Example:

```javascript
const username = "Sandip";

const message = `Welcome, ${username}`;

console.log(message);
```

Output:

```text
Welcome, Sandip
```

This is called **string interpolation**.

---

# 3. Multiple Variables

```javascript
const product = "Laptop";
const price = 85000;

const message = `${product} costs Rs. ${price}.`;

console.log(message);
```

Output:

```text
Laptop costs Rs. 85000.
```

---

# 4. Expressions Inside Template Literals

You can put JavaScript expressions inside `${}`.

```javascript
const price = 500;
const quantity = 3;

const message = `Total: Rs. ${price * quantity}`;

console.log(message);
```

Output:

```text
Total: Rs. 1500
```

You are not limited to simple variables.

---

# 5. Function Calls

Functions can also be used inside `${}`.

```javascript
function getStatus() {
  return "Available";
}

const message = `Food status: ${getStatus()}`;

console.log(message);
```

Output:

```text
Food status: Available
```

---

# 6. Object Properties

```javascript
const user = {
  name: "Sandip",
  role: "Admin"
};

const message = `${user.name} is an ${user.role}`;

console.log(message);
```

Output:

```text
Sandip is an Admin
```

---

# 7. Array Values

```javascript
const technologies = [
  "React",
  "Node.js",
  "MongoDB"
];

const message = `Technologies: ${technologies.join(", ")}`;

console.log(message);
```

Output:

```text
Technologies: React, Node.js, MongoDB
```

---

# 8. Multi-Line Strings

Normal strings require special handling for multiple lines.

Template literals support multi-line text directly:

```javascript
const message = `Hello Sandip,
Welcome to JavaScript.
Keep learning and building projects.`;

console.log(message);
```

Output:

```text
Hello Sandip,
Welcome to JavaScript.
Keep learning and building projects.
```

---

# 9. New Lines

You can create new lines naturally:

```javascript
const address = `Sandip Kushwaha
Birgunj
Nepal`;
```

No `\n` is required.

You can still use `\n` when needed:

```javascript
const message = `Line 1\nLine 2`;
```

---

# 10. Conditional Expression

Template literals can contain conditional expressions.

```javascript
const isLoggedIn = true;

const message = `User is ${
  isLoggedIn ? "logged in" : "logged out"
}`;

console.log(message);
```

Output:

```text
User is logged in
```

---

# 11. Number Formatting

```javascript
const price = 1250;
const quantity = 4;

const message = `Total amount: Rs. ${price * quantity}`;

console.log(message);
```

Output:

```text
Total amount: Rs. 5000
```

---

# 12. Building Dynamic URLs

Template literals are useful for API URLs.

```javascript
const userId = 25;

const url = `/api/users/${userId}`;

console.log(url);
```

Output:

```text
/api/users/25
```

Another example:

```javascript
const categoryId = "food";
const url = `/api/v1/categories/${categoryId}`;
```

---

# 13. Query Strings

```javascript
const page = 2;
const limit = 10;

const url = `/api/news?page=${page}&limit=${limit}`;

console.log(url);
```

Result:

```text
/api/news?page=2&limit=10
```

---

# 14. Creating Messages Dynamically

```javascript
const customer = "Sandip";
const table = "T-05";

const message = `${customer} is sitting at table ${table}.`;

console.log(message);
```

Result:

```text
Sandip is sitting at table T-05.
```

---

# 15. Template Literals With Objects

Suppose an order contains:

```javascript
const order = {
  orderNumber: "ORD-101",
  status: "preparing",
  total: 850
};
```

You can create a readable message:

```javascript
const message = `
Order: ${order.orderNumber}
Status: ${order.status}
Total: Rs. ${order.total}
`;

console.log(message);
```

---

# 16. Template Literals With Functions

```javascript
function getGreeting(name) {
  return `Welcome, ${name}!`;
}

console.log(getGreeting("Sandip"));
```

Output:

```text
Welcome, Sandip!
```

---

# 17. Escaping Backticks

Because template literals use backticks, you need to escape a backtick if it appears inside the string.

```javascript
const message = `Use \`const\` when reassignment is not needed.`;

console.log(message);
```

Output:

```text
Use `const` when reassignment is not needed.
```

---

# 18. Quotes Inside Template Literals

You can freely use single and double quotes.

```javascript
const message = `He said "Hello" and it's fine.`;
```

This is one advantage of template literals.

---

# 19. Returning Template Literals

Functions can return formatted strings.

```javascript
function createUserMessage(name, role) {
  return `${name} has the role ${role}.`;
}

const message = createUserMessage(
  "Sandip",
  "Admin"
);

console.log(message);
```

---

# 20. Template Literals in Array Methods

Template literals work well with `map()`.

```javascript
const foods = [
  "Momo",
  "Chowmein",
  "Coffee"
];

const labels = foods.map(
  food => `Food: ${food}`
);

console.log(labels);
```

Result:

```text
[
  "Food: Momo",
  "Food: Chowmein",
  "Food: Coffee"
]
```

---

# 21. Generating HTML

Template literals can create HTML strings.

```javascript
const title = "JavaScript";
const description = "Learn modern JavaScript.";

const html = `
  <article>
    <h2>${title}</h2>
    <p>${description}</p>
  </article>
`;
```

The resulting value is a string containing HTML.

> When inserting user-controlled content into HTML, be careful about XSS. Do not blindly insert untrusted data into `innerHTML`.

---

# 22. Generating a List

```javascript
const foods = [
  "Momo",
  "Pizza",
  "Burger"
];

const html = foods
  .map(food => `<li>${food}</li>`)
  .join("");
```

This produces:

```html
<li>Momo</li>
<li>Pizza</li>
<li>Burger</li>
```

---

# 23. Template Literals in React

JSX already supports JavaScript expressions with `{}`.

But template literals are useful when creating dynamic strings.

```jsx
const userId = 25;

const profileUrl = `/users/${userId}`;
```

Another example:

```jsx
const className = `card ${isActive ? "active" : "inactive"}`;
```

---

# 24. Dynamic CSS Class Names

```javascript
const isActive = true;

const className = `button ${
  isActive ? "active" : "disabled"
}`;

console.log(className);
```

Result:

```text
button active
```

This is common in frontend development.

---

# 25. Combining Template Literals With Destructuring

```javascript
const user = {
  name: "Sandip",
  role: "Developer"
};

const {
  name,
  role
} = user;

const message = `${name} works as a ${role}.`;

console.log(message);
```

Destructuring extracts the data, while the template literal formats it.

---

# 26. Nested Expressions

Expressions inside `${}` can be more complex.

```javascript
const price = 1200;
const discount = 200;

const message = `Final price: Rs. ${price - discount}`;
```

Output:

```text
Final price: Rs. 1000
```

You can also call methods:

```javascript
const name = "sandip";

const message = `User: ${name.toUpperCase()}`;
```

Output:

```text
User: SANDIP
```

---

# 27. Empty Template Literal

```javascript
const message = ``;

console.log(message);
```

The result is an empty string.

---

# 28. Whitespace Matters

Everything outside `${}` is treated as part of the string.

For example:

```javascript
const message = `
Hello
World
`;
```

The spaces and line breaks inside the template literal are preserved.

This is useful for multi-line content but can also produce unwanted whitespace.

---

# 29. Template Literals vs Concatenation

Traditional concatenation:

```javascript
const name = "Sandip";
const age = 22;

const message =
  "Name: " + name + ", Age: " + age;
```

Template literal:

```javascript
const message =
  `Name: ${name}, Age: ${age}`;
```

Template literals are generally easier to read for dynamic strings.

---

# 30. Template Literals vs `String()`

Template literals can convert embedded values to strings:

```javascript
const age = 22;

const message = `Age: ${age}`;
```

This produces a string.

For explicit conversion, you can also use:

```javascript
const value = String(age);
```

The two approaches serve different purposes.

---

# 31. Special Characters

Template literals support normal escape sequences.

```javascript
const message = `First line\nSecond line`;
```

Output:

```text
First line
Second line
```

Common escapes include:

```text
\n  New line
\t  Tab
\\  Backslash
\`  Backtick
```

---

# 32. Tagged Template Literals

A more advanced feature is the **tagged template literal**.

Example:

```javascript
function tag(strings, name) {
  console.log(strings);
  console.log(name);
}

const name = "Sandip";

tag`Hello ${name}`;
```

The function receives the template's text and interpolated values separately.

Tagged templates are used in some libraries and advanced applications.

You do not need them for normal string formatting.

---

# 33. Important Difference

This works:

```javascript
const name = "Sandip";

const message = `Hello ${name}`;
```

This does **not** interpolate the variable:

```javascript
const message = "Hello ${name}";
```

Because `${}` interpolation works inside **template literals**, not normal quoted strings.

---

# 34. Practical API Example

```javascript
const baseURL = "https://example.com/api";
const userId = 42;

const url = `${baseURL}/users/${userId}`;

console.log(url);
```

Result:

```text
https://example.com/api/users/42
```

This pattern is common when building API requests.

---

# 35. Practical Logging Example

Instead of:

```javascript
console.log(
  "User " + name + " has order " + orderId
);
```

Use:

```javascript
console.log(
  `User ${name} has order ${orderId}`
);
```

This becomes especially useful when a message contains many dynamic values.

---

# 36. Common Mistakes

### Mistake 1: Using quotes instead of backticks

Incorrect:

```javascript
const message = "Hello ${name}";
```

Correct:

```javascript
const message = `Hello ${name}`;
```

---

### Mistake 2: Forgetting `${}`

This:

```javascript
const message = `Hello name`;
```

prints:

```text
Hello name
```

To insert the variable:

```javascript
const message = `Hello ${name}`;
```

---

### Mistake 3: Forgetting that expressions are evaluated

```javascript
const a = 10;
const b = 20;

const result = `${a + b}`;
```

The result is:

```text
30
```

not:

```text
10 + 20
```

---

### Mistake 4: Unexpected whitespace

Because template literals preserve whitespace:

```javascript
const message = `
  Hello
  Sandip
`;
```

may contain leading spaces and newlines.

Format multi-line templates carefully when whitespace matters.

---

# 37. Quick Reference

### Basic

```javascript
const message = `Hello`;
```

### Variable

```javascript
const message = `Hello ${name}`;
```

### Expression

```javascript
const message = `Total: ${price * quantity}`;
```

### Function

```javascript
const message = `Status: ${getStatus()}`;
```

### Property

```javascript
const message = `User: ${user.name}`;
```

### Multi-line

```javascript
const message = `
Line 1
Line 2
`;
```

### Dynamic URL

```javascript
const url = `/users/${userId}`;
```

### Conditional

```javascript
const text = `Status: ${active ? "Active" : "Inactive"}`;
```

---

# 38. Key Takeaways

* Template literals use backticks `` ` ``.
* `${}` is used for interpolation.
* Expressions can be placed inside `${}`.
* Function calls and object properties can be used inside `${}`.
* Template literals support multi-line strings.
* They are useful for dynamic URLs and messages.
* They work well with arrays, objects, functions, and React.
* Whitespace and line breaks inside the template are preserved.
* `${}` does not work inside normal single or double quoted strings.
* Tagged templates are an advanced feature.

## Remember

```text
Backticks  → ``
Interpolation → ${}
```

Example:

```javascript
const name = "Sandip";
const role = "Developer";

const message = `Hello ${name}, you are a ${role}.`;
```

---
