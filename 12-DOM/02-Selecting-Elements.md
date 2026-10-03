# JavaScript DOM Selecting Elements

Selecting elements is one of the most common DOM operations.

Before JavaScript can modify an HTML element, you usually need to **select it first**.

Common selection methods include:

* `getElementById()`
* `getElementsByClassName()`
* `getElementsByTagName()`
* `querySelector()`
* `querySelectorAll()`

---

# 1. `getElementById()`

Selects an element using its `id`.

HTML:

```html
<h1 id="title">Hello World</h1>
```

JavaScript:

```javascript
const title = document.getElementById("title");

console.log(title);
```

The `#` is **not** used with `getElementById()`.

Correct:

```javascript
document.getElementById("title");
```

Not:

```javascript
document.getElementById("#title");
```

---

# 2. Selecting by ID

Example:

```html
<div id="profile">
    <h2>Sandip</h2>
</div>
```

JavaScript:

```javascript
const profile = document.getElementById("profile");

console.log(profile);
```

You can then modify it:

```javascript
profile.textContent = "My Profile";
```

---

# 3. What Happens If the ID Does Not Exist?

```javascript
const element = document.getElementById("doesNotExist");

console.log(element);
```

Result:

```text
null
```

So always remember that an element lookup can fail.

---

# 4. `getElementsByClassName()`

Selects elements based on their class name.

HTML:

```html
<p class="message">Hello</p>
<p class="message">Welcome</p>
<p class="message">Goodbye</p>
```

JavaScript:

```javascript
const messages = document.getElementsByClassName("message");

console.log(messages);
```

It returns an **HTMLCollection**.

---

# 5. Accessing an HTMLCollection

You can access individual elements by index:

```javascript
const messages = document.getElementsByClassName("message");

console.log(messages[0]);
console.log(messages[1]);
console.log(messages[2]);
```

Indexes start at:

```text
0
1
2
```

---

# 6. HTMLCollection Length

You can check how many elements were found:

```javascript
const messages = document.getElementsByClassName("message");

console.log(messages.length);
```

For:

```html
<p class="message">One</p>
<p class="message">Two</p>
<p class="message">Three</p>
```

Output:

```text
3
```

---

# 7. `getElementsByTagName()`

Selects elements by their HTML tag name.

Example:

```html
<p>One</p>
<p>Two</p>
<p>Three</p>
```

JavaScript:

```javascript
const paragraphs = document.getElementsByTagName("p");

console.log(paragraphs);
```

It returns an **HTMLCollection**.

---

# 8. Selecting All Div Elements

```javascript
const divs = document.getElementsByTagName("div");

console.log(divs.length);
```

This selects all matching `<div>` elements within the document.

---

# 9. Selecting All Elements

You can use:

```javascript
const elements = document.getElementsByTagName("*");

console.log(elements);
```

The `*` means all elements.

---

# 10. `querySelector()`

`querySelector()` uses a **CSS selector** and returns the first matching element.

Example:

```html
<h1 class="title">Hello</h1>
<h1 class="title">Welcome</h1>
```

JavaScript:

```javascript
const title = document.querySelector(".title");

console.log(title);
```

Only the first matching `<h1>` is returned.

---

# 11. Selecting by ID with `querySelector()`

With `querySelector()`, use the CSS `#` selector.

```javascript
const title = document.querySelector("#title");
```

For:

```html
<h1 id="title">Hello</h1>
```

This is equivalent to:

```javascript
const title = document.getElementById("title");
```

---

# 12. Selecting by Class

Use `.` for a class.

HTML:

```html
<p class="message">Hello</p>
```

JavaScript:

```javascript
const message = document.querySelector(".message");
```

---

# 13. Selecting by Tag

You can select an element by its tag name.

```javascript
const heading = document.querySelector("h1");
```

This returns the first `<h1>` element.

---

# 14. CSS Selectors

Because `querySelector()` accepts CSS selectors, you can use many CSS selector patterns.

