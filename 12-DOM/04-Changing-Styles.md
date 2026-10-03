# JavaScript DOM Changing Styles

JavaScript can change the appearance of HTML elements by modifying their styles and CSS classes.

Common approaches include:

* `element.style`
* `classList.add()`
* `classList.remove()`
* `classList.toggle()`
* `classList.contains()`
* CSS custom properties

---

# 1. Using `element.style`

The `style` property allows JavaScript to modify an element's **inline CSS styles**.

HTML:

```html
<h1 id="title">Hello JavaScript</h1>
```

JavaScript:

```javascript
const title = document.querySelector("#title");

title.style.color = "blue";
```

The browser applies:

```css
color: blue;
```

to that element.

---

# 2. Changing Multiple Styles

You can modify several properties:

```javascript
const title = document.querySelector("#title");

title.style.color = "blue";
title.style.fontSize = "32px";
title.style.fontWeight = "bold";
```

The corresponding CSS is conceptually:

```css
color: blue;
font-size: 32px;
font-weight: bold;
```

---

# 3. CSS Property Names in JavaScript

CSS normally uses kebab-case:

```css
background-color: black;
font-size: 20px;
margin-top: 10px;
```

JavaScript style properties normally use camelCase:

```javascript
element.style.backgroundColor = "black";
element.style.fontSize = "20px";
element.style.marginTop = "10px";
```

Examples:

| CSS                | JavaScript        |
| ------------------ | ----------------- |
| `background-color` | `backgroundColor` |
| `font-size`        | `fontSize`        |
| `margin-top`       | `marginTop`       |
| `border-radius`    | `borderRadius`    |
| `text-align`       | `textAlign`       |

---

# 4. Background Color

HTML:

```html
<div id="box">Content</div>
```

JavaScript:

```javascript
const box = document.querySelector("#box");

box.style.backgroundColor = "lightblue";
```

---

# 5. Text Color

```javascript
const message = document.querySelector("#message");

message.style.color = "green";
```

---

# 6. Font Size

```javascript
const heading = document.querySelector("h1");

heading.style.fontSize = "40px";
```

---

# 7. Width and Height

```javascript
const card = document.querySelector(".card");

card.style.width = "300px";
card.style.height = "200px";
```

CSS units can be used:

```javascript
card.style.width = "50%";
card.style.height = "20rem";
```

---

# 8. Margin and Padding

```javascript
const box = document.querySelector(".box");

box.style.margin = "20px";
box.style.padding = "16px";
```

Individual properties can also be changed:

```javascript
box.style.marginTop = "10px";
box.style.paddingLeft = "20px";
```

---

# 9. Border

```javascript
const box = document.querySelector(".box");

box.style.border = "1px solid black";
box.style.borderRadius = "8px";
```

---

# 10. Display

You can change the `display` property.

```javascript
const menu = document.querySelector(".menu");

menu.style.display = "none";
```

To show it again:

```javascript
menu.style.display = "block";
```

For flex layouts:

```javascript
menu.style.display = "flex";
```

---

# 11. Visibility

You can also use:

```javascript
element.style.visibility = "hidden";
```

and:

```javascript
element.style.visibility = "visible";
```

There is an important difference:

```text
display: none
```

usually removes the element from the layout.

While:

```text
visibility: hidden
```

keeps its layout space but hides it visually.

---

# 12. Opacity

```javascript
const image = document.querySelector("img");

image.style.opacity = "0.5";
```

Values normally range from:

```text
0 → completely transparent
1 → completely opaque
```

---

# 13. CSS Classes Are Often Better

Instead of changing many inline styles:

```javascript
element.style.color = "red";
element.style.backgroundColor = "white";
element.style.padding = "10px";
```

it is often cleaner to define a CSS class.

CSS:

```css
.error {
    color: red;
    background-color: white;
    padding: 10px;
}
```

JavaScript:

```javascript
element.classList.add("error");
```

This keeps presentation in CSS and behavior in JavaScript.

---

# 14. `classList.add()`

Adds one or more classes.

HTML:

```html
<div id="box">Box</div>
```

JavaScript:

```javascript
const box = document.querySelector("#box");

box.classList.add("active");
```

Multiple classes:

```javascript
box.classList.add("active", "visible");
```

---

# 15. `classList.remove()`

Removes a class.

```javascript
box.classList.remove("active");
```

Multiple classes:

```javascript
box.classList.remove("active", "visible");
```

---

# 16. `classList.toggle()`

`toggle()` adds a class if it does not exist and removes it if it already exists.

```javascript
box.classList.toggle("active");
```

The behavior is:

```text
Not present
    ↓
toggle()
    ↓
Added

Present
    ↓
toggle()
    ↓
Removed
```

This is commonly used for:

* Dark mode
* Mobile menus
* Dropdowns
* Modals
* Active states

---

# 17. `classList.contains()`

Checks whether an element has a specific class.

```javascript
if (box.classList.contains("active")) {
    console.log("Box is active");
}
```

It returns:

```text
true
```

or:

```text
false
```

---

# 18. `className`

You can access the complete class attribute using:

```javascript
console.log(element.className);
```

For:

```html
<div class="card active"></div>
```

the result is approximately:

```text
card active
```

You can also assign:

```javascript
element.className = "card active";
```

However, `classList` is usually safer for adding or removing individual classes because `className` replaces the whole class value.

---

# 19. `classList.replace()`

You can replace one class with another.

```javascript
element.classList.replace(
    "old-class",
    "new-class"
);
```

Example:

```javascript
box.classList.replace(
    "inactive",
    "active"
);
```

---

# 20. `classList.toggle()` with a Condition

`toggle()` can accept a second argument.

```javascript
element.classList.toggle(
    "active",
    true
);
```

This ensures the class is present.

```javascript
element.classList.toggle(
    "active",
    false
);
```

This ensures the class is removed.

Example:

```javascript
const isLoggedIn = true;

button.classList.toggle("logged-in", isLoggedIn);
```

---

# 21. Adding a CSS Class on a Button Click

HTML:

```html
<button id="menuBtn">
    Menu
</button>

<nav id="menu">
    Navigation
</nav>
```

CSS:

```css
.open {
    display: block;
}
```

JavaScript:

```javascript
const button = document.querySelector("#menuBtn");
const menu = document.querySelector("#menu");

button.addEventListener("click", () => {
    menu.classList.toggle("open");
});
```

Each click changes the menu's state.

---

# 22. Dark Mode Example

CSS:

```css
.dark {
    background-color: #111;
    color: white;
}
```

HTML:

```html
<button id="themeBtn">
    Toggle Theme
</button>
```

JavaScript:

```javascript
const button = document.querySelector("#themeBtn");

button.addEventListener("click", () => {
    document.body.classList.toggle("dark");
});
```

The class is added or removed from the `<body>`.

---

# 23. Using CSS Custom Properties

CSS variables can also be changed with JavaScript.

CSS:

```css
:root {
    --primary-color: blue;
}

button {
    background-color: var(--primary-color);
}
```

JavaScript:

```javascript
document.documentElement.style.setProperty(
    "--primary-color",
    "green"
);
```

The CSS variable changes from:

```text
blue
```

to:

```text
green
```

---

# 24. Reading CSS Custom Properties

You can read a CSS custom property using:

```javascript
const value = getComputedStyle(document.documentElement)
    .getPropertyValue("--primary-color");

console.log(value);
```

---

# 25. `style.setProperty()`

You can also use `setProperty()` for CSS properties.

```javascript
element.style.setProperty(
    "background-color",
    "black"
);
```

This is particularly useful when working with CSS custom properties.

Example:

```javascript
element.style.setProperty(
    "--card-color",
    "lightblue"
);
```

---

# 26. Removing an Inline Style

You can remove an inline style using:

```javascript
element.style.removeProperty("color");
```

Example:

```javascript
const title = document.querySelector("#title");

title.style.color = "red";

title.style.removeProperty("color");
```

The inline `color` declaration is removed.

---

# 27. Reading Inline Styles

Suppose:

```javascript
element.style.color = "red";
```

You can read it:

```javascript
console.log(element.style.color);
```

Output:

```text
red
```

But remember:

> `element.style` mainly represents inline styles.

It does not necessarily tell you the final style coming from external stylesheets.

---

# 28. `getComputedStyle()`

To get the computed style of an element:

```javascript
const styles = getComputedStyle(element);

console.log(styles.color);
console.log(styles.fontSize);
```

Example CSS:

```css
.title {
    color: blue;
    font-size: 32px;
}
```

JavaScript:

```javascript
const title = document.querySelector(".title");

const styles = getComputedStyle(title);

console.log(styles.color);
console.log(styles.fontSize);
```

This gives the browser's computed values.

---

# 29. `style` vs `getComputedStyle()`

### `element.style`

Works primarily with inline styles:

```javascript
element.style.color = "red";
```

### `getComputedStyle()`

Reads the final computed styles:

```javascript
const styles = getComputedStyle(element);

console.log(styles.color);
```

For example, if the CSS comes from:

```css
.title {
    color: blue;
}
```

then:

```javascript
element.style.color
```

may be empty because there is no inline `style`.

But:

```javascript
getComputedStyle(element).color
```

can return the computed color.

---

# 30. Changing Styles Based on Data

Suppose:

```javascript
const status = "available";
```

You could use CSS classes:

```javascript
const badge = document.querySelector(".badge");

badge.classList.toggle(
    "available",
    status === "available"
);

badge.classList.toggle(
    "unavailable",
    status !== "available"
);
```

This is generally cleaner than manually setting many style properties.

---

# 31. Practical Status Example

CSS:

```css
.status {
    padding: 6px 10px;
    border-radius: 6px;
}

.status.available {
    background-color: green;
    color: white;
}

.status.unavailable {
    background-color: gray;
    color: white;
}
```

HTML:

```html
<span class="status">Available</span>
```

JavaScript:

```javascript
const status = document.querySelector(".status");

status.classList.add("available");
```

For another state:

```javascript
status.classList.remove("available");
status.classList.add("unavailable");
```

---

# 32. Avoiding Repeated Style Code

Instead of:

```javascript
element.style.color = "white";
element.style.backgroundColor = "green";
element.style.padding = "5px";
element.style.borderRadius = "5px";
```

define:

```css
.success {
    color: white;
    background-color: green;
    padding: 5px;
    border-radius: 5px;
}
```

Then:

```javascript
element.classList.add("success");
```

This is easier to maintain.

---

# 33. Style Changes and Reflow

Some style changes can cause the browser to recalculate layout.

Examples include changes to:

* Width
* Height
* Margin
* Padding
* Position
* Display

Browsers optimize rendering internally, but repeatedly forcing layout calculations can hurt performance.

For larger UI changes, using CSS classes is often cleaner and can make updates easier to manage.

---

# 34. Batch Changes with Classes

Instead of changing many properties individually:

```javascript
element.style.width = "300px";
element.style.padding = "20px";
element.style.backgroundColor = "black";
element.style.color = "white";
```

Use:

```javascript
element.classList.add("expanded");
```

CSS:

```css
.expanded {
    width: 300px;
    padding: 20px;
    background-color: black;
    color: white;
}
```

---

# 35. Practical Example: Form Validation

HTML:

```html
<input id="email" type="email">

<p id="error"></p>
```

CSS:

```css
.error {
    border: 1px solid red;
}

.message {
    color: red;
}
```

JavaScript:

```javascript
const email = document.querySelector("#email");
const error = document.querySelector("#error");

const value = email.value.trim();

if (!value) {
    email.classList.add("error");

    error.textContent = "Email is required";
    error.classList.add("message");
}
```

This separates:

```text
JavaScript → behavior
CSS        → appearance
HTML       → structure
```

---

# 36. Practical Example: Active Navigation

HTML:

```html
<nav>
    <a class="nav-link active" href="/">Home</a>
    <a class="nav-link" href="/about">About</a>
    <a class="nav-link" href="/contact">Contact</a>
</nav>
```

JavaScript:

```javascript
const links = document.querySelectorAll(".nav-link");

links.forEach((link) => {
    link.addEventListener("click", () => {
        links.forEach((item) => {
            item.classList.remove("active");
        });

        link.classList.add("active");
    });
});
```

Only the clicked link receives the `active` class.

---

# 37. Practical Example: Show/Hide Password

HTML:

```html
<input id="password" type="password">

<button id="togglePassword">
    Show
</button>
```

JavaScript:

```javascript
const password = document.querySelector("#password");
const button = document.querySelector("#togglePassword");

button.addEventListener("click", () => {
    const isPassword = password.type === "password";

    password.type = isPassword
        ? "text"
        : "password";

    button.textContent = isPassword
        ? "Hide"
        : "Show";
});
```

This example changes both an element property and its text.

---

# 38. Inline Style vs CSS Class

| Approach              | Best Use                           |
| --------------------- | ---------------------------------- |
| `element.style`       | Small, dynamic style changes       |
| `classList`           | UI states and reusable styles      |
| CSS custom properties | Dynamic theme/configuration values |
| `getComputedStyle()`  | Reading final computed styles      |

A common approach is:

```text
JavaScript
    ↓
classList / CSS variables
    ↓
CSS
    ↓
Visual appearance
```

---

# 39. Common Mistakes

### Mistake 1: Using kebab-case in JavaScript

Wrong:

```javascript
element.style.background-color = "red";
```

Correct:

```javascript
element.style.backgroundColor = "red";
```

---

### Mistake 2: Replacing all classes accidentally

This:

```javascript
element.className = "active";
```

replaces the existing class list.

If you only want to add a class:

```javascript
element.classList.add("active");
```

---

### Mistake 3: Using too many inline styles

This:

```javascript
element.style.color = "red";
element.style.padding = "10px";
element.style.borderRadius = "5px";
```

can become difficult to maintain.

For reusable styles, prefer CSS classes.

---

### Mistake 4: Confusing inline style with computed style

```javascript
element.style.color
```

does not necessarily show the final color applied by all stylesheets.

Use:

```javascript
getComputedStyle(element).color
```

when you need the computed value.

---

# 40. Key Takeaways

* `element.style` changes inline CSS.
* CSS property names use camelCase in JavaScript.
* `classList` is useful for managing CSS classes.
* `add()` adds classes.
* `remove()` removes classes.
* `toggle()` adds/removes a class.
* `contains()` checks for a class.
* `replace()` replaces a class.
* `getComputedStyle()` reads computed CSS values.
* CSS custom properties can be changed with `setProperty()`.
* CSS classes are often cleaner than many inline styles.
* Keep structure in HTML, appearance in CSS, and behavior in JavaScript.

> **For reusable UI states, prefer CSS classes; use `element.style` for small or highly dynamic style changes.**

---

## Related Topics

* [DOM Introduction](./01-DOM-Introduction.md)
* [Selecting Elements](./02-Selecting-Elements.md)
* [Changing Content](./03-Changing-Content.md)
* [Creating Elements](./05-Creating-Elements.md)
* [Removing Elements](./06-Removing-Elements.md)
* [DOM Traversal](./07-DOM-Traversal.md)
* [Events](../13-Events/01-Events.md)
