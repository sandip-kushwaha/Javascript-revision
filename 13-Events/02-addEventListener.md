# JavaScript `addEventListener()`

`addEventListener()` is used to tell JavaScript:

> "When this event happens on this element, run this function."

It is one of the most important APIs for handling browser events.

Basic syntax:

```javascript
element.addEventListener("event", handler);
```

Example:

```javascript
const button = document.querySelector("#button");

button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

---

# 1. Basic Syntax

The general syntax is:

```javascript
element.addEventListener(
    eventType,
    listener
);
```

Example:

```javascript
button.addEventListener("click", handleClick);
```

There are two main parts:

```text
"click"       → Event type
handleClick   → Function to execute
```

---

# 2. Using an Anonymous Function

You can directly provide a function:

```javascript
button.addEventListener("click", () => {
    console.log("Clicked");
});
```

This is useful when the handler is short and only needed for this event.

---

# 3. Using a Named Function

You can define the function separately:

```javascript
function handleClick() {
    console.log("Button clicked");
}

button.addEventListener("click", handleClick);
```

This is useful when:

* The function is longer
* The function is reused
* You need to remove the listener later

---

# 4. Do Not Call the Function Immediately

Correct:

```javascript
button.addEventListener("click", handleClick);
```

Incorrect:

```javascript
button.addEventListener("click", handleClick());
```

Why?

```javascript
handleClick
```

passes the function.

But:

```javascript
handleClick()
```

calls the function immediately and passes its return value to `addEventListener()`.

---

# 5. Passing an Event Object

The browser passes an event object to the handler.

```javascript
button.addEventListener("click", (event) => {
    console.log(event);
});
```

You can name it:

```javascript
button.addEventListener("click", (event) => {
    console.log("Event:", event);
});
```

The event object contains information about what happened.

---

# 6. Event Type

The first argument specifies the event type:

```javascript
button.addEventListener("click", handler);
```

Examples:

```javascript
input.addEventListener("input", handler);

form.addEventListener("submit", handler);

document.addEventListener("keydown", handler);

window.addEventListener("resize", handler);
```

The event type should normally be provided without the `on` prefix.

Correct:

```javascript
"click"
```

Not:

```javascript
"onclick"
```

---

# 7. Click Event

```javascript
const button = document.querySelector("#save");

button.addEventListener("click", () => {
    console.log("Save clicked");
});
```

---

# 8. Input Event

```javascript
const search = document.querySelector("#search");

search.addEventListener("input", () => {
    console.log(search.value);
});
```

The handler runs as the input value changes.

---

# 9. Change Event

```javascript
const category = document.querySelector("#category");

category.addEventListener("change", () => {
    console.log(category.value);
});
```

This is commonly used with:

* `<select>`
* Checkboxes
* Radio buttons
* Other form controls

---

# 10. Submit Event

```javascript
const form = document.querySelector("#loginForm");

form.addEventListener("submit", (event) => {
    event.preventDefault();

    console.log("Form submitted");
});
```

`preventDefault()` stops the browser's default form submission behavior.

---

# 11. Keyboard Events

You can listen for keyboard events:

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.key);
});
```

For example:

```text
a
Enter
Escape
ArrowUp
ArrowDown
```

---

# 12. Mouse Events

```javascript
const card = document.querySelector(".card");

card.addEventListener("mouseenter", () => {
    console.log("Mouse entered");
});

card.addEventListener("mouseleave", () => {
    console.log("Mouse left");
});
```

---

# 13. Multiple Event Listeners

An element can have multiple listeners.

```javascript
button.addEventListener("click", handleClick);

button.addEventListener("mouseenter", handleMouseEnter);

button.addEventListener("mouseleave", handleMouseLeave);
```

Each listener responds to its own event.

---

# 14. Multiple Listeners for the Same Event

You can register multiple handlers for the same event.

```javascript
function saveData() {
    console.log("Saving data");
}

function showMessage() {
    console.log("Data saved");
}

button.addEventListener("click", saveData);
button.addEventListener("click", showMessage);
```

When the button is clicked, both listeners can run.

---

# 15. Event Listener Execution Order

For listeners registered on the same target and event, they generally run in the order they were registered.

```javascript
button.addEventListener("click", () => {
    console.log("First");
});

button.addEventListener("click", () => {
    console.log("Second");
});
```

Output:

```text
First
Second
```

Do not rely on listener registration order as a substitute for explicitly controlling application logic.

---

# 16. Removing an Event Listener

Use:

```javascript
element.removeEventListener(
    "event",
    handler
);
```

Example:

```javascript
function handleClick() {
    console.log("Clicked");
}

button.addEventListener("click", handleClick);

button.removeEventListener("click", handleClick);
```

