# JavaScript Event Capturing

**Event capturing** is one phase of DOM event propagation.

When an event occurs on a deeply nested element, the event can travel **from the outer elements toward the target** before reaching the target.

The simplified event flow is:

```text
1. Capturing Phase
        ↓
2. Target Phase
        ↓
3. Bubbling Phase
```

For example:

```text
document
    ↓
body
    ↓
parent
    ↓
button
    ↑
parent
    ↑
body
    ↑
document
```

The downward part is **capturing**.

The upward part is **bubbling**.

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

parent.addEventListener(
    "click",
    () => {
        console.log("Parent");
    },
    true
);

child.addEventListener("click", () => {
    console.log("Child");
});
```

Clicking the button can produce:

```text
Parent
Child
```

The `true` tells the browser to use the capturing phase for that listener.

---

# 2. Capturing vs Bubbling

### Capturing

The event travels from ancestor toward target:

```text
Parent
   ↓
Child
```

### Bubbling

The event travels from target toward ancestor:

```text
Child
   ↑
Parent
```

---

# 3. Event Propagation Phases

A simplified event propagation model contains three phases.

```text
Capturing
    ↓
Target
    ↓
Bubbling
```

Example:

```text
document
    ↓
body
    ↓
div
    ↓
button
    ↑
div
    ↑
body
    ↑
document
```

The event reaches the target after capturing and can then bubble back through ancestors.

---

# 4. Enabling Capturing

The third argument of `addEventListener()` can enable capturing.

```javascript
element.addEventListener(
    "click",
    handler,
    true
);
```

The equivalent options object is:

```javascript
element.addEventListener(
    "click",
    handler,
    {
        capture: true
    }
);
```

The options object is usually easier to understand when several options are involved.

---

# 5. `capture: true`

Example:

```javascript
parent.addEventListener(
    "click",
    () => {
        console.log("Parent capture");
    },
    {
        capture: true
    }
);
```

This listener participates in the capturing phase.

---

# 6. Capturing Example with Multiple Levels

HTML:

```html
<div id="grandparent">
    <div id="parent">
        <button id="child">
            Click
        </button>
    </div>
</div>
```

JavaScript:

```javascript
const grandparent = document.querySelector("#grandparent");
const parent = document.querySelector("#parent");
const child = document.querySelector("#child");

grandparent.addEventListener(
    "click",
    () => {
        console.log("Grandparent");
    },
    true
);

parent.addEventListener(
    "click",
    () => {
        console.log("Parent");
    },
    true
);

child.addEventListener("click", () => {
    console.log("Child");
});
```

Clicking the button results in:

```text
Grandparent
Parent
Child
```

The capturing listeners run while the event travels toward the target.

---

# 7. Capturing and `event.target`

During capturing, `event.target` still represents the original event target.

```javascript
parent.addEventListener(
    "click",
    (event) => {
        console.log(event.target);
    },
    true
);
```

If the button was clicked:

```text
event.target
    ↓
button
```

It does not change simply because the event is currently in the capturing phase.

---

# 8. Capturing and `event.currentTarget`

`event.currentTarget` represents the element whose listener is currently executing.

```javascript
parent.addEventListener(
    "click",
    (event) => {
        console.log(event.currentTarget);
    },
    true
);
```

Here:

```text
event.currentTarget
    ↓
parent
```

So:

```text
event.target
    → Original event source

event.currentTarget
    → Current listener's element
```

---

# 9. Capturing Listener vs Bubbling Listener

You can register listeners for different phases.

```javascript
parent.addEventListener(
    "click",
    () => {
        console.log("Capture");
    },
    {
        capture: true
    }
);

parent.addEventListener(
    "click",
    () => {
        console.log("Bubble");
    }
);
```

The first listener participates in capturing.

The second uses the default bubbling phase.

---

# 10. Capturing and Target Phase

Suppose:

```html
<div id="parent">
    <button id="button">
        Click
    </button>
</div>
```

You can add both capturing and normal listeners:

```javascript
parent.addEventListener(
    "click",
    () => {
        console.log("Parent capture");
    },
    true
);

button.addEventListener("click", () => {
    console.log("Button");
});

parent.addEventListener("click", () => {
    console.log("Parent bubble");
});
```

A simplified output is:

```text
Parent capture
Button
Parent bubble
```

This demonstrates:

```text
Capturing
    ↓
Target
    ↓
Bubbling
```

---

# 11. Stopping Propagation During Capturing

You can stop propagation during the capturing phase.

```javascript
parent.addEventListener(
    "click",
    (event) => {
        event.stopPropagation();

        console.log("Parent capture");
    },
    true
);
```

The event will not continue normally beyond that point in the propagation path.

Use this carefully because it can prevent other code from receiving the event.

---

# 12. `stopPropagation()` vs `preventDefault()`

These methods have different purposes.

### `stopPropagation()`

Controls event propagation:

```javascript
event.stopPropagation();
```

### `preventDefault()`

Prevents the browser's default action:

```javascript
event.preventDefault();
```

For example:

```javascript
link.addEventListener("click", (event) => {
    event.preventDefault();
});
```

prevents navigation.

It does not mean:

```javascript
event.stopPropagation();
```

---

# 13. Capturing with `addEventListener()`

The modern and readable approach is:

```javascript
element.addEventListener(
    "click",
    handler,
    {
        capture: true
    }
);
```

Instead of:

```javascript
element.addEventListener(
    "click",
    handler,
    true
);
```

Both can enable capturing, but the options object makes the purpose clearer.

---

# 14. Capturing with Other Options

Options can be combined:

```javascript
button.addEventListener(
    "click",
    handleClick,
    {
        capture: true,
        once: true
    }
);
```

This means:

```text
capture: true
→ Use capturing phase

