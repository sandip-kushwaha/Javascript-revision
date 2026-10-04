# JavaScript Performance Tips

JavaScript performance means making an application respond quickly while using resources efficiently.

Good performance can improve:

* Page loading
* User experience
* Responsiveness
* Memory usage
* CPU usage
* Network usage
* Battery usage

Performance optimization does not mean making every line of code extremely complex.

The goal is:

```text
Simple Code
    ↓
Efficient Code
    ↓
Fast Application
    ↓
Better User Experience
```

---

# 1. Avoid Unnecessary Work

Do not perform calculations that are not needed.

Instead of repeatedly calculating the same value:

```javascript
function getTotal(price, quantity) {
    return price * quantity;
}

console.log(getTotal(100, 5));
console.log(getTotal(100, 5));
console.log(getTotal(100, 5));
```

If the value does not change, avoid unnecessary repeated work.

---

# 2. Use Efficient Array Methods

For large arrays, unnecessary operations can increase processing time.

Instead of:

```javascript
const activeUsers = users
    .filter(user => user.isActive)
    .map(user => user.name);
```

Sometimes multiple operations are perfectly readable and fast enough.

Do not optimize prematurely.

For very large datasets or expensive operations, consider whether the work can be reduced.

---

# 3. Avoid Unnecessary Loops

Example:

```javascript
const numbers = [1, 2, 3, 4, 5];

for (const number of numbers) {
    console.log(number);
}
```

Do not create multiple loops when one pass is sufficient.

Instead of:

```javascript
const evenNumbers = [];

for (const number of numbers) {
    if (number % 2 === 0) {
        evenNumbers.push(number);
    }
}

const doubled = [];

for (const number of evenNumbers) {
    doubled.push(number * 2);
}
```

You can sometimes combine the work:

```javascript
const result = [];

for (const number of numbers) {
    if (number % 2 === 0) {
        result.push(number * 2);
    }
}
```

However, readability should remain the priority.

---

# 4. Choose Appropriate Data Structures

Different data structures have different performance characteristics.

For example:

```javascript
const users = new Map();

users.set(1, "Sandip");

console.log(users.get(1));
```

A `Map` is useful when frequent key-based lookups are required.

A `Set` is useful when you need unique values:

```javascript
const ids = new Set([
    1,
    2,
    3
]);
```

Choose a structure based on what the application needs.

---

# 5. Avoid Excessive DOM Manipulation

DOM operations can be expensive when performed repeatedly.

Instead of repeatedly changing the DOM:

```javascript
element.textContent = "Hello";
element.textContent = "Hello Sandip";
element.textContent = "Hello Sandip Kushwaha";
```

Make the required update once:

```javascript
element.textContent =
    "Hello Sandip Kushwaha";
```

For larger updates, prepare the content first and then update the DOM.

---

# 6. Cache DOM References

If an element is used repeatedly, store its reference.

Instead of:

```javascript
document.querySelector("#title")
    .textContent = "Hello";

document.querySelector("#title")
    .classList.add("active");
```

Use:

```javascript
const title =
    document.querySelector("#title");

title.textContent = "Hello";

title.classList.add("active");
```

This improves readability and avoids repeating the selector operation.

---

# 7. Avoid Unnecessary Event Handlers

Adding too many event listeners can increase work.

For example:

```javascript
items.forEach(item => {
    item.addEventListener(
        "click",
        handleClick
    );
});
```

For a large dynamic list, event delegation can sometimes be more efficient:

```javascript
container.addEventListener(
    "click",
    (event) => {
        if (
            event.target.matches(".item")
        ) {
            handleClick(event);
        }
    }
);
```

Event delegation can also work well when elements are dynamically added.

---

# 8. Use Debouncing

Debouncing is useful when you only need to perform work after frequent activity stops.

Example:

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

Useful for:

```text
Search
Autocomplete
Form validation
API requests
Autosave
```

Example:

```javascript
const searchUsers =
    debounce(
        fetchUsers,
        500
    );
```

---

# 9. Use Throttling

Throttling is useful when work should continue periodically but not on every event.

Example:

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

Useful for:

```text
Scroll
Resize
Mouse movement
Dragging
Continuous UI events
```

---

# 10. Avoid Memory Leaks

A memory leak occurs when memory remains unnecessarily reachable and cannot be reclaimed.

