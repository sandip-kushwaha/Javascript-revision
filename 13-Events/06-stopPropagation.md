# JavaScript `stopPropagation()`

`stopPropagation()` is an event method used to stop an event from continuing through the DOM's propagation path.

```javascript
event.stopPropagation();
```

It is mainly used with **event bubbling** and **event capturing**.

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
    console.log("Parent");
});

child.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("Child");
});
```

Clicking the button:

```text
Child
```

The event does not bubble to the parent.

---

# 2. What Does `stopPropagation()` Do?

Normally:

```text
button
   ↑
parent
   ↑
body
   ↑
document
```

With:

```javascript
event.stopPropagation();
```

the propagation can stop at the point where the method is called.

```text
button
   ↑
STOP
```

It prevents the event from continuing to other nodes in the propagation path.

---

# 3. Event Propagation

A simplified event flow is:

```text
Capturing
    ↓
Target
    ↓
Bubbling
```

`stopPropagation()` can stop propagation during either phase.

---

# 4. Stop Bubbling

This is one of the most common uses.

```javascript
child.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

Without it:

```text
Child
  ↓
Parent
  ↓
Grandparent
```

With it:

```text
Child
  ↓
STOP
```

---

# 5. Stop Propagation During Capturing

It can also be used during capturing.

```javascript
parent.addEventListener(
    "click",
    (event) => {
        event.stopPropagation();

        console.log("Parent capture");
    },
    {
        capture: true
    }
);
```

The event will not continue normally through the remaining propagation path.

---

# 6. `stopPropagation()` Does Not Prevent Default Actions

This is very important.

`stopPropagation()`:

```javascript
event.stopPropagation();
```

controls event propagation.

`preventDefault()`:

```javascript
event.preventDefault();
```

prevents a browser's default action when the event is cancelable.

They solve different problems.

---

# 7. Example: Link

HTML:

```html
<a href="/dashboard" id="dashboardLink">
    Dashboard
</a>
```

To stop the event from reaching an ancestor:

```javascript
dashboardLink.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

The link can still navigate.

To prevent navigation:

```javascript
dashboardLink.addEventListener("click", (event) => {
    event.preventDefault();
});
```

To do both:

```javascript
dashboardLink.addEventListener("click", (event) => {
    event.preventDefault();
    event.stopPropagation();
});
```

---

# 8. `stopPropagation()` vs `preventDefault()`

| Method                       | Purpose                                                  |
| ---------------------------- | -------------------------------------------------------- |
| `stopPropagation()`          | Stops event propagation                                  |
| `preventDefault()`           | Prevents default browser action                          |
| `stopImmediatePropagation()` | Stops propagation and later listeners on the same target |

---

# 9. `stopImmediatePropagation()`

There is another method:

```javascript
event.stopImmediatePropagation();
```

It is stronger than `stopPropagation()`.

Example:

```javascript
button.addEventListener("click", (event) => {
    event.stopImmediatePropagation();

    console.log("First");
});

button.addEventListener("click", () => {
    console.log("Second");
});
```

The second listener will not run because the first listener called:

```javascript
event.stopImmediatePropagation();
```

---

# 10. Important Difference

### `stopPropagation()`

Stops the event from continuing to other nodes in the propagation path.

It does **not** generally stop other listeners on the same element.

### `stopImmediatePropagation()`

Stops:

* Further propagation
* Remaining listeners on the same target

Example:

```text
stopPropagation()
    ↓
Stops movement to other elements

stopImmediatePropagation()
    ↓
Stops movement
+
Stops remaining listeners on current target
```

---

# 11. Multiple Listeners on One Element

Consider:

```javascript
button.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("First");
});