### ID

```javascript
document.querySelector("#title");
```

### Class

```javascript
document.querySelector(".card");
```

### Tag

```javascript
document.querySelector("button");
```

### Attribute

```javascript
document.querySelector("[type='email']");
```

---

# 15. Descendant Selector

You can select an element inside another element.

HTML:

```html
<div class="card">
    <h2>Product</h2>
</div>
```

JavaScript:

```javascript
const heading = document.querySelector(".card h2");
```

This selects the `<h2>` inside `.card`.

---

# 16. Child Selector

The `>` selector selects a direct child.

HTML:

```html
<div class="card">
    <h2>Product</h2>
</div>
```

JavaScript:

```javascript
const heading = document.querySelector(".card > h2");
```

This means:

> Select an `h2` that is a direct child of `.card`.

---

# 17. Multiple Matching Elements

Consider:

```html
<p class="item">One</p>
<p class="item">Two</p>
<p class="item">Three</p>
```

If you use:

```javascript
const item = document.querySelector(".item");
```

Only the first matching element is returned.

```text
One
```

---

# 18. `querySelectorAll()`

Use `querySelectorAll()` when you want **all matching elements**.

```javascript
const items = document.querySelectorAll(".item");

console.log(items);
```

This returns a **NodeList**.

---

# 19. Accessing a NodeList

You can use indexes:

```javascript
const items = document.querySelectorAll(".item");

console.log(items[0]);
console.log(items[1]);
console.log(items[2]);
```

---

# 20. NodeList Length

```javascript
const items = document.querySelectorAll(".item");

console.log(items.length);
```

Example:

```html
<p class="item">One</p>
<p class="item">Two</p>
```

Output:

```text
2
```

---

# 21. `querySelectorAll()` with Different Selectors

You can select multiple elements using any valid CSS selector.

### All paragraphs

```javascript
document.querySelectorAll("p");
```

### All cards

```javascript
document.querySelectorAll(".card");
```

### Elements with an ID

An ID is normally unique, so `querySelector()` is more appropriate:

```javascript
document.querySelector("#profile");
```

---

# 22. NodeList `forEach()`

A NodeList returned by `querySelectorAll()` can normally be iterated with `forEach()`.

```javascript
const items = document.querySelectorAll(".item");

items.forEach((item) => {
    console.log(item.textContent);
});
```

For:

```html
<p class="item">One</p>
<p class="item">Two</p>
<p class="item">Three</p>
```

Output:

```text
One
Two
Three
```

---

# 23. Changing Multiple Elements

Example:

```javascript
const items = document.querySelectorAll(".item");

items.forEach((item) => {
    item.classList.add("active");
});
```

Every selected element receives the `active` class.

---

# 24. Selecting Inside a Specific Element

You do not always need to search the entire document.

HTML:

```html
<div id="products">
    <p class="item">Laptop</p>
    <p class="item">Phone</p>
</div>

<div>
    <p class="item">Other item</p>
</div>
```

First select the container:

```javascript
const products = document.querySelector("#products");
```

Then search inside it:

```javascript
const items = products.querySelectorAll(".item");
```

Only the items inside `#products` are selected.

---

# 25. `document.querySelector()` vs `element.querySelector()`

Both use CSS selectors.

### Document

```javascript
document.querySelector(".card");
```

Searches the document.

### Element

```javascript
container.querySelector(".card");
```

Searches within that container.

This is useful when working with larger DOM structures.

---

# 26. Selecting Form Elements

HTML:

```html
<form>
    <input type="text" name="username">
    <input type="email" name="email">
</form>
```

You can use:

```javascript
const username = document.querySelector(
    'input[name="username"]'
);
```

And:

```javascript
const email = document.querySelector(
    'input[name="email"]'
);
```

---

# 27. Attribute Selectors

CSS attribute selectors are useful with `querySelector()`.

### Type

```javascript
document.querySelector('input[type="email"]');
```

