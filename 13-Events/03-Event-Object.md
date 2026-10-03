# JavaScript Event Object

The **Event Object** contains information about an event that happened in the browser.

When an event occurs, the browser automatically creates an event object and passes it to the event handler.

```javascript
button.addEventListener("click", (event) => {
    console.log(event);
});
```

The parameter is commonly named:

```javascript
event
```

or:

```javascript
e
```

Both are valid.

---

# 1. Basic Example

```javascript
const button = document.querySelector("#button");

button.addEventListener("click", (event) => {
    console.log(event);
});
```

The `event` object provides information such as:

```text
Event type
Target element
Current target
Mouse position
Keyboard key
Modifier keys
Default behavior
Propagation control
```

The available properties depend on the type of event.

---

# 2. `event.type`

Returns the type of event.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.type);
});
```

Output:

```text
click
```

Another example:

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.type);
});
```

Output:

```text
keydown
```

---

# 3. `event.target`

`event.target` is the element where the event originally occurred.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.target);
});
```

If the button itself is clicked:

```text
event.target → button
```

If a child element inside the button is clicked, the child can become the target.

Example:

```html
<button id="saveButton">
    <span>Save</span>
</button>
```

```javascript
const button = document.querySelector("#saveButton");

button.addEventListener("click", (event) => {
    console.log(event.target);
});
```

Clicking the `<span>` can produce:

```text
<span>Save</span>
```

as the target.

---

# 4. `event.currentTarget`

`event.currentTarget` refers to the element whose listener is currently running.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.currentTarget);
});
```

If the listener is attached to the button:

```text
event.currentTarget → button
```

---

# 5. `target` vs `currentTarget`

Consider:

```html
<button id="button">
    <span>Save</span>
</button>
```

JavaScript:

```javascript
const button = document.querySelector("#button");

button.addEventListener("click", (event) => {
    console.log("Target:", event.target);
    console.log("Current Target:", event.currentTarget);
});
```

If the `<span>` is clicked:

```text
target
    ↓
<span>

currentTarget
    ↓
<button>
```

### Remember

```text
target        → where the event started
currentTarget → where the listener is attached
```

---

# 6. `event.preventDefault()`

`preventDefault()` prevents the browser's default action for a cancelable event.

Example:

```html
<a href="https://example.com" id="link">
    Visit
</a>
```

```javascript
const link = document.querySelector("#link");

link.addEventListener("click", (event) => {
    event.preventDefault();

    console.log("Navigation prevented");
});
```

The link will not perform its normal navigation.

---

# 7. Form Example

```javascript
const form = document.querySelector("#loginForm");

form.addEventListener("submit", (event) => {
    event.preventDefault();

    console.log("Form handled with JavaScript");
});
```

This is commonly used when sending form data through JavaScript or an API.

---

# 8. `event.stopPropagation()`

`stopPropagation()` prevents the event from continuing through the event propagation path.

```javascript
button.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

This is related to event bubbling and capturing.

It does **not** cancel the browser's default action.

---

# 9. `event.stopImmediatePropagation()`

This method is stronger than `stopPropagation()`.

```javascript
event.stopImmediatePropagation();
```

It prevents:

* Further propagation
* Other listeners on the same element from running

Example:

```javascript
button.addEventListener("click", (event) => {
    event.stopImmediatePropagation();

    console.log("First handler");
});
```

---

# 10. `event.defaultPrevented`

This property tells you whether the default action has already been prevented.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.defaultPrevented);
});
```

Normally:

```text
false
```

After:

```javascript
event.preventDefault();
```

it can become:

```text
true
```

---

# 11. `event.bubbles`

This property indicates whether the event is configured to bubble.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.bubbles);
});
```

For many common events such as `click`:

```text
true
```

Not every event bubbles.

---

# 12. `event.cancelable`

This property tells you whether the event's default action can be canceled.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.cancelable);
});
```

If it is `true`, `preventDefault()` can cancel the event's default action.

---

# 13. `event.composed`

For events that cross certain DOM boundaries, such as Shadow DOM boundaries, `composed` indicates whether the event can propagate across that boundary.

```javascript
element.addEventListener("click", (event) => {
    console.log(event.composed);
});
```

This is mainly useful when working with Web Components and Shadow DOM.

---

# 14. Keyboard Event Object

