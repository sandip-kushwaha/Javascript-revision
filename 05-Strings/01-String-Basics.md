# JavaScript String Basics

A **string** is a sequence of characters used to store text in JavaScript.

Examples:

```javascript
let name = "Sandip";
let city = "Birgunj";
let message = "Hello World!";
```

---

## 1. What is a String?

A string represents text.

```javascript
let username = "Sandip";
let food = "Pizza";
let message = "Welcome to our hotel";
```

Strings can contain:

* Letters
* Numbers
* Spaces
* Symbols
* Special characters

```javascript
let text = "Hello 123!";
```

Even though `123` looks like a number, everything inside the quotes is part of the string.

---

## 2. Creating Strings

JavaScript provides three common ways to create strings.

### Single Quotes

```javascript
let name = 'Sandip';
```

### Double Quotes

```javascript
let name = "Sandip";
```

### Backticks

```javascript
let name = `Sandip`;
```

All three create strings.

```javascript
console.log(typeof "Hello");
console.log(typeof 'Hello');
console.log(typeof `Hello`);
```

Output:

```text
string
string
string
```

---

## 3. Single Quotes vs Double Quotes

There is no major difference between:

```javascript
let name = "Sandip";
```

and:

```javascript
let name = 'Sandip';
```

Choose one style and use it consistently.

---

## 4. Backticks

Backticks are also used to create strings.

```javascript
let message = `Hello World`;

console.log(message);
```

Backticks are especially useful for:

* Multi-line strings
* Template literals
* Embedding variables

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

Template literals are covered in more detail in:

```text
05-Strings/03-Template-Literals.md
```

---

## 5. String Indexing

Each character in a string has an index.

Indexes start from `0`.

```javascript
let name = "Sandip";
```

The indexes are:

```text
S  a  n  d  i  p
0  1  2  3  4  5
```

You can access a character using square brackets.

```javascript
console.log(name[0]);
```

Output:

```text
S
```

More examples:

```javascript
console.log(name[1]); // a
console.log(name[2]); // n
console.log(name[3]); // d
console.log(name[4]); // i
console.log(name[5]); // p
```

---

## 6. Accessing the Last Character

You can use the string length to access the last character.

```javascript
let name = "Sandip";

console.log(name[name.length - 1]);
```

Output:

```text
p
```

Why?

```text
name.length = 6
```

The last index is:

```text
6 - 1 = 5
```

Therefore:

```javascript
name[5]
```

returns:

```text
p
```

---

## 7. String Length

The `.length` property tells you how many characters are in a string.

```javascript
let name = "Sandip";

console.log(name.length);
```

Output:

```text
6
```

Example:

```javascript
let message = "Hello World";

console.log(message.length);
```

Output:

```text
11
```

The space is also counted as a character.

---

## 8. `charAt()`

You can also access a character using `charAt()`.

```javascript
let name = "Sandip";

console.log(name.charAt(0));
```

Output:

```text
S
```

Example:

```javascript
console.log(name.charAt(1)); // a
console.log(name.charAt(2)); // n
console.log(name.charAt(5)); // p
```

---

## 9. Bracket Notation vs `charAt()`

Both can access characters.

### Bracket notation

```javascript
let name = "Sandip";

console.log(name[0]);
```

### `charAt()`

```javascript
console.log(name.charAt(0));
```

Both return:

```text
S
```

Bracket notation is commonly used because it is shorter.

---

## 10. Invalid Index

If you access an index that does not exist:

```javascript
let name = "Sandip";

console.log(name[10]);
```

Output:

```text
undefined
```

Using `charAt()`:

```javascript
console.log(name.charAt(10));
```

Output:

```text
```

`charAt()` returns an empty string for an invalid index.

---

## 11. Strings Are Immutable

Strings in JavaScript are **immutable**.

This means you cannot directly change an individual character.

```javascript
let name = "Sandip";

name[0] = "X";

console.log(name);
```

The original string remains:

```text
Sandip
```

You cannot do:

```javascript
name[0] = "X";
```

to change the string.

Instead, create a new string.

```javascript
let name = "Sandip";

name = "X" + name.slice(1);

console.log(name);
```

Output:

```text
Xandip
```

---

## 12. Reassigning a String

Although strings are immutable, a variable can be assigned a completely new string.

```javascript
let name = "Sandip";

name = "Prasad";

console.log(name);
```

Output:

```text
Prasad
```

Here, the original string was not modified. The variable now refers to a new string value.

---

## 13. String Concatenation

Concatenation means joining strings together.

The `+` operator can be used.

```javascript
let firstName = "Sandip";
let lastName = "Kushwaha";

let fullName = firstName + " " + lastName;

console.log(fullName);
```

Output:

```text
Sandip Kushwaha
```

---

## 14. Concatenating Multiple Strings

```javascript
let firstName = "Sandip";
let middleName = "Prasad";
let lastName = "Kushwaha";

let fullName = firstName + " " + middleName + " " + lastName;

console.log(fullName);
```

Output:

```text
Sandip Prasad Kushwaha
```

---

## 15. Strings and Numbers

Be careful when using `+` with strings and numbers.

```javascript
let age = 22;

console.log("Age: " + age);
```

Output:

