# JavaScript Event Bubbling

**Event bubbling** is the process where an event starts from the element where it happened and then moves upward through its parent elements.

For example:

```text
button
   ↑
div
   ↑
body
   ↑
html
   ↑
document
```

This behavior is important when working with nested elements and **event delegation**.

---

# 1. Basic Example

HTML:

```html
<div id="parent">
    <button id="child">
        Click Me
    </button>
</div>
```

JavaScript:

```javascript
const parent = document.querySelector("#parent");
const child = document.querySelector("#child");

parent.addEventListener("click", () => {
    console.log("Parent clicked");
});

child.addEventListener("click", () => {
    console.log("Child clicked");
});
```

When the button is clicked, the output is generally:

```text
Child clicked
Parent clicked
```

The event starts at the button and then bubbles to its parent.

---

# 2. Why Is It Called Bubbling?

The event moves upward through the DOM:

```text
Child
  ↑
Parent
  ↑
Grandparent
  ↑
Body
  ↑
Document
```

It is called **bubbling** because the event moves from the deepest target toward its ancestors.

---

# 3. Event Propagation

Event propagation describes how an event travels through the DOM.

A simplified model has three phases:

```text
1. Capturing
       ↓
2. Target
       ↓
3. Bubbling
       ↑
```

For bubbling:

```text
document
    ↓
parent
    ↓
button
    ↑
parent
    ↑
document
```

The event reaches the target and then moves back upward through ancestors.

---

# 4. Simple Nested Example

HTML:

```html
<div id="outer">
    <div id="middle">
        <button id="inner">
            Click
        </button>
    </div>
</div>
```

JavaScript:

```javascript
const outer = document.querySelector("#outer");
const middle = document.querySelector("#middle");
const inner = document.querySelector("#inner");

outer.addEventListener("click", () => {
    console.log("Outer");
});

middle.addEventListener("click", () => {
    console.log("Middle");
});

inner.addEventListener("click", () => {
    console.log("Inner");
});
```

Clicking the button produces:

```text
Inner
Middle
Outer
```

---

# 5. `event.target` During Bubbling

The `event.target` normally remains the original element where the event started.

```javascript
inner.addEventListener("click", (event) => {
    console.log(event.target);
});
```

If the button is clicked:

```text
event.target
    ↓
button
```

Even while the event bubbles through its parents, the original target remains the same.

---

# 6. `event.currentTarget` During Bubbling

`event.currentTarget` changes depending on which listener is currently running.

```javascript
outer.addEventListener("click", (event) => {
    console.log(event.currentTarget);
});
```

Here:

```text
event.currentTarget
    ↓
outer
```

If the listener is running on `middle`:

```text
event.currentTarget
    ↓
middle
```

Therefore:

```text
event.target
    → Original event source

event.currentTarget
    → Element whose listener is executing
```

---

# 7. Example of Target and Current Target

HTML:

```html
<div id="parent">
    <button id="child">
        Save
    </button>
</div>
```

JavaScript:

```javascript
const parent = document.querySelector("#parent");

parent.addEventListener("click", (event) => {
    console.log("Target:", event.target);
    console.log("Current Target:", event.currentTarget);
});
```

Clicking the button:

```text
Target
  ↓
button

Current Target
  ↓
parent
```

The listener is attached to the parent, but the event originated from the button.

---

# 8. Stopping Bubbling

You can stop the event from continuing to propagate using:

```javascript
event.stopPropagation();
```

Example:

```javascript
const parent = document.querySelector("#parent");
const child = document.querySelector("#child");

parent.addEventListener("click", () => {
    console.log("Parent");
});

child.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("Child");
});
```

Now clicking the child produces:

```text
Child
```

The event does not continue to the parent.

---

# 9. `stopPropagation()` Does Not Cancel Default Actions

These methods have different purposes.

```javascript
event.stopPropagation();
```

Controls event propagation.

```javascript
event.preventDefault();
```

Controls the browser's default action.

For example:

```javascript
link.addEventListener("click", (event) => {
    event.preventDefault();
});
```

prevents navigation.

But:

```javascript
event.stopPropagation();
```

does not automatically prevent navigation.

---

# 10. Bubbling with Multiple Parent Levels

Consider:

```html
<div id="grandparent">
    <div id="parent">
        <button id="child">
            Click
        </button>
    </div>
</div>
```

Listeners:

```javascript
grandparent.addEventListener("click", () => {
    console.log("Grandparent");
});

parent.addEventListener("click", () => {
    console.log("Parent");
});

child.addEventListener("click", () => {
    console.log("Child");
});
```

Clicking the button:

```text
Child
Parent
Grandparent
```

The event travels upward through the ancestor chain.

---

# 11. Events That Bubble

Many common events bubble, including:

```text
click
dblclick
input
change
keydown
keyup
submit
```

However, **not every event bubbles**.

Always check the behavior of the specific event when propagation matters.

---

# 12. Event Bubbling and Dynamic Elements

Event bubbling becomes especially useful when elements are created dynamically.

Suppose:

```html
<ul id="users">
    <li>User 1</li>
    <li>User 2</li>
</ul>
```

Instead of attaching a listener to every list item, you can attach one to the parent.

```javascript
const users = document.querySelector("#users");

users.addEventListener("click", (event) => {
    console.log(event.target);
});
```

Clicking a list item causes the event to bubble to the `<ul>`.

This idea leads to **event delegation**.

---

# 13. Event Bubbling and Event Delegation

Example:

```javascript
const list = document.querySelector("#users");

list.addEventListener("click", (event) => {
    if (event.target.matches("li")) {
        console.log("User:", event.target.textContent);
    }
});
```

The parent handles clicks from its children.

This can be useful when:

* There are many child elements
* Child elements are created dynamically
* You want fewer event listeners

More details are covered in:

```text
07-Event-Delegation.md
```

---

# 14. Bubbling with `closest()`

Sometimes the clicked element is inside the element you actually care about.

HTML:

```html
<div id="products">
    <button class="product">
        <span>Delete</span>
    </button>
</div>
```

JavaScript:

```javascript
const products = document.querySelector("#products");

products.addEventListener("click", (event) => {
    const button = event.target.closest(".product");

    if (!button) {
        return;
    }

    console.log("Product button clicked");
});
```

The event bubbles to `products`, and `closest()` finds the relevant ancestor.

---

# 15. Bubbling and `event.target`

Be careful when a target contains child elements.

HTML:

```html
<button class="delete">
    <span>Delete</span>
</button>
```

If the user clicks the `<span>`:

```javascript
event.target
```

may be:

```text
span
```

rather than:

```text
button
```

This is why code such as:

```javascript
if (event.target.matches(".delete")) {
    // ...
}
```

may not work when clicking a child element.

A common solution is:

```javascript
const button = event.target.closest(".delete");
```

---

# 16. Bubbling with Forms

A form can receive events from controls inside it.

```html
<form id="form">
    <input id="username">
    <button type="submit">
        Submit
    </button>
</form>
```

You can listen to the form:

```javascript
const form = document.querySelector("#form");

form.addEventListener("submit", (event) => {
    event.preventDefault();

    console.log("Form submitted");
});
```

The submit event is handled at the form level.

---

# 17. Bubbling with Keyboard Events

Keyboard events can also participate in event propagation.

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.key);
});
```

A keyboard event from a focused element can propagate through its event path.

---

# 18. Bubbling and `stopImmediatePropagation()`

Consider:

```javascript
button.addEventListener("click", (event) => {
    event.stopImmediatePropagation();

    console.log("First");
});

button.addEventListener("click", () => {
    console.log("Second");
});
```

The second listener may not run because:

```javascript
event.stopImmediatePropagation();
```

stops other listeners on the same target as well as further propagation.

---

# 19. Bubbling vs Capturing

### Bubbling

Event moves:

```text
Child
  ↑
Parent
  ↑
Grandparent
```

### Capturing

Event moves:

```text
Grandparent
     ↓
Parent
     ↓
Child
```

The next topic covers capturing in more detail.

---

# 20. Practical Example: Delete Button

HTML:

```html
<div id="products">
    <div class="product">
        <span>Laptop</span>
        <button class="delete">Delete</button>
    </div>

    <div class="product">
        <span>Phone</span>
        <button class="delete">Delete</button>
    </div>
</div>
```

JavaScript:

```javascript
const products = document.querySelector("#products");

products.addEventListener("click", (event) => {
    const deleteButton = event.target.closest(".delete");

    if (!deleteButton) {
        return;
    }

    const product = deleteButton.closest(".product");

    product.remove();
});
```

Here:

```text
Click Delete
      ↓
Button
      ↓
Product
      ↓
Products container
      ↓
Listener handles the event
```

This is a practical use of event bubbling and delegation.

---

# 21. Practical Example: Menu

HTML:

```html
<div id="menu">
    <button data-action="home">Home</button>
    <button data-action="profile">Profile</button>
    <button data-action="logout">Logout</button>
</div>
```

JavaScript:

```javascript
const menu = document.querySelector("#menu");

menu.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button) {
        return;
    }

    console.log("Action:", button.dataset.action);
});
```

Instead of adding three separate listeners, the parent handles the events.

---

# 22. Bubbling and `stopPropagation()` Example

HTML:

```html
<div id="card">
    <button id="deleteButton">
        Delete
    </button>
</div>
```

JavaScript:

```javascript
const card = document.querySelector("#card");
const deleteButton = document.querySelector("#deleteButton");

card.addEventListener("click", () => {
    console.log("Card clicked");
});

deleteButton.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("Delete clicked");
});
```

Clicking the delete button:

```text
Delete clicked
```

The card listener does not receive the bubbled event.

---

# 23. When to Use Bubbling

Event bubbling is useful when:

* Working with nested DOM elements
* Handling events at a parent level
* Implementing event delegation
* Supporting dynamically created elements
* Reducing the number of event listeners
* Managing lists, menus, tables, and cards

---

# 24. Important Things to Remember

### Event starts at the target

```text
Target
```

Then it can bubble upward:

```text
Target
  ↑
Parent
  ↑
Ancestor
```

### `target`

```javascript
event.target
```

Original event source.

### `currentTarget`

```javascript
event.currentTarget
```

Element whose listener is currently running.

### Stop propagation

```javascript
event.stopPropagation();
```

### Prevent default action

```javascript
event.preventDefault();
```

These are different operations.

---

# 25. Key Takeaways

* Event bubbling moves an event from the target toward its ancestors.
* Many common DOM events bubble.
* `event.target` normally remains the original event source.
* `event.currentTarget` identifies the element whose listener is currently executing.
* `stopPropagation()` can stop further propagation.
* `preventDefault()` does something different: it prevents a default browser action when possible.
* Event bubbling makes event delegation possible.
* Bubbling is especially useful for dynamic lists, menus, tables, and buttons.
* `closest()` can help identify the intended ancestor when the clicked target is a nested element.

---
