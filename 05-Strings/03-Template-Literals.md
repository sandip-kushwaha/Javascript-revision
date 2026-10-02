# JavaScript Template Literals

**Template literals** are a modern way to create strings in JavaScript.

They use **backticks** instead of single or double quotes.

```javascript
let message = `Hello World`;

console.log(message);
```

Template literals are useful for:

* Embedding variables
* Creating dynamic strings
* Writing multi-line strings
* Using expressions inside strings
* Building readable messages

---

## 1. Basic Template Literal

Normal string:

```javascript
let name = "Sandip";
```

Template literal:

```javascript
let name = `Sandip`;
```

Both create strings.

```javascript
console.log(typeof `Hello`);
```

Output:

```text
string
```

---

## 2. Backticks

Template literals use:

```text
`
```

This character is called a **backtick**.

Example:

```javascript
let message = `Hello JavaScript`;

console.log(message);
```

Do not confuse backticks with:

```text
'   Single quote
"   Double quote
`   Backtick
```

---

## 3. String Interpolation

One of the biggest advantages of template literals is **string interpolation**.

String interpolation means putting a variable or expression directly inside a string.

Use:

```text
${}
```

Example:

```javascript
let name = "Sandip";

let message = `Hello ${name}`;

console.log(message);
```

Output:

```text
Hello Sandip
```

---

## 4. Without Template Literals

Before template literals, you might write:

```javascript
let name = "Sandip";

let message = "Hello " + name;

console.log(message);
```

This works, but template literals are often easier to read:

```javascript
let name = "Sandip";

let message = `Hello ${name}`;

console.log(message);
```

---

## 5. Multiple Variables

You can use multiple variables.

```javascript
let firstName = "Sandip";
let lastName = "Kushwaha";

let fullName = `${firstName} ${lastName}`;

console.log(fullName);
```

Output:

```text
Sandip Kushwaha
```

---

## 6. Expressions Inside Template Literals

You can put JavaScript expressions inside `${}`.

Example:

```javascript
let a = 10;
let b = 20;

let result = `Total: ${a + b}`;

console.log(result);
```

Output:

```text
Total: 30
```

---

## 7. Mathematical Expressions

```javascript
let price = 500;
let quantity = 2;

let message = `Total price: ${price * quantity}`;

console.log(message);
```

Output:

```text
Total price: 1000
```

---

## 8. Function Calls

You can call a function inside `${}`.

```javascript
function greet() {
    return "Hello";
}

let message = `${greet()} Sandip`;

console.log(message);
```

Output:

```text
Hello Sandip
```

---

## 9. Method Calls

String methods can also be used.

```javascript
let name = "sandip";

let message = `Hello ${name.toUpperCase()}`;

console.log(message);
```

Output:

```text
Hello SANDIP
```

---

## 10. Conditional Expression

You can use a conditional expression inside a template literal.

```javascript
let age = 22;

let message = `Status: ${age >= 18 ? "Adult" : "Minor"}`;

console.log(message);
```

Output:

```text
Status: Adult
```

---

## 11. Multi-Line Strings

Template literals make multi-line strings easy.

```javascript
let message = `Hello Sandip
Welcome to JavaScript
Keep learning!`;

console.log(message);
```

Output:

```text
Hello Sandip
Welcome to JavaScript
Keep learning!
```

With normal quotes, creating multi-line strings requires different syntax.

---

## 12. Multi-Line HTML

Template literals are useful when creating HTML strings.

```javascript
let name = "Sandip";

let html = `
    <div>
        <h2>Hello ${name}</h2>
        <p>Welcome to our website.</p>
    </div>
`;

console.log(html);
```

This is commonly useful when generating dynamic text or markup.

---

## 13. Object Properties

You can access object properties inside `${}`.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

let message = `Name: ${user.name}, Age: ${user.age}`;

console.log(message);
```

Output:

```text
Name: Sandip, Age: 22
```

---

## 14. Array Values

You can access array values.

```javascript
let foods = ["Momo", "Pizza", "Burger"];

let message = `First food: ${foods[0]}`;

console.log(message);
```

Output:

```text
First food: Momo
```

---

## 15. Function Parameters

Template literals work well inside functions.

```javascript
function greet(name) {
    return `Hello ${name}`;
}

console.log(greet("Sandip"));
```

Output:

```text
Hello Sandip
```

Another example:

```javascript
function getPrice(item, price) {
    return `${item} costs Rs. ${price}`;
}

console.log(getPrice("Momo", 250));
```

Output:

```text
Momo costs Rs. 250
```

---

## 16. Practical Hotel Example

Suppose a hotel system has food information:

```javascript
let foodName = "Chicken Momo";
let price = 250;

let message = `${foodName} costs Rs. ${price}`;

console.log(message);
```

Output:

```text
Chicken Momo costs Rs. 250
```

---

## 17. Order Example

```javascript
let customerName = "Sandip";
let foodName = "Chicken Momo";
let quantity = 2;
let price = 250;

let total = quantity * price;

let orderMessage = `
Customer: ${customerName}
Food: ${foodName}
Quantity: ${quantity}
Total: Rs. ${total}
`;

console.log(orderMessage);
```

Output:

```text
Customer: Sandip
Food: Chicken Momo
Quantity: 2
Total: Rs. 500
```

---

## 18. Calling Methods Inside `${}`

You can combine template literals with string methods.

```javascript
let foodName = "chicken momo";

let message = `Food: ${foodName.toUpperCase()}`;

console.log(message);
```

Output:

```text
Food: CHICKEN MOMO
```

---

## 19. Nested Expressions

Expressions can contain other expressions.

```javascript
let price = 100;
let quantity = 3;
let discount = 20;

let total = price * quantity;
let finalPrice = total - discount;

