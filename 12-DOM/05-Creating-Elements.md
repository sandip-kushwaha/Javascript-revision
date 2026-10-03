# JavaScript DOM Creating Elements

JavaScript can create new HTML elements dynamically.

This is useful when building:

* Dynamic lists
* Cards
* Notifications
* Tables
* Menus
* Comments
* Product items
* Dashboard components

The basic process is:

```text
Create element
     ↓
Add content
     ↓
Add attributes/classes
     ↓
Add element to the DOM
```

---

# 1. `document.createElement()`

The `createElement()` method creates a new HTML element.

```javascript
const heading = document.createElement("h1");
```

This creates an `<h1>` element in memory.

It is not visible on the page yet.

You must add it to the DOM.

---

# 2. Adding Text

You can use `textContent`:

```javascript
const heading = document.createElement("h1");

heading.textContent = "Hello JavaScript";
```

The element now represents:

```html
<h1>Hello JavaScript</h1>
```

---

# 3. Adding the Element to the Page

Use `append()` or `appendChild()`.

```javascript
const heading = document.createElement("h1");

heading.textContent = "Hello JavaScript";

document.body.append(heading);
```

Now the heading appears on the page.

---

# 4. `append()`

`append()` adds content at the end of an element.

```javascript
const paragraph = document.createElement("p");

paragraph.textContent = "This paragraph was created using JavaScript.";

document.body.append(paragraph);
```

You can append multiple items:

```javascript
const title = document.createElement("h2");
const text = document.createElement("p");

title.textContent = "Products";
text.textContent = "Available products";

document.body.append(title, text);
```

---

# 5. `appendChild()`

`appendChild()` also adds an element as the last child.

```javascript
const listItem = document.createElement("li");

listItem.textContent = "JavaScript";

const list = document.querySelector("ul");

list.appendChild(listItem);
```

### `append()` vs `appendChild()`

| `append()`             | `appendChild()`           |
| ---------------------- | ------------------------- |
| Can add multiple nodes | Adds one node             |
| Can add strings        | Requires a Node           |
| Modern and flexible    | Older and widely used     |
| Returns `undefined`    | Returns the appended node |

---

# 6. Creating a Complete Element

You can create an element step by step.

```javascript
const card = document.createElement("div");

card.classList.add("card");

card.textContent = "Product Card";

document.body.append(card);
```

The resulting HTML is approximately:

```html
<div class="card">Product Card</div>
```

---

# 7. Creating Nested Elements

You can create elements inside other elements.

HTML:

```html
<div id="products"></div>
```

JavaScript:

```javascript
const container = document.querySelector("#products");

const card = document.createElement("div");
const title = document.createElement("h2");
const price = document.createElement("p");

title.textContent = "Laptop";
price.textContent = "$800";

card.classList.add("card");

card.append(title, price);
container.append(card);
```

Result:

```html
<div id="products">
    <div class="card">
        <h2>Laptop</h2>
        <p>$800</p>
    </div>
</div>
```

---

# 8. `prepend()`

`prepend()` adds content at the beginning of an element.

```javascript
const list = document.querySelector("ul");

const firstItem = document.createElement("li");

firstItem.textContent = "First Item";

list.prepend(firstItem);
```

If the list originally contains:

```html
<ul>
    <li>Second Item</li>
</ul>
```

it becomes:

```html
<ul>
    <li>First Item</li>
    <li>Second Item</li>
</ul>
```

---

# 9. `before()`

`before()` inserts an element before another element.

```javascript
const title = document.querySelector("h1");

const message = document.createElement("p");

message.textContent = "Welcome!";

title.before(message);
```

Result:

```html
<p>Welcome!</p>
<h1>...</h1>
```

---

# 10. `after()`

`after()` inserts an element after another element.

```javascript
const title = document.querySelector("h1");

const message = document.createElement("p");

message.textContent = "This comes after the heading.";

title.after(message);
```

Result:

```html
<h1>...</h1>
<p>This comes after the heading.</p>
```

---

# 11. Adding Classes

Use `classList.add()`.

```javascript
const button = document.createElement("button");

button.textContent = "Save";

button.classList.add("btn", "btn-primary");

document.body.append(button);
```

Result:

```html
<button class="btn btn-primary">
    Save
</button>
```

---

# 12. Adding an ID

Use the `id` property:

```javascript
const section = document.createElement("section");

section.id = "about";

document.body.append(section);
```

Result:

```html
<section id="about"></section>
```

---

# 13. Adding Attributes

Use `setAttribute()`.

```javascript
const image = document.createElement("img");

image.setAttribute("src", "profile.jpg");
image.setAttribute("alt", "Profile picture");

document.body.append(image);
```

Result:

```html
<img src="profile.jpg" alt="Profile picture">
```

---

# 14. Reading Attributes

Use `getAttribute()`.

```javascript
const image = document.querySelector("img");

const source = image.getAttribute("src");

console.log(source);
```

---

# 15. Checking an Attribute

Use `hasAttribute()`.

