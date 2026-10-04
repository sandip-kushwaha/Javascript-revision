# Debouncing in JavaScript

**Debouncing** is a technique that delays a function until a specified amount of time has passed without another call to that function.

It is useful when an event can happen many times in a short period.

Common examples:

* Search input
* Autocomplete
* API requests
* Form validation
* Window resize
* Input fields
* Filtering data

---

# 1. The Problem

Suppose we have a search input:

```html
<input id="search" type="text" />
```

If the user types:

```text
J
Ja
Jav
Java
Javas
JavaS
JavaSc
JavaScr
JavaScript
```

the `input` event can fire many times.

Without debouncing:

```javascript
const search = document.querySelector("#search");

search.addEventListener("input", () => {
    console.log("Search API called");
});
```

The function can execute for every keystroke.

---

# 2. Why This Can Be a Problem

Imagine every input sends an API request:

```text
J
 ↓
API request

Ja
 ↓
API request

Jav
 ↓
API request

Java
 ↓
API request
```

A user typing one search term can generate many requests.

This can cause:

```text
Unnecessary API requests
More server work
More network traffic
Slower applications
Poor user experience
```

---

# 3. Debouncing Concept

With debouncing:

```text
User types
    ↓
Wait
    ↓
User types again
    ↓
Reset timer
    ↓
Wait
    ↓
User types again
    ↓
Reset timer
    ↓
User stops typing
    ↓
Delay finishes
    ↓
Function executes
```

The function runs only after the activity stops for the specified delay.

---

# 4. Simple Example

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Create a debounced function:

```javascript
const search = debounce(() => {
    console.log("Search API called");
}, 500);
```

Use it:

```javascript
search();
```

If `search()` is called repeatedly within 500 milliseconds, the timer keeps getting reset.

---

# 5. How `clearTimeout()` Helps

Consider:

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Every call does:

```text
clear previous timer
        ↓
create new timer
```

Therefore, only the latest timer can normally reach the callback after the user stops triggering the function.

---

# 6. Timeline Example

Suppose the delay is:

```text
500ms
```

User actions:

```text
0ms    → type J
100ms  → type Ja
200ms  → type Jav
300ms  → type Java
400ms  → type JavaS
```

Each action resets the timer.

After the final action:

```text
400ms
  ↓
wait 500ms
  ↓
900ms
  ↓
callback executes
```

The callback does not execute at:

```text
0ms
100ms
200ms
300ms
400ms
```

It executes after the final delay.

---

# 7. Search Example

HTML:

```html
<input
    id="search"
    type="text"
    placeholder="Search users"
/>
```

JavaScript:

```javascript
const searchInput =
    document.querySelector("#search");

function searchUsers(value) {
    console.log("Searching:", value);
}

const debouncedSearch = debounce(
    searchUsers,
    500
);

searchInput.addEventListener(
    "input",
    (event) => {
        debouncedSearch(event.target.value);
    }
);
```

Now the search function waits until the user stops typing.

---

# 8. Debouncing API Requests

Suppose:

```javascript
async function searchUsers(query) {
    const response = await fetch(
        `/api/users?search=${encodeURIComponent(query)}`
    );

    const users = await response.json();

    console.log(users);
}
```

Create a debounced version:

```javascript
const debouncedSearch = debounce(
    searchUsers,
    500
);
```

Then:

```javascript
searchInput.addEventListener(
    "input",
    (event) => {
        debouncedSearch(event.target.value);
    }
);
```

This prevents an API request from being sent for every keystroke.

---

# 9. Complete Search Example

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}

async function searchUsers(query) {
    if (!query.trim()) {
        return;
    }

    const response = await fetch(
        `/api/users?search=${encodeURIComponent(query)}`
    );

    const users = await response.json();

    console.log(users);
}

const searchInput =
    document.querySelector("#search");

const debouncedSearch = debounce(
    searchUsers,
    500
);

searchInput.addEventListener(
    "input",
    (event) => {
        debouncedSearch(event.target.value);
    }
);
```

---

# 10. Passing Arguments

A good debounce implementation should preserve function arguments.

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Now:

```javascript
function greet(name) {
    console.log(`Hello ${name}`);
}

const debouncedGreet = debounce(
    greet,
    500
);

debouncedGreet("Sandip");
```

The argument `"Sandip"` is passed to the original function.

---

# 11. Using `this`

If a debounced function needs to preserve the calling context, use `apply()`:

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        const context = this;

        timer = setTimeout(() => {
            callback.apply(context, args);
        }, delay);
    };
}
```

This preserves the original `this` value when the callback runs.

---

# 12. Debouncing and Function Calls

Suppose:

