# JavaScript Events

An **event** is an action or occurrence that happens in a web page.

JavaScript can detect these events and execute code when they happen.

Examples:

* User clicks a button
* User types in an input
* Mouse moves over an element
* Form is submitted
* Keyboard key is pressed
* Page finishes loading
* An element receives focus
* An input loses focus

The basic idea is:

```text
Event happens
     ↓
JavaScript detects it
     ↓
Event handler runs
     ↓
Application responds
```

---

# 1. What is an Event?

Consider a button:

```html
<button>Click Me</button>
```

When the user clicks it, a **click event** occurs.

JavaScript can respond:

```javascript
const button = document.querySelector("button");

button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

---

# 2. Common JavaScript Events

| Event              | When it happens               |
| ------------------ | ----------------------------- |
| `click`            | Element is clicked            |
| `dblclick`         | Element is double-clicked     |
| `mousedown`        | Mouse button is pressed       |
| `mouseup`          | Mouse button is released      |
| `mousemove`        | Mouse moves                   |
| `mouseenter`       | Mouse enters an element       |
| `mouseleave`       | Mouse leaves an element       |
| `keydown`          | Keyboard key is pressed       |
| `keyup`            | Keyboard key is released      |
| `input`            | Input value changes           |
| `change`           | Value is committed/changed    |
| `focus`            | Element receives focus        |
| `blur`             | Element loses focus           |
| `submit`           | Form is submitted             |
| `reset`            | Form is reset                 |
| `load`             | Resource finishes loading     |
| `DOMContentLoaded` | HTML document has been parsed |

---

# 3. Click Event

The `click` event occurs when an element is clicked.

HTML:

```html
<button id="saveBtn">Save</button>
```

JavaScript:

```javascript
const button = document.querySelector("#saveBtn");

button.addEventListener("click", () => {
    console.log("Saved");
});
```

---

# 4. Double Click Event

Use `dblclick` for double-click actions.

```javascript
const box = document.querySelector(".box");

box.addEventListener("dblclick", () => {
    console.log("Double clicked");
});
```

---

# 5. Mouse Events

JavaScript provides several mouse-related events.

Example:

```javascript
const box = document.querySelector(".box");

box.addEventListener("mouseenter", () => {
    console.log("Mouse entered");
});

box.addEventListener("mouseleave", () => {
    console.log("Mouse left");
});
```

These are commonly used for:

* Hover effects
* Tooltips
* Menus
* Interactive cards

---

# 6. Keyboard Events

Keyboard events allow JavaScript to respond to keyboard activity.

### `keydown`

Runs when a key is pressed:

```javascript
document.addEventListener("keydown", () => {
    console.log("Key pressed");
});
```

### `keyup`

Runs when a key is released:

```javascript
document.addEventListener("keyup", () => {
    console.log("Key released");
});
```

---

# 7. Detecting a Specific Key

You can check which key was pressed:

```javascript
document.addEventListener("keydown", (event) => {
    if (event.key === "Enter") {
        console.log("Enter pressed");
    }
});
```

Another example:

```javascript
document.addEventListener("keydown", (event) => {
    if (event.key === "Escape") {
        console.log("Escape pressed");
    }
});
```

---

# 8. Input Events

The `input` event runs when the value of an input changes as the user types.

HTML:

```html
<input id="search" type="text">
```

JavaScript:

```javascript
const search = document.querySelector("#search");

search.addEventListener("input", () => {
    console.log(search.value);
});
```

If the user types:

```text
JavaScript
```

the event runs as the value changes.

This is useful for:

* Search boxes
* Live validation
* Character counters
* Filtering data

---

# 9. Change Event

The `change` event is commonly used with form controls when their value is changed and committed.

Example:

```html
<select id="category">
    <option value="all">All</option>
    <option value="food">Food</option>
    <option value="drink">Drink</option>
</select>
```

JavaScript:

```javascript
const category = document.querySelector("#category");

category.addEventListener("change", () => {
    console.log(category.value);
});
```

---

# 10. Focus Event

The `focus` event occurs when an element receives focus.

```javascript
const input = document.querySelector("#email");

input.addEventListener("focus", () => {
    console.log("Input focused");
});
```

For example, clicking an input usually gives it focus.

---

# 11. Blur Event

The `blur` event occurs when an element loses focus.

```javascript
input.addEventListener("blur", () => {
    console.log("Input lost focus");
});
```

This is commonly used for:

* Form validation
* Showing hints
* Removing focus states

---

# 12. Form Submit Event

Forms have a `submit` event.

HTML:

```html
<form id="loginForm">
    <input type="email">
    <input type="password">

    <button type="submit">
        Login
    </button>
</form>
```

JavaScript:

```javascript
const form = document.querySelector("#loginForm");

