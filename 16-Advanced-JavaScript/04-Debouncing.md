# JavaScript Debouncing

**Debouncing** is a technique that delays function execution until a certain amount of time has passed without another call.

It is useful when a function could be called many times in a short period.

Common examples:

* Search input
* Autocomplete
* Window resize
* Form validation
* API requests
* Filtering large datasets

---

# 1. The Problem

Consider a search input:

```javascript
searchInput.addEventListener("input", () => {
    searchProducts();
});
```

If the user types:

```text
l
la
lap
lapt
lapto
laptop
```

the function may run six times.

For an API search, this could produce six requests.

Debouncing allows us to wait until the user stops typing.

---

# 2. Basic Debounce

```javascript
function debounce(callback, delay) {
    let timer;

    return function (...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Usage:

```javascript
const search = debounce(() => {
    console.log("Searching...");
}, 500);
```

Now:

```javascript
search();
search();
search();
```

does not immediately execute the callback.

Each new call resets the timer.

---

# 3. How Debouncing Works

Suppose the delay is:

```text
500ms
```

The user triggers the function repeatedly:

```text
Call 1
  ↓
500ms timer starts

Call 2
  ↓
Timer reset

Call 3
  ↓
Timer reset

Call 4
  ↓
Timer reset

No more calls
  ↓
500ms passes
  ↓
Callback executes
```

The important idea:

```text
New call → reset timer
No new call → execute after delay
```

---

# 4. Search Input Example

HTML:

```html
<input
    id="search"
    type="text"
    placeholder="Search products"
/>
```

JavaScript:

```javascript
const input = document.querySelector("#search");

const searchProducts = debounce((event) => {
    console.log("Searching:", event.target.value);
}, 500);

