# JavaScript Event Delegation

**Event delegation** is a technique where you attach one event listener to a parent element instead of adding separate listeners to many child elements.

It works mainly because of **event bubbling**.

For example:

```text id="q7w2ka"
Parent
 ├── Child
 ├── Child
 └── Child
```

Instead of:

```text id="r4m2xk"
Child → listener
Child → listener
Child → listener
```

you can use:

```text id="5z5x9s"
Parent → one listener
```

---

# 1. Basic Example

HTML:

```html id="3f3l3a"
<ul id="users">
    <li>Sandip</li>
    <li>Ram</li>
    <li>Sita</li>
</ul>
```

Instead of adding a listener to every `<li>`:

```javascript id="v4nd4d"
document.querySelectorAll("#users li").forEach((item) => {
    item.addEventListener("click", () => {
        console.log(item.textContent);
    });
});
```

You can attach one listener to the parent:

```javascript id="1d2g4h"
const users = document.querySelector("#users");

users.addEventListener("click", (event) => {
    console.log(event.target.textContent);
});
```

When a list item is clicked, the event bubbles to the `<ul>`.

---

# 2. How Event Delegation Works

Suppose:

```text id="2e9j9j"
<ul>
   ├── <li>One</li>
   ├── <li>Two</li>
   └── <li>Three</li>
</ul>
```

Clicking:

```text id="s7kq1a"
<li>Two</li>
```

The event travels:

```text id="w4g4u3"
li
 ↓
ul
 ↓
document
```

The listener on `<ul>` receives the event.

---

# 3. Basic Delegation Pattern

```javascript id="5b0k1w"
parent.addEventListener("click", (event) => {
    if (event.target.matches(".child")) {
        // Handle child event
    }
});
```

The important parts are:

```javascript id="2p3f6h"
event.target
```

and:

```javascript id="3n4n4w"
event.target.matches()
```

---

# 4. Using `matches()`

HTML:

```html id="0e7v9u"
<div id="actions">
    <button class="edit">Edit</button>
    <button class="delete">Delete</button>
</div>
```

JavaScript:

```javascript id="l9r8m6"
const actions = document.querySelector("#actions");

actions.addEventListener("click", (event) => {
    if (event.target.matches(".edit")) {
        console.log("Edit");
    }

    if (event.target.matches(".delete")) {
        console.log("Delete");
    }
});
```

The parent handles both buttons.

---

# 5. Problem with Nested Elements

Consider:

```html id="5t2jcv"
<button class="delete">
    <span>Delete</span>
</button>
```

If the user clicks the `<span>`:

```javascript id="7u3wq9"
event.target
```

may be:

```html id="7r8w3j"
<span>Delete</span>
```

Therefore:

```javascript id="u1f1v0"
event.target.matches(".delete")
```

returns `false`.

The target is the child `<span>`, not the button.

---

# 6. Using `closest()`

A better approach for nested elements is:

```javascript id="ujm4b2"
const button = event.target.closest(".delete");
```

Example:

```javascript id="d2y2sd"
actions.addEventListener("click", (event) => {
    const button = event.target.closest(".delete");

    if (!button) {
        return;
    }

    console.log("Delete clicked");
});
```

`closest()` searches the target and its ancestors for a matching element.

---

# 7. Complete Example

HTML:

```html id="6x1rqo"
<div id="actions">
    <button class="edit">
        <span>Edit</span>
    </button>

    <button class="delete">
        <span>Delete</span>
    </button>
</div>
```

JavaScript:

```javascript id="s0g9q5"
const actions = document.querySelector("#actions");

actions.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button) {
        return;
    }

    if (button.classList.contains("edit")) {
        console.log("Edit");
    }

    if (button.classList.contains("delete")) {
        console.log("Delete");
    }
});
```

This works even if the user clicks the `<span>` inside the button.

---

# 8. Dynamic Elements

One of the biggest advantages of event delegation is handling elements created later.

Suppose:

```javascript id="d2p1x4"
const list = document.querySelector("#list");

list.addEventListener("click", (event) => {
    const item = event.target.closest(".item");

    if (!item) {
        return;
    }

    console.log(item.textContent);
});
```