form.addEventListener("submit", (event) => {
    console.log("Form submitted");
});
```

---

# 13. Preventing Default Form Submission

Normally, submitting a form can cause browser navigation or a page reload.

You can prevent the default behavior:

```javascript
form.addEventListener("submit", (event) => {
    event.preventDefault();

    console.log("Form handled by JavaScript");
});
```

This is commonly used when sending form data with `fetch()` or another API client.

---

# 14. Load Event

The `load` event occurs when a resource has finished loading.

For example:

```javascript
window.addEventListener("load", () => {
    console.log("Page resources loaded");
});
```

The `load` event waits for the page's resources, such as images, to finish loading.

---

# 15. `DOMContentLoaded`

`DOMContentLoaded` occurs when the HTML document has been parsed.

```javascript
document.addEventListener("DOMContentLoaded", () => {
    console.log("HTML is ready");
});
```

It does not wait for all images and other resources in the same way that `load` does.

A common use is:

```javascript
document.addEventListener("DOMContentLoaded", () => {
    const button = document.querySelector("#saveBtn");

    button.addEventListener("click", () => {
        console.log("Saved");
    });
});
```

---

# 16. Event Handler

An **event handler** is code that responds to an event.

Example:

```javascript
button.addEventListener("click", () => {
    console.log("Clicked");
});
```

Here:

```text
click
  ↓
event
  ↓
callback function
  ↓
console.log()
```

The callback function handles the event.

---

# 17. `addEventListener()`

The recommended general way to register an event handler is:

```javascript
element.addEventListener(
    "event",
    handler
);
```

Example:

```javascript
button.addEventListener(
    "click",
    () => {
        console.log("Hello");
    }
);
```

The first argument is the event type.

The second argument is the function that should run.

---

# 18. Using a Named Function

Instead of an inline callback:

```javascript
function handleClick() {
    console.log("Button clicked");
}

button.addEventListener("click", handleClick);
```

Notice:

```javascript
handleClick
```

not:

```javascript
handleClick()
```

Passing `handleClick` gives `addEventListener()` the function.

Calling `handleClick()` would execute it immediately.

---

# 19. One Element Can Have Multiple Events

```javascript
const button = document.querySelector("button");

button.addEventListener("click", () => {
    console.log("Clicked");
});

button.addEventListener("mouseenter", () => {
    console.log("Mouse entered");
});

button.addEventListener("mouseleave", () => {
    console.log("Mouse left");
});
```

The same element can respond to different events.

---

# 20. Multiple Handlers for the Same Event

You can register multiple handlers for the same event.

```javascript
button.addEventListener("click", () => {
    console.log("First handler");
});

button.addEventListener("click", () => {
    console.log("Second handler");
});
```

Both handlers can run when the button is clicked.

---

# 21. Event Handler Properties

You may also see:

```javascript
button.onclick = () => {
    console.log("Clicked");
};
```

This works, but assigning the property repeatedly replaces the previous handler.

For example:

```javascript
button.onclick = firstHandler;
button.onclick = secondHandler;
```

Only `secondHandler` remains assigned through `onclick`.

With `addEventListener()`:

```javascript
button.addEventListener("click", firstHandler);
button.addEventListener("click", secondHandler);
```

both handlers can be registered.

For most applications, `addEventListener()` is the more flexible approach.

---

# 22. Common Event Categories

## Mouse Events

```text
click
dblclick
mousedown
mouseup
mousemove
mouseenter
mouseleave
```

## Keyboard Events

```text
keydown
keyup
```

## Form Events

```text
input
change
focus
blur
submit
reset
```

## Document/Window Events

```text
DOMContentLoaded
load
resize
scroll
```

---

# 23. Window Resize Event

You can detect browser window resizing:

```javascript
window.addEventListener("resize", () => {
    console.log("Window resized");
});
```

This can be useful for responsive behavior.

However, resize events can fire many times during one resize operation, so expensive work should be handled carefully.

---

# 24. Scroll Event

You can listen for scrolling:

```javascript
window.addEventListener("scroll", () => {
    console.log(window.scrollY);
});
```

For example, you might use it to:

* Show a back-to-top button
* Change a navbar style
* Load more content
* Track scroll position

For expensive scroll handlers, techniques such as throttling can help.

---

# 25. Event-Driven Programming

JavaScript in the browser is often **event-driven**.

Instead of constantly checking:

```text
Did the user click?
Did the user type?
Did the form submit?
```

you register handlers:

```text
click event  → run function
input event  → run function
submit event → run function
```

This allows the browser to notify your JavaScript when something happens.

---

# 26. Event Flow

When an event occurs on a nested element, the event travels through the DOM.

A simplified flow is:

```text
Window
   ↓
Document
   ↓
Ancestor elements
   ↓
Target element
   ↓
Ancestor elements
   ↑
```

This leads to two important phases:

```text
Capturing
    ↓
Target
    ↓
Bubbling
```

These are covered in more detail in later event files.

---

# 27. Event Target

When an event occurs, JavaScript can identify the element involved.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.target);
});
```

If the button itself was clicked, `event.target` can refer to that button.

The complete event object contains much more information, which is covered in the next file.

---

