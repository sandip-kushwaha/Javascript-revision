# Throttling in JavaScript

**Throttling** is a performance technique that limits how often a function can execute during a period of frequent events.

It is useful when an event can happen many times in a short period, but we still want the function to run at controlled intervals.

Common examples:

* Scroll events
* Mouse movement
* Window resize
* Dragging
* Touch events
* Continuous UI updates

---

# 1. The Problem

Some browser events can fire many times.

For example:

```javascript
window.addEventListener("scroll", () => {
    console.log("Scrolling");
});
```

While scrolling, this function may execute many times.

This can cause:

```text
Too many function calls
More CPU usage
Unnecessary calculations
Slower UI
Poor performance
```

---

# 2. What Throttling Does

Throttling limits how frequently a function can execute.

For example:

```text
Allow execution
     ↓
Ignore repeated calls
     ↓
Wait for interval
     ↓
Allow execution
     ↓
Ignore repeated calls
     ↓
Wait
```

Suppose the throttle interval is:

```text
500ms
```

The function can execute at most once during each 500ms period.

---

# 3. Simple Example

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function(...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;

            callback(...args);
        }
    };
}
```

Usage:

```javascript
const handleScroll = throttle(() => {
    console.log("Scroll handled");
}, 500);
```

Then:

```javascript
window.addEventListener(
    "scroll",
    handleScroll
);
```

The handler will not execute for every scroll event.

---

# 4. How the Timer Works

Suppose:

```text
delay = 500ms
```

Events occur:

```text
0ms
50ms
100ms
150ms
200ms
300ms
400ms
500ms
```

The throttled function might execute around:

```text
0ms
500ms
```

The events between those executions are limited rather than causing an execution each time.

---

# 5. Timeline

Without throttling:

```text
Event → Function
Event → Function
Event → Function
Event → Function
Event → Function
Event → Function
```

With throttling:

```text
Event → Function
Event
Event
Event
Event
Event → Function
```

The exact execution pattern depends on the throttle implementation.

---

# 6. Scroll Example

HTML:

```html
<div class="content">
    Long content here...
</div>
```

JavaScript:

```javascript
function handleScroll() {
    console.log(window.scrollY);
}

const throttledScroll =
    throttle(handleScroll, 200);

window.addEventListener(
    "scroll",
    throttledScroll
);
```

Instead of processing every scroll event, the application processes them at a controlled rate.

---

# 7. Tracking Scroll Position

```javascript
function updateScrollPosition() {
    const position = window.scrollY;

    console.log(
        "Scroll position:",
        position
    );
}

const throttledUpdate =
    throttle(
        updateScrollPosition,
        100
    );

window.addEventListener(
    "scroll",
    throttledUpdate
);
```

This can be useful for:

* Scroll progress
* Sticky navigation
* Animation calculations
* Lazy loading logic
* Reading indicators

---

# 8. Mouse Movement

Mouse movement can generate many events.

```javascript
document.addEventListener(
    "mousemove",
    (event) => {
        console.log(
            event.clientX,
            event.clientY
        );
    }
);
```

A throttled version:

```javascript
const handleMouseMove =
    throttle(
        (event) => {
            console.log(
                event.clientX,
                event.clientY
            );
        },
        100
    );

document.addEventListener(
    "mousemove",
    handleMouseMove
);
```

This reduces the number of expensive operations.

---

# 9. Window Resize

Resize events can fire repeatedly:

```javascript
window.addEventListener(
    "resize",
    () => {
        console.log(
            window.innerWidth
        );
    }
);
```

Use throttling:

```javascript
const handleResize =
    throttle(
        () => {
            console.log(
                window.innerWidth
            );
        },
        200
    );

window.addEventListener(
    "resize",
    handleResize
);
```

---

# 10. Dragging

Dragging can generate many events.

```javascript
element.addEventListener(
    "mousemove",
    (event) => {
        moveElement(
            event.clientX,
            event.clientY
        );
    }
);
```

Throttle expensive calculations:

```javascript
const handleDrag =
    throttle(
        (event) => {
            moveElement(
                event.clientX,
                event.clientY
            );
        },
        50
    );
```

This can make drag-related operations more controlled.

---

# 11. Passing Arguments

A throttle function should usually pass arguments to the callback.

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function(...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;

            callback(...args);
        }
    };
}
```

Example:

```javascript
function showPosition(x, y) {
    console.log(x, y);
}

const throttledPosition =
    throttle(
        showPosition,
        100
    );

throttledPosition(100, 200);
```

---

# 12. Preserving `this`

When the callback depends on `this`, preserve the calling context.

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function(...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;

            callback.apply(this, args);
        }
    };
}
```

Here:

```javascript
callback.apply(this, args);
```

calls the original function with the current context and arguments.

---

# 13. Throttling API Requests

Throttling can be useful when an application needs controlled requests during continuous activity.

For example:

```text
User scrolls
    ↓