Later, JavaScript adds:

```javascript id="3n0x5x"
const item = document.createElement("div");

item.className = "item";
item.textContent = "New Item";

list.append(item);
```

The new element can still be handled by the existing parent listener.

You do not need to attach another listener to the new element.

---

# 9. Without Event Delegation

Without delegation:

```javascript id="c6j4s0"
document.querySelectorAll(".item").forEach((item) => {
    item.addEventListener("click", handleClick);
});
```

If new items are added later, they do not automatically receive the listener.

You would need to register another listener.

---

# 10. With Event Delegation

With delegation:

```javascript id="l0v5uq"
container.addEventListener("click", (event) => {
    const item = event.target.closest(".item");

    if (!item) {
        return;
    }

    handleClick(item);
});
```

New matching elements are automatically covered as long as the event bubbles to the container.

---

# 11. Practical Example: Todo List

HTML:

```html id="b5q3vh"
<ul id="todoList">
    <li class="todo">
        <span>Learn JavaScript</span>
        <button class="delete">Delete</button>
    </li>

    <li class="todo">
        <span>Learn React</span>
        <button class="delete">Delete</button>
    </li>
</ul>
```

JavaScript:

```javascript id="3w8q1z"
const todoList = document.querySelector("#todoList");

todoList.addEventListener("click", (event) => {
    const deleteButton = event.target.closest(".delete");

    if (!deleteButton) {
        return;
    }

    const todo = deleteButton.closest(".todo");

    todo.remove();
});
```

One listener handles all delete buttons.

---

# 12. Practical Example: Shopping Cart

HTML:

```html id="v2k8q5"
<div id="cart">
    <div class="cart-item" data-id="101">
        <span>Laptop</span>
        <button class="remove">Remove</button>
    </div>

    <div class="cart-item" data-id="102">
        <span>Mouse</span>
        <button class="remove">Remove</button>
    </div>
</div>
```

JavaScript:

```javascript id="7f5m2q"
const cart = document.querySelector("#cart");

cart.addEventListener("click", (event) => {
    const removeButton = event.target.closest(".remove");

    if (!removeButton) {
        return;
    }

    const item = removeButton.closest(".cart-item");

    console.log("Remove:", item.dataset.id);
});
```

The `data-id` identifies the item.

---

# 13. Practical Example: Table Actions

This pattern is useful for dashboard tables.

HTML:

```html id="8k1w4n"
<table id="usersTable">
    <tbody>
        <tr data-user-id="101">
            <td>Sandip</td>
            <td>
                <button class="edit">Edit</button>
                <button class="delete">Delete</button>
            </td>
        </tr>

        <tr data-user-id="102">
            <td>Ram</td>
            <td>
                <button class="edit">Edit</button>
                <button class="delete">Delete</button>
            </td>
        </tr>
    </tbody>
</table>
```

JavaScript:

```javascript id="1l4s2x"
const table = document.querySelector("#usersTable");

table.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button) {
        return;
    }

    const row = button.closest("tr");
    const userId = row.dataset.userId;

    if (button.classList.contains("edit")) {
        console.log("Edit user:", userId);
    }

    if (button.classList.contains("delete")) {
        console.log("Delete user:", userId);
    }
});
```

This is a common pattern in admin dashboards.

---

# 14. Practical Example: Menu

HTML:

```html id="f0n8uw"
<nav id="menu">
    <button data-page="home">Home</button>
    <button data-page="products">Products</button>
    <button data-page="contact">Contact</button>
</nav>
```

JavaScript:

```javascript id="f5k4e2"
const menu = document.querySelector("#menu");

menu.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button) {
        return;
    }

    console.log("Navigate to:", button.dataset.page);
});
```

One listener handles all menu buttons.

---

# 15. Using `data-*` Attributes

Event delegation works very well with custom data attributes.

HTML:

```html id="v4l0tq"
<div id="actions">
    <button data-action="edit">Edit</button>
    <button data-action="delete">Delete</button>
    <button data-action="view">View</button>
</div>
```

JavaScript:

```javascript id="l1q2xs"
actions.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button) {
        return;
    }

    const action = button.dataset.action;

    console.log(action);
});
```

