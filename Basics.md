# 🚀 JavaScript Basics — Introduction

JavaScript is one of the most important programming languages for modern web development.

It is used to build:

* Interactive websites
* Web applications
* Frontend applications
* Backend APIs
* Full-stack applications
* Server-side applications
* Browser-based applications

---

# What is JavaScript?

**JavaScript is a high-level, dynamically typed programming language mainly used to make web applications interactive and to build applications across browsers, servers, and other environments.**

For example, HTML gives a webpage its structure:

```html
<h1>Hello</h1>
```

CSS gives it appearance:

```css
h1 {
    color: blue;
}
```

JavaScript gives it behavior:

```js
const heading = document.querySelector("h1");

heading.addEventListener("click", () => {
    alert("Hello Sandip!");
});
```

So a simple way to remember:

```text
HTML       → Structure
CSS        → Presentation
JavaScript → Behavior / Logic
```

---

# JavaScript Example

The simplest JavaScript program:

```js
console.log("Hello World!");
```

`console.log()` prints information to the console.

In a browser:

```text
Open Chrome
    ↓
Press F12
    ↓
Open Console
    ↓
Hello World!
```

You can also open the browser developer tools using:

```text
F12
```

or:

```text
Ctrl + Shift + I
```

---

# Where Can JavaScript Run?

JavaScript is not limited to web browsers.

## 1. Browser

JavaScript can run inside modern browsers such as:

```text
Chrome
Firefox
Edge
Safari
```

Example:

```js
console.log("Running in the browser");
```

---

## 2. Server

JavaScript can also run on servers using JavaScript runtimes such as:

```text
Node.js
```

Example:

```js
console.log("Running on the server");
```

---

## 3. Other Environments

JavaScript runtimes are also used for:

```text
Desktop Applications
Mobile Applications
Command-Line Tools
Build Tools
Server Applications
Cloud Applications
```

---

# JavaScript in MERN Development

For MERN stack development, JavaScript is used throughout the application.

```text
React
   ↓
JavaScript
   ↓
Node.js
   ↓
Express.js
   ↓
MongoDB
```

A typical MERN application can be understood as:

```text
React
  ↓
Frontend
  ↓
API Request
  ↓
Express.js
  ↓
Node.js
  ↓
MongoDB
```

JavaScript is therefore an important foundation for learning the MERN stack.

---

# JavaScript Engine

A **JavaScript engine** is a program that reads, processes, and executes JavaScript code.

Different environments use different JavaScript engines.

| Environment | JavaScript Engine |
| ----------- | ----------------- |
| Chrome      | V8                |
| Node.js     | V8                |
| Firefox     | SpiderMonkey      |
| Safari      | JavaScriptCore    |
| Edge        | V8                |

For example:

```js
const x = 10;
const y = 20;

console.log(x + y);
```

The JavaScript engine processes and executes this code.

The result is:

```text
30
```

---

# JavaScript Engine Examples

## V8

V8 is developed by Google and is used by:

```text
Google Chrome
Node.js
```

## SpiderMonkey

SpiderMonkey is Mozilla's JavaScript engine and is used by:

```text
Firefox
```

## JavaScriptCore

JavaScriptCore is Apple's JavaScript engine and is used by:

```text
Safari
```

---

# Comments

Comments are ignored during program execution.

They are mainly used to:

* Explain code
* Document important decisions
* Leave notes
* Temporarily disable code during development

---

## Single-Line Comment

Use `//` for a single-line comment.

```js
// This is a comment

const age = 22;
```

Another example:

```js
const name = "Sandip"; // User's name
```

---

## Multi-Line Comment

Use `/* */` for multi-line comments.

```js
/*
   This is
   a multi-line comment
*/

const age = 22;
```

Another example:

```js
/*
  Calculate the total
  price of the shopping cart.
*/

const total = price * quantity;
```

### Good Practice

Comments should usually explain **why** something is done rather than simply repeating what the code already says.

For example:

```js
// Bad: add 10 to age
age = age + 10;
```

Better:

```js
// Calculate the user's age after 10 years
age = age + 10;
```

---

# Statements

A **statement** represents an instruction that JavaScript can execute.

Example:

```js
const name = "Sandip";

console.log(name);
```

There are two statements here:

```js
const name = "Sandip";
```

and:

```js
console.log(name);
```

---

## Semicolons

JavaScript allows statements to be written with semicolons:

```js
const name = "Sandip";
console.log(name);
```

JavaScript also has **Automatic Semicolon Insertion (ASI)**, so semicolons are often optional.

However, using semicolons consistently can make code style clearer.

---

# Expressions

An **expression** is code that produces a value.

Example:

```js
10 + 20
```

produces:

```text
30
```

Another example:

```js
age > 18
```

produces:

```text
true
```

---

## Expression Example

```js
const result = 10 + 20;
```

Here:

```text
10 + 20          → Expression
const result =   → Variable declaration
Complete line    → Statement
```

Another example:

```js
const isAdult = age >= 18;
```

Here:

```text
age >= 18        → Expression
isAdult = ...    → Assignment
Complete line    → Statement
```

---

# Statement vs Expression

