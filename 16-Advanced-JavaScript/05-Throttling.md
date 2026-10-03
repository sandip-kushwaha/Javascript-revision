# JavaScript Throttling

**Throttling** is a technique that limits how often a function can execute within a specific time interval.

It is useful when an event fires many times in a short period.

Common examples:

* Scroll events
* Resize events
* Mouse movement
* Pointer movement
* Dragging
* Window events
* Frequent UI updates

---

# 1. The Problem

Some browser events can fire many times very quickly.

For example:

```javascript
window.addEventListener("scroll", () => {
    console.log(window.scrollY);
});
```

While scrolling, this function may execute many times.

If the function performs expensive work, it can affect performance.

Throttling limits how frequently the function runs.

---

# 2. Basic Throttle

A simple throttle implementation:

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function (...args) {
        const now = Date.now();

        if (now - lastCall < delay) {
            return;
        }

        lastCall = now;

        callback(...args);
    };
}
```

Usage:

```javascript
const handleScroll = throttle(() => {
    console.log("Scrolling...");
}, 200);
```

Then:

```javascript
window.addEventListener(
    "scroll",
    handleScroll
);
```

The callback can execute at most once during each 200ms interval.

---

# 3. How Throttling Works

Suppose the delay is:

```text
200ms
```

The event fires repeatedly:

```text
Event
 ↓
Execute
 ↓
Events ignored during 200ms
 ↓
200ms passes
 ↓
Next event can execute
 ↓
Events ignored during 200ms
 ↓
Repeat
```

The important idea:

```text
Many calls
     ↓
Controlled execution
     ↓
One execution per interval
```

---

# 4. Timeline Example

Suppose an event fires at:

```text
0ms
50ms
100ms
150ms
200ms
250ms
300ms
```

With:

```text
delay = 200ms
```

A simple leading throttle may execute around:

```text
0ms
200ms
400ms
...
```

Calls between allowed executions are ignored.

The exact behavior depends on the throttle implementation.

---

# 5. Scroll Example

```javascript
function updateScrollPosition() {
    console.log(
        "Scroll:",
        window.scrollY
    );
}

const handleScroll = throttle(
    updateScrollPosition,
    200
);

window.addEventListener(
    "scroll",
    handleScroll
);
```

Instead of responding to every scroll event, the handler executes at a controlled frequency.

---

# 6. Mouse Movement

Mouse movement can generate many events.

```javascript
const handleMouseMove = throttle(
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

The function will not execute for every mouse movement event.

---

# 7. Resize Example

```javascript
const handleResize = throttle(() => {
    console.log(
        window.innerWidth,
        window.innerHeight
    );
}, 200);

window.addEventListener(
    "resize",
    handleResize
);
```

This is useful when resize calculations are expensive.

---

# 8. Passing Arguments

A throttle function can forward arguments.

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function (...args) {
        const now = Date.now();

        if (now - lastCall < delay) {
            return;
        }

        lastCall = now;

        callback(...args);
    };
}
```

Example:

```javascript
const handleMove = throttle(
    (x, y) => {
        console.log(x, y);
    },
    100
);

handleMove(100, 200);
```

The `...args` collects the arguments and passes them to the callback.

---

# 9. Leading Throttle

The basic throttle shown above is commonly called a **leading throttle**.

It executes immediately when the first allowed call occurs.

Example:

```text
Call
 ↓
Execute immediately
 ↓
Block repeated calls
 ↓
Delay expires
 ↓
Allow another call
```

This is useful when the first event should be handled immediately.

---

# 10. Trailing Throttle

Sometimes you also want the latest event to execute after the waiting period.

For example:

```text
Events:
A → B → C → D

Throttle interval:
     ↓

Execute A immediately

Wait

Execute D after interval
```

Here:

* The first event is handled immediately.
* The latest event can be handled after the interval.

This can be useful when the final state matters.

---

# 11. Leading and Trailing Throttle

A more complete throttle can support both behaviors.

```javascript
function throttle(
    callback,
    delay,
    options = {}
) {
    let timer = null;
    let lastArgs;
    let lastThis;
    let lastCallTime = 0;

    const leading = options.leading !== false;
    const trailing = options.trailing !== false;

    function throttled(...args) {
        const now = Date.now();

        if (!lastCallTime && !leading) {
            lastCallTime = now;
        }

        const remaining =
            delay - (now - lastCallTime);

        lastArgs = args;
        lastThis = this;

        if (remaining <= 0) {
            if (timer) {
                clearTimeout(timer);
                timer = null;
            }

            lastCallTime = now;

            callback.apply(
                lastThis,
                lastArgs
            );

            lastArgs = null;
            lastThis = null;
        } else if (!timer && trailing) {
            timer = setTimeout(() => {
                lastCallTime =
                    leading
                        ? Date.now()
                        : 0;

                timer = null;

                callback.apply(
                    lastThis,
                    lastArgs
                );

                lastArgs = null;
                lastThis = null;
            }, remaining);
        }
    }

    return throttled;
}
```

Usage:

```javascript
const handleScroll = throttle(
    () => {
        console.log(window.scrollY);
    },
    200,
    {
        leading: true,
        trailing: true
    }
);
```

For learning the concept, the simple throttle implementation is usually enough.

---

# 12. Throttle vs Debounce

Both techniques control frequent function calls, but they behave differently.

| Throttle                     | Debounce                              |
| ---------------------------- | ------------------------------------- |
| Limits execution frequency   | Waits for activity to stop            |
| Can execute repeatedly       | Usually executes once after the pause |
| Good for scrolling           | Good for search                       |
| Good for mouse movement      | Good for autocomplete                 |
| Good for continuous events   | Good for final input state            |
| Runs at controlled intervals | Runs after a quiet period             |

Simple rule:

```text
Throttle
→ "Run periodically."

