# 🚀 JavaScript introduction

JavaScript is one of the most important programming languages for modern web development.

It is used to build:

* Interactive websites
* Web applications
* Frontend applications
* Backend APIs
* Full-stack applications
* Desktop applications
* Mobile applications
* Developer tools

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

A simple way to remember:

```text
HTML       → Structure
CSS        → Presentation
JavaScript → Behavior / Logic
```

---

# JavaScript Example

```js
console.log("Hello World!");
```

`console.log()` prints information to the console.

In a browser:

```text
Open Chrome
    ↓
F12
    ↓
Console
    ↓
Hello World!
```

---

# Where Can JavaScript Run?

JavaScript is not limited to web browsers.

## Browser

JavaScript can run inside browsers such as:

```text
Chrome
Firefox
Edge
Safari
```

---

## Server

JavaScript can also run on servers.

A popular runtime is:

```text
Node.js
```

For example, Node.js can be used to build:

* REST APIs
* Backend applications
* Authentication systems
* Real-time applications
* CLI tools

---

## Other Environments

JavaScript runtimes are also used for:

* Desktop applications
* Mobile applications
* Developer tools
* Build tools
* Server-side applications

---

# JavaScript in MERN Development

JavaScript is especially important for MERN development.

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

A MERN developer uses JavaScript across much of the application stack.

```text
Frontend
   ↓
React + JavaScript
   ↓
Backend
   ↓
Node.js + Express.js
   ↓
Database
   ↓
MongoDB
```

---

# JavaScript Engine

A **JavaScript engine** is software that executes JavaScript code.

Different environments use different JavaScript engines.

| Environment | Engine         |
| ----------- | -------------- |
| Chrome      | V8             |
| Node.js     | V8             |
| Firefox     | SpiderMonkey   |
| Safari      | JavaScriptCore |

For example:

```js
const x = 10;
const y = 20;

console.log(x + y);
```

The JavaScript engine processes and executes this code.

---

# JavaScript Engine and Runtime

It is useful to distinguish between an **engine** and a **runtime**.

## JavaScript Engine

The engine executes JavaScript.

Examples:

```text
V8
SpiderMonkey
JavaScriptCore
```

## JavaScript Runtime

A runtime provides JavaScript execution plus additional APIs and capabilities.

Examples:

```text
Browser
Node.js
Deno
Bun
```

For example, a browser provides APIs such as:

```js
document
window
fetch()
localStorage
```

Node.js provides APIs such as:

```js
fs
http
process
Buffer
```

---

# Comments

Comments are ignored during program execution.

They are useful for documenting code.

## Single-Line Comment

```js
// This is a comment

const age = 22;
```

---

## Multi-Line Comment

```js
/*
   This is
   a multi-line comment
*/
```

---

## Good Comment Practice

Comments should usually explain **why** something exists rather than simply repeating what the code already says.

For example:

```js
// Use cached data to avoid unnecessary API requests.
const cachedUsers = getCachedUsers();
```

Less useful:

```js
// Create a variable called age.
const age = 22;
```

The code already makes that obvious.

---

# Statements

A **statement** represents an instruction that JavaScript can execute.

Example:

```js
const name = "Sandip";

console.log(name);
```

There are two statements:

```js
const name = "Sandip";
```

and:

```js
console.log(name);
```

Another example:

```js
const age = 22;

if (age >= 18) {
    console.log("Adult");
}
```

The declaration, condition, and function call are all part of JavaScript's statement syntax.

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

Example:

```js
const result = 10 + 20;
```

Here:

```text
10 + 20             → expression
const result = ...  → statement
```

---

# Statement vs Expression

| Concept    | Meaning                        | Example           |
| ---------- | ------------------------------ | ----------------- |
| Statement  | Performs an action/instruction | `const age = 22;` |
| Expression | Produces a value               | `10 + 20`         |

Another example:

```js
const result = age >= 18;
```

Here:

```text
age >= 18 → expression
const result = ... → statement
```

---