| Expression       | Statement               |
| ---------------- | ----------------------- |
| Produces a value | Performs an instruction |
| `10 + 20`        | `const x = 10`          |
| `age > 18`       | `if (age > 18) {}`      |
| `"Hello"`        | `console.log("Hello")`  |
| `user.name`      | `return user.name`      |

A simple way to remember:

```text
Expression → produces a value
Statement  → performs an action/instruction
```

---

# Strict Mode

JavaScript provides **Strict Mode** to enable stricter parsing and error handling for certain problematic behaviors.

Enable it using:

```js
"use strict";
```

Example:

```js
"use strict";

x = 10;
```

This causes an error because `x` was not declared.

Without strict mode, some older JavaScript behavior could create an unintended global variable.

---

# Strict Mode Example

Correct code:

```js
"use strict";

const x = 10;

console.log(x);
```

Output:

```text
10
```

Incorrect code:

```js
"use strict";

x = 10;
```

This produces a `ReferenceError`.

---

# Why Strict Mode Is Useful

Strict mode helps detect certain programming mistakes.

It can help prevent things such as:

* Accidentally creating global variables
* Some unsafe assignments
* Certain duplicate parameter declarations
* Some problematic legacy JavaScript behavior

Example:

```js
"use strict";

name = "Sandip";
```

JavaScript reports an error because `name` was not declared.

---

# JavaScript File

JavaScript code is commonly stored in files ending with:

```text
.js
```

Example:

```text
app.js
script.js
main.js
server.js
```

Example `app.js`:

```js
const name = "Sandip";

console.log(`Hello ${name}`);
```

---

# Connecting JavaScript to HTML

JavaScript can be included in an HTML document using the `<script>` element.

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript Example</title>
</head>

<body>

    <h1>Hello JavaScript</h1>

    <script>
        console.log("Hello World!");
    </script>

</body>
</html>
```

---

# External JavaScript File

For larger applications, JavaScript is usually placed in a separate file.

### HTML

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript</title>
</head>

<body>

    <h1>Hello JavaScript</h1>

    <script src="script.js"></script>

</body>
</html>
```

### script.js

```js
console.log("Hello from JavaScript!");
```

This approach keeps:

```text
HTML       → Structure
CSS        → Styling
JavaScript → Logic
```

separated.

---

# Basic JavaScript Syntax

JavaScript is case-sensitive.

These are different variables:

```js
const name = "Sandip";
const Name = "Ram";
```

For example:

```js
console.log(name);
console.log(Name);
```

They refer to different identifiers.

---

# Identifiers

An **identifier** is a name used to identify something in JavaScript.

Examples:

```js
const name = "Sandip";

function greet() {
    console.log("Hello");
}
```

Here:

```text
name  → Identifier
greet → Identifier
```

---

## Identifier Rules

An identifier can contain:

```text
Letters
Digits
_
$
```

But it cannot start with a digit.

Valid:

```js
const name = "Sandip";
const user1 = "Ram";
const _value = 10;
const $price = 100;
```

Invalid:

```js
const 1user = "Ram";
```

JavaScript also has reserved keywords that cannot normally be used as variable names.

Examples:

```text
const
let
class
function
return
if
else
for
while
```

---

# JavaScript Is Dynamically Typed

JavaScript is dynamically typed.

This means a variable can hold different types of values during its lifetime.

Example:

```js
let value = 10;

console.log(value);
// 10

value = "Hello";

console.log(value);
// Hello

value = true;

console.log(value);
// true
```

The variable itself does not have a permanently fixed type.

The value currently stored in it has a type.

---

# First JavaScript Program

Let's combine the basic concepts:

```js
"use strict";

const name = "Sandip";
const age = 22;

console.log("Name:", name);
console.log("Age:", age);
console.log(`Hello ${name}!`);
```

Output:

```text
Name: Sandip
Age: 22
Hello Sandip!
```

---

# Quick Revision

```text
JavaScript
    ↓
Programming Language
    ↓
Adds behavior and logic
    ↓
Runs in browsers and other JavaScript runtimes
    ↓
Used by React, Node.js, Express, and many other tools
```

Important concepts from this chapter:

```text
JavaScript
JavaScript Engine
V8
SpiderMonkey
JavaScriptCore
Comments
Statements
Expressions
Strict Mode
Identifiers
Syntax
Dynamic Typing
```

---

# 🧠 Remember

```text
HTML       → Structure
CSS        → Presentation
JavaScript → Behavior
```

And:

```text
Expression → Produces a value
Statement  → Performs an instruction
```

---

# ✅ Practice

Try writing the following programs yourself.

### 1. Print your name

```js
console.log("Sandip");
```

### 2. Print your age

```js
console.log(22);
```

### 3. Add two numbers

```js
console.log(10 + 20);
```

### 4. Create a simple greeting

```js
const name = "Sandip";

console.log(`Hello ${name}!`);
```

### 5. Create a simple calculation

```js
const price = 100;
const quantity = 3;

const total = price * quantity;

console.log(total);
```

---

# 📌 Next Topic

After understanding JavaScript introduction and syntax, continue with:

```text
01-Basics/
    ↓
02-Variables.md
```

In the next topic, learn:

```text
var
let
const
Variable Declaration
Variable Assignment
Reassignment
Constants
Naming Conventions
Scope Basics
```

---

**Previous:** Introduction
**Next:** [Variables](./02-Variables.md)