Debounce
→ "Wait until activity stops."
```

---

# 13. When to Use Throttling

Throttling is useful when the application needs updates while the event is still happening.

Examples:

```text
User scrolling
       ↓
Update scroll progress

User dragging
       ↓
Update position

User moving mouse
       ↓
Update coordinates

User resizing
       ↓
Update layout

User moving pointer
       ↓
Update UI
```

The important point is that the application still needs periodic updates during the activity.

---

# 14. When Not to Use Throttling

Throttling is not always necessary.

For a small operation:

```javascript
window.addEventListener("resize", () => {
    console.log(window.innerWidth);
});
```

the normal event handler may be sufficient.

Do not add throttling just because an event fires frequently.

Use it when repeated execution causes unnecessary work or performance problems.

---

# 15. Throttling with `requestAnimationFrame`

For visual updates, `requestAnimationFrame()` can be useful.

Example:

```javascript
let ticking = false;

window.addEventListener("scroll", () => {
    if (!ticking) {
        requestAnimationFrame(() => {
            updateUI();

            ticking = false;
        });

        ticking = true;
    }
});
```

Example function:

```javascript
function updateUI() {
    console.log(window.scrollY);
}
```

This pattern allows the browser to schedule the UI update around its rendering cycle.

---

# 16. `requestAnimationFrame()` vs Time-Based Throttle

A time-based throttle:

```javascript
throttle(callback, 200);
```

controls execution based on a time interval.

`requestAnimationFrame()`:

```javascript
requestAnimationFrame(callback);
```

schedules work for a browser rendering opportunity.

Use `requestAnimationFrame()` when the main goal is smooth visual updates.

Use time-based throttling when you specifically want to limit execution frequency.

---

# 17. Throttling API Requests

Throttling can also limit how frequently requests are started.

For example:

```javascript
const sendRequest = throttle(
    async (query) => {
        const response = await fetch(
            `/api/search?q=${encodeURIComponent(query)}`
        );

        const data = await response.json();

        console.log(data);
    },
    500
);
```

However, throttling does not automatically cancel requests that are already running.

For situations where old requests are no longer useful, consider:

```text
Throttle
+
AbortController
```

---

# 18. Throttling in a Hotel Dashboard

Suppose your hotel dashboard displays a live scroll or drag interaction.

For example:

```javascript
const handleTableDrag = throttle(
    (event) => {
        console.log(
            event.clientX,
            event.clientY
        );
    },
    100
);
```

Then:

```javascript
tableElement.addEventListener(
    "pointermove",
    handleTableDrag
);
```

Instead of processing every pointer event, the application processes them at a controlled frequency.

This can help reduce unnecessary UI work.

---

# 19. Throttling a Scroll Progress Bar

HTML:

```html
<div id="progress"></div>
```

JavaScript:

```javascript
const progress = document.querySelector(
    "#progress"
);

const updateProgress = throttle(() => {
    const scrollTop =
        window.scrollY;

    const documentHeight =
        document.documentElement.scrollHeight;

    const viewportHeight =
        window.innerHeight;

    const scrollable =
        documentHeight - viewportHeight;

    const percentage =
        (scrollTop / scrollable) * 100;

    progress.style.width =
        `${percentage}%`;
}, 100);

window.addEventListener(
    "scroll",
    updateProgress
);
```

The progress bar updates periodically instead of responding to every scroll event.

---

# 20. Throttling and React

In React, the important issue is keeping the throttled function stable.

A simple approach is to perform throttling inside an effect:

```jsx
import { useEffect } from "react";