### Name

```javascript
document.querySelector('input[name="username"]');
```

### Data attribute

HTML:

```html
<button data-action="save">Save</button>
```

JavaScript:

```javascript
const button = document.querySelector(
    '[data-action="save"]'
);
```

---

# 28. Selecting by Multiple Classes

HTML:

```html
<div class="card active"></div>
```

Select an element containing both classes:

```javascript
const card = document.querySelector(".card.active");
```

Notice there is no space.

```text
.card.active
```

means the same element has both classes.

---

# 29. Selecting Multiple Types

You can use CSS selector lists.

```javascript
const elements = document.querySelectorAll(
    "h1, h2, h3"
);
```

This selects all:

* `<h1>`
* `<h2>`
* `<h3>`

---

# 30. `getElementById()` vs `querySelector()`

Both can select an element by ID.

### `getElementById()`

```javascript
const title = document.getElementById("title");
```

### `querySelector()`

```javascript
const title = document.querySelector("#title");
```

The main difference is that `querySelector()` uses CSS selector syntax.

---

# 31. `querySelector()` vs `querySelectorAll()`

| Method               | Returns                |
| -------------------- | ---------------------- |
| `querySelector()`    | First matching element |
| `querySelectorAll()` | All matching elements  |

Example:

```javascript
document.querySelector(".card");
```

Returns:

```text
First .card
```

While:

```javascript
document.querySelectorAll(".card");
```

Returns:

```text
All .card elements
```

---

# 32. HTMLCollection vs NodeList

Some older DOM selection methods return an **HTMLCollection**:

```javascript
document.getElementsByClassName("item");
```

```javascript
document.getElementsByTagName("p");
```

`querySelectorAll()` returns a **NodeList**:

```javascript
document.querySelectorAll(".item");
```

A simplified comparison:

| Feature       | HTMLCollection                                     | NodeList                                     |
| ------------- | -------------------------------------------------- | -------------------------------------------- |
| Common source | `getElementsBy...`                                 | `querySelectorAll()`                         |
| Index access  | Yes                                                | Yes                                          |
| `.length`     | Yes                                                | Yes                                          |
| `forEach()`   | Not universally the same across older environments | Yes for modern NodeList                      |
| Can be live   | Often                                              | `querySelectorAll()` returns static NodeList |

---

# 33. Live vs Static Collections

This is an important difference.

Some DOM collections are **live**, meaning they can automatically reflect later DOM changes.

For example:

```javascript
const items = document.getElementsByClassName("item");
```

The collection can update when matching elements are added or removed.

`querySelectorAll()` returns a **static NodeList**.

```javascript
const items = document.querySelectorAll(".item");
```

Later DOM changes do not automatically update that existing NodeList.

Example:

```javascript
const items = document.querySelectorAll(".item");

const newItem = document.createElement("p");

newItem.className = "item";

document.body.appendChild(newItem);
```

The existing `items` NodeList does not automatically include the newly added element.

---

# 34. Checking Whether an Element Exists

When using `querySelector()`:

```javascript
const button = document.querySelector("#save");

if (button) {
    button.textContent = "Save";
}
```

If the element does not exist:

```javascript
button === null;
```

So checking the result can prevent errors.

---

# 35. Selecting Elements Safely

Instead of immediately doing:

```javascript
document.querySelector("#button").textContent = "Save";
```

you can use:

```javascript
const button = document.querySelector("#button");

if (button) {
    button.textContent = "Save";
}
```

This is useful when the element may not exist on every page.

---

# 36. `closest()`

`closest()` finds the nearest ancestor that matches a CSS selector.

HTML:

```html
<div class="card">
    <button class="delete">Delete</button>
</div>
```

JavaScript:

```javascript
const button = document.querySelector(".delete");

const card = button.closest(".card");

console.log(card);
```

The `.card` element is returned.

This is especially useful for event delegation.

---

# 37. `matches()`

`matches()` checks whether an element matches a CSS selector.