```javascript
if (image.hasAttribute("alt")) {
    console.log("Alt text exists");
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

# 16. Removing an Attribute

Use `removeAttribute()`.

```javascript
image.removeAttribute("alt");
```

The `alt` attribute is removed.

---

# 17. Using Direct Properties for Common Attributes

Many HTML attributes have convenient DOM properties.

Instead of:

```javascript
image.setAttribute("src", "profile.jpg");
```

you can write:

```javascript
image.src = "profile.jpg";
```

For an input:

```javascript
input.type = "email";
input.placeholder = "Enter your email";
```

For a link:

```javascript
link.href = "/about";
```

---

# 18. Creating a Link

```javascript
const link = document.createElement("a");

link.textContent = "Visit Website";
link.href = "https://example.com";

document.body.append(link);
```

You can also add:

```javascript
link.target = "_blank";
link.rel = "noopener noreferrer";
```

---

# 19. Creating an Input

```javascript
const input = document.createElement("input");

input.type = "text";
input.placeholder = "Enter your name";

document.body.append(input);
```

---

# 20. Creating a Button

```javascript
const button = document.createElement("button");

button.textContent = "Submit";
button.type = "button";

document.body.append(button);
```

You can attach an event:

```javascript
button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

---

# 21. Creating a List Dynamically

HTML:

```html
<ul id="languages"></ul>
```

JavaScript:

```javascript
const languages = [
    "JavaScript",
    "Python",
    "C++",
    "Java"
];

const list = document.querySelector("#languages");

languages.forEach((language) => {
    const item = document.createElement("li");

    item.textContent = language;

    list.append(item);
});
```

Result:

```html
<ul id="languages">
    <li>JavaScript</li>
    <li>Python</li>
    <li>C++</li>
    <li>Java</li>
</ul>
```

---

# 22. Creating a Product Card

Suppose your data is:

```javascript
const product = {
    name: "Laptop",
    price: 850,
    category: "Electronics"
};
```

Create the card:

```javascript
const card = document.createElement("article");

const title = document.createElement("h2");
const price = document.createElement("p");
const category = document.createElement("span");

title.textContent = product.name;
price.textContent = `$${product.price}`;
category.textContent = product.category;

card.classList.add("product-card");

card.append(
    title,
    price,
    category
);

document.body.append(card);
```

---

# 23. Creating Multiple Cards

```javascript
const products = [
    {
        name: "Laptop",
        price: 850
    },
    {
        name: "Phone",
        price: 500
    },
    {
        name: "Keyboard",
        price: 80
    }
];

const container = document.querySelector("#products");

products.forEach((product) => {
    const card = document.createElement("article");

    const title = document.createElement("h2");
    const price = document.createElement("p");

    title.textContent = product.name;
    price.textContent = `$${product.price}`;

    card.classList.add("product-card");

    card.append(title, price);
    container.append(card);
});
```

This is a common pattern for rendering dynamic data.

---

# 24. `insertAdjacentHTML()`

You can also insert HTML using:

```javascript
element.insertAdjacentHTML(position, html);
```

Example:

```javascript
const list = document.querySelector("ul");

list.insertAdjacentHTML(
    "beforeend",
    "<li>JavaScript</li>"
);
```

The available positions are:

```text
beforebegin
afterbegin
beforeend
afterend
```

---

# 25. Understanding `insertAdjacentHTML()` Positions

Suppose:

```html
<div id="box">
    Content
</div>
```

### `beforebegin`

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

### `afterbegin`

```javascript
box.insertAdjacentHTML(
    "afterbegin",
    "<p>First child</p>"
);
```

Result:

```html
<div id="box">
    <p>First child</p>
    Content
</div>
```

### `beforeend`

```javascript
box.insertAdjacentHTML(
    "beforeend",
    "<p>Last child</p>"
);
```

Result:

```html
<div id="box">
    Content
    <p>Last child</p>
</div>
```

### `afterend`

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

# 26. `createElement()` vs `insertAdjacentHTML()`

| `createElement()`                | `insertAdjacentHTML()`               |
| -------------------------------- | ------------------------------------ |
| Creates DOM nodes                | Parses an HTML string                |
| Easy to control individual nodes | Convenient for HTML snippets         |
| Good for dynamic data            | Good for known HTML templates        |
| Avoids parsing HTML strings      | Must handle untrusted HTML carefully |

---

# 27. Security: Avoid Untrusted HTML

Be careful when inserting user-controlled data into HTML strings.

Avoid:

```javascript
const username = userInput;

container.insertAdjacentHTML(
    "beforeend",
    `<p>${username}</p>`
);
```

If `username` contains malicious HTML, it may create a security vulnerability.

For plain text, prefer:

```javascript
const paragraph = document.createElement("p");

paragraph.textContent = username;

container.append(paragraph);
```

`textContent` treats the value as text rather than parsing it as HTML.

---

# 28. Creating a Document Fragment

`DocumentFragment` can be useful when creating many elements.

