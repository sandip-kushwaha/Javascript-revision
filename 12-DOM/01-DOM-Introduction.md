# JavaScript DOM Introduction

## 1. What is the DOM?

**DOM** stands for **Document Object Model**.

The DOM is a programming interface that represents an HTML document as a **tree of objects**.

JavaScript can use the DOM to:

* Find HTML elements
* Change text
* Change HTML
* Change styles
* Create elements
* Remove elements
* Handle events
* Modify attributes
* Traverse the document

Example HTML:

```html
<h1>Hello</h1>
<p>Welcome to my website.</p>
```

The browser creates a DOM representation of this document.

```text
Document
│
└── html
    ├── head
    └── body
        ├── h1
        │   └── "Hello"
        │
        └── p
            └── "Welcome to my website."
```

JavaScript can interact with these DOM objects.

---

# 2. HTML vs DOM

HTML is the document structure written in markup.

```html
<h1>Hello</h1>
```

The browser parses the HTML and creates a DOM representation.

JavaScript then interacts with that representation.

```javascript
const heading = document.querySelector("h1");

console.log(heading);
```

So the basic relationship is:

```text
HTML
 ↓
Browser parses HTML
 ↓
DOM
 ↓
JavaScript interacts with DOM
 ↓
Web page changes
```

---

# 3. The `document` Object

The global `document` object represents the loaded HTML document.

Example:

```javascript
console.log(document);
```

You can use `document` to access elements and information about the page.

For example:

```javascript
console.log(document.title);
```

To change the page title:

```javascript
document.title = "My Website";
```

---

# 4. DOM Tree

The DOM is organized as a tree.

Consider:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>My Page</title>
    </head>

    <body>
        <h1>Hello</h1>

        <p>Welcome</p>
    </body>
</html>
```

A simplified DOM tree looks like:

```text
Document
│
└── html
    ├── head
    │   └── title
    │       └── "My Page"
    │
    └── body
        ├── h1
        │   └── "Hello"
        │
        └── p
            └── "Welcome"
```

Each part is represented as a node.

---

# 5. What is a Node?

A **node** is an item in the DOM tree.

Common node types include:

* Document node
* Element node
* Text node
* Comment node

For example:

```html
<p>Hello</p>
```

The DOM contains:

```text
Element Node
    ↓
   <p>
    ↓
Text Node
    ↓
  Hello
```

---

# 6. Element Nodes

HTML elements become element nodes.

Example:

```html
<div>Hello</div>
```

The `<div>` is an element node.

JavaScript:

```javascript
const div = document.querySelector("div");

console.log(div);
```

---

# 7. Text Nodes

The text inside an element can be represented as a text node.

Example:

```html
<h1>Hello World</h1>
```

Conceptually:

```text
h1
└── "Hello World"
```

You can access text through properties such as:

```javascript
const heading = document.querySelector("h1");

console.log(heading.textContent);
```

---

# 8. Parent and Child

DOM elements can have parent-child relationships.

HTML:

```html
<div>
    <p>Hello</p>
</div>
```

Relationship:

```text
div
└── p
```

Here:

* `div` is the parent.
* `p` is the child.

JavaScript:

```javascript
const paragraph = document.querySelector("p");

console.log(paragraph.parentElement);
```

---

# 9. Siblings

Elements at the same level are siblings.

Example:

```html
<div>
    <p>One</p>
    <p>Two</p>
    <p>Three</p>
</div>
```

DOM structure:

```text
div
├── p
├── p
└── p
```

The three `<p>` elements are siblings.

---

# 10. Accessing the Root Document

You can access the main HTML element:

```javascript
console.log(document.documentElement);
```

This usually represents:

```html
<html>
```

You can access the body:

```javascript
console.log(document.body);
```

And the head:

```javascript
console.log(document.head);
```

---

# 11. DOM and JavaScript

JavaScript can modify the DOM.

Example:

```html
<h1 id="title">Old Title</h1>
```

JavaScript:

```javascript
const title = document.querySelector("#title");

title.textContent = "New Title";
```

The page changes from:

```text
Old Title
```

to:

```text
New Title
```

The HTML source file itself is not necessarily rewritten; JavaScript changes the current DOM in memory.

---

# 12. Selecting an Element

One of the most common DOM operations is selecting an element.

HTML:

```html
<h1 id="title">Hello</h1>
```

JavaScript:

```javascript
const title = document.getElementById("title");
```

Another approach:

```javascript
const title = document.querySelector("#title");
```

After selecting the element, you can work with it.

```javascript
title.textContent = "Welcome";
```

---

# 13. Changing Text

Example:

```html
<p id="message">Old message</p>
```

JavaScript:

```javascript
const message = document.querySelector("#message");