Common causes:

```text
Unused event listeners
Uncleared timers
Long-lived references
Detached DOM elements
Unnecessary global variables
Growing caches
```

Example:

```javascript
const timer = setInterval(() => {
    console.log("Running");
}, 1000);
```

If it is no longer needed:

```javascript
clearInterval(timer);
```

---

# 11. Clean Up Event Listeners

If an event listener is no longer needed:

```javascript
element.addEventListener(
    "click",
    handleClick
);
```

remove it:

```javascript
element.removeEventListener(
    "click",
    handleClick
);
```

The same function reference must be used.

---

# 12. Clean Up Timers

For `setTimeout()`:

```javascript
const timer = setTimeout(() => {
    console.log("Hello");
}, 5000);
```

Cancel it when necessary:

```javascript
clearTimeout(timer);
```

For `setInterval()`:

```javascript
const interval =
    setInterval(() => {
        console.log("Running");
    }, 1000);
```

Stop it:

```javascript
clearInterval(interval);
```

---

# 13. React Cleanup

In React, effects that create subscriptions, timers, or event listeners should clean them up.

Example:

```jsx
useEffect(() => {
    const handleResize = () => {
        console.log(
            window.innerWidth
        );
    };

    window.addEventListener(
        "resize",
        handleResize
    );

    return () => {
        window.removeEventListener(
            "resize",
            handleResize
        );
    };
}, []);
```

Cleanup prevents unnecessary listeners from remaining active.

---

# 14. Avoid Unnecessary API Requests

Network requests can be expensive.

Avoid repeatedly requesting the same data when it is not necessary.

For example:

```javascript
fetch("/api/products");
fetch("/api/products");
fetch("/api/products");
```

Consider whether the result can be reused.

Possible techniques:

```text
Caching
Pagination
Debouncing
Request cancellation
Server-side filtering
```

---

# 15. Use Pagination

Do not load thousands of records when the user only needs a small portion.

Instead of:

```text
100,000 products
      ↓
Send everything
```

Use:

```text
Page 1 → 20 products
Page 2 → 20 products
Page 3 → 20 products
```

Example API:

```text
/api/products?page=1&limit=20
```

Pagination reduces:

```text
Network data
Memory usage
Rendering work
Server response size
```

---

# 16. Use Server-Side Filtering

Instead of downloading every record:

```javascript
const products =
    await fetch("/api/products");
```

and filtering everything in the browser:

```javascript
products.filter(
    product =>
        product.name.includes("phone")
);
```

For large datasets, let the server/database perform the filtering:

```text
/api/products?search=phone
```

This can significantly reduce the amount of data transferred.

---

# 17. Optimize API Response Size

Do not send unnecessary fields.

Instead of:

```json
{
    "id": 1,
    "name": "Laptop",
    "price": 800,
    "description": "...",
    "createdAt": "...",
    "updatedAt": "...",
    "internalNotes": "...",
    "largeData": "..."
}
```

If the UI only needs:

```json
{
    "id": 1,
    "name": "Laptop",
    "price": 800
}
```

return only the required data when practical.

---

# 18. Use Lazy Loading

Lazy loading means loading something only when it is needed.

Examples:

```text
Images
Components
Routes
Large modules
Data
```

Instead of loading everything immediately:

```text
Application
    ↓
Load everything
    ↓
Show page
```

Lazy loading can work like:

```text
Application
    ↓
Load required content
    ↓
User requests another feature
    ↓
Load that feature
```

---

# 19. Lazy Loading Images

HTML provides native lazy loading:

```html
<img
    src="food.jpg"
    loading="lazy"
    alt="Food"
/>
```

This tells the browser that the image can be loaded lazily.

Useful for pages containing many images.

---

# 20. Code Splitting

Large JavaScript bundles can increase initial loading time.

Instead of:

```text
One huge JavaScript file
```

split the application into smaller chunks:

```text
Main bundle
    ↓
Home
    ↓
Dashboard
    ↓
Settings
    ↓
Admin
```

Modern bundlers such as Vite can perform code splitting when the application uses dynamic imports.

Example:

```javascript
const Admin =
    () => import("./Admin.jsx");
```

---

# 21. Dynamic Import

Dynamic imports load modules when required.

```javascript
const module =
    await import("./heavy-module.js");
```