```javascript
const fragment = document.createDocumentFragment();

for (let i = 1; i <= 5; i++) {
    const item = document.createElement("li");

    item.textContent = `Item ${i}`;

    fragment.append(item);
}

document.querySelector("ul").append(fragment);
```

The fragment acts as a temporary container for the nodes.

---

# 29. Why Use `DocumentFragment()`?

It can make code easier to organize when building many nodes before inserting them into the document.

Pattern:

```text
Create fragment
     ↓
Create many elements
     ↓
Add elements to fragment
     ↓
Append fragment to DOM
```

Modern browsers already optimize many DOM operations, so `DocumentFragment` should be used when it makes the code clearer or when batching DOM construction is useful, rather than assuming it is always a major performance improvement.

---

# 30. Cloning an Existing Element

You can copy an existing element using:

```javascript
const copy = element.cloneNode(true);
```

The `true` means clone the element and its descendants.

Example:

```javascript
const original = document.querySelector(".card");

const copy = original.cloneNode(true);

document.body.append(copy);
```

---

# 31. Shallow vs Deep Clone

### Shallow clone

```javascript
const copy = element.cloneNode(false);
```

Copies the element itself but not its children.

### Deep clone

```javascript
const copy = element.cloneNode(true);
```

Copies the element and its descendants.

---

# 32. Important Point About Cloning

`cloneNode()` copies the DOM structure and attributes, but it does not copy event listeners that were added using `addEventListener()`.

For example:

```javascript
button.addEventListener("click", handleClick);

const copy = button.cloneNode(true);
```

The copied button does not automatically receive the event listener.

---

# 33. Creating Elements from Data

A common application pattern is:

```text
API / Database
      ↓
JavaScript data
      ↓
Create DOM elements
      ↓
Add content
      ↓
Append to page
```

For example:

```javascript
const users = [
    {
        name: "Sandip",
        role: "Developer"
    },
    {
        name: "Ram",
        role: "Designer"
    }
];

const container = document.querySelector("#users");

users.forEach((user) => {
    const card = document.createElement("div");

    const name = document.createElement("h3");
    const role = document.createElement("p");

    name.textContent = user.name;
    role.textContent = user.role;

    card.append(name, role);
    container.append(card);
});
```

This pattern is common in dashboards, ecommerce pages, admin panels, and other data-driven interfaces.

---

# 34. Useful DOM Creation Methods

| Method                     | Purpose                         |
| -------------------------- | ------------------------------- |
| `createElement()`          | Create an element               |
| `append()`                 | Add at the end                  |
| `appendChild()`            | Add one child                   |
| `prepend()`                | Add at the beginning            |
| `before()`                 | Insert before an element        |
| `after()`                  | Insert after an element         |
| `setAttribute()`           | Add/change an attribute         |
| `getAttribute()`           | Read an attribute               |
| `hasAttribute()`           | Check an attribute              |
| `removeAttribute()`        | Remove an attribute             |
| `insertAdjacentHTML()`     | Insert HTML                     |
| `cloneNode()`              | Clone an element                |
| `createDocumentFragment()` | Create a temporary DOM fragment |

---

# 35. Common Mistakes

### Mistake 1: Creating an element but not appending it

```javascript
const heading = document.createElement("h1");

heading.textContent = "Hello";
```

This creates the element but does not put it on the page.

You need:

```javascript
document.body.append(heading);
```

---

### Mistake 2: Using `innerHTML` for untrusted data

Avoid inserting user input directly into HTML strings.

Prefer:

```javascript
element.textContent = userInput;
```

when the value should be plain text.

---

### Mistake 3: Forgetting to select the parent

You need a parent/container to insert the new element:

```javascript
const container = document.querySelector("#container");

container.append(element);
```

---

### Mistake 4: Confusing `append()` and `prepend()`

```javascript
parent.append(child);
```

adds to the end.

```javascript
parent.prepend(child);
```

adds to the beginning.

---

# 36. Key Takeaways

* `document.createElement()` creates new DOM elements.
* Creating an element does not automatically display it.
* Use `append()` or another insertion method to add it to the DOM.
* `append()` can add multiple nodes.
* `prepend()` adds content at the beginning.
* `before()` and `after()` insert siblings.
* `setAttribute()` manages HTML attributes.
* `classList` is useful for adding CSS classes.
* `insertAdjacentHTML()` can insert HTML strings.
* Avoid inserting untrusted data as HTML.
* `textContent` is safer for plain text.
* `DocumentFragment` can help organize batched DOM creation.
* `cloneNode()` can duplicate existing DOM structures.

---

## Related Topics

* [DOM Introduction](./01-DOM-Introduction.md)
* [Selecting Elements](./02-Selecting-Elements.md)
* [Changing Content](./03-Changing-Content.md)
* [Changing Styles](./04-Changing-Styles.md)
* [Removing Elements](./06-Removing-Elements.md)
* [DOM Traversal](./07-DOM-Traversal.md)
* [Events](../13-Events/01-Events.md)
