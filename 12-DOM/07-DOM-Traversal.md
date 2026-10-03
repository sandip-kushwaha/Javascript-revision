# JavaScript DOM Traversal

DOM traversal means **moving through the DOM tree** to find related elements.

For example, from one element you can find:

* Its parent
* Its children
* Its siblings
* Its ancestors
* Its descendants

A simple DOM structure looks like:

```text
document
   │
   └── body
        │
        └── div.container
             │
             ├── h2
             ├── p
             └── button
```

DOM traversal allows JavaScript to move between these elements.

---

# 1. What is DOM Traversal?

Suppose you have:

```html
<div class="card">
    <h2>Product</h2>
    <p>Description</p>
    <button>Delete</button>
</div>
```

From the button, you might want to find:

```text
button
   ↓
.card
   ↓
h2
```

DOM traversal provides methods and properties for doing this.

---

# 2. `parentElement`

`parentElement` returns the parent HTML element.

```javascript
const button = document.querySelector("button");

const parent = button.parentElement;

console.log(parent);
```

For:

```html
<div class="card">
    <button>Delete</button>
</div>
```

the parent of the button is:

```html
<div class="card">
```

---

# 3. `parentNode`

You can also use:

```javascript
const parent = element.parentNode;
```

`parentNode` returns the parent node, which can include node types that are not elements.

For normal HTML element traversal, `parentElement` is often more convenient.

---

# 4. `children`

The `children` property returns an `HTMLCollection` containing the element's child elements.

HTML:

```html
<div id="container">
    <h2>Title</h2>
    <p>Description</p>
    <button>Click</button>
</div>
```

JavaScript:

```javascript
const container = document.querySelector("#container");

console.log(container.children);
```

The collection contains:

```text
h2
p
button
```

---

# 5. Accessing a Specific Child

Because `children` is collection-like, you can access an item by index.

```javascript
const firstChild = container.children[0];

console.log(firstChild);
```

The result is:

```html
<h2>Title</h2>
```

Another example:

```javascript
const secondChild = container.children[1];
```

This selects:

```html
<p>Description</p>
```

---

# 6. `children.length`

You can find the number of child elements:

```javascript
console.log(container.children.length);
```

For:

```html
<div>
    <h2></h2>
    <p></p>
    <button></button>
</div>
```

the result is:

```text
3
```

---

# 7. `firstElementChild`

Returns the first child element.

```javascript
const first = container.firstElementChild;

console.log(first);
```

Example:

```html
<div id="container">
    <h2>Title</h2>
    <p>Description</p>
</div>
```

Result:

```html
<h2>Title</h2>
```

---

# 8. `lastElementChild`

Returns the last child element.

```javascript
const last = container.lastElementChild;

console.log(last);
```

Result:

```html
<p>Description</p>
```

---

# 9. `nextElementSibling`

Returns the next sibling element.

HTML:

```html
<div>
    <h2>Title</h2>
    <p>Description</p>
    <button>Delete</button>
</div>
```

JavaScript:

```javascript
const heading = document.querySelector("h2");

const next = heading.nextElementSibling;

console.log(next);
```

Result:

```html
<p>Description</p>
```

---

# 10. `previousElementSibling`

Returns the previous sibling element.

```javascript
const button = document.querySelector("button");

const previous = button.previousElementSibling;

console.log(previous);
```

Result:

```html
<p>Description</p>
```

---

# 11. Sibling Traversal

Consider:

```html
<div>
    <h2>Title</h2>
    <p>Description</p>
    <button>Delete</button>
</div>
```

The relationships are:

```text
h2
 ↓
p
 ↓
button
```

From `p`:

```javascript
p.previousElementSibling
```

returns:

```text
h2
```

And:

```javascript
p.nextElementSibling
```

returns:

```text
button
```

---

# 12. `closest()`

`closest()` finds the nearest ancestor that matches a CSS selector.

HTML:

```html
<div class="card">
    <div class="content">
        <button class="delete-btn">
            Delete
        </button>
    </div>
</div>
```

JavaScript:

```javascript
const button = document.querySelector(".delete-btn");

const card = button.closest(".card");

console.log(card);
```

It finds:

```html
<div class="card">
```

even though `.card` is not the button's direct parent.

---

# 13. `closest()` with Conditions

You can check whether an ancestor exists:

```javascript
const card = button.closest(".card");

if (card) {
    console.log("Card found");
}
```

You can also use optional chaining:

```javascript
button.closest(".card")?.remove();
```

If the card exists, it is removed.

---

# 14. `matches()`

`matches()` checks whether an element matches a CSS selector.

Example:

```javascript
const button = document.querySelector("button");

if (button.matches(".delete-btn")) {
    console.log("This is a delete button");
}
```

It returns:

```text
true
```

or:

```text
false
```

---

# 15. `querySelector()` on an Element

`querySelector()` is not limited to `document`.

You can search inside a specific element.

HTML:

```html
<div class="card">
    <h2>Product</h2>
    <button>Delete</button>
</div>
```

JavaScript:

```javascript
const card = document.querySelector(".card");

const button = card.querySelector("button");

console.log(button);
```

This searches for the button **inside the card**.

---

# 16. `querySelectorAll()` on an Element

You can also search for multiple descendants:

```javascript
const card = document.querySelector(".card");

const elements = card.querySelectorAll("p");

console.log(elements);
```

Only matching elements inside that card are returned.

---

# 17. Parent → Child Traversal

Example:

```javascript
const card = document.querySelector(".card");

const title = card.querySelector("h2");
```

The direction is:

```text
card
 ↓
h2
```

You can also use:

```javascript
card.children
```

to access direct child elements.

---

# 18. Child → Parent Traversal

Start with a button:

```javascript
const button = document.querySelector("button");

const card = button.parentElement;
```

The direction is:

```text
button
  ↑
card
```

For a specific ancestor:

```javascript
const card = button.closest(".card");
```

---

# 19. Child → Sibling Traversal

Suppose:

```html
<div>
    <h2>Product</h2>
    <p>Price: $500</p>
    <button>Buy</button>
</div>
```

From the button:

```javascript
const button = document.querySelector("button");

const previous = button.previousElementSibling;

console.log(previous);
```

Result:

```html
<p>Price: $500</p>
```

---

# 20. Traversing Multiple Levels

You can move through multiple levels.

HTML:

```html
<div class="page">
    <section class="products">
        <article class="card">
            <button>Delete</button>
        </article>
    </section>
</div>
```

From the button:

```javascript
const button = document.querySelector("button");

const section = button
    .closest(".products");

console.log(section);
```

Or find the page:

```javascript
const page = button
    .closest(".page");

console.log(page);
```

Using `closest()` is often clearer than chaining multiple `parentElement` calls.

---

# 21. `childNodes` vs `children`

There is an important difference.

### `children`

Returns only element nodes:

```javascript
element.children
```

### `childNodes`

Returns all child nodes, including:

* Elements
* Text nodes
* Comments

Example:

```javascript
console.log(element.childNodes);
```

Whitespace between HTML elements can appear as text nodes.

---

# 22. `firstChild` vs `firstElementChild`

These are not always the same.

```javascript
element.firstChild
```

returns the first node.

```javascript
element.firstElementChild
```

returns the first element.

For example:

```html
<div>
    <p>Hello</p>
</div>
```

Whitespace may create a text node before the `<p>`.

Therefore:

```javascript
element.firstChild
```

may be a text node.

While:

```javascript
element.firstElementChild
```

returns:

```html
<p>Hello</p>
```

For HTML element traversal, `firstElementChild` is often more predictable.

---

# 23. `lastChild` vs `lastElementChild`

Similarly:

```javascript
element.lastChild
```

returns the last node.

While:

```javascript
element.lastElementChild
```

returns the last element.

---

# 24. Useful Traversal Properties

| Property                 | Purpose                  |
| ------------------------ | ------------------------ |
| `parentElement`          | Parent element           |
| `parentNode`             | Parent node              |
| `children`               | Child elements           |
| `childNodes`             | All child nodes          |
| `firstElementChild`      | First child element      |
| `lastElementChild`       | Last child element       |
| `nextElementSibling`     | Next sibling element     |
| `previousElementSibling` | Previous sibling element |
| `firstChild`             | First child node         |
| `lastChild`              | Last child node          |

---

# 25. Useful Traversal Methods

| Method               | Purpose                           |
| -------------------- | --------------------------------- |
| `closest()`          | Find nearest matching ancestor    |
| `matches()`          | Check if element matches selector |
| `querySelector()`    | Find first matching descendant    |
| `querySelectorAll()` | Find matching descendants         |

---

# 26. Practical Example: Delete Card

HTML:

```html
<div class="card">
    <h2>Laptop</h2>
    <p>$850</p>
    <button class="delete-btn">
        Delete
    </button>
</div>
```

JavaScript:

```javascript
const button = document.querySelector(".delete-btn");

button.addEventListener("click", () => {
    const card = button.closest(".card");

    card?.remove();
});
```

Traversal:

```text
button
   ↓
closest(".card")
   ↓
card
   ↓
remove()
```

---

# 27. Practical Example: Update a Card

HTML:

```html
<article class="card">
    <h2>Hotel Room</h2>
    <p class="status">Available</p>
    <button class="book-btn">Book</button>
</article>
```

JavaScript:

```javascript
const button = document.querySelector(".book-btn");

button.addEventListener("click", () => {
    const card = button.closest(".card");

    const status = card.querySelector(".status");

    status.textContent = "Booked";
});
```

The button finds its card first and then finds the status inside that card.

---

# 28. Practical Example: Navigate Between Siblings

HTML:

```html
<div class="steps">
    <button class="step active">Step 1</button>
    <button class="step">Step 2</button>
    <button class="step">Step 3</button>
</div>
```

JavaScript:

```javascript
const activeStep = document.querySelector(".step.active");

const nextStep = activeStep.nextElementSibling;

nextStep?.classList.add("active");
```

This moves from one sibling to the next.

---

# 29. Traversal with `forEach()`

You can traverse a collection of children:

```javascript
const container = document.querySelector("#container");

Array.from(container.children).forEach((child) => {
    console.log(child);
});
```

Modern collections such as `NodeList` can often be used directly with `forEach()`:

```javascript
const items = container.querySelectorAll(".item");

items.forEach((item) => {
    console.log(item);
});
```

---

# 30. DOM Traversal Pattern

A common UI pattern is:

```text
User clicks an element
        ↓
Find related parent
        ↓
Find child inside parent
        ↓
Change / remove / update it
```

Example:

```javascript
button.addEventListener("click", () => {
    const card = button.closest(".card");
    const title = card.querySelector(".title");

    title.textContent = "Updated";
});
```

This is especially useful for dynamically generated components.

---

# 31. Traversal and Dynamic UI

Suppose many cards exist:

```html
<div class="card">
    <h2>Product A</h2>
    <button class="delete">Delete</button>
</div>

<div class="card">
    <h2>Product B</h2>
    <button class="delete">Delete</button>
</div>
```

A button can find **its own card**:

```javascript
const buttons = document.querySelectorAll(".delete");

buttons.forEach((button) => {
    button.addEventListener("click", () => {
        const card = button.closest(".card");

        card.remove();
    });
});
```

Each button operates on its related card.

---

# 32. Traversal vs Selection

These concepts are related but different.

### Selection

Starting from the document:

```javascript
document.querySelector(".card");
```

### Traversal

Starting from an existing element:

```javascript
button.closest(".card");
```

or:

```javascript
card.querySelector(".title");
```

A useful way to think about it:

```text
Selection
document
   ↓
find element

Traversal
existing element
   ↓
find related element
```

---

# 33. Common Mistakes

### Mistake 1: Assuming `parentElement` is always the desired parent

```javascript
button.parentElement
```

only gives the immediate parent.

If you need a specific ancestor:

```javascript
button.closest(".card")
```

is usually better.

---

### Mistake 2: Confusing `children` and `childNodes`

```javascript
element.children
```

contains element children.

```javascript
element.childNodes
```

can contain text nodes and comments too.

---

### Mistake 3: Forgetting that traversal can return `null`

For example:

```javascript
const next = element.nextElementSibling;
```

If there is no next element, the result is:

```text
null
```

Use a check:

```javascript
if (next) {
    next.classList.add("active");
}
```

or:

```javascript
next?.classList.add("active");
```

---

### Mistake 4: Traversing too many levels manually

Instead of:

```javascript
button.parentElement.parentElement.parentElement
```

prefer:

```javascript
button.closest(".card");
```

It is easier to understand and less dependent on the exact HTML structure.

---

# 34. Key Takeaways

* DOM traversal means moving between related DOM nodes.
* `parentElement` finds the immediate parent element.
* `children` finds direct child elements.
* `firstElementChild` and `lastElementChild` find the first and last child elements.
* `nextElementSibling` finds the next sibling.
* `previousElementSibling` finds the previous sibling.
* `closest()` finds the nearest matching ancestor.
* `matches()` checks whether an element matches a selector.
* `querySelector()` can search inside an existing element.
* `children` contains elements, while `childNodes` contains all node types.
* Traversal is very useful for dynamic cards, lists, tables, forms, and dashboards.
* Use `closest()` when you need a specific ancestor rather than chaining many `parentElement` calls.

---

## Related Topics

* [DOM Introduction](./01-DOM-Introduction.md)
* [Selecting Elements](./02-Selecting-Elements.md)
* [Changing Content](./03-Changing-Content.md)
* [Changing Styles](./04-Changing-Styles.md)
* [Creating Elements](./05-Creating-Elements.md)
* [Removing Elements](./06-Removing-Elements.md)
* [Events](../13-Events/01-Events.md)