```text
Age: 22
```

The number is converted to a string during concatenation.

Example:

```javascript
console.log("10" + 5);
```

Output:

```text
105
```

Because `"10"` is a string.

But:

```javascript
console.log(10 + 5);
```

Output:

```text
15
```

---

## 16. Converting a Value to String

You can use `String()` to convert a value into a string.

```javascript
let age = 22;

let result = String(age);

console.log(result);
console.log(typeof result);
```

Output:

```text
22
string
```

Other examples:

```javascript
String(100);       // "100"
String(true);      // "true"
String(false);     // "false"
String(null);      // "null"
String(undefined); // "undefined"
```

---

## 17. Empty String

An empty string contains no characters.

```javascript
let message = "";

console.log(message.length);
```

Output:

```text
0
```

Example:

```javascript
let username = "";

if (username === "") {
    console.log("Username is empty");
}
```

---

## 18. Quotes Inside Strings

You can use different types of quotes inside a string.

```javascript
let message = "It's a beautiful day";

console.log(message);
```

You can also use single quotes outside:

```javascript
let message = 'He said "Hello"';

console.log(message);
```

---

## 19. Escape Characters

Sometimes you need to use the same quote inside a string.

You can escape it using `\`.

### Double quote

```javascript
let message = "He said \"Hello\"";

console.log(message);
```

Output:

```text
He said "Hello"
```

### Single quote

```javascript
let message = 'It\'s JavaScript';

console.log(message);
```

Output:

```text
It's JavaScript
```

---

## 20. Common Escape Characters

| Escape | Meaning      |
| ------ | ------------ |
| `\'`   | Single quote |
| `\"`   | Double quote |
| `\\`   | Backslash    |
| `\n`   | New line     |
| `\t`   | Tab          |

Example:

```javascript
let message = "Hello\nWorld";

console.log(message);
```

Output:

```text
Hello
World
```

---

## 21. Multi-Line Strings

Backticks allow strings to span multiple lines.

```javascript
let message = `Hello
Welcome to JavaScript
Have a nice day`;

console.log(message);
```

Output:

```text
Hello
Welcome to JavaScript
Have a nice day
```

---

## 22. Comparing Strings

Strings can be compared using comparison operators.

```javascript
console.log("apple" === "apple");
```

Output:

```text
true
```

Example:

```javascript
console.log("apple" === "orange");
```

Output:

```text
false
```

---

## 23. Strings Are Case-Sensitive

JavaScript strings are case-sensitive.

```javascript
console.log("hello" === "Hello");
```

Output:

```text
false
```

Because:

```text
hello
Hello
```

are different strings.

Example:

```javascript
let username = "Sandip";

console.log(username === "sandip");
```

Output:

```text
false
```

---

## 24. String Comparison with `<` and `>`

Strings can also be compared using:

```javascript
<
>
<=
>=
```

Example:

```javascript
console.log("apple" < "banana");
```

Output:

```text
true
```

JavaScript compares strings based on their character values.

For everyday application code, use these comparisons carefully and use methods such as `localeCompare()` when you need language-aware alphabetical sorting.

---

## 25. String Example

```javascript
let foodName = "Chicken Momo";
let price = 250;

console.log("Food:", foodName);
console.log("Price:", price);
console.log("Food name length:", foodName.length);
console.log("First character:", foodName[0]);
```

Output:

```text
Food: Chicken Momo
Price: 250
Food name length: 12
First character: C
```

---

## 26. Practical Example

Suppose a hotel system stores a customer's name.

```javascript
let customerName = "Sandip Kushwaha";

console.log("Customer:", customerName);
console.log("Characters:", customerName.length);
console.log("First character:", customerName[0]);
console.log("Last character:", customerName[customerName.length - 1]);
```

Output:

```text
Customer: Sandip Kushwaha
Characters: 15
First character: S
Last character: a
```

---

## 27. String Basics Cheat Sheet

| Task              | Example         |
| ----------------- | --------------- |
| Create string     | `"Hello"`       |
| Single quotes     | `'Hello'`       |
| Double quotes     | `"Hello"`       |
| Backticks         | `` `Hello` ``   |
| Get length        | `str.length`    |
| Get character     | `str[0]`        |
| Get character     | `str.charAt(0)` |
| Concatenate       | `str1 + str2`   |
| Convert to string | `String(value)` |
| Empty string      | `""`            |
| Compare strings   | `str1 === str2` |

---

## 28. Important Points

* A string stores text.
* Strings can use single quotes, double quotes, or backticks.
* String indexes start from `0`.
* `.length` returns the number of characters.
* `str[index]` accesses a character.
* `charAt()` can also access a character.
* Strings are immutable.
* `+` can concatenate strings.
* `String()` converts values into strings.
* Strings are case-sensitive.
* Empty strings have a length of `0`.
* Backticks are useful for multi-line strings and template literals.

---

## 29. Quick Example

```javascript
let name = "Sandip";

console.log(name);
console.log(name.length);
console.log(name[0]);
console.log(name[name.length - 1]);
console.log(name.charAt(2));

let greeting = "Hello " + name;

console.log(greeting);
```

Output:

```text
Sandip
6
S
p
n
Hello Sandip
```

---