once: true
→ Run only once
```

---

# 15. Capturing and `once`

Example:

```javascript
parent.addEventListener(
    "click",
    () => {
        console.log("Runs once during capture");
    },
    {
        capture: true,
        once: true
    }
);
```

After the first invocation, the listener is removed.

---

# 16. Capturing and `passive`

You can also combine:

```javascript
element.addEventListener(
    "touchstart",
    handleTouch,
    {
        capture: true,
        passive: true
    }
);
```

Remember that a passive listener should not attempt to cancel the event with:

```javascript
event.preventDefault();
```

---

# 17. Capturing on `document`

You can listen for events during capturing from a high level:

```javascript
document.addEventListener(
    "click",
    (event) => {
        console.log("Captured:", event.target);
    },
    {
        capture: true
    }
);
```

This can allow code to observe events while they travel toward their target.

---

# 18. Practical Example: Global Click Observation

```javascript
document.addEventListener(
    "click",
    (event) => {
        console.log("Clicked:", event.target);
    },
    {
        capture: true
    }
);
```

This can be useful for application-level event handling.

However, global listeners should be designed carefully so they do not interfere with unrelated components.

---

# 19. Capturing and Nested Menus

Suppose:

```html
<div id="menu">
    <button id="profile">
        Profile
    </button>
</div>
```

You can observe clicks during capturing:

```javascript
menu.addEventListener(
    "click",
    (event) => {
        console.log("Menu capture:", event.target);
    },
    {
        capture: true
    }
);
```

The event reaches the menu through the capturing phase before reaching the button.

---

# 20. Capturing and Event Delegation

Event delegation commonly uses bubbling:

```javascript
list.addEventListener("click", handler);
```

Capturing can also be used:

```javascript
list.addEventListener(
    "click",
    handler,
    {
        capture: true
    }
);
```

However, capturing and bubbling have different event-flow behavior, so choose the phase based on what the application needs.

---

# 21. When Capturing Is Useful

Event capturing can be useful when:

* You need to observe an event before it reaches a descendant.
* You need parent-level control during the capture phase.
* You are working with complex nested components.
* You need to understand or control event propagation.
* You are building custom interaction systems.

For ordinary button and form handlers, the default bubbling phase is usually sufficient.

---

# 22. Capturing vs Bubbling Example

HTML:

```html
<div id="parent">
    <button id="button">
        Click
    </button>
</div>
```

JavaScript:

```javascript
const parent = document.querySelector("#parent");
const button = document.querySelector("#button");

parent.addEventListener(
    "click",
    () => {
        console.log("Capture");
    },
    {
        capture: true
    }
);

button.addEventListener("click", () => {
    console.log("Target");
});

parent.addEventListener("click", () => {
    console.log("Bubble");
});
```

Clicking the button:

```text
Capture
Target
Bubble
```

This represents the simplified propagation order.

---

# 23. A Complete Event Flow

Consider:

```text
document
    |
    ↓
body
    |
    ↓
div
    |
    ↓
button
```

When the button is clicked:

### Capturing

```text
document
    ↓
body
    ↓
div
```

### Target

```text
button
```

### Bubbling

```text
div
    ↑
body
    ↑
document
```

So the complete simplified flow is:

```text
document
   ↓
body
   ↓
div
   ↓
button
   ↑
div
   ↑
body
   ↑
document
```

---

# 24. Important Note About Event Flow

The actual DOM event system has more details than this simplified diagram.

For everyday JavaScript, remember:

```text
Capturing → Target → Bubbling
```

And:

```text
capture: true
```

makes a listener participate during the capturing phase.

The exact propagation path can also involve details such as the window, document, shadow DOM, and event-specific behavior.

---

# 25. Common Mistakes

## Mistake 1: Confusing `capture` with `preventDefault()`

Wrong idea:

```javascript
{
    capture: true
}
```

does not prevent the browser's default action.

It only controls which propagation phase the listener participates in.

---

## Mistake 2: Thinking all events bubble

Not every event bubbles.

Always consider the behavior of the specific event.

---

## Mistake 3: Confusing target and currentTarget

Remember:

```javascript
event.target
```

means the original event source.

```javascript
event.currentTarget
```

means the element whose listener is currently executing.

---

## Mistake 4: Using `true` without understanding it

This:

```javascript
element.addEventListener("click", handler, true);
```

enables capture.

For readability, you can write:

```javascript
element.addEventListener(
    "click",
    handler,
    {
        capture: true
    }
);
```

---

# 26. Capturing and Bubbling Comparison

| Feature                | Capturing                                  | Bubbling                       |
| ---------------------- | ------------------------------------------ | ------------------------------ |
| Direction              | Ancestor → Target                          | Target → Ancestor              |
| Default listener phase | No                                         | Yes                            |
| Enable with            | `capture: true`                            | Default                        |
| Useful for             | Observing before target                    | Delegation and parent handling |
| Example                | `addEventListener(..., { capture: true })` | `addEventListener(...)`        |

---

# 27. Key Takeaways

* Event capturing is the first major phase of event propagation.
* Events travel from ancestors toward the target during capturing.
* Use `capture: true` to register a listener for the capturing phase.
* `event.target` remains the original event source.
* `event.currentTarget` identifies the element whose listener is executing.
* After the target phase, many events continue through the bubbling phase.
* `stopPropagation()` controls propagation.
* `preventDefault()` controls the browser's default action.
* Not every event bubbles.
* Most everyday event handlers use the default bubbling phase.
* Understanding capturing is important for advanced DOM event handling.

---