After removal, the handler no longer responds to that event.

---

# 17. The Function Reference Must Match

This works:

```javascript
function handleClick() {
    console.log("Clicked");
}

button.addEventListener("click", handleClick);

button.removeEventListener("click", handleClick);
```

This does not:

```javascript
button.addEventListener("click", () => {
    console.log("Clicked");
});

button.removeEventListener("click", () => {
    console.log("Clicked");
});
```

These are two different function objects.

---

# 18. Why Named Functions Can Be Useful

Consider:

```javascript
function handleClick() {
    console.log("Clicked");
}

button.addEventListener("click", handleClick);
```

Later:

```javascript
button.removeEventListener("click", handleClick);
```

Because the same function reference is available, the listener can be removed.

---

# 19. Event Listener Options

`addEventListener()` can accept a third argument.

```javascript
element.addEventListener(
    "click",
    handler,
    options
);
```

Example:

```javascript
button.addEventListener(
    "click",
    handleClick,
    {
        once: true
    }
);
```

---

# 20. `once`

The `once` option makes the listener run only once.

```javascript
button.addEventListener(
    "click",
    () => {
        console.log("This runs once");
    },
    {
        once: true
    }
);
```

After the first click, the listener is automatically removed.

Useful for:

* One-time notifications
* Initialization actions
* One-time confirmation actions

---

# 21. `capture`

The `capture` option controls whether the listener participates during the capturing phase.

```javascript
element.addEventListener(
    "click",
    handler,
    {
        capture: true
    }
);
```

Equivalent boolean form:

```javascript
element.addEventListener(
    "click",
    handler,
    true
);
```

For most everyday event handling, the default is:

```javascript
capture: false
```

which means the listener runs during the bubbling phase.

---

# 22. `passive`

A passive listener tells the browser that the handler will not call `preventDefault()`.

```javascript
element.addEventListener(
    "touchstart",
    handleTouch,
    {
        passive: true
    }
);
```

This can help the browser optimize scrolling-related input handling.

If a listener is passive, calling:

```javascript
event.preventDefault();
```

is not allowed to cancel the event.

---

# 23. `signal`

You can associate an event listener with an `AbortController`.

```javascript
const controller = new AbortController();

button.addEventListener(
    "click",
    handleClick,
    {
        signal: controller.signal
    }
);
```

Later:

```javascript
controller.abort();
```

The listener is removed.

This can be useful when a component needs to clean up multiple listeners.

---

# 24. Combining Options

Options can be combined:

```javascript
button.addEventListener(
    "click",
    handleClick,
    {
        once: true,
        capture: false
    }
);
```

Common options include:

```text
once
capture
passive
signal
```

---

# 25. `this` Inside an Event Handler

With a regular function, `this` refers to the element on which the listener was registered.

```javascript
button.addEventListener("click", function () {
    console.log(this);
});
```

Here, `this` refers to the button.

However, arrow functions do not create their own `this`:

```javascript
button.addEventListener("click", () => {
    console.log(this);
});
```

For event handlers, using `event.currentTarget` is often clearer:

```javascript
button.addEventListener("click", (event) => {
    console.log(event.currentTarget);
});
```

---

# 26. `event.target` vs `event.currentTarget`

These are important concepts.

### `event.target`

The element where the event originated.

### `event.currentTarget`

The element whose event listener is currently running.

Example:

```html
<button id="button">
    <span>Save</span>
</button>
```

JavaScript:

```javascript
const button = document.querySelector("#button");

button.addEventListener("click", (event) => {
    console.log(event.target);
    console.log(event.currentTarget);
});
```

If the user clicks the `<span>`:

```text
event.target
    ↓
<span>

event.currentTarget
    ↓
<button>
```

This difference becomes especially important with event bubbling and delegation.

---

# 27. `preventDefault()`

Some browser actions have default behavior.

For example, links navigate:

```html
<a href="/profile" id="profileLink">
    Profile
</a>
```

You can prevent navigation:

```javascript
const link = document.querySelector("#profileLink");

link.addEventListener("click", (event) => {
    event.preventDefault();

    console.log("Navigation prevented");
});
```

---

# 28. `stopPropagation()`

`stopPropagation()` prevents the event from continuing through the DOM event flow.

```javascript
button.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

This is different from:

```javascript
event.preventDefault();
```

### `preventDefault()`

Stops the browser's default action.

### `stopPropagation()`

Stops further event propagation.

---

# 29. `stopImmediatePropagation()`

There is also:

```javascript
event.stopImmediatePropagation();
```

This prevents:

* Further propagation
* Other listeners on the same element from running

Example:

```javascript
button.addEventListener("click", (event) => {
    event.stopImmediatePropagation();

    console.log("First handler");
});
```

This is more aggressive than `stopPropagation()`.

---

# 30. Event Listener on `window`

`addEventListener()` is not limited to HTML elements.

You can listen on `window`:

```javascript
window.addEventListener("resize", () => {
    console.log(window.innerWidth);
});
```

---

# 31. Event Listener on `document`

You can listen on the document:

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.key);
});
```