message.textContent = "New message";
```

Result:

```text
New message
```

`textContent` is useful when you want to work with text rather than HTML markup.

---

# 14. Changing HTML

You can use `innerHTML` to read or replace HTML inside an element.

Example:

```html
<div id="content"></div>
```

JavaScript:

```javascript
const content = document.querySelector("#content");

content.innerHTML = "<strong>Hello</strong>";
```

The DOM becomes conceptually:

```text
div
└── strong
    └── "Hello"
```

The `<strong>` element is interpreted as HTML.

---

# 15. `textContent` vs `innerHTML`

### `textContent`

Treats the assigned value as text.

```javascript
element.textContent = "<strong>Hello</strong>";
```

Displayed content:

```text
<strong>Hello</strong>
```

### `innerHTML`

Treats the assigned value as HTML.

```javascript
element.innerHTML = "<strong>Hello</strong>";
```

Displayed content:

```text
Hello
```

with a `<strong>` element around it.

---

# 16. Why `innerHTML` Needs Care

Avoid inserting untrusted user input directly into `innerHTML`.

For example:

```javascript
element.innerHTML = userInput;
```

If `userInput` contains malicious HTML or script-related markup, it can create security problems such as **Cross-Site Scripting (XSS)** depending on the context.

For plain text, prefer:

```javascript
element.textContent = userInput;
```

Example:

```javascript
const message = document.querySelector("#message");

message.textContent = userInput;
```

This treats the input as text.

---

# 17. DOM Attributes

HTML elements can have attributes.

Example:

```html
<img
    id="profile"
    src="profile.jpg"
    alt="Profile picture"
>
```

JavaScript can access attributes.

```javascript
const image = document.querySelector("#profile");

console.log(image.getAttribute("src"));
```

Output:

```text
profile.jpg
```

---

# 18. Changing an Attribute

You can use:

```javascript
element.setAttribute(name, value);
```

Example:

```javascript
const image = document.querySelector("#profile");

image.setAttribute("alt", "User profile");
```

You can also modify common properties directly:

```javascript
image.src = "new-profile.jpg";
```

---

# 19. Checking an Attribute

Use:

```javascript
element.hasAttribute("disabled");
```

Example:

```javascript
const button = document.querySelector("button");

if (button.hasAttribute("disabled")) {
    console.log("Button is disabled");
}
```

---

# 20. Removing an Attribute

Use:

```javascript
element.removeAttribute("disabled");
```

Example:

```javascript
const button = document.querySelector("button");

button.removeAttribute("disabled");
```

---

# 21. DOM Styles

JavaScript can change inline styles.

HTML:

```html
<p id="message">Hello</p>
```

JavaScript:

```javascript
const message = document.querySelector("#message");

message.style.fontSize = "24px";
message.style.fontWeight = "bold";
```

The browser applies these styles to the element.

---

# 22. Classes

A better approach for larger styling changes is usually to work with CSS classes.

HTML:

```html
<p id="message">Hello</p>
```

CSS:

```css
.highlight {
    font-weight: bold;
    text-decoration: underline;
}
```

JavaScript:

```javascript
const message = document.querySelector("#message");

message.classList.add("highlight");
```

---

# 23. `classList`

The `classList` property provides methods for working with classes.

### Add

```javascript
element.classList.add("active");
```

### Remove

```javascript
element.classList.remove("active");
```

### Toggle

```javascript
element.classList.toggle("active");
```

### Check

```javascript
element.classList.contains("active");
```

Example:

```javascript
const menu = document.querySelector(".menu");

menu.classList.add("open");

console.log(menu.classList.contains("open"));
```

Output:

```text
true
```

---

# 24. Creating an Element

JavaScript can create new DOM elements.

```javascript
const paragraph = document.createElement("p");
```

Now you can configure it:

```javascript
paragraph.textContent = "New paragraph";
```

Then add it to the document.

```javascript
document.body.appendChild(paragraph);
```

---

# 25. Removing an Element

You can remove an element from the DOM.

```javascript
const message = document.querySelector("#message");

message.remove();
```

The selected element is removed from the current DOM.

---

# 26. DOM Is Live

The DOM represents the current document structure.

Suppose:

```javascript
const list = document.querySelector("#list");

const item = document.createElement("li");

item.textContent = "New Item";

list.appendChild(item);
```

The DOM is updated immediately from JavaScript's point of view, and the browser can reflect that change visually.

---

# 27. DOM Is Not the Same as HTML Source

There is an important difference between:

```text
HTML source
```

and:

```text
Current DOM
```

For example:

```javascript
document.body.appendChild(document.createElement("p"));
```

This creates a new element in the current DOM.

It does not mean your original `.html` source file has been permanently rewritten.

The browser maintains the current document representation in memory.

---

# 28. DOM Manipulation Example

HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>DOM Example</title>
</head>

<body>
    <h1 id="title">Old Title</h1>

    <button id="changeBtn">
        Change Title
    </button>

    <script src="script.js"></script>
</body>
</html>
```