This can be useful for large or rarely used functionality.

---

# 22. Avoid Large JavaScript Bundles

Large bundles can increase:

```text
Download time
Parsing time
Compilation time
Execution time
Memory usage
```

Review dependencies and remove packages that are not needed.

---

# 23. Avoid Unnecessary Dependencies

Before installing a package, ask:

```text
Do I really need it?
Can JavaScript already do this?
Is the package maintained?
How large is it?
Does it add significant bundle size?
```

For example, a tiny utility may not require a large dependency.

---

# 24. Use Efficient Images

Images can have a major impact on web performance.

Prefer modern formats when appropriate:

```text
WebP
AVIF
```

Also consider:

```text
Compression
Correct dimensions
Responsive images
Lazy loading
```

Avoid loading a 4000×3000 image when the UI only displays it at 400×300.

---

# 25. Avoid Blocking the Main Thread

JavaScript running on the browser's main thread can block user interactions.

Heavy work such as:

```text
Large calculations
Data processing
Complex loops
Large JSON processing
```

can make the UI unresponsive.

Possible solutions include:

```text
Break work into smaller pieces
Use Web Workers
Move processing to the server
Optimize the algorithm
```

---

# 26. Web Workers

A Web Worker can execute JavaScript in a separate worker context.

Example:

```javascript
const worker =
    new Worker("worker.js");
```

Main thread:

```javascript
worker.postMessage(
    largeData
);
```

Worker:

```javascript
self.onmessage = (event) => {
    const result =
        processData(event.data);

    self.postMessage(result);
};
```

Workers are useful for CPU-heavy operations that would otherwise block the main UI thread.

---

# 27. Use `requestAnimationFrame()` for Visual Updates

For browser animations, use:

```javascript
requestAnimationFrame();
```

Example:

```javascript
function animate() {
    element.style.transform =
        `translateX(${position}px)`;

    requestAnimationFrame(animate);
}

requestAnimationFrame(animate);
```

This allows the browser to schedule visual updates appropriately.

---

# 28. Avoid Layout Thrashing

Repeatedly reading and writing layout-related properties can cause unnecessary browser work.

For example:

```javascript
const height =
    element.offsetHeight;

element.style.height =
    `${height + 10}px`;
```

Repeated read/write operations inside large loops can become expensive.

Prefer grouping operations when possible.

---

# 29. Use `DocumentFragment` for Large DOM Updates

When creating many DOM elements, a `DocumentFragment` can help build the structure before inserting it.

```javascript
const fragment =
    document.createDocumentFragment();

for (let i = 0; i < 1000; i++) {
    const item =
        document.createElement("div");

    item.textContent =
        `Item ${i}`;

    fragment.appendChild(item);
}

container.appendChild(fragment);
```

This allows the elements to be assembled before being attached to the document.

---

# 30. Avoid Excessive Logging

During development:

```javascript
console.log(data);
```

is useful.

But excessive logging in production can:

```text
Increase console work
Expose information
Make debugging harder
Add unnecessary processing
```

Remove unnecessary logs before production when appropriate.

---

# 31. Use Efficient Algorithms

Algorithm choice can have a much larger impact than small syntax optimizations.

For example:

```text
O(n)
```

is generally more scalable than:

```text
O(n²)
```

for large input sizes.

Example:

```javascript
for (const user of users) {
    // O(n)
}
```

Nested loops can become expensive:

```javascript
for (const user of users) {
    for (const order of orders) {
        // potentially O(n × m)
    }
}
```

Look for ways to avoid unnecessary repeated searches.

---

# 32. Use `Map` for Frequent Lookups

Suppose you repeatedly search users by ID.

An array approach:

```javascript
const user =
    users.find(
        user => user.id === id
    );
```

If this happens many times, a `Map` can be useful:

```javascript
const userMap =
    new Map(
        users.map(
            user => [user.id, user]
        )
    );

const user =
    userMap.get(id);
```

The best approach depends on the application and access pattern.

---

# 33. Avoid Unnecessary Object Creation

Creating objects repeatedly can increase allocations.

For example:

```javascript
for (let i = 0; i < 100000; i++) {
    const data = {
        value: i
    };

    process(data);
}
```

This may be completely reasonable.

Do not avoid objects simply because they are objects.