This is useful for document-wide keyboard interactions.

---

# 32. Event Listener on Dynamic Elements

Suppose JavaScript creates a button:

```javascript
const button = document.createElement("button");

button.textContent = "Delete";

button.addEventListener("click", () => {
    console.log("Delete clicked");
});

document.body.append(button);
```

The newly created element can immediately receive event listeners.

---

# 33. Event Listener with DOM Creation

Example:

```javascript
const button = document.createElement("button");

button.textContent = "Remove";

button.addEventListener("click", () => {
    button.remove();
});

document.body.append(button);
```

The button removes itself when clicked.

---

# 34. Event Listener Cleanup

In applications with dynamically created components, listeners may need cleanup when the component is no longer needed.

One approach:

```javascript
function handleClick() {
    console.log("Clicked");
}

button.addEventListener("click", handleClick);

// Later
button.removeEventListener("click", handleClick);
```

Another approach uses `AbortController`:

```javascript
const controller = new AbortController();

button.addEventListener("click", handleClick, {
    signal: controller.signal
});

// Cleanup
controller.abort();
```

---

# 35. Practical Example: Toggle Menu

HTML:

```html
<button id="menuButton">
    Menu
</button>

<nav id="menu">
    Navigation
</nav>
```

CSS:

```css
.hidden {
    display: none;
}
```

JavaScript:

```javascript
const button = document.querySelector("#menuButton");
const menu = document.querySelector("#menu");

button.addEventListener("click", () => {
    menu.classList.toggle("hidden");
});
```

The event listener changes the menu state whenever the button is clicked.

---

# 36. Practical Example: Form Handling

```javascript
const form = document.querySelector("#loginForm");

form.addEventListener("submit", async (event) => {
    event.preventDefault();

    const formData = new FormData(form);

    console.log(formData);
});
```

The form is handled by JavaScript instead of following the browser's default submission behavior.

---

# 37. Practical Example: Search

```javascript
const search = document.querySelector("#search");

search.addEventListener("input", (event) => {
    const query = event.target.value.trim();

    console.log("Query:", query);
});
```

Using `event.target` means the handler does not need to separately reference the input.

---

# 38. Practical Example: Keyboard Shortcut

```javascript
document.addEventListener("keydown", (event) => {
    if (event.ctrlKey && event.key === "s") {
        event.preventDefault();

        console.log("Custom save action");
    }
});
```

This detects:

```text
Ctrl + S
```

and prevents the browser's normal save-page behavior.

---

# 39. Common Mistakes

### Mistake 1: Calling the handler

Wrong:

```javascript
button.addEventListener("click", handleClick());
```

Correct:

```javascript
button.addEventListener("click", handleClick);
```

---

### Mistake 2: Using `onclick` as the event name

Wrong:

```javascript
button.addEventListener("onclick", handleClick);
```

Correct:

```javascript
button.addEventListener("click", handleClick);
```

---

### Mistake 3: Removing a different function

Wrong:

```javascript
button.addEventListener("click", () => {
    console.log("Clicked");
});

button.removeEventListener("click", () => {
    console.log("Clicked");
});
```

The two arrow functions are different objects.

---

### Mistake 4: Confusing `target` and `currentTarget`

```javascript
event.target
```

is where the event originated.

```javascript
event.currentTarget
```

is the element whose listener is currently executing.

---

### Mistake 5: Using `preventDefault()` for propagation

This:

```javascript
event.preventDefault();
```

does not stop bubbling.

For propagation control:

```javascript
event.stopPropagation();
```

---

# 40. Key Takeaways

* `addEventListener()` registers an event handler.
* The first argument is the event type.
* The second argument is the handler function.
* Pass a function reference instead of calling the function immediately.
* Multiple listeners can be registered.
* `removeEventListener()` removes a listener when given the same function reference and matching listener options.
* `once` automatically removes a listener after its first invocation.
* `capture` controls whether the listener participates in capturing.
* `passive` indicates that the listener will not call `preventDefault()`.
* `signal` can connect a listener to an `AbortController`.
* `event.target` is the event's originating target.
* `event.currentTarget` is the element whose listener is currently running.
* `preventDefault()` stops a default browser action.
* `stopPropagation()` controls event propagation.
* `addEventListener()` works with elements, `document`, and `window`.

---