Keyboard events provide additional information.

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event);
});
```

Important properties include:

```text
event.key
event.code
event.altKey
event.ctrlKey
event.shiftKey
event.metaKey
```

---

# 15. `event.key`

`event.key` represents the key value.

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.key);
});
```

Examples:

```text
a
A
Enter
Escape
ArrowUp
ArrowDown
Backspace
```

For example:

```javascript
if (event.key === "Enter") {
    console.log("Enter pressed");
}
```

---

# 16. `event.code`

`event.code` identifies the physical key position.

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.code);
});
```

For example:

```text
KeyA
Enter
Space
ArrowUp
Digit1
```

### `key` vs `code`

```text
event.key
→ What key value was produced?

event.code
→ Which physical keyboard key was pressed?
```

For keyboard shortcuts, `code` can be useful when physical key position matters.

---

# 17. Modifier Keys

Keyboard events provide modifier-key properties.

```javascript
document.addEventListener("keydown", (event) => {
    console.log(event.ctrlKey);
    console.log(event.shiftKey);
    console.log(event.altKey);
    console.log(event.metaKey);
});
```

They return:

```text
true
false
```

depending on whether the modifier is active.

---

# 18. Detecting a Keyboard Shortcut

```javascript
document.addEventListener("keydown", (event) => {
    if (event.ctrlKey && event.key === "s") {
        event.preventDefault();

        console.log("Save shortcut");
    }
});
```

This checks whether:

```text
Ctrl + S
```

was pressed.

---

# 19. Mouse Event Object

Mouse events provide pointer information.

```javascript
button.addEventListener("click", (event) => {
    console.log(event);
});
```

Useful properties include:

```text
clientX
clientY
pageX
pageY
screenX
screenY
button
buttons
```

---

# 20. `clientX` and `clientY`

These represent the pointer position relative to the viewport.

```javascript
document.addEventListener("mousemove", (event) => {
    console.log(event.clientX);
    console.log(event.clientY);
});
```

Conceptually:

```text
clientX → horizontal position in viewport
clientY → vertical position in viewport
```

---

# 21. `pageX` and `pageY`

These represent pointer coordinates relative to the document.

```javascript
document.addEventListener("mousemove", (event) => {
    console.log(event.pageX);
    console.log(event.pageY);
});
```

Unlike viewport coordinates, page coordinates account for document scrolling.

---

# 22. `screenX` and `screenY`

These represent coordinates relative to the user's screen.

```javascript
document.addEventListener("mousemove", (event) => {
    console.log(event.screenX);
    console.log(event.screenY);
});
```

---

# 23. Mouse Button Information

For mouse button events:

```javascript
button.addEventListener("mousedown", (event) => {
    console.log(event.button);
});
```

Common values:

```text
0 → Main button
1 → Middle button
2 → Secondary button
```

---

# 24. `event.buttons`

`event.buttons` can indicate which mouse buttons are currently held down.

```javascript
document.addEventListener("mousemove", (event) => {
    console.log(event.buttons);
});
```

This can be useful for drawing or drag interactions.

---

# 25. Form Event Object

Form controls also provide useful event information.

```javascript
const input = document.querySelector("#username");

input.addEventListener("input", (event) => {
    console.log(event.target.value);
});
```

Here:

```javascript
event.target
```

is the input element.

And:

```javascript
event.target.value
```

is its current value.

---

# 26. Checkbox Example

```javascript
const checkbox = document.querySelector("#terms");

checkbox.addEventListener("change", (event) => {
    console.log(event.target.checked);
});
```

`checked` returns:

```text
true
false
```

---

# 27. Select Example

```javascript
const select = document.querySelector("#category");

select.addEventListener("change", (event) => {
    console.log(event.target.value);
});
```

This is useful when working with category filters, status selectors, and forms.

---

# 28. Event Time Information

Events provide:

```javascript
event.timeStamp
```

Example:

```javascript
button.addEventListener("click", (event) => {
    console.log(event.timeStamp);
});
```

It represents a timestamp associated with the event.

The exact reference point can depend on the browser environment, so it should generally be used for relative timing rather than treated as a Unix timestamp.

---

# 29. Checking Event Properties

You can inspect an event:

```javascript
button.addEventListener("click", (event) => {
    console.log(event.type);
    console.log(event.target);
    console.log(event.currentTarget);
    console.log(event.bubbles);
    console.log(event.cancelable);
});
```

This is useful when learning how browser events work.

---

# 30. Event Object with Named Function

You can also receive the event object in a separate function.

```javascript
function handleClick(event) {
    console.log(event.type);
    console.log(event.target);
}