Possible output:

```text id="m5u0h6"
edit
delete
view
```

---

# 16. Delegation with `closest()`

A useful general pattern is:

```javascript id="w9z3pa"
container.addEventListener("click", (event) => {
    const element = event.target.closest(".item");

    if (!element || !container.contains(element)) {
        return;
    }

    // Handle item
});
```

The `contains()` check can be useful when the event target is outside the intended container but `closest()` finds a matching ancestor elsewhere.

---

# 17. `closest()` vs `matches()`

### `matches()`

Checks the current element:

```javascript id="y7k8m3"
event.target.matches(".button");
```

### `closest()`

Searches the current element and its ancestors:

```javascript id="n8x5v1"
event.target.closest(".button");
```

For nested buttons or controls, `closest()` is often more robust.

---

# 18. Event Delegation and Bubbling

Event delegation normally depends on bubbling.

```text id="4q8z3m"
Child event
     ↓
Parent receives bubbled event
     ↓
Parent identifies child
     ↓
Parent handles action
```

This is why:

```javascript id="0n7j8c"
event.stopPropagation();
```

can interfere with delegated handlers.

---

# 19. Delegation with `stopPropagation()`

Suppose:

```javascript id="0f8f2v"
list.addEventListener("click", (event) => {
    console.log("Delegated handler");
});
```

A child does:

```javascript id="j9v2l3"
child.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

The event may not reach the list.

Therefore, avoid stopping propagation unless it is actually required.

---

# 20. Delegation and Non-Bubbling Events

Event delegation depends on events reaching the ancestor.

If an event does not bubble, a normal delegated listener will not receive it through bubbling.

For example, some event types have different propagation behavior.

When choosing an event for delegation, verify that the event bubbles or use another appropriate strategy.

---

# 21. Delegation for Form Controls

Example:

```html id="c0p1o2"
<form id="form">
    <input name="username">
    <input name="email">

    <button type="submit">
        Submit
    </button>
</form>
```

You can listen at the form level:

```javascript id="4d8v5j"
const form = document.querySelector("#form");

form.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button) {
        return;
    }

    console.log("Button clicked");
});
```

For form submission itself, listen to:

```javascript id="d4b6l1"
form.addEventListener("submit", handler);
```

rather than trying to treat every form action as a click.

---

# 22. Delegation with Dynamic Content

Suppose an API loads products:

```javascript id="x6r3vn"
products.forEach((product) => {
    container.insertAdjacentHTML(
        "beforeend",
        `
        <div class="product" data-id="${product.id}">
            <span>${product.name}</span>
            <button class="delete">Delete</button>
        </div>
        `
    );
});
```

Instead of attaching listeners after every insertion:

```javascript id="h5u7ps"
container.addEventListener("click", (event) => {
    const button = event.target.closest(".delete");

    if (!button) {
        return;
    }

    const product = button.closest(".product");

    console.log("Delete:", product.dataset.id);
});
```

The single listener can handle current and future matching elements.

---

# 23. Delegation Reduces Listener Count

Suppose there are 1,000 buttons.

Without delegation:

```text id="o0z7a1"
1,000 buttons
    ↓
1,000 listeners
```

With delegation:

```text id="9n6r2s"
1 container
    ↓
1 listener
```

This can simplify event management.

However, performance is not the only reason to use delegation. The ability to handle dynamically added elements is often more important.

---

# 24. Delegation and Performance

Event delegation can reduce the number of registered handlers.

But do not assume:

> One listener is always faster.

Actual performance depends on:

* Number of elements
* Event frequency
* Handler complexity
* DOM structure
* Application architecture

Use delegation when it makes the event-handling design simpler and appropriate.

---

# 25. Delegation with Keyboard Events

Delegation can also be used for keyboard interactions when the event bubbles appropriately.

Example:

```javascript id="c3w7a8"
container.addEventListener("keydown", (event) => {
    const input = event.target.closest("input");

    if (!input) {
        return;
    }

    if (event.key === "Enter") {
        console.log("Enter:", input.value);
    }
});
```

---

# 26. Common Mistakes

## Mistake 1: Checking Only `event.target`

Suppose:

```html id="4xj5v0"
<button class="delete">
    <span>Delete</span>
