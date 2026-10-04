# JavaScript — Pure Functions

A **pure function** is a function that:

1. Returns the same output when given the same inputs.
2. Does not produce side effects outside the function.

Pure functions make JavaScript code easier to test, understand, and maintain.

---

## 1. Basic Function

```javascript
function add(a, b) {
    return a + b;
}

console.log(add(10, 20));
```

Output:

```text
30
```

This function calculates a result using its inputs.

## 2. What Makes a Function Pure?

Consider:

```javascript
function multiply(a, b) {
    return a * b;
}

console.log(multiply(4, 5)); // 20
console.log(multiply(4, 5)); // 20
```

The same inputs always produce the same output, and the function does not change anything outside itself.

Therefore, `multiply()` is a pure function.

---

## 3. Example of an Impure Function

```javascript
let total = 0;

function addToTotal(amount) {
    total += amount;
    return total;
}

console.log(addToTotal(10)); // 10
console.log(addToTotal(10)); // 20
```

The result depends on the changing external variable `total`.

This function modifies state outside itself, so it is impure.

A pure alternative is:

```javascript
function addToTotal(total, amount) {
    return total + amount;
}

console.log(addToTotal(0, 10));  // 10
console.log(addToTotal(10, 10)); // 20
```

The function receives its required state through parameters instead of modifying an external variable.

---

## 4. Side Effects

A **side effect** is a change or action beyond calculating and returning a value.

Common examples include:

* Changing a global variable
* Modifying an object received from outside
* Writing to a file
* Sending an API request
* Updating the DOM
* Logging to the console

Example of a side effect:

```javascript
let username = "Sandip";

function updateUsername() {
    username = "Ram";
}

updateUsername();

console.log(username); // Ram
```

The function changes external state.

A pure alternative:

```javascript
function updateUsername(username) {
    return "Ram";
}

const updatedUsername =
    updateUsername("Sandip");

console.log(updatedUsername); // Ram
```

The original variable is not changed.

---

## 5. Pure Functions with Arrays

Avoid modifying an existing array when you only need a transformed result.

Impure example:

```javascript
function addItem(items, item) {
    items.push(item);
    return items;
}

const foods = ["Pizza", "Burger"];

addItem(foods, "Momo");

console.log(foods);
// ["Pizza", "Burger", "Momo"]
```

The original array is modified.

Pure alternative:

```javascript
function addItem(items, item) {
    return [...items, item];
}

const foods = ["Pizza", "Burger"];

const updatedFoods =
    addItem(foods, "Momo");

console.log(foods);
// ["Pizza", "Burger"]

console.log(updatedFoods);
// ["Pizza", "Burger", "Momo"]
```

The original array remains unchanged.

---

## 6. Pure Functions with Objects

Impure example:

```javascript
function updatePrice(product, price) {
    product.price = price;
    return product;
}

const product = {
    name: "Keyboard",
    price: 1500
};

updatePrice(product, 2000);
```

The original object is modified.

Pure alternative:

```javascript
function updatePrice(product, price) {
    return {
        ...product,
        price
    };
}

const product = {
    name: "Keyboard",
    price: 1500
};

const updatedProduct =
    updatePrice(product, 2000);

console.log(product.price);        // 1500
console.log(updatedProduct.price); // 2000
```

The spread operator creates a new outer object.

**Important:** This is a shallow copy. Nested objects may still be shared.

---

## 7. Pure Functions in Array Methods

Methods such as `map()` and `filter()` are useful for functional programming because they create new arrays rather than directly modifying the original array.

### Using `map()`

```javascript
const prices = [100, 200, 300];

const updatedPrices =
    prices.map(price => price * 1.1);

console.log(updatedPrices);
// [110, 220, 330]

console.log(prices);
// [100, 200, 300]
```

### Using `filter()`

```javascript
const numbers = [10, 15, 20, 25, 30];

const result =
    numbers.filter(number => number >= 20);

console.log(result);
// [20, 25, 30]
```

The callbacks are pure because they calculate results without modifying external state.

The methods themselves do not guarantee purity if their callbacks contain side effects.

---

## 8. Pure Functions in React

Pure functions are especially useful in React because predictable calculations help components render consistently.

Example:

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}

const total = calculateTotal(500, 3);

console.log(total); // 1500
```

A component can use the same calculation:

```jsx
function ProductTotal({ price, quantity }) {
    const total = price * quantity;

    return <p>Total: Rs. {total}</p>;
}
```

Avoid modifying props or existing state objects directly. Instead, create new values when updating state.

---

## 9. Pure vs Impure Functions

| Pure function                       | Impure function                              |
| ----------------------------------- | -------------------------------------------- |
| Same inputs produce the same output | Output may depend on changing external state |
| No external side effects            | May cause side effects                       |
| Easier to test                      | Can require additional setup                 |
| Does not mutate external data       | May mutate external data                     |
| Easier to reason about              | Behavior can depend on execution order       |

Example:

```javascript
// Pure
function square(number) {
    return number * number;
}

// Impure
let multiplier = 2;

function calculate(number) {
    return number * multiplier;
}
```

The second function depends on an external variable. If `multiplier` changes, the same argument can produce a different result.

---

## 10. Practical Example — Shopping Cart

```javascript
function calculateCartTotal(cart) {
    return cart.reduce((total, item) => {
        return total + item.price * item.quantity;
    }, 0);
}

const cart = [
    { name: "Burger", price: 200, quantity: 2 },
    { name: "Pizza", price: 500, quantity: 1 }
];

console.log(calculateCartTotal(cart));
// 900
```

This function reads the cart and calculates the total without changing the cart.

---

## 11. Important Considerations

A function is not automatically pure just because it uses `return`.

For example:

```javascript
const user = {
    name: "Sandip"
};

function getName(user) {
    user.name = "Ram";
    return user.name;
}
```

This function modifies the supplied object.

Also, a function that reads the current time or generates a random number does not return a predictable result for identical arguments:

```javascript
function getCurrentTime() {
    return Date.now();
}

function getRandomNumber() {
    return Math.random();
}
```

These functions depend on changing external conditions.

---

## 12. Best Practices

* Pass required values through function parameters.
* Return results instead of modifying external variables.
* Avoid mutating arrays and objects received as arguments.
* Prefer `map()`, `filter()`, and `reduce()` for transformations when appropriate.
* Keep calculations separate from API requests, DOM updates, and other side effects.
* Remember that spread syntax creates shallow copies, not automatic deep copies.
* Use pure functions for calculations, formatting, and data transformations.

---

## Quick Cheat Sheet

```javascript
// Pure calculation
const add = (a, b) => a + b;

// Pure transformation
const double = numbers =>
    numbers.map(number => number * 2);

// Pure filtering
const adults = users =>
    users.filter(user => user.age >= 18);

// Pure object update
const updateUser = (user, name) => ({
    ...user,
    name
});

// Pure array update
const addItem = (items, item) => [
    ...items,
    item
];
```

---

## Key Takeaways

* A pure function produces predictable results for the same inputs.
* A pure function does not cause external side effects.
* Avoid modifying global variables and input objects.
* Pure functions are easier to test and reuse.
* Immutable transformations help preserve original data.
* Pure functions are valuable in React and general JavaScript development.