```javascript
const button = document.querySelector("button");

if (button.matches(".primary")) {
    console.log("Primary button");
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

# 38. Practical Example

HTML:

```html
<section id="products">
    <article class="product">
        <h2>Laptop</h2>
    </article>

    <article class="product">
        <h2>Phone</h2>
    </article>

    <article class="product">
        <h2>Keyboard</h2>
    </article>
</section>
```

JavaScript:

```javascript
const products = document.querySelector("#products");

const productCards = products.querySelectorAll(".product");

productCards.forEach((product) => {
    product.classList.add("available");
});
```

The result is that every product card receives:

```text
available
```

as a CSS class.

---

# 39. Selection Methods Summary

| Method                     | Example                                   | Result                    |
| -------------------------- | ----------------------------------------- | ------------------------- |
| `getElementById()`         | `document.getElementById("title")`        | One element               |
| `getElementsByClassName()` | `document.getElementsByClassName("card")` | HTMLCollection            |
| `getElementsByTagName()`   | `document.getElementsByTagName("p")`      | HTMLCollection            |
| `querySelector()`          | `document.querySelector(".card")`         | First matching element    |
| `querySelectorAll()`       | `document.querySelectorAll(".card")`      | Static NodeList           |
| `closest()`                | `element.closest(".card")`                | Closest matching ancestor |
| `matches()`                | `element.matches(".active")`              | Boolean                   |

---

# 40. Which Method Should You Use?

For modern JavaScript, `querySelector()` and `querySelectorAll()` are often convenient because they support CSS selectors.

Use:

```javascript
document.querySelector("#id");
```

for one element.

Use:

```javascript
document.querySelectorAll(".items");
```

for multiple elements.

Use:

```javascript
document.getElementById("id");
```

when you specifically want a simple ID lookup.

---

# 41. Common Mistakes

### Mistake 1: Adding `#` to `getElementById()`

Wrong:

```javascript
document.getElementById("#title");
```

Correct:

```javascript
document.getElementById("title");
```

---

### Mistake 2: Expecting `querySelector()` to return everything

```javascript
document.querySelector(".item");
```

returns only the first matching element.

For all matches:

```javascript
document.querySelectorAll(".item");
```

---

### Mistake 3: Forgetting `.` for a class

Wrong:

```javascript
document.querySelector("card");
```

Correct:

```javascript
document.querySelector(".card");
```

---

### Mistake 4: Forgetting `#` for an ID

Wrong:

```javascript
document.querySelector("title");
```

Correct:

```javascript
document.querySelector("#title");
```

when `title` is an ID.

---

### Mistake 5: Using an element before it exists

If the DOM has not created the element yet:

```javascript
const button = document.querySelector("#save");
```

may return:

```javascript
null
```

Make sure the code runs at an appropriate time.

---

# 42. Key Takeaways

* DOM elements must often be selected before they can be modified.
* `getElementById()` selects by ID.
* `getElementsByClassName()` selects by class.
* `getElementsByTagName()` selects by tag.
* `querySelector()` returns the first matching element.
* `querySelectorAll()` returns all matching elements.
* `querySelector()` and `querySelectorAll()` use CSS selectors.
* `querySelectorAll()` returns a static NodeList.
* Some `getElementsBy...` methods return live HTMLCollections.
* `closest()` finds a matching ancestor.
* `matches()` checks whether an element matches a selector.
* Always consider that an element lookup can return no match.

> **Select the correct DOM element first; then read, modify, create, or remove it.**

---

## Related Topics

* [DOM Introduction](./01-DOM-Introduction.md)
* [Changing Content](./03-Changing-Content.md)
* [Changing Styles](./04-Changing-Styles.md)
* [Creating Elements](./05-Creating-Elements.md)
* [Removing Elements](./06-Removing-Elements.md)
* [DOM Traversal](./07-DOM-Traversal.md)
* [Events](../13-Events/01-Events.md)