function ScrollTracker() {
    useEffect(() => {
        let lastCall = 0;

        const handleScroll = () => {
            const now = Date.now();

            if (now - lastCall < 200) {
                return;
            }

            lastCall = now;

            console.log(
                window.scrollY
            );
        };

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

    return null;
}
```

The cleanup removes the event listener when the component unmounts.

---

# 21. Cleanup Matters

When using throttling with event listeners, remember to remove the listener when it is no longer needed.

```javascript
window.addEventListener(
    "scroll",
    handleScroll
);
```

Remove it:

```javascript
window.removeEventListener(
    "scroll",
    handleScroll
);
```

The same function reference must be used.

For example:

```javascript
const handleScroll = throttle(
    updateScroll,
    200
);

window.addEventListener(
    "scroll",
    handleScroll
);

window.removeEventListener(
    "scroll",
    handleScroll
);
```

---

# 22. Throttle with `setTimeout`

Another approach uses a timer.

```javascript
function throttle(callback, delay) {
    let waiting = false;

    return function (...args) {
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

Usage:

```javascript
const handleScroll = throttle(
    () => {
        console.log(
            window.scrollY
        );
    },
    200
);
```

Flow:

```text
Call
 ↓
Execute
 ↓
waiting = true
 ↓
Ignore calls
 ↓
200ms
 ↓
waiting = false
 ↓
Ready again
```

---

# 23. Timestamp vs Timer Throttle

Two common implementations are:

### Timestamp-based

```javascript
const now = Date.now();

if (now - lastCall >= delay) {
    lastCall = now;
    callback();
}
```

### Timer-based

```javascript
if (!waiting) {
    callback();

    waiting = true;

    setTimeout(() => {
        waiting = false;
    }, delay);
}
```

Both can be useful.

The exact behavior differs around leading and trailing execution.

---

# 24. Choosing the Interval

There is no single correct throttle interval.

Common values include:

```text
50ms
100ms
200ms
300ms
```

The correct value depends on the work being performed.

For example:

```text
Animation-related work
→ shorter interval or requestAnimationFrame

Expensive calculations
→ potentially longer interval

API requests
→ based on API and UX requirements
```

Always balance:

```text
Responsiveness
+
CPU usage
+
Network usage
```

---

# 25. Throttling Does Not Mean Parallel Execution

Throttling controls how frequently a function is started.

It does not automatically make the function asynchronous or parallel.

For example:

```javascript
const handleScroll = throttle(
    () => {
        expensiveCalculation();
    },
    200
);
```

The calculation still runs on the JavaScript thread.

If the calculation itself is very expensive, throttling reduces how often it runs but does not make each execution faster.

---

# 26. Throttling vs Request Cancellation

Consider:

```text
Request A starts
      ↓
Request B starts later
      ↓
Request A finishes later
```

Throttling controls when requests start.

It does not automatically cancel Request A.

For APIs where older results are no longer useful, request cancellation can be handled separately with:

```javascript
AbortController
```

---

# 27. Common Throttling Mistakes

## Mistake 1 — Creating the throttle repeatedly

Avoid recreating the throttle state unnecessarily.

```javascript
const handler = throttle(
    callback,
    200
);
```

The same throttled function should normally remain attached to the event.

---

## Mistake 2 — Forgetting cleanup

In component-based applications, remove event listeners when the component is destroyed.

```javascript
window.removeEventListener(
    "scroll",
    handler
);
```

---

## Mistake 3 — Using throttle when debounce is needed

If you only need the final result after activity stops, debounce may be more appropriate.

Example:

```text
Search input
→ debounce
```

For continuous updates:

```text
Scroll position
→ throttle
```

---

# 28. Throttle Flow

```text
Event occurs
      ↓
Check last execution
      ↓
Interval available?
   ┌──┴──┐
  Yes    No
   ↓      ↓
Execute  Ignore
   ↓
Update last execution
      ↓
Wait for next interval
```

---

# 29. Throttle vs Debounce Example

Imagine a user scrolls for three seconds.

### Throttle

```text
Scroll
 ↓
Run
 ↓
Wait
 ↓
Run
 ↓
Wait
 ↓
Run
 ↓
Continue
```

### Debounce

```text
Scroll
 ↓
Timer
 ↓
More scroll
 ↓
Reset timer
 ↓
More scroll
 ↓
Reset timer
 ↓
Scrolling stops
 ↓
Run once
```

So:

```text
Continuous updates → Throttle

Final result after activity → Debounce
```

---

# 30. Key Takeaways

* Throttling limits how frequently a function executes.
* It is useful for high-frequency events.
* Common uses include scroll, resize, mousemove, and pointermove.
* A simple throttle can use `Date.now()` to track the last execution.
* Another implementation can use `setTimeout()`.
* Leading throttle executes immediately when allowed.
* Trailing throttle can execute the latest call after the interval.
* `requestAnimationFrame()` is useful for visual updates.
* Throttling does not automatically cancel running requests.
* `AbortController` can be used separately for request cancellation.
* Event listeners should be cleaned up when no longer needed.
* Choose the interval based on responsiveness and workload.
* Use throttle for continuous activity.
* Use debounce when you mainly care about the final state after activity stops.

---

# Quick Cheat Sheet

```text
Throttle
    ↓
Limit function execution frequency
    ↓
Run periodically while activity continues
```

Basic pattern:

```javascript
function throttle(callback, delay) {
    let lastCall = 0;

    return function (...args) {
        const now = Date.now();

        if (now - lastCall < delay) {
            return;
        }

        lastCall = now;

        callback(...args);
    };
}
```

Common uses:

```text
Scroll
Resize
Mouse movement
Pointer movement
Dragging
Frequent UI updates
```

Remember:

```text
Throttle
→ run at controlled intervals

Debounce
→ wait for a pause
```

---