Scroll event
    ↓
Check throttle
    ↓
API request
    ↓
Ignore repeated events
    ↓
Wait
    ↓
Next allowed request
```

However, for search input, debouncing is often more appropriate because the desired behavior is usually to wait until typing stops.

---

# 14. Throttling Scroll-Based Data Loading

Imagine a long list:

```text
Page
 ↓
User scrolls
 ↓
Check position
 ↓
Throttle
 ↓
Check whether more data is needed
 ↓
Load next page
```

Example:

```javascript
function checkForMoreData() {
    const nearBottom =
        window.innerHeight +
        window.scrollY >=
        document.body.offsetHeight - 500;

    if (nearBottom) {
        console.log(
            "Load more data"
        );
    }
}

const throttledCheck =
    throttle(
        checkForMoreData,
        200
    );

window.addEventListener(
    "scroll",
    throttledCheck
);
```

---

# 15. Throttle with a Timer

Another common implementation uses `setTimeout()`.

```javascript
function throttle(callback, delay) {
    let waiting = false;

    return function(...args) {
        if (waiting) {
            return;
        }

        callback(...args);

        waiting = true;

        setTimeout(() => {
            waiting = false;
        }, delay);
    };
}
```

The basic behavior is:

```text
First call
   ↓
Execute
   ↓
waiting = true
   ↓
Ignore calls
   ↓
Delay finishes
   ↓
waiting = false
   ↓
Next call can execute
```

---

# 16. Timestamp vs Timer

Two common throttle approaches are:

### Timestamp

```javascript
const now = Date.now();

if (now - lastCall >= delay) {
    // execute
}
```

### Timer

```javascript
if (!waiting) {
    // execute

    waiting = true;

    setTimeout(() => {
        waiting = false;
    }, delay);
}
```

Both can be useful.

The exact behavior around leading and trailing executions can differ.

---

# 17. Leading Execution

A common throttle behavior executes immediately on the first call.

```text
First event
    ↓
Execute immediately
    ↓
Block repeated calls
    ↓
Wait for interval
    ↓
Allow another execution
```

Example:

```javascript
const throttledScroll =
    throttle(
        handleScroll,
        200
    );
```

The first allowed event can execute immediately.

---

# 18. Trailing Execution

Some throttle implementations also execute the latest event after the interval finishes.

Conceptually:

```text
Event
 ↓
Execute immediately

More events
 ↓
Remember latest event

Interval ends
 ↓
Execute latest event
```

Whether trailing execution is supported depends on the implementation.

---

# 19. Debouncing vs Throttling

This is one of the most important differences.

| Debouncing                        | Throttling                       |
| --------------------------------- | -------------------------------- |
| Waits for activity to stop        | Limits execution frequency       |
| Usually executes after inactivity | Executes at controlled intervals |
| Good for search                   | Good for scrolling               |
| Good for autocomplete             | Good for mouse movement          |
| Good for delayed validation       | Good for dragging                |
| Resets timer on each call         | Limits calls during an interval  |

Simple rule:

```text
Debounce
→ "Wait until the user stops."

Throttle
→ "Don't run too frequently."
```

---

# 20. Example Comparison

### Search

User types:

```text
J
Ja
Jav
Java
JavaScript
```

Usually use:

```text
Debounce
```

because you normally want the search after typing stops.

### Scroll

User continuously scrolls:

```text
scroll
scroll
scroll
scroll
scroll
```

Usually use:

```text
Throttle
```

because you want periodic updates while scrolling.

---

# 21. Throttling in React

For simple React state updates, avoid adding unnecessary throttling.

For expensive browser events, throttling can help.

Example:

```jsx
import {
    useEffect,
    useState
} from "react";

function ScrollTracker() {
    const [scrollY, setScrollY] =
        useState(0);

    useEffect(() => {
        const handleScroll = throttle(
            () => {
                setScrollY(
                    window.scrollY
                );
            },
            100
        );

        window.addEventListener(
            "scroll",
            handleScroll
        );

        return () => {
            window.removeEventListener(
                "scroll",
                handleScroll
            );
        };
    }, []);

    return (
        <p>
            Scroll: {scrollY}px
        </p>
    );
}
```

The event listener is also removed during cleanup.

---

# 22. Important React Consideration

Avoid creating event handlers repeatedly without understanding their lifecycle.

For example, when using a throttled function inside an effect:

```javascript
useEffect(() => {
    const throttledHandler =
        throttle(handleScroll, 100);

    window.addEventListener(
        "scroll",
        throttledHandler
    );

    return () => {
        window.removeEventListener(
            "scroll",
            throttledHandler
        );
    };
}, []);
```

The same function reference is used for:

```text
addEventListener()
```

and:

```text
removeEventListener()
```

This is important for proper cleanup.

---

# 23. Common Mistakes

## Mistake 1: Calling the expensive function directly

Bad:

```javascript
window.addEventListener(
    "scroll",
    expensiveFunction
);
```

when `expensiveFunction` performs heavy work on every event.

Better:

```javascript
const throttledFunction =
    throttle(
        expensiveFunction,
        100
    );