button.addEventListener("click", handleClick);
```

The browser automatically supplies the event object when it invokes the listener.

---

# 31. Event Object and `addEventListener()`

These concepts work together:

```javascript
element.addEventListener("click", (event) => {
    // event object
});
```

The browser:

```text
1. Detects an event
       ↓
2. Creates/provides event information
       ↓
3. Calls the registered listener
       ↓
4. Passes the event object
```

---

# 32. Practical Example: Clicked Button Text

```javascript
document.querySelectorAll(".action-button").forEach((button) => {
    button.addEventListener("click", (event) => {
        console.log(event.target.textContent);
    });
});
```

If the buttons contain:

```text
Edit
Delete
View
```

the clicked button's text can be read through the event target.

---

# 33. Practical Example: Form Validation

```javascript
const form = document.querySelector("#registerForm");

form.addEventListener("submit", (event) => {
    const username = document.querySelector("#username");

    if (username.value.trim() === "") {
        event.preventDefault();

        console.log("Username is required");
    }
});
```

The event object allows the default submission to be stopped when validation fails.

---

# 34. Practical Example: Keyboard Escape

```javascript
document.addEventListener("keydown", (event) => {
    if (event.key === "Escape") {
        console.log("Close modal");
    }
});
```

This is commonly used for:

* Closing modals
* Closing dropdowns
* Canceling actions
* Exiting overlays

---

# 35. Practical Example: Mouse Position

```javascript
const area = document.querySelector("#area");

area.addEventListener("mousemove", (event) => {
    console.log({
        x: event.clientX,
        y: event.clientY
    });
});
```

This can be used for:

* Drawing applications
* Dragging
* Custom cursor effects
* Interactive visualizations

---

# 36. Important Difference: Event vs Event Handler

An **event** is something that happens.

Examples:

```text
click
keydown
submit
input
change
```

An **event handler** is the function that responds to it.

```javascript
function handleClick(event) {
    console.log("Clicked");
}
```

The event object contains information about that event.

---

# 37. Important Properties Summary

| Property           | Purpose                                |
| ------------------ | -------------------------------------- |
| `type`             | Event type                             |
| `target`           | Original event target                  |
| `currentTarget`    | Element whose listener is running      |
| `bubbles`          | Whether event bubbles                  |
| `cancelable`       | Whether default action can be canceled |
| `defaultPrevented` | Whether default action was prevented   |
| `timeStamp`        | Event timing information               |
| `key`              | Keyboard key value                     |
| `code`             | Physical keyboard key                  |
| `ctrlKey`          | Ctrl pressed                           |
| `shiftKey`         | Shift pressed                          |
| `altKey`           | Alt pressed                            |
| `metaKey`          | Meta/Command/Windows key pressed       |
| `clientX`          | Pointer X relative to viewport         |
| `clientY`          | Pointer Y relative to viewport         |
| `pageX`            | Pointer X relative to document         |
| `pageY`            | Pointer Y relative to document         |
| `screenX`          | Pointer X relative to screen           |
| `screenY`          | Pointer Y relative to screen           |
| `button`           | Mouse button involved                  |
| `buttons`          | Mouse buttons currently pressed        |

---

# 38. Important Methods Summary

| Method                       | Purpose                                                 |
| ---------------------------- | ------------------------------------------------------- |
| `preventDefault()`           | Prevent default browser action                          |
| `stopPropagation()`          | Stop further event propagation                          |
| `stopImmediatePropagation()` | Stop propagation and other listeners on the same target |

---

# 39. Key Takeaways

* The browser provides an **event object** to event listeners.
* The event object contains information about what happened.
* `event.type` tells you the event type.
* `event.target` identifies where the event originated.
* `event.currentTarget` identifies the element whose listener is executing.
* `preventDefault()` prevents a default action when the event is cancelable.
* `stopPropagation()` controls event propagation.
* Keyboard events provide properties such as `key`, `code`, and modifier keys.
* Mouse events provide pointer coordinates and button information.
* Form events can access values through `event.target`.
* Event properties depend on the specific event type.
* Understanding the event object is essential for DOM event handling.

---