Optimize object creation only when profiling shows it matters.

---

# 34. Do Not Optimize Prematurely

One of the most important performance rules:

```text
First make it correct.
Then make it readable.
Then measure.
Then optimize.
```

Do not make code complicated just because it might be slightly faster.

Bad approach:

```text
Guess performance problem
       ↓
Rewrite everything
       ↓
Create complicated code
```

Better:

```text
Build application
       ↓
Measure performance
       ↓
Find bottleneck
       ↓
Optimize bottleneck
       ↓
Measure again
```

---

# 35. Use Browser Performance Tools

Modern browsers provide performance tools.

In Chrome DevTools:

```text
DevTools
   ↓
Performance
   ↓
Record
   ↓
Perform action
   ↓
Stop recording
   ↓
Analyze
```

You can investigate:

```text
JavaScript execution
Rendering
Layout
Painting
Long tasks
Frames
Network activity
```

---

# 36. Use the Network Panel

Chrome DevTools:

```text
Network
```

can help identify:

```text
Slow API requests
Large files
Large images
Repeated requests
Failed requests
Caching problems
```

Useful columns include:

```text
Name
Status
Size
Time
Waterfall
```

---

# 37. Check JavaScript Bundle Size

For frontend applications, inspect the production bundle.

Large bundles may contain:

```text
Unused dependencies
Large libraries
Duplicate dependencies
Unused code
```

Tools such as Vite's build output and bundle analyzers can help identify large modules.

---

# 38. Optimize React Rendering

In React, unnecessary renders can affect performance.

Common causes include:

```text
Changing state unnecessarily
Large component trees
Unstable props
Expensive calculations
Large lists
```

Useful techniques include:

```text
Component splitting
Memoization when measured to help
Virtualization for large lists
Stable event handlers where appropriate
Efficient state design
```

Do not add optimization tools everywhere without measuring the actual problem.

---

# 39. Virtualize Large Lists

Rendering thousands of elements at once can be expensive.

Instead of:

```text
10,000 items
 ↓
Render 10,000 DOM elements
```

virtualization can render only the visible portion:

```text
10,000 items
      ↓
Visible items
      ↓
Render only what user can see
```

This is useful for:

```text
Large tables
Chat messages
Product lists
Admin dashboards
Data grids
```

---

# 40. Optimize Node.js Applications

Node.js performance also depends on avoiding unnecessary work.

Important areas:

```text
Efficient database queries
Caching
Pagination
Streaming
Connection management
Async operations
Avoiding blocking code
```

Avoid heavy synchronous operations in request handlers when possible.

For example:

```javascript
const data =
    fs.readFileSync(
        "large-file.json"
    );
```

For server applications, asynchronous or streaming approaches may be more appropriate for large files.

---

# 41. Use Streaming for Large Data

Instead of loading a huge file into memory:

```javascript
const data =
    fs.readFileSync(
        "large-file.txt"
    );
```

Node.js can stream data:

```javascript
import fs from "fs";

const stream =
    fs.createReadStream(
        "large-file.txt"
    );

stream.on(
    "data",
    chunk => {
        console.log(chunk);
    }
);
```

Streaming reduces the need to keep the entire file in memory at once.

---

# 42. Database Performance Matters

For full-stack applications, JavaScript may not be the bottleneck.

For example:

```text
React
  ↓
Node.js
  ↓
Express
  ↓
MongoDB
```

A slow database query can make the whole request slow.

Optimize:

```text
Indexes
Queries
Pagination
Projection
Aggregation
Connection usage
```

Performance must be considered across the entire system.

---

# 43. Caching

Caching stores frequently used data so it does not need to be generated or fetched repeatedly.

Examples:

```text
Browser cache
API cache
Memory cache
Redis
CDN cache
Database query cache
```

Example concept:

```text
Request
   ↓
Cache has data?
 ↙          ↘
Yes          No
 ↓            ↓
Return      Fetch data
              ↓
           Store cache
              ↓
           Return data
```

---

# 44. Use HTTP Caching

Browser caching can reduce repeated downloads.

For static resources such as:

```text
JavaScript
CSS
Images
Fonts
```

proper cache headers can improve performance.

---

# 45. Reduce Network Requests

Every request has overhead.

Instead of many unnecessary requests:

```text
Request 1
Request 2
Request 3
Request 4
Request 5
```

consider whether some data can be:

```text
Combined
Cached
Lazy-loaded
Fetched only when needed
```

However, fewer requests are not always automatically better. Modern HTTP and application architecture can make parallel requests useful.

---

# 46. Use Compression

Large responses can be compressed before transmission.

Common compression formats include:

```text
Gzip
Brotli
```

Compression can reduce network transfer size.

This is especially useful for:

```text
JavaScript
CSS
HTML
JSON
```

---

# 47. Performance Optimization Workflow

A practical workflow:

```text
1. Build the feature
       ↓
2. Measure performance
       ↓
3. Find the bottleneck
       ↓
4. Identify the cause
       ↓
5. Apply a targeted optimization
       ↓
6. Measure again
       ↓
7. Keep the optimization only if it helps
```

---

# 48. Performance Checklist

Before optimizing, check:

```text
[ ] Are API requests necessary?
[ ] Are responses too large?
[ ] Are images optimized?
[ ] Are unnecessary components rendering?
[ ] Are expensive events throttled?
[ ] Are search inputs debounced?
[ ] Are timers cleaned up?
[ ] Are event listeners cleaned up?
[ ] Are memory leaks present?
[ ] Are large lists virtualized?
[ ] Are database queries optimized?
[ ] Is pagination used?
[ ] Is caching useful?
[ ] Are large modules lazy-loaded?
[ ] Are production bundles optimized?
```

---

# 49. Full-Stack Performance Flow

For a MERN-style application:

```text
React
  ↓
Optimize rendering
  ↓
Lazy loading
  ↓
Efficient state
  ↓
Debounce / Throttle
  ↓
API
  ↓
Reduce requests
  ↓
Node.js / Express
  ↓
Efficient processing
  ↓
MongoDB
  ↓
Indexes + optimized queries
  ↓
Response
  ↓
Caching / Compression
```

---

# 50. Most Important Performance Rules

```text
1. Measure before optimizing.

2. Avoid unnecessary work.

3. Avoid unnecessary API requests.

4. Use debounce for "after activity stops" behavior.

5. Use throttle for controlled continuous execution.

6. Clean up timers and event listeners.

7. Avoid memory leaks.

8. Optimize large arrays and data structures when necessary.

9. Use pagination for large datasets.

10. Optimize images and assets.

11. Lazy-load content that is not immediately needed.

12. Keep JavaScript bundles reasonable.

13. Avoid blocking the main thread.

14. Use Web Workers for suitable CPU-heavy browser work.

15. Optimize database queries.

16. Use caching when appropriate.

17. Use streaming for large data.

18. Profile real bottlenecks instead of guessing.

19. Prefer readable code over unnecessary micro-optimizations.

20. Optimize only when there is a measurable reason.
```

---

# Quick Performance Cheat Sheet

```text
Debounce
→ Wait until activity stops.

Throttle
→ Limit execution frequency.

Pagination
→ Load data in smaller pages.

Lazy Loading
→ Load something when needed.

Code Splitting
→ Split large JavaScript bundles.

Caching
→ Reuse previously available data.

Virtualization
→ Render only visible large-list items.

Web Worker
→ Move suitable heavy work away from the main UI thread.

Streaming
→ Process large data in smaller chunks.

Garbage Collection
→ Automatically reclaims unreachable memory.

Profiling
→ Measure where performance problems actually occur.
```

---

# Key Takeaways

* Performance optimization should be based on measurement.
* Avoid unnecessary calculations, renders, API requests, and DOM operations.
* Use debounce when work should happen after frequent activity stops.
* Use throttle when work should happen periodically during frequent activity.
* Clean up timers and event listeners to avoid memory problems.
* Use pagination and server-side filtering for large datasets.
* Lazy loading and code splitting can improve initial page loading.
* Optimize images because they can consume significant network bandwidth.
* Avoid blocking the browser's main thread with heavy JavaScript work.
* Web Workers can handle suitable CPU-intensive tasks separately.
* Large lists may benefit from virtualization.
* Node.js applications should avoid unnecessary blocking operations.
* Database queries can be a major source of application latency.
* Caching can reduce repeated work and network requests.
* Streaming is useful for large files and datasets.
* The best optimization is usually the one that fixes a measured bottleneck.