# 28. Practical Example: Character Counter

HTML:

```html
<textarea id="message"></textarea>

<p>
    Characters:
    <span id="count">0</span>
</p>
```

JavaScript:

```javascript
const message = document.querySelector("#message");
const count = document.querySelector("#count");

message.addEventListener("input", () => {
    count.textContent = message.value.length;
});
```

As the user types, the count updates.

---

# 29. Practical Example: Search Input

HTML:

```html
<input
    id="search"
    type="search"
    placeholder="Search..."
>
```

JavaScript:

```javascript
const search = document.querySelector("#search");

search.addEventListener("input", () => {
    const query = search.value.trim();

    console.log("Searching for:", query);
});
```

This pattern is commonly used in search interfaces.

---

# 30. Practical Example: Enter Key

```javascript
const search = document.querySelector("#search");

search.addEventListener("keydown", (event) => {
    if (event.key === "Enter") {
        console.log("Search submitted");
    }
});
```

This allows the user to press **Enter** instead of clicking a button.

---

# 31. Practical Example: Form Validation

```javascript
const form = document.querySelector("#loginForm");

form.addEventListener("submit", (event) => {
    event.preventDefault();

    const email = document.querySelector("#email");

    if (!email.value.trim()) {
        console.log("Email is required");
        return;
    }

    console.log("Form is valid");
});
```

The form submission is intercepted and handled with JavaScript.

---

# 32. Event Listener Cleanup

You can remove an event listener using:

```javascript
element.removeEventListener(
    "click",
    handleClick
);
```

The function reference must be the same one that was registered.

Example:

```javascript
function handleClick() {
    console.log("Clicked");
}

button.addEventListener("click", handleClick);

// Later
button.removeEventListener("click", handleClick);
```

---

# 33. Event Listener Options

`addEventListener()` can accept a third argument.

For example:

```javascript
element.addEventListener(
    "click",
    handleClick,
    {
        once: true
    }
);
```

With `once: true`, the listener automatically removes itself after running once.

Another option is:

```javascript
element.addEventListener(
    "click",
    handleClick,
    {
        capture: true
    }
);
```

This is related to the event capturing phase.

---

# 34. `once`

Example:

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

After the first click, the listener is removed.

---

# 35. `passive`

Some events can use:

```javascript
element.addEventListener(
    "touchstart",
    handleTouch,
    {
        passive: true
    }
);
```

A passive listener tells the browser that the handler will not call `preventDefault()`.

This can help browser scrolling performance for certain input events.

---

# 36. `signal`

An event listener can also be connected to an `AbortController`.

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

The listener associated with that signal is removed.

This can be useful when cleaning up groups of listeners.

---

# 37. Common Mistakes

### Mistake 1: Calling the handler immediately

Wrong:

```javascript
button.addEventListener("click", handleClick());
```

This calls the function immediately.

Correct:

```javascript
button.addEventListener("click", handleClick);
```

---

### Mistake 2: Forgetting the event name

Wrong:

```javascript
button.addEventListener(handleClick);
```

Correct:

```javascript
button.addEventListener("click", handleClick);
```

---

### Mistake 3: Using `onclick` repeatedly

```javascript
button.onclick = firstHandler;
button.onclick = secondHandler;
```

The second assignment replaces the first.

Prefer:

```javascript
button.addEventListener("click", firstHandler);
button.addEventListener("click", secondHandler);
```

---

### Mistake 4: Forgetting `preventDefault()` for custom form handling

If you want to handle a form submission without the browser's normal navigation behavior:

```javascript
form.addEventListener("submit", (event) => {
    event.preventDefault();

    // Custom logic
});
```

---

# 38. Event Handling Pattern

A common pattern is:

```javascript
const element = document.querySelector("#element");

element.addEventListener("event", (event) => {
    // Handle event
});
```

For example:

```javascript
const button = document.querySelector("#save");

button.addEventListener("click", (event) => {
    console.log("Save clicked");
});
```

---

# 39. Events in Modern Applications

Events are fundamental to frontend applications.

For example, an ecommerce page might use:

```text
Click "Add to Cart"
        ↓
click event
        ↓
Update cart state
        ↓
Update UI
```

A login form:

```text
Submit form
      ↓
submit event
      ↓
Validate input
      ↓
Send API request
      ↓
Show result
```

A search page:

```text
User types
    ↓
input event
    ↓
Read search value
    ↓
Filter / request data
    ↓
Update results
```

---

# 40. Key Takeaways

* An event represents something that happens in the browser.
* `addEventListener()` is the main way to listen for events.
* Common events include `click`, `input`, `change`, `submit`, `keydown`, `focus`, and `blur`.
* An event handler is a function that responds to an event.
* `event.preventDefault()` prevents the browser's default action.
* `event.target` identifies the event's target element.
* `removeEventListener()` removes a registered handler.
* `once` can make a listener run only once.
* Events are a core part of event-driven JavaScript.
* Events can travel through the DOM using capturing and bubbling.

---