let message = `Final Price: Rs. ${finalPrice}`;

console.log(message);
```

Output:

```text
Final Price: Rs. 280
```

---

## 20. Template Literals with Objects

```javascript
let product = {
    name: "Laptop",
    price: 80000,
    quantity: 1
};

let message = `
Product: ${product.name}
Price: Rs. ${product.price}
Quantity: ${product.quantity}
`;

console.log(message);
```

---

## 21. Template Literals with Arrays

```javascript
let skills = ["JavaScript", "React", "Node.js"];

let message = `My skills: ${skills.join(", ")}`;

console.log(message);
```

Output:

```text
My skills: JavaScript, React, Node.js
```

---

## 22. Using Backticks Inside Strings

If you need a backtick inside a template literal, escape it using `\`.

```javascript
let message = `JavaScript uses \`backticks\` for template literals.`;

console.log(message);
```

Output:

```text
JavaScript uses `backticks` for template literals.
```

---

## 23. Escaping Characters

Template literals also support escape sequences.

```javascript
let message = `Hello\nWorld`;

console.log(message);
```

Output:

```text
Hello
World
```

Some common escape sequences:

| Escape | Meaning   |
| ------ | --------- |
| `\n`   | New line  |
| `\t`   | Tab       |
| ```    | Backtick  |
| `\\`   | Backslash |

---

## 24. Template Literal vs Concatenation

### Concatenation

```javascript
let name = "Sandip";
let age = 22;

let message = "My name is " + name + " and I am " + age + " years old.";

console.log(message);
```

### Template Literal

```javascript
let name = "Sandip";
let age = 22;

let message = `My name is ${name} and I am ${age} years old.`;

console.log(message);
```

The second version is generally easier to read when a string contains many variables.

---

## 25. Template Literals with Ternary Operator

```javascript
let isLoggedIn = true;

let message = `Status: ${isLoggedIn ? "Logged In" : "Logged Out"}`;

console.log(message);
```

Output:

```text
Status: Logged In
```

---

## 26. Template Literals with Functions

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}

let price = 250;
let quantity = 3;

let message = `Total: Rs. ${calculateTotal(price, quantity)}`;

console.log(message);
```

Output:

```text
Total: Rs. 750
```

---

## 27. Template Literals in React

Template literals are commonly used in React and JavaScript applications.

Example:

```javascript
const name = "Sandip";

const message = `Welcome, ${name}!`;
```

Inside JSX, JavaScript expressions normally use `{}` rather than `${}`:

```jsx
function Welcome() {
    const name = "Sandip";

    return <h1>Welcome, {name}!</h1>;
}
```

So remember:

```text
JavaScript template literal → ${variable}

JSX expression             → {variable}
```

---

## 28. Template Literals and URLs

Template literals can make dynamic URLs easier to read.

```javascript
let userId = 101;

let url = `/users/${userId}`;

console.log(url);
```

Output:

```text
/users/101
```

Example:

```javascript
let foodId = 25;

let url = `/api/v1/foods/${foodId}`;

console.log(url);
```

Output:

```text
/api/v1/foods/25
```

---

## 29. Template Literals and API Messages

```javascript
let userName = "Sandip";

let message = `Welcome ${userName}, your account was created successfully.`;

console.log(message);
```

This is useful for dynamic messages in applications.

---

## 30. Tagged Template Literals

JavaScript also supports **tagged template literals**.

A function can process a template literal.

Example:

```javascript
function tag(strings, name) {
    return `${strings[0]}${name}${strings[1]}`;
}

let name = "Sandip";

let result = tag`Hello ${name}!`;

console.log(result);
```

Output:

```text
Hello Sandip!
```

Tagged templates are an advanced feature and are less common in everyday beginner JavaScript.

---

## 31. Important Difference

This:

```javascript
let message = `Hello ${name}`;
```

is a template literal.

But this:

```javascript
let message = "Hello ${name}";
```

does **not** perform interpolation.

It produces the literal text:

```text
Hello ${name}
```

Interpolation works with backticks.

---

## 32. Common Mistake

### Incorrect

```javascript
let name = "Sandip";

let message = "Hello ${name}";

console.log(message);
```

Output:

```text
Hello ${name}
```

### Correct

```javascript
let name = "Sandip";

let message = `Hello ${name}`;

console.log(message);
```

Output:

```text
Hello Sandip
```

---

## 33. Another Common Mistake

Do not forget the closing backtick.

Incorrect:

```javascript
let message = `Hello World;
```

Correct:

```javascript
let message = `Hello World`;
```

---

## 34. Template Literal Cheat Sheet

| Feature         | Example                                  |
| --------------- | ---------------------------------------- |
| Create string   | `` `Hello` ``                            |
| Variable        | `` `Hello ${name}` ``                    |
| Expression      | `` `Total: ${price * quantity}` ``       |
| Function        | `` `Result: ${getResult()}` ``           |
| Object property | `` `Name: ${user.name}` ``               |
| Array value     | `` `Food: ${foods[0]}` ``                |
| Multi-line      | `` `Hello<br>World` ``                   |
| Conditional     | `` `${age >= 18 ? "Adult" : "Minor"}` `` |
| Dynamic URL     | `` `/users/${id}` ``                     |

---

## 35. Key Takeaways

* Template literals use backticks.
* They are useful for dynamic strings.
* `${}` is used for interpolation.
* JavaScript expressions can be placed inside `${}`.
* Variables can be directly inserted into strings.
* Functions and methods can be used inside `${}`.
* Template literals support multi-line strings.
* They are often easier to read than string concatenation.
* Backticks inside template literals can be escaped with ```.
* Tagged templates are an advanced feature.
* Template literals are widely used in modern JavaScript and frontend development.

---