```javascript
const debouncedFunction = debounce(
    () => {
        console.log("Executed");
    },
    1000
);
```

Then:

```javascript
debouncedFunction();
debouncedFunction();
debouncedFunction();
```

If these calls happen before the 1-second delay completes, the timer is repeatedly reset.

The callback executes after the final call and the delay expires.

---

# 13. Debouncing Form Validation

Suppose a username field needs validation.

Without debouncing:

```javascript
input.addEventListener(
    "input",
    validateUsername
);
```

Validation can happen on every keystroke.

With debouncing:

```javascript
const debouncedValidation =
    debounce(
        validateUsername,
        400
    );

input.addEventListener(
    "input",
    (event) => {
        debouncedValidation(
            event.target.value
        );
    }
);
```

This can reduce unnecessary validation work.

---

# 14. Debouncing Window Resize

The `resize` event can fire many times while the browser window is being resized.

Without debouncing:

```javascript
window.addEventListener(
    "resize",
    () => {
        console.log("Resize");
    }
);
```

With debouncing:

```javascript
const handleResize = debounce(
    () => {
        console.log(
            "Resize finished"
        );
    },
    300
);

window.addEventListener(
    "resize",
    handleResize
);
```

The callback executes after resizing stops for 300 milliseconds.

---

# 15. Debouncing Search Filters

Suppose a product list contains many items:

```javascript
const products = [
    {
        name: "Laptop",
        price: 800
    },
    {
        name: "Mouse",
        price: 20
    },
    {
        name: "Keyboard",
        price: 50
    }
];
```

Instead of filtering on every single keystroke:

```javascript
function filterProducts(query) {
    return products.filter(
        (product) =>
            product.name
                .toLowerCase()
                .includes(query.toLowerCase())
    );
}
```

Use:

```javascript
const debouncedFilter = debounce(
    filterProducts,
    300
);
```

This is useful when filtering work is expensive or events occur very frequently.

---

# 16. Debouncing in React

A simple React example:

```jsx
import { useEffect, useState } from "react";

function Search() {
    const [query, setQuery] = useState("");

    useEffect(() => {
        const timer = setTimeout(() => {
            if (query.trim()) {
                console.log(
                    "Search:",
                    query
                );
            }
        }, 500);

        return () => {
            clearTimeout(timer);
        };
    }, [query]);

    return (
        <input
            value={query}
            onChange={(event) =>
                setQuery(event.target.value)
            }
        />
    );
}
```

Here:

```text
User types
    ↓
query changes
    ↓
effect runs
    ↓
timer starts
    ↓
another change
    ↓
previous timer is cleared
    ↓
new timer starts
```

The search runs after the user stops typing.

---

# 17. React Debounced API Search

```jsx
import {
    useEffect,
    useState
} from "react";

function SearchUsers() {
    const [query, setQuery] =
        useState("");

    const [users, setUsers] =
        useState([]);

    useEffect(() => {
        if (!query.trim()) {
            setUsers([]);
            return;
        }

        const timer = setTimeout(
            async () => {
                const response =
                    await fetch(
                        `/api/users?search=${encodeURIComponent(query)}`
                    );

                const data =
                    await response.json();

                setUsers(data);
            },
            500
        );

        return () => {
            clearTimeout(timer);
        };
    }, [query]);

    return (
        <div>
            <input
                value={query}
                onChange={(event) =>
                    setQuery(
                        event.target.value
                    )
                }
            />

            {users.map((user) => (
                <p key={user.id}>
                    {user.name}
                </p>
            ))}
        </div>
    );
}
```

The cleanup function prevents an old timer from continuing after the query changes.

---

# 18. Debouncing with API Cancellation

Debouncing controls when a request starts, but it does not automatically cancel a request that has already started.

For requests that may overlap, `AbortController` can help.

```javascript
let controller;

async function searchUsers(query) {
    if (controller) {
        controller.abort();
    }

    controller = new AbortController();

    const response = await fetch(
        `/api/users?search=${encodeURIComponent(query)}`,
        {
            signal: controller.signal
        }
    );

    return response.json();
}
```

You can combine request cancellation with debouncing for more robust search behavior.

---

# 19. Debouncing vs Delaying

Debouncing is not simply:

```javascript
setTimeout(...);
```

The important part is:

```javascript
clearTimeout(previousTimer);
```

Every new call cancels the previous scheduled execution.

Conceptually:

```text
Normal delay:

Call
 ↓
Wait
 ↓
Execute

Debounce:

Call
 ↓
Start timer
 ↓
New call
 ↓
Cancel old timer
 ↓
Start new timer
 ↓
No more calls
 ↓
Execute
```