input.addEventListener(
    "input",
    searchProducts
);
```

Now the search runs after the user pauses typing for 500ms.

---

# 5. Passing Arguments

The debounce function can forward arguments:

```javascript
function debounce(callback, delay) {
    let timer;

    return function (...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Example:

```javascript
const logSearch = debounce((query) => {
    console.log("Search:", query);
}, 500);

logSearch("lap");
logSearch("laptop");
```

Only the latest call's arguments are used when the timer finally executes.

---

# 6. Returning the Debounced Function

The function:

```javascript
debounce(callback, delay);
```

returns another function.

Example:

```javascript
const handleSearch = debounce(
    searchProducts,
    500
);
```

This returned function controls when:

```javascript
searchProducts();
```

is actually executed.

---

# 7. Debouncing API Requests

A common use case is search.

```javascript
const searchProducts = debounce(
    async (query) => {
        if (!query.trim()) {
            return;
        }

        const response = await fetch(
            `/api/products?search=${encodeURIComponent(query)}`
        );

        const products = await response.json();

        console.log(products);
    },
    500
);
```

Then:

```javascript
input.addEventListener(
    "input",
    (event) => {
        searchProducts(event.target.value);
    }
);
```

The API is called after the user stops typing.

---

# 8. Debouncing Form Validation

Suppose an email field is validated while the user types.

Without debouncing:

```javascript
emailInput.addEventListener("input", validateEmail);
```

Validation may run on every keystroke.

With debouncing:

```javascript
const validateEmailLater = debounce(
    validateEmail,
    300
);

emailInput.addEventListener(
    "input",
    validateEmailLater
);
```

This reduces unnecessary validation work.

---

# 9. Debouncing Window Resize

Resize events can fire many times while the user changes the browser size.

```javascript
const handleResize = debounce(() => {
    console.log(
        window.innerWidth,
        window.innerHeight
    );
}, 300);

window.addEventListener(
    "resize",
    handleResize
);
```

The function executes after resizing pauses.

---

# 10. Debouncing with React

A simple React example:

```jsx
import { useEffect, useState } from "react";

function Search() {
    const [query, setQuery] = useState("");

    useEffect(() => {
        const timer = setTimeout(() => {
            if (query.trim()) {
                console.log("Search:", query);
            }
        }, 500);

        return () => {
            clearTimeout(timer);
        };
    }, [query]);

    return (
        <input
            value={query}
            onChange={(event) => {
                setQuery(event.target.value);
            }}
        />
    );
}
```

The cleanup:

```javascript
clearTimeout(timer);
```

cancels the previous timer when `query` changes.

This is a common React debouncing pattern.

---

# 11. Reusable React Debounce Hook

For repeated use, you can create a custom hook:

```jsx
import { useEffect, useState } from "react";

function useDebounce(value, delay) {
    const [debouncedValue, setDebouncedValue] =
        useState(value);

    useEffect(() => {
        const timer = setTimeout(() => {
            setDebouncedValue(value);
        }, delay);

        return () => {
            clearTimeout(timer);
        };
    }, [value, delay]);

    return debouncedValue;
}
```

Usage:

```jsx
function Search() {
    const [query, setQuery] = useState("");

    const debouncedQuery = useDebounce(
        query,
        500
    );

    useEffect(() => {
        if (!debouncedQuery.trim()) {
            return;
        }

        console.log(
            "Search:",
            debouncedQuery
        );
    }, [debouncedQuery]);

    return (
        <input
            value={query}
            onChange={(event) => {
                setQuery(event.target.value);
            }}
        />
    );
}
```

The component updates immediately, while the search uses the delayed value.

---

# 12. Debounce vs Throttle

These techniques solve different problems.

| Debounce                   | Throttle                     |
| -------------------------- | ---------------------------- |
| Waits for activity to stop | Limits execution frequency   |
| Runs after a pause         | Runs at controlled intervals |
| Good for search            | Good for scrolling           |
| Good for autocomplete      | Good for mouse movement      |
| Good for validation        | Good for resize handling     |

Simple rule:

```text
Debounce
→ "Wait until the user stops."

Throttle
→ "Run at most once during an interval."
```

---

# 13. Debounce with Leading Execution

The basic debounce waits until the calls stop.

Sometimes you want the function to execute immediately on the first call and then ignore repeated calls until the delay expires.

Conceptually:

```text
First call
   ↓
Execute immediately
   ↓
Block repeated calls
   ↓
Delay expires
   ↓
Ready again
```

Example:

```javascript
function debounceLeading(callback, delay) {
    let timer;

    return function (...args) {
        const shouldCallNow = !timer;

        clearTimeout(timer);

        timer = setTimeout(() => {
            timer = undefined;
        }, delay);

        if (shouldCallNow) {
            callback(...args);
        }
    };
}
```

Usage:

```javascript
const handleClick = debounceLeading(
    () => {
        console.log("Clicked");
    },
    1000
);
```

---

# 14. Leading vs Trailing

### Trailing debounce

The function executes after activity stops.

```text
Calls → Calls → Calls → Pause → Execute
```

This is the common search-input behavior.

### Leading debounce

The function executes immediately, then waits before allowing another execution.

```text
Call → Execute → Block → Delay → Ready
```

The choice depends on the interaction you are building.

---

# 15. Canceling a Debounced Call

A useful debounce implementation can expose a `cancel()` method.

```javascript
function debounce(callback, delay) {
    let timer;

    function debounced(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    }

    debounced.cancel = () => {
        clearTimeout(timer);
        timer = undefined;
    };

    return debounced;
}
```

Usage:

```javascript
const search = debounce(
    (query) => {
        console.log(query);
    },
    500
);

search("laptop");

search.cancel();
```

The pending callback is canceled.

---

# 16. Why `clearTimeout()` Matters

Without:

```javascript
clearTimeout(timer);
```

every call creates another timer.

For example:

```javascript
function badDebounce(callback, delay) {
    return function (...args) {
        setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Calling:

```javascript
search("l");
search("la");
search("lap");
search("laptop");
```

creates four timers.

That is not proper debouncing.

---

# 17. Debouncing and API Performance

Suppose a search field generates:

```text
l
la
lap
lapt
lapto
laptop
```

Without debouncing:

```text
6 input events
↓
6 API requests
```

With a 500ms debounce and the user typing continuously:

```text
6 input events
↓
timer repeatedly reset
↓
1 API request
```

This can reduce unnecessary network traffic.

However, debouncing does not replace:

* Server-side rate limiting
* Request cancellation
* Caching
* Validation
* Authentication
* Authorization

---

# 18. Debouncing vs Request Cancellation

Debouncing prevents many requests from being started.

But a previous request may already be running.

For example:

```text
Search "lap"
    ↓
Request starts

Search "laptop"
    ↓
New request starts
```

The first request may still finish later.

For search applications, you may combine debouncing with:

```javascript
AbortController
```

to cancel outdated requests.

---

# 19. Debounced Fetch with AbortController

```javascript
let controller;

const searchProducts = debounce(
    async (query) => {
        controller?.abort();

        controller = new AbortController();

        try {
            const response = await fetch(
                `/api/products?search=${encodeURIComponent(query)}`,
                {
                    signal: controller.signal
                }
            );

            if (!response.ok) {
                throw new Error(
                    "Request failed"
                );
            }

            const data = await response.json();

            console.log(data);
        } catch (error) {
            if (error.name === "AbortError") {
                return;
            }

            console.error(error);
        }
    },
    500
);
```

This gives two levels of control:

```text
Debounce
→ delay new requests

AbortController
→ cancel outdated requests
```

---

# 20. Choosing a Delay

There is no universal debounce delay.

Common values might be:

```text
200ms
300ms
500ms
700ms
```

The appropriate value depends on the interaction.

For example:

```text
Search/autocomplete
→ often a few hundred milliseconds

Expensive validation
→ possibly longer

Resize calculations
→ depends on UI complexity
```

The goal is to balance:

```text
Responsiveness
+
Reduced work
```

---

# 21. Common Debounce Mistake

Creating the debounce function repeatedly can defeat the purpose.

For example, in React, avoid recreating uncontrolled debounce state on every render.

Instead, use:

* A `useEffect` timer pattern.
* A stable debounced function.
* A well-designed custom hook.

The important requirement is that the timer survives long enough to be reset by subsequent calls.

---

# 22. Debouncing Search in a Hotel System

For a hotel dashboard, consider a table search:

```text
User types:
T
T-
T-0
T-03
```

Instead of requesting:

```text
GET /tables?search=T
GET /tables?search=T-
GET /tables?search=T-0
GET /tables?search=T-03
```

you can debounce the search:

```text
T
 ↓
timer

T-
 ↓
reset

T-0
 ↓
reset

T-03
 ↓
reset

pause
 ↓
GET /tables?search=T-03
```

This is useful for admin dashboards with server-side searching.

---

# 23. Debouncing Client-Side Filtering

Debouncing can also be used without an API.

```javascript
const filterProducts = debounce(
    (query) => {
        const result = products.filter(
            product =>
                product.name
                    .toLowerCase()
                    .includes(query.toLowerCase())
        );

        renderProducts(result);
    },
    200
);
```

This can be useful when filtering a large dataset is relatively expensive.

For small arrays, debouncing may add unnecessary complexity.

---

# 24. Debouncing and Event Frequency

Some browser events can fire very frequently:

```text
input
resize
scroll
mousemove
pointermove
```

Debouncing is useful when only the final state matters.

For example:

```text
Resize
→ wait until resizing stops
→ calculate final layout
```

For continuously updating UI, throttling may be more appropriate.

---

# 25. Important Characteristics

A debounced function:

* Delays execution.
* Resets its timer when called again.
* Usually executes once after calls stop.
* Can forward arguments.
* Can expose cancellation.
* Is commonly implemented with `setTimeout()`.
* Uses `clearTimeout()` to reset pending execution.
* Is useful for reducing unnecessary work.
* Does not automatically cancel already-running asynchronous requests.
* Can be combined with `AbortController` for request cancellation.

---

# 26. Basic Debounce Pattern

```javascript
function debounce(callback, delay) {
    let timer;

    return (...args) => {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Usage:

```javascript
const search = debounce(
    (query) => {
        console.log(query);
    },
    500
);

search("j");
search("ja");
search("jav");
search("java");
```

Only the final call is executed after the delay if the calls occur before the timer expires.

---

# 27. Debounce Flow

```text
Function called
      ↓
Clear previous timer
      ↓
Start new timer
      ↓
Another call?
   ┌──┴──┐
  Yes    No
   ↓      ↓
Reset   Wait
timer     ↓
        Execute
```

---

# 28. Key Takeaways

* Debouncing delays execution until calls stop for a specified period.
* Each new call resets the timer.
* `setTimeout()` schedules the delayed execution.
* `clearTimeout()` cancels the previous scheduled execution.
* Search boxes are one of the most common use cases.
* Debouncing can reduce unnecessary API requests.
* Debouncing can also be used for resize and validation events.
* Trailing debounce runs after activity stops.
* Leading debounce can run immediately and then wait.
* A debounced function can expose a `cancel()` method.
* Debouncing does not cancel requests that have already started.
* `AbortController` can cancel outdated Fetch requests.
* In React, `useEffect` cleanup is a simple way to implement debouncing.
* Debouncing and throttling are different techniques.

---

# Quick Cheat Sheet

```text
Debounce
    ↓
Wait until activity stops
    ↓
Execute once
```

Basic pattern:

```javascript
function debounce(callback, delay) {
    let timer;

    return (...args) => {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Common uses:

```text
Search
Autocomplete
Form validation
Resize
Expensive filtering
API requests
```

Remember:

```text
Debounce  → wait for a pause
Throttle  → limit execution frequency
```

---
