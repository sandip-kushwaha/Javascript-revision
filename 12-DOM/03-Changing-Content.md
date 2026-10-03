# JavaScript DOM Changing Content

JavaScript can change the content of HTML elements after the page has loaded.

The most commonly used properties are:

* `textContent`
* `innerHTML`
* `innerText`

These properties look similar, but they behave differently.

---

# 1. `textContent`

`textContent` gets or changes the text content of an element.

HTML:

```html
<h1 id="title">Hello World</h1>
```

JavaScript:

```javascript
const title = document.querySelector("#title");

console.log(title.textContent);
```

Output:

```text
Hello World
```

---

# 2. Changing Text with `textContent`

```javascript
const title = document.querySelector("#title");

title.textContent = "Welcome to JavaScript";
```

The page changes from:

```text
Hello World
```

to:

```text
Welcome to JavaScript
```

---

# 3. `textContent` Treats HTML as Text

Consider:

```javascript
const message = document.querySelector("#message");

message.textContent = "<strong>Hello</strong>";
```

The browser displays:

```text
<strong>Hello</strong>
```

It does **not** create a `<strong>` element.

This makes `textContent` useful when the value should be treated as plain text.

---

# 4. `innerHTML`

`innerHTML` gets or changes the HTML inside an element.

HTML:

```html
<div id="content">
    <p>Hello</p>
</div>
```

JavaScript:

```javascript
const content = document.querySelector("#content");

console.log(content.innerHTML);
```

The result contains the HTML inside the element.

---

# 5. Changing HTML with `innerHTML`

```javascript
const content = document.querySelector("#content");

content.innerHTML = "<strong>Hello JavaScript</strong>";
```

The browser interprets the string as HTML.

DOM structure:

```text
div
└── strong
    └── "Hello JavaScript"
```

---

# 6. `textContent` vs `innerHTML`

Consider:

```javascript
const element = document.querySelector("#message");
```

Using:

```javascript
element.textContent = "<strong>Hello</strong>";
```

produces text:

```text
<strong>Hello</strong>
```

Using:

```javascript
element.innerHTML = "<strong>Hello</strong>";
```

creates:

```html
<strong>Hello</strong>
```

So:

| Property      | Interprets HTML? |
| ------------- | ---------------- |
| `textContent` | No               |
| `innerHTML`   | Yes              |

---

# 7. Reading `textContent`

HTML:

```html
<div id="message">
    Hello
    <strong>JavaScript</strong>
</div>
```

JavaScript:

```javascript
const message = document.querySelector("#message");

console.log(message.textContent);
```

`textContent` represents the text content of the element and its descendants.

---

# 8. Reading `innerHTML`

Using the same HTML:

```html
<div id="message">
    Hello
    <strong>JavaScript</strong>
</div>
```

JavaScript:

```javascript
const message = document.querySelector("#message");

console.log(message.innerHTML);
```

This returns the HTML markup inside the element.

Conceptually:

```html
Hello
<strong>JavaScript</strong>
```

---

# 9. `innerText`

`innerText` represents the rendered text of an element.

Example:

```html
<div id="content">
    Hello
    <span>JavaScript</span>
</div>
```

JavaScript:

```javascript
const content = document.querySelector("#content");

console.log(content.innerText);
```

Unlike `textContent`, `innerText` is influenced by CSS and rendering.

For example, hidden content may not be included in `innerText`.

---

# 10. `textContent` vs `innerText`

The two are not identical.

### `textContent`

Works with the DOM text content.

```javascript
element.textContent;
```

### `innerText`

Represents rendered/visible text more closely.

```javascript
element.innerText;
```

Example:

```html
<div>
    Visible
    <span style="display: none;">Hidden</span>
</div>
```

Conceptually:

```javascript
element.textContent;
```

can include:

```text
Visible Hidden
```

while:

```javascript
element.innerText;
```

is generally based on rendered text and may return:

```text
Visible
```

`innerText` can also trigger layout calculations, so `textContent` is often preferred when rendered visibility is not relevant.

---

# 11. Changing Text Safely

Suppose you receive user input:

```javascript
const username = "Sandip";
```

You can safely insert it as text:

```javascript
const message = document.querySelector("#message");

message.textContent = `Welcome, ${username}`;
```

Result:

```text
Welcome, Sandip
```

---

# 12. User Input and `innerHTML`

Be careful with:

```javascript
message.innerHTML = userInput;
```

If `userInput` is untrusted, inserting it as HTML can create security vulnerabilities such as **Cross-Site Scripting (XSS)** depending on the context.

For plain text, use:

```javascript
message.textContent = userInput;
```

Example:

```javascript
const userInput = "<img src=x onerror=alert('XSS')>";

message.textContent = userInput;
```

The value is treated as text rather than being parsed as HTML.

---

# 13. Creating HTML with `innerHTML`

`innerHTML` can be useful when you intentionally need to create HTML.

```javascript
const list = document.querySelector("#list");

list.innerHTML = `
    <li>JavaScript</li>
    <li>React</li>
    <li>Node.js</li>
`;
```

The browser creates the corresponding DOM elements.

---

# 14. Template Literals with `innerHTML`

Template literals are useful for generating HTML strings.

```javascript
const product = {
    name: "Laptop",
    price: 85000
};

const container = document.querySelector("#product");

container.innerHTML = `
    <h2>${product.name}</h2>
    <p>Price: Rs. ${product.price}</p>
`;
```

The resulting DOM contains:

```html
<h2>Laptop</h2>
<p>Price: Rs. 85000</p>
```

Only use this pattern with properly trusted or safely escaped data.

---

# 15. Replacing Existing Content

Suppose:

```html
<div id="content">
    <h2>Old Heading</h2>
    <p>Old paragraph</p>
</div>
```

Using:

```javascript
const content = document.querySelector("#content");

content.innerHTML = "<h2>New Heading</h2>";
```

The previous children are replaced.

The result is:

```html
<div id="content">
    <h2>New Heading</h2>
</div>
```

---

# 16. `innerHTML = ""`

You can remove all child content using:

```javascript
const container = document.querySelector("#container");

container.innerHTML = "";
```

This leaves:

```html
<div id="container"></div>
```

This is sometimes useful for clearing a container before rendering new content.

---

# 17. Adding HTML Without Replacing Everything

You can use:

```javascript
element.insertAdjacentHTML();
```

Example:

```javascript
const list = document.querySelector("#list");

list.insertAdjacentHTML(
    "beforeend",
    "<li>New Item</li>"
);
```

The existing content remains, and the new HTML is inserted.

---

# 18. `insertAdjacentHTML()` Positions

It supports four main positions:

```text
beforebegin
afterbegin
beforeend
afterend
```

Example:

```javascript
element.insertAdjacentHTML(
    "beforeend",
    "<p>Hello</p>"
);
```

Meaning:

```text
element
└── existing content
└── new <p>
```

---

# 19. `beforebegin`

HTML:

```html
<div id="box">
    Content
</div>
```

JavaScript:

```javascript
box.insertAdjacentHTML(
    "beforebegin",
    "<p>Before</p>"
);
```

Result:

```html
<p>Before</p>

<div id="box">
    Content
</div>
```

---

# 20. `afterbegin`

```javascript
box.insertAdjacentHTML(
    "afterbegin",
    "<p>First Child</p>"
);
```

Result:

```html
<div id="box">
    <p>First Child</p>
    Content
</div>
```

---

# 21. `beforeend`

```javascript
box.insertAdjacentHTML(
    "beforeend",
    "<p>Last Child</p>"
);
```

Result:

```html
<div id="box">
    Content
    <p>Last Child</p>
</div>
```

---

# 22. `afterend`

```javascript
box.insertAdjacentHTML(
    "afterend",
    "<p>After</p>"
);
```

Result:

```html
<div id="box">
    Content
</div>

<p>After</p>
```

---

# 23. Using `createElement()` Instead

Instead of creating an HTML string, you can create DOM elements directly.

```javascript
const paragraph = document.createElement("p");

paragraph.textContent = "Hello JavaScript";

document.body.appendChild(paragraph);
```

This creates:

```html
<p>Hello JavaScript</p>
```

---

# 24. `textContent` vs `createElement()`

For plain text:

```javascript
const paragraph = document.createElement("p");

paragraph.textContent = "Hello";

container.appendChild(paragraph);
```

This is useful when you want to create DOM elements without constructing an HTML string.

---

# 25. Updating Content from an Object

A common real-world pattern is rendering data.

```javascript
const user = {
    name: "Sandip",
    role: "Developer"
};

const nameElement = document.querySelector("#name");
const roleElement = document.querySelector("#role");

nameElement.textContent = user.name;
roleElement.textContent = user.role;
```

HTML:

```html
<h2 id="name"></h2>
<p id="role"></p>
```

The page becomes:

```text
Sandip
Developer
```

---

# 26. Updating a List

HTML:

```html
<ul id="skills"></ul>
```

JavaScript:

```javascript
const skills = [
    "JavaScript",
    "React",
    "Node.js"
];

const list = document.querySelector("#skills");

skills.forEach((skill) => {
    const item = document.createElement("li");

    item.textContent = skill;

    list.appendChild(item);
});
```

Result:

```html
<ul id="skills">
    <li>JavaScript</li>
    <li>React</li>
    <li>Node.js</li>
</ul>
```

This approach avoids treating the skill names as HTML.

---

# 27. Clearing Before Rendering

Suppose the list may already contain content.

You can clear it first:

```javascript
list.textContent = "";
```

Then add new elements:

```javascript
skills.forEach((skill) => {
    const item = document.createElement("li");

    item.textContent = skill;

    list.appendChild(item);
});
```

This avoids leaving old content behind.

---

# 28. Changing Content on a Button Click

HTML:

```html
<h1 id="title">Original Title</h1>

<button id="changeBtn">
    Change
</button>
```

JavaScript:

```javascript
const title = document.querySelector("#title");
const button = document.querySelector("#changeBtn");

button.addEventListener("click", () => {
    title.textContent = "Updated Title";
});
```

The DOM changes when the user clicks the button.

---

# 29. Dynamic Content Example

HTML:

```html
<div id="product"></div>
```

JavaScript:

```javascript
const product = {
    name: "Mechanical Keyboard",
    price: 4500
};

const container = document.querySelector("#product");

const name = document.createElement("h2");
name.textContent = product.name;

const price = document.createElement("p");
price.textContent = `Rs. ${product.price}`;

container.append(name, price);
```

Result:

```text
Mechanical Keyboard
Rs. 4500
```

---

# 30. `append()` vs `appendChild()`

Both can add content to an element.

### `appendChild()`

Adds a Node.

```javascript
container.appendChild(paragraph);
```

### `append()`

Can add nodes and strings.

```javascript
container.append(
    paragraph,
    "Additional text"
);
```

For DOM manipulation, both can be useful.

---

# 31. Replacing Text vs Replacing HTML

Use:

```javascript
element.textContent = "Hello";
```

when you need plain text.

Use:

```javascript
element.innerHTML = "<strong>Hello</strong>";
```

when you intentionally need HTML markup.

Use:

```javascript
element.appendChild(child);
```

or:

```javascript
element.append(child);
```

when building DOM elements programmatically.

---

# 32. Practical Comparison

| Method                 | Main Purpose                       |
| ---------------------- | ---------------------------------- |
| `textContent`          | Read/write text                    |
| `innerText`            | Work with rendered text            |
| `innerHTML`            | Read/write HTML markup             |
| `createElement()`      | Create DOM elements                |
| `appendChild()`        | Add a DOM node                     |
| `append()`             | Add nodes or strings               |
| `insertAdjacentHTML()` | Insert HTML at a specific position |

---

# 33. Common Mistakes

### Mistake 1: Using `innerHTML` for untrusted text

Avoid:

```javascript
element.innerHTML = userInput;
```

Prefer:

```javascript
element.textContent = userInput;
```

when HTML is not required.

---

### Mistake 2: Thinking `textContent` creates HTML

```javascript
element.textContent = "<b>Hello</b>";
```

This creates text, not a `<b>` element.

---

### Mistake 3: Forgetting that `innerHTML` replaces children

```javascript
element.innerHTML = "<p>New</p>";
```

Existing child elements inside `element` are replaced.

---

### Mistake 4: Re-rendering without clearing old content

If you repeatedly append items without clearing or updating existing nodes, duplicate content can appear.

---

# 34. Key Takeaways

* `textContent` reads and changes text content.
* `innerHTML` reads and changes HTML markup.
* `innerText` works with rendered text.
* `textContent` is generally preferred for plain text.
* Be careful when inserting untrusted data with `innerHTML`.
* `createElement()` creates new DOM elements.
* `appendChild()` adds a node.
* `append()` can add nodes or strings.
* `insertAdjacentHTML()` inserts HTML without replacing the entire element.
* Setting `innerHTML` replaces the element's existing child content.
* Dynamic content is commonly created from JavaScript data.

> **Use `textContent` for text, `innerHTML` when you intentionally need HTML, and DOM creation methods when building elements programmatically.**

---

## Related Topics

* [DOM Introduction](./01-DOM-Introduction.md)
* [Selecting Elements](./02-Selecting-Elements.md)
* [Changing Styles](./04-Changing-Styles.md)
* [Creating Elements](./05-Creating-Elements.md)
* [Removing Elements](./06-Removing-Elements.md)
* [DOM Traversal](./07-DOM-Traversal.md)
* [Events](../13-Events/01-Events.md)