# Strict Mode

JavaScript provides **strict mode**.

It can be enabled with:

```js
"use strict";
```

Strict mode changes certain JavaScript behaviors and helps detect some programming mistakes.

Example:

```js
"use strict";

x = 10;
```

This causes an error because `x` was not declared.

Correct:

```js
"use strict";

const x = 10;
```

---

# Why Use Strict Mode?

Strict mode can help detect problems such as:

* Accidentally creating global variables
* Some invalid assignments
* Certain duplicate declarations
* Other problematic language behaviors

Modern JavaScript modules are automatically strict mode, so you generally don't need to manually write `"use strict"` in ES modules.

---

# JavaScript is Case-Sensitive

JavaScript distinguishes between uppercase and lowercase letters.

These are different identifiers:

```js
const name = "Sandip";
const Name = "Ram";
const NAME = "Hari";
```

JavaScript treats:

```text
name
Name
NAME
```

as different identifiers.

---

# JavaScript Syntax

JavaScript syntax defines how JavaScript code should be written.

Example:

```js
const name = "Sandip";

console.log(name);
```

Important syntax elements include:

```text
Variables
Functions
Operators
Expressions
Statements
Blocks
Objects
Arrays
Keywords
```

---

# Semicolons

JavaScript allows semicolons to be omitted in many situations because of **Automatic Semicolon Insertion (ASI)**.

Both can work:

```js
const name = "Sandip";

console.log(name);
```

and:

```js
const name = "Sandip"

console.log(name)
```

Many JavaScript projects use semicolons consistently:

```js
const name = "Sandip";

console.log(name);
```

The important thing is to follow the style used by your project.

---

# JavaScript Keywords

JavaScript has reserved keywords with special meanings.

Examples:

```text
let
const
var
if
else
for
while
function
return
class
new
this
switch
case
try
catch
throw
import
export
```

You cannot normally use these keywords as ordinary variable names.

Invalid:

```js
const let = 10;
```

---

# JavaScript Execution

Consider:

```js
const x = 10;
const y = 20;

console.log(x + y);
```

Conceptually:

```text
JavaScript Source Code
        ↓
JavaScript Engine
        ↓
Parse / Process Code
        ↓
Execute Code
        ↓
Output
```

Result:

```text
30
```

JavaScript execution becomes more complex when asynchronous operations, the call stack, queues, and the event loop are involved.

These concepts will be covered later.

---

# Why Learn JavaScript?

JavaScript is important because it is used throughout modern web development.

You can use JavaScript to learn:

```text
Frontend
   ↓
React
   ↓
Backend
   ↓
Node.js
   ↓
Express.js
   ↓
Database Integration
   ↓
Full-Stack Development
```

It is also an important foundation for learning:

* React
* Next.js
* Node.js
* Express.js
* APIs
* Full-stack development
* TypeScript

---

# JavaScript Learning Path

A good learning order is:

```text
JavaScript Basics
       ↓
Variables
       ↓
Data Types
       ↓
Operators
       ↓
Conditions
       ↓
Loops
       ↓
Functions
       ↓
Arrays
       ↓
Objects
       ↓
Modern JavaScript
       ↓
Async JavaScript
       ↓
DOM
       ↓
APIs
       ↓
Advanced JavaScript
       ↓
React
       ↓
Node.js
       ↓
Express.js
       ↓
Full-Stack Development
```

---

# Quick Revision

Remember these points:

```text
JavaScript
    ↓
Programming Language

HTML
    ↓
Structure

CSS
    ↓
Presentation

JavaScript
    ↓
Behavior / Logic
```

JavaScript can run in:

```text
Browsers
Node.js
Deno
Bun
Other JavaScript runtimes
```

JavaScript engines include:

```text
V8
SpiderMonkey
JavaScriptCore
```

Important concepts:

```text
Statement     → instruction
Expression    → produces a value
Comment       → ignored during execution
Strict Mode   → stricter JavaScript behavior
Keyword       → reserved language word
```

---