window.addEventListener(
    "scroll",
    throttledFunction
);
```

---

## Mistake 2: Using Debounce When Continuous Updates Are Required

For example, a scroll progress indicator may need periodic updates while scrolling.

Using a long debounce delay can make the UI feel delayed.

Throttle is often more suitable.

---

## Mistake 3: Forgetting Event Cleanup

In applications such as React:

```javascript
window.addEventListener(
    "scroll",
    throttledHandler
);
```

should generally have corresponding cleanup:

```javascript
window.removeEventListener(
    "scroll",
    throttledHandler
);
```

---

# 24. Choosing a Throttle Interval

There is no universal value.

Common starting points:

```text
50ms
100ms
200ms
```

The correct value depends on the task.

Consider:

```text
How expensive is the function?
How frequently does the event fire?
How quickly must the UI respond?
How much delay is acceptable?
```

For visual updates, smaller intervals may feel smoother.

For expensive calculations, a larger interval may reduce work more significantly.

---

# 25. Performance Benefits

Throttling can reduce:

```text
Function calls
CPU usage
DOM calculations
Layout work
API requests
Rendering work
```

For example:

```text
1000 events
     ↓
Throttle
     ↓
100 controlled executions
```

The exact reduction depends on the event frequency and interval.

---

# 26. Real-World Example — Hotel Menu

Suppose your hotel ordering application has a long menu.

A customer scrolls through the menu:

```text
Customer scrolls
      ↓
Scroll events
      ↓
Throttle
      ↓
Check visible section
      ↓
Update active category
```

Instead of recalculating the active category for every scroll event, the calculation can run at controlled intervals.

---

# 27. Real-World Example — Infinite Scroll

A news application can use throttling to check whether the user is near the bottom.

```text
User scrolls
     ↓
Throttle
     ↓
Check scroll position
     ↓
Near bottom?
   ↙       ↘
 Yes        No
 ↓           ↓
Load data   Wait
```

This can help avoid excessive checks.

---

# 28. Real-World Example — Mouse Tracking

A drawing application may receive many mouse movement events:

```text
mousemove
mousemove
mousemove
mousemove
mousemove
```

Throttle can limit expensive calculations:

```javascript
const updateDrawing =
    throttle(
        draw,
        16
    );

canvas.addEventListener(
    "mousemove",
    updateDrawing
);
```

A 16ms interval is roughly one update per 60Hz frame, although actual rendering behavior depends on the application and browser.

---

# 29. Throttle Pattern

```text
Frequent Events
      ↓
Check last execution
      ↓
Interval passed?
   ↙          ↘
 No            Yes
 ↓              ↓
Ignore       Execute
               ↓
          Update timestamp
```

---

# 30. Basic Throttle Implementation

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function(...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;

            callback(...args);
        }
    };
}
```

Usage:

```javascript
const throttledHandler =
    throttle(
        () => {
            console.log("Executed");
        },
        200
    );
```

---

# 31. Quick Reference

### Throttle

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function(...args) {
        const now = Date.now();

        if (now - lastCall >= delay) {
            lastCall = now;

            callback(...args);
        }
    };
}
```

### Scroll

```javascript
const handleScroll =
    throttle(
        () => {
            console.log(
                window.scrollY
            );
        },
        100
    );

window.addEventListener(
    "scroll",
    handleScroll
);
```

### Resize

```javascript
const handleResize =
    throttle(
        () => {
            console.log(
                window.innerWidth
            );
        },
        200
    );

window.addEventListener(
    "resize",
    handleResize
);
```

---

# 32. Key Takeaways

* Throttling limits how frequently a function executes.
* It is useful for high-frequency events.
* Common uses include scroll, resize, mouse movement, and dragging.
* A timestamp-based throttle compares the current time with the previous execution time.
* A timer-based throttle can block execution for a fixed interval.
* Throttling allows periodic execution while an event continues.
* Debouncing usually waits until activity stops.
* Throttling usually allows execution at controlled intervals.
* Use debounce for search and autocomplete in many cases.
* Use throttle for continuous events such as scrolling and mouse movement.
* Always clean up event listeners when appropriate.
* Choose the interval based on performance requirements and user experience.