button.addEventListener("click", () => {
    console.log("Second");
});
```

Both listeners on the same button can still run.

`stopPropagation()` does not mean:

> Stop every listener immediately.

For that behavior:

```javascript
event.stopImmediatePropagation();
```

is the relevant method.

---

# 12. Parent and Child Example

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

Clicking Delete:

```text
Delete clicked
```

The card does not receive the bubbled click.

---

# 13. Why This Can Be Useful

Suppose a card has its own click behavior:

```javascript
card.addEventListener("click", () => {
    openDetails();
});
```

Inside the card there is a delete button:

```javascript
deleteButton.addEventListener("click", () => {
    deleteItem();
});
```

Without controlling propagation:

```text
Click Delete
    ↓
Delete item
    ↓
Card click also runs
    ↓
Details may open
```

You can prevent the card's click handler from receiving the event:

```javascript
deleteButton.addEventListener("click", (event) => {
    event.stopPropagation();

    deleteItem();
});
```

---

# 14. Practical Card Example

HTML:

```html
<div class="card" id="productCard">
    <h3>Laptop</h3>

    <button id="deleteButton">
        Delete
    </button>
</div>
```

JavaScript:

```javascript
const card = document.querySelector("#productCard");
const deleteButton = document.querySelector("#deleteButton");

card.addEventListener("click", () => {
    console.log("Open product details");
});

deleteButton.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("Delete product");
});
```

Result:

### Click card

```text
Open product details
```

### Click Delete

```text
Delete product
```

The delete click does not bubble to the card.

---

# 15. Nested Elements

Consider:

```html
<div id="outer">
    <div id="middle">
        <button id="inner">
            Click
        </button>
    </div>
</div>
```

Listeners:

```javascript
outer.addEventListener("click", () => {
    console.log("Outer");
});

middle.addEventListener("click", () => {
    console.log("Middle");
});

inner.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("Inner");
});
```

Clicking the button:

```text
Inner
```

The event does not continue to:

```text
Middle
Outer
```

---

# 16. Capturing Example

Suppose listeners use capturing:

```javascript
outer.addEventListener(
    "click",
    (event) => {
        console.log("Outer capture");

        event.stopPropagation();
    },
    {
        capture: true
    }
);

middle.addEventListener(
    "click",
    () => {
        console.log("Middle capture");
    },
    {
        capture: true
    }
);

inner.addEventListener("click", () => {
    console.log("Inner");
});
```

When the button is clicked, propagation can be stopped during the capture phase.

The exact listeners that run depend on where propagation is stopped and the event's propagation path.

---

# 17. `event.target` Still Works

Stopping propagation does not change the event target.

```javascript
button.addEventListener("click", (event) => {
    console.log(event.target);

    event.stopPropagation();
});
```

`event.target` still represents the original event source.

---

# 18. `event.currentTarget` Still Works

Inside the handler:

```javascript
button.addEventListener("click", (event) => {
    console.log(event.currentTarget);

    event.stopPropagation();
});
```

`event.currentTarget` still refers to the element whose listener is executing.

---

# 19. `stopPropagation()` Does Not Remove the Listener

Calling:

```javascript
event.stopPropagation();
```

does not permanently remove the event listener.

The listener remains registered.

```javascript
button.addEventListener("click", handleClick);
```

Calling:

```javascript
event.stopPropagation();
```

only affects the current event's propagation.

It does not do:

```javascript
button.removeEventListener(...);
```

---

# 20. Future Events Still Work

Example:

```javascript
button.addEventListener("click", (event) => {
    event.stopPropagation();

    console.log("Clicked");
});
```

If the button is clicked three times:

```text
Clicked
Clicked
Clicked
```

The listener still runs for future events.

`stopPropagation()` affects the current event dispatch.

---

# 21. Event Delegation Consideration

Event delegation normally depends on bubbling.

Example:

```javascript
const list = document.querySelector("#list");