---

# 20. Leading and Trailing Execution

A basic debounce usually executes on the **trailing edge**.

That means:

```text
Wait for activity to stop
        ↓
Execute
```

Some debounce implementations also support **leading execution**:

```text
First call
   ↓
Execute immediately
   ↓
Ignore repeated calls
   ↓
Wait for the debounce period
```

Leading and trailing behavior depends on the implementation.

---

# 21. Basic Trailing Debounce

The implementation used above:

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Behavior:

```text
Call
 ↓
Wait
 ↓
Another call
 ↓
Reset
 ↓
Wait
 ↓
No more calls
 ↓
Execute
```

---

# 22. Debounce with `cancel()`

A more complete implementation can expose a cancel method:

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
    };

    return debounced;
}
```

Use:

```javascript
const search = debounce(
    searchUsers,
    500
);
```

Cancel:

```javascript
search.cancel();
```

This can be useful when a component or feature is being removed.

---

# 23. Choosing a Delay

There is no universal delay.

Common values might be:

```text
200ms
300ms
400ms
500ms
```

The appropriate value depends on the application.

For search:

```text
300–500ms
```

is often a reasonable starting point.

But always consider:

```text
Network speed
API cost
User experience
Amount of computation
Expected typing speed
```

---

# 24. When to Use Debouncing

Debouncing is useful when you care about the **final state after activity stops**.

Examples:

```text
Search input
Autocomplete
API search
Form validation
Window resize
Expensive filtering
Autosave after typing stops
```

---

# 25. When Not to Use Debouncing

Do not debounce every event.

For example, some interactions need immediate feedback:

```text
Button click
Checkbox change
Simple local state update
Keyboard controls requiring immediate response
```

Adding a delay where it is unnecessary can make an interface feel slow.

---

# 26. Debouncing vs Throttling

These are different techniques.

| Debouncing                  | Throttling                       |
| --------------------------- | -------------------------------- |
| Waits for activity to stop  | Limits execution frequency       |
| Executes after inactivity   | Executes at controlled intervals |
| Good for search             | Good for scroll                  |
| Good for autocomplete       | Good for resize                  |
| Good for delayed validation | Good for mouse movement          |

Conceptually:

```text
Debounce
    ↓
Wait until activity stops


Throttle
    ↓
Run at most once per interval
```

---

# 27. Real-World Search Flow

A typical search feature:

```text
User types
    ↓
Input event
    ↓
Debounce
    ↓
Wait 300–500ms
    ↓
Send API request
    ↓
Receive results
    ↓
Display results
```

With request cancellation:

```text
User types
    ↓
Debounce
    ↓
Cancel previous request if needed
    ↓
Send latest request
    ↓
Display latest result
```

---

# 28. Common Mistakes

## Mistake 1: Creating a new timer without clearing the old one

Bad:

```javascript
function debounce(callback, delay) {
    return function(...args) {
        setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

This schedules a new callback every time.

---

## Mistake 2: Forgetting cleanup in React

Bad:

```javascript
useEffect(() => {
    setTimeout(() => {
        console.log("Search");
    }, 500);
}, [query]);
```

Better:

```javascript
useEffect(() => {
    const timer = setTimeout(() => {
        console.log("Search");
    }, 500);

    return () => {
        clearTimeout(timer);
    };
}, [query]);
```

---

# 29. Debounce Pattern

```text
Repeated Events
      ↓
Clear Previous Timer
      ↓
Start New Timer
      ↓
Repeated Event?
   ↙          ↘
 Yes           No
 ↓              ↓
Reset Timer    Wait
                ↓
             Execute
```

---

# 30. Quick Reference

Basic debounce:

```javascript
function debounce(callback, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            callback(...args);
        }, delay);
    };
}
```

Usage:

```javascript
const debouncedSearch =
    debounce(searchUsers, 500);
```

Event:

```javascript
input.addEventListener(
    "input",
    (event) => {
        debouncedSearch(
            event.target.value
        );
    }
);
```

---

# 31. Key Takeaways

* Debouncing delays execution until activity stops for a specified period.
* Every new call resets the timer.
* `clearTimeout()` is the key part of a basic debounce implementation.
* Debouncing is useful for search, autocomplete, validation, filtering, and resize events.
* Debouncing can reduce unnecessary API requests.
* Debouncing does not automatically cancel an API request that has already started.
* `AbortController` can be used when request cancellation is required.
* React effects should clean up debounce timers.
* A trailing debounce executes after the final call and delay.
* Leading debounce behavior executes immediately and then controls subsequent calls.
* Do not debounce interactions that need immediate feedback.
* Debouncing and throttling solve different timing problems.