JavaScript:

```javascript
const title = document.querySelector("#title");
const button = document.querySelector("#changeBtn");

button.addEventListener("click", () => {
    title.textContent = "New Title";
});
```

When the button is clicked:

```text
Old Title
     ↓
Button clicked
     ↓
JavaScript runs
     ↓
DOM changes
     ↓
New Title
```

---

# 29. DOM Workflow

A common DOM workflow is:

```text
1. Select element
       ↓
2. Read or modify data
       ↓
3. Add/remove classes
       ↓
4. Create/remove elements if needed
       ↓
5. Attach event handlers
```

Example:

```javascript
const button = document.querySelector("#save");

button.classList.add("active");

button.textContent = "Saved";
```

---

# 30. DOM APIs You Will Use Frequently

| API                           | Purpose                       |
| ----------------------------- | ----------------------------- |
| `document.querySelector()`    | Select first matching element |
| `document.querySelectorAll()` | Select all matching elements  |
| `document.getElementById()`   | Select by ID                  |
| `document.createElement()`    | Create element                |
| `element.textContent`         | Read/change text              |
| `element.innerHTML`           | Read/change HTML              |
| `element.getAttribute()`      | Read attribute                |
| `element.setAttribute()`      | Set attribute                 |
| `element.removeAttribute()`   | Remove attribute              |
| `element.hasAttribute()`      | Check attribute               |
| `element.classList`           | Manage classes                |
| `element.style`               | Modify inline styles          |
| `element.appendChild()`       | Add child                     |
| `element.remove()`            | Remove element                |
| `element.parentElement`       | Access parent element         |

---

# 31. DOM vs BOM

The **DOM** and **BOM** are related but different.

### DOM

Deals mainly with the web document.

```javascript
document.querySelector("#title");
```

### BOM

**BOM = Browser Object Model**

It provides browser-related objects such as:

```javascript
window
location
history
navigator
```

Example:

```javascript
console.log(window.innerWidth);
```

The DOM is primarily about the document, while the BOM provides access to browser/environment features.

---

# 32. DOM and React

When working with React, you normally do not manipulate most DOM elements directly.

Instead of:

```javascript
document.querySelector("#title").textContent = "Hello";
```

React commonly uses:

```jsx
function App() {
    return <h1>Hello</h1>;
}
```

React manages the DOM based on component state and rendering.

However, understanding the DOM is still important because React ultimately runs in the browser and renders to the DOM.

---

# 33. Common Mistakes

### Mistake 1: Selecting before the element exists

If JavaScript runs before an element is available:

```javascript
const title = document.querySelector("#title");
```

the result may be:

```javascript
null
```

Make sure the script runs after the required HTML exists, or use an appropriate initialization strategy.

---

### Mistake 2: Using `innerHTML` for plain text

Instead of:

```javascript
element.innerHTML = userInput;
```

prefer:

```javascript
element.textContent = userInput;
```

when HTML is not required.

---

### Mistake 3: Confusing HTML source with DOM

JavaScript modifies the current document representation.

It does not automatically rewrite your original HTML file on disk.

---

### Mistake 4: Excessive inline styles

Instead of:

```javascript
element.style.color = "red";
element.style.fontSize = "20px";
element.style.fontWeight = "bold";
```

a CSS class is often cleaner:

```javascript
element.classList.add("error");
```

---

# 34. Key Takeaways

* **DOM = Document Object Model.**
* The browser creates a DOM representation from HTML.
* The DOM is organized as a tree.
* HTML elements become DOM element nodes.
* JavaScript can read and modify the DOM.
* `document` represents the current HTML document.
* `querySelector()` is commonly used to select elements.
* `textContent` works with text.
* `innerHTML` works with HTML markup.
* `classList` manages CSS classes.
* `createElement()` creates new elements.
* `remove()` removes elements.
* Attributes can be read and modified using DOM APIs.
* DOM manipulation changes the current page representation.
* React normally manages the DOM for you, but DOM knowledge remains important.

> **The DOM is the bridge between JavaScript and the HTML document displayed in the browser.**

---

## Related Topics

* [Selecting Elements](./02-Selecting-Elements.md)
* [Changing Content](./03-Changing-Content.md)
* [Changing Styles](./04-Changing-Styles.md)
* [Creating Elements](./05-Creating-Elements.md)
* [Removing Elements](./06-Removing-Elements.md)
* [DOM Traversal](./07-DOM-Traversal.md)
* [Events](../13-Events/01-Events.md)