</button>
```

This may fail:

```javascript id="f2t8z3"
if (event.target.matches(".delete")) {
    // ...
}
```

when the `<span>` is clicked.

Use:

```javascript id="j0p8b2"
const button = event.target.closest(".delete");
```

---

## Mistake 2: Forgetting to Check for `null`

`closest()` can return `null`.

Wrong:

```javascript id="n2z1f5"
const button = event.target.closest(".delete");

button.remove();
```

Safer:

```javascript id="w5r7k4"
const button = event.target.closest(".delete");

if (!button) {
    return;
}

button.remove();
```

---

# 27. Common Mistake: Using `stopPropagation()` Unnecessarily

If a delegated parent listener is not working, check whether a child calls:

```javascript id="3y8z4f"
event.stopPropagation();
```

That may prevent the event from reaching the parent.

---

# 28. Common Mistake: Delegating to the Wrong Parent

Choose a container that:

* Contains the target elements
* Exists when the listener is registered
* Receives the relevant bubbling event

Example:

```javascript id="p9y2r4"
const list = document.querySelector("#list");

list.addEventListener("click", handler);
```

This is usually better than attaching everything to `document` without a reason.

---

# 29. Event Delegation Pattern

A reusable pattern:

```javascript id="v1s3d8"
container.addEventListener("click", (event) => {
    const element = event.target.closest(".target");

    if (!element || !container.contains(element)) {
        return;
    }

    // Handle the event
});
```

For multiple actions:

```javascript id="a2c5m7"
container.addEventListener("click", (event) => {
    const button = event.target.closest("button");

    if (!button || !container.contains(button)) {
        return;
    }

    const action = button.dataset.action;

    if (action === "edit") {
        // Edit
    }

    if (action === "delete") {
        // Delete
    }
});
```

---

# 30. Event Delegation in Real Applications

Event delegation is commonly useful for:

* Todo lists
* Shopping carts
* Product lists
* Admin tables
* Navigation menus
* Dropdown menus
* Dynamic forms
* Notification lists
* Comment sections
* Chat interfaces

For example, a hotel dashboard could have many dynamically rendered table or order actions:

```text id="u7d3h2"
Orders Container
 ├── Order 101 → View / Accept / Cancel
 ├── Order 102 → View / Accept / Cancel
 └── Order 103 → View / Accept / Cancel
```

One parent listener can handle these actions based on:

```javascript id="w8h5k2"
event.target.closest("button")
```

and:

```javascript id="3b7j9m"
button.dataset.action
```

---

# 31. Event Delegation vs Direct Listeners

| Feature                     | Direct Listener     | Event Delegation            |
| --------------------------- | ------------------- | --------------------------- |
| Listener location           | Each element        | Parent/container            |
| Dynamic elements            | Need extra handling | Usually works automatically |
| Number of listeners         | Potentially many    | Usually fewer               |
| Requires bubbling           | No                  | Usually yes                 |
| Useful for lists            | Yes                 | Very useful                 |
| Useful for dynamic content  | More work           | Very useful                 |
| Uses `target` / `closest()` | Optional            | Common                      |

---

# 32. When to Use Event Delegation

Use event delegation when:

* Many similar elements need the same behavior.
* Elements are dynamically created.
* A parent container naturally owns the interaction.
* The event bubbles.
* Centralizing the handler makes the code easier to maintain.

Direct listeners can be simpler when:

* There are only a few elements.
* Each element has completely different behavior.
* The event does not bubble.
* Delegation would make the code harder to understand.

---

# 33. Key Takeaways

* Event delegation uses a parent listener to handle events from child elements.
* It relies mainly on event bubbling.
* `event.target` identifies the original event source.
* `closest()` is useful when the clicked element contains nested elements.
* Dynamic elements can be handled without registering new listeners for each one.
* `data-*` attributes are useful for identifying actions and IDs.
* `stopPropagation()` can prevent delegated events from reaching the parent.
* Delegation can reduce the number of listeners, but its main benefit is often simpler handling of dynamic content.
* Choose the smallest sensible container rather than automatically attaching delegated listeners to `document`.

---