list.addEventListener("click", (event) => {
    const item = event.target.closest(".item");

    if (!item) {
        return;
    }

    console.log("Item clicked");
});
```

If a child listener calls:

```javascript
event.stopPropagation();
```

the event may never reach the delegated listener on the parent.

Therefore, stopping propagation can interfere with event delegation.

---

# 22. Example with Dynamic List

HTML:

```html
<ul id="users">
    <li class="user">
        Sandip
        <button class="delete">Delete</button>
    </li>
</ul>
```

Parent listener:

```javascript
users.addEventListener("click", (event) => {
    const deleteButton = event.target.closest(".delete");

    if (!deleteButton) {
        return;
    }

    console.log("Delete user");
});
```

If another child listener does:

```javascript
event.stopPropagation();
```

the parent listener may not receive the event.

This is why propagation should not be stopped unnecessarily.

---

# 23. Avoid Using It Everywhere

It can be tempting to solve every event problem with:

```javascript
event.stopPropagation();
```

This is usually not a good approach.

Excessive use can make event behavior harder to understand because other components may depend on the event reaching their ancestors.

Use it when there is a clear propagation requirement.

---

# 24. Practical Modal Example

Suppose clicking the background closes a modal:

```javascript
modal.addEventListener("click", () => {
    closeModal();
});
```

But clicking inside the modal content should not close it:

```javascript
modalContent.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

Now:

```text
Click background
    ↓
Close modal

Click modal content
    ↓
Propagation stopped
    ↓
Modal remains open
```

---

# 25. Practical Dropdown Example

```javascript
document.addEventListener("click", () => {
    closeDropdown();
});

dropdown.addEventListener("click", (event) => {
    event.stopPropagation();
});
```

This can keep the dropdown open when the user interacts with its contents.

However, in larger applications, a more explicit state-management approach may be easier to maintain than relying heavily on propagation control.

---

# 26. Common Mistake: Confusing It with Listener Removal

Wrong assumption:

```javascript
event.stopPropagation();
```

means:

```text
Remove this listener
```

It does not.

Listener removal requires:

```javascript
element.removeEventListener("click", handler);
```

---

# 27. Common Mistake: Confusing It with Default Actions

Wrong assumption:

```javascript
event.stopPropagation();
```

prevents:

* Link navigation
* Form submission
* Checkbox changes
* Other browser default actions

It does not generally do that.

Use:

```javascript
event.preventDefault();
```

when the goal is to cancel a cancelable default action.

---

# 28. Common Mistake: Using It to Fix Every Event Problem

If a component behaves unexpectedly, first understand:

```text
Where did the event start?
        ↓
Which listeners receive it?
        ↓
Which propagation phase are they using?
        ↓
Is bubbling required?
```

Then decide whether `stopPropagation()` is actually necessary.

---

# 29. Quick Comparison

| Method                       | Main Purpose                                                   |
| ---------------------------- | -------------------------------------------------------------- |
| `stopPropagation()`          | Stop propagation to other nodes                                |
| `stopImmediatePropagation()` | Stop propagation and remaining listeners on the current target |
| `preventDefault()`           | Cancel a default browser action                                |
| `removeEventListener()`      | Remove a registered listener                                   |

---

# 30. Event Flow Summary

Normal bubbling:

```text
Button
   ↑
Parent
   ↑
Document
```

With `stopPropagation()` on the button:

```text
Button
   ↑
STOP
```

With capturing:

```text
Document
   ↓
Parent
   ↓
Button
```

If propagation is stopped during capture:

```text
Document
   ↓
STOP
```

---

# 31. Key Takeaways

* `stopPropagation()` controls event propagation.
* It can stop an event from continuing to ancestor elements.
* It works during both capturing and bubbling.
* It does not prevent the browser's default action.
* It does not remove the event listener.
* It does not normally stop other listeners on the same target.
* `stopImmediatePropagation()` also stops remaining listeners on the current target.
* Excessive use can make event handling difficult to understand.
* It can interfere with event delegation because delegation often depends on bubbling.
* Use it when there is a clear reason to stop propagation.

---

