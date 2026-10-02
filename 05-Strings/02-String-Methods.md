# JavaScript String Methods

JavaScript provides many built-in methods for working with strings.

String methods can help you:

* Change text
* Search text
* Remove extra spaces
* Extract parts of a string
* Replace text
* Split strings
* Check whether text exists

Example:

```javascript
let message = "Hello JavaScript";

console.log(message.toUpperCase());
```

Output:

```text
HELLO JAVASCRIPT
```

---

## 1. `toUpperCase()`

Converts a string to uppercase.

```javascript
let name = "Sandip";

console.log(name.toUpperCase());
```

Output:

```text
SANDIP
```

The original string is not changed.

```javascript
let name = "Sandip";

name.toUpperCase();

console.log(name);
```

Output:

```text
Sandip
```

To save the result:

```javascript
name = name.toUpperCase();

console.log(name);
```

---

## 2. `toLowerCase()`

Converts a string to lowercase.

```javascript
let name = "SANDIP";

console.log(name.toLowerCase());
```

Output:

```text
sandip
```

Useful when comparing text without caring about capitalization:

```javascript
let username = "SANDIP";

if (username.toLowerCase() === "sandip") {
    console.log("Username matched");
}
```

---

## 3. `trim()`

Removes whitespace from the beginning and end of a string.

```javascript
let name = "   Sandip   ";

console.log(name.trim());
```

Output:

```text
Sandip
```

It does not remove spaces between words.

```javascript
let name = "   Sandip Kushwaha   ";

console.log(name.trim());
```

Output:

```text
Sandip Kushwaha
```

### Practical Example

Useful for form input:

```javascript
let username = "   sandip   ";

username = username.trim();

console.log(username);
```

---

## 4. `trimStart()`

Removes whitespace from the beginning.

```javascript
let name = "   Sandip   ";

console.log(name.trimStart());
```

Output:

```text
Sandip   
```

---

## 5. `trimEnd()`

Removes whitespace from the end.

```javascript
let name = "   Sandip   ";

console.log(name.trimEnd());
```

Output:

```text
   Sandip
```

---

## 6. `includes()`

Checks whether a string contains another string.

It returns:

```text
true
false
```

Example:

```javascript
let message = "Hello JavaScript";

console.log(message.includes("JavaScript"));
```

Output:

```text
true
```

Example:

```javascript
console.log(message.includes("Python"));
```

Output:

```text
false
```

### Case-Sensitive

```javascript
let message = "Hello JavaScript";

console.log(message.includes("javascript"));
```

Output:

```text
false
```

Because uppercase `J` and lowercase `j` are different.

---

## 7. `startsWith()`

Checks whether a string starts with specific text.

```javascript
let message = "Hello JavaScript";

console.log(message.startsWith("Hello"));
```

Output:

```text
true
```

Example:

```javascript
console.log(message.startsWith("JavaScript"));
```

Output:

```text
false
```

---

## 8. `endsWith()`

Checks whether a string ends with specific text.

```javascript
let fileName = "profile.jpg";

console.log(fileName.endsWith(".jpg"));
```

Output:

```text
true
```

Another example:

```javascript
console.log(fileName.endsWith(".png"));
```

Output:

```text
false
```

---

## 9. `indexOf()`

Returns the position of the first occurrence of a string.

```javascript
let message = "Hello JavaScript";

console.log(message.indexOf("JavaScript"));
```

Output:

```text
6
```

Remember that indexes start from `0`.

```text
H e l l o   J a v a S c r i p t
0 1 2 3 4 5 6 ...
```

If the text is not found:

```javascript
console.log(message.indexOf("Python"));
```

Output:

```text
-1
```

---

## 10. `lastIndexOf()`

Returns the position of the last occurrence.

```javascript
let text = "hello hello";

console.log(text.lastIndexOf("hello"));
```

Output:

```text
6
```

Compare:

```javascript
console.log(text.indexOf("hello"));     // 0
console.log(text.lastIndexOf("hello")); // 6
```

---

## 11. `charAt()`

Returns the character at a specific index.

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
console.log(name.charAt(3));
```

Output:

```text
d
```

---

## 12. `at()`

The `at()` method also returns a character at a specific position.

```javascript
let name = "Sandip";

console.log(name.at(0));
```

Output:

```text
S
```

One useful feature is negative indexing.

```javascript
console.log(name.at(-1));
```

Output:

```text
p
```

```javascript
console.log(name.at(-2));
```

Output:

```text
i
```

This is convenient for accessing characters from the end.

---

## 13. `slice()`

Extracts part of a string.

Syntax:

```javascript
string.slice(start, end);
```

Example:

```javascript
let name = "Sandip";

console.log(name.slice(0, 3));
```

Output:

```text
San
```

The `end` index is not included.

```text
S a n d i p
0 1 2 3 4 5
```

`slice(0, 3)` returns indexes `0`, `1`, and `2`.

---

## 14. `slice()` Without End

If you provide only the starting position, it continues to the end.

```javascript
let name = "Sandip";

console.log(name.slice(3));
```

Output:

```text
dip
```

---

## 15. Negative `slice()`

You can use negative indexes with `slice()`.

```javascript
let name = "Sandip";

console.log(name.slice(-3));
```

Output:

```text
dip
```

Another example:

```javascript
console.log(name.slice(-2));
```

Output:

```text
ip
```

---

## 16. `substring()`

`substring()` extracts characters between two indexes.

```javascript
let name = "Sandip";

console.log(name.substring(0, 3));
```

Output:

```text
San
```

Like `slice()`, the ending index is not included.

---

## 17. `slice()` vs `substring()`

| Feature             | `slice()` | `substring()`  |
| ------------------- | --------- | -------------- |
| Extract text        | Yes       | Yes            |
| End excluded        | Yes       | Yes            |
| Negative indexes    | Supported | Treated as `0` |
| Can reverse indexes | No        | Swaps them     |
| Common choice       | Yes       | Yes            |

Example:

```javascript
let text = "JavaScript";

console.log(text.slice(-6));
```

Output:

```text
Script
```

With `substring()`:

```javascript
console.log(text.substring(-6));
```

Negative values are treated as `0`.

---

## 18. `replace()`

Replaces the first matching occurrence.

```javascript
let message = "Hello World";

let result = message.replace("World", "JavaScript");

console.log(result);
```

Output:

```text
Hello JavaScript
```

The original string remains unchanged.

---

## 19. `replaceAll()`

Replaces all matching occurrences.

```javascript
let message = "Hello World World";

let result = message.replaceAll("World", "JavaScript");

console.log(result);
```

Output:

```text
Hello JavaScript JavaScript
```

---

## 20. `split()`

Splits a string into an array.

```javascript
let name = "Sandip Kushwaha";

let result = name.split(" ");

console.log(result);
```

Output:

```text
["Sandip", "Kushwaha"]
```

The separator is a space.

---

## 21. Splitting by Comma

```javascript
let fruits = "apple,banana,mango";

let result = fruits.split(",");

console.log(result);
```

Output:

```text
["apple", "banana", "mango"]
```

---

## 22. Splitting Every Character

Use an empty string as the separator.

```javascript
let name = "Sandip";

console.log(name.split(""));
```

Output:

```text
["S", "a", "n", "d", "i", "p"]
```

---

## 23. `concat()`

Joins strings together.

```javascript
let firstName = "Sandip";
let lastName = "Kushwaha";

let fullName = firstName.concat(" ", lastName);

console.log(fullName);
```

Output:

```text
Sandip Kushwaha
```

However, the `+` operator or template literals are usually simpler for normal string joining.

---

## 24. `repeat()`

Repeats a string a specified number of times.

```javascript
let text = "Hi ";

console.log(text.repeat(3));
```

Output:

```text
Hi Hi Hi
```

Example:

```javascript
console.log("*".repeat(10));
```

Output:

```text
**********
```

---

## 25. `padStart()`

Adds characters to the beginning until the string reaches a specified length.

```javascript
let number = "5";

console.log(number.padStart(3, "0"));
```

Output:

```text
005
```

Another example:

```javascript
let id = "42";

console.log(id.padStart(5, "0"));
```

Output:

```text
00042
```

---

## 26. `padEnd()`

Adds characters to the end until the string reaches a specified length.

```javascript
let number = "5";

console.log(number.padEnd(3, "0"));
```

Output:

```text
500
```

---

## 27. `localeCompare()`

Compares two strings according to locale-aware sorting rules.

```javascript
let result = "apple".localeCompare("banana");

console.log(result);
```

The exact numeric result can vary by environment, but a negative result indicates that `"apple"` comes before `"banana"` according to the comparison.

Example:

```javascript
let names = ["Mango", "Apple", "Banana"];

names.sort((a, b) => a.localeCompare(b));

console.log(names);
```

Output:

```text
["Apple", "Banana", "Mango"]
```

---

## 28. Chaining String Methods

You can use multiple methods together.

```javascript
let username = "   SANDIP   ";

let result = username.trim().toLowerCase();

console.log(result);
```

Output:

```text
sandip
```

Another example:

```javascript
let message = "   Hello JavaScript   ";

let result = message.trim().toUpperCase();

console.log(result);
```

Output:

```text
HELLO JAVASCRIPT
```

---

## 29. Practical Form Example

Suppose a user enters a username with extra spaces.

```javascript
let username = "   Sandip   ";

username = username.trim().toLowerCase();

console.log(username);
```

Output:

```text
sandip
```

This is useful when normalizing user input.

---

## 30. Practical Hotel Example

Suppose a hotel system receives a food name:

```javascript
let foodName = "   Chicken Momo   ";

let cleanName = foodName.trim();

console.log(cleanName);
console.log(cleanName.toUpperCase());
console.log(cleanName.toLowerCase());
```

Output:

```text
Chicken Momo
CHICKEN MOMO
chicken momo
```

---

## 31. Common String Methods

| Method            | Purpose                    | Example                             |
| ----------------- | -------------------------- | ----------------------------------- |
| `toUpperCase()`   | Uppercase                  | `"hello".toUpperCase()`             |
| `toLowerCase()`   | Lowercase                  | `"HELLO".toLowerCase()`             |
| `trim()`          | Remove outer whitespace    | `" hi ".trim()`                     |
| `trimStart()`     | Remove starting whitespace | `" hi".trimStart()`                 |
| `trimEnd()`       | Remove ending whitespace   | `"hi ".trimEnd()`                   |
| `includes()`      | Check text                 | `"hello".includes("ell")`           |
| `startsWith()`    | Check beginning            | `"hello".startsWith("he")`          |
| `endsWith()`      | Check ending               | `"hello".endsWith("lo")`            |
| `indexOf()`       | Find first position        | `"hello".indexOf("l")`              |
| `lastIndexOf()`   | Find last position         | `"hello".lastIndexOf("l")`          |
| `charAt()`        | Get character              | `"hello".charAt(0)`                 |
| `at()`            | Get character              | `"hello".at(-1)`                    |
| `slice()`         | Extract text               | `"hello".slice(1, 4)`               |
| `substring()`     | Extract text               | `"hello".substring(1, 4)`           |
| `replace()`       | Replace first match        | `"hi hi".replace("hi", "hello")`    |
| `replaceAll()`    | Replace all matches        | `"hi hi".replaceAll("hi", "hello")` |
| `split()`         | Convert to array           | `"a,b".split(",")`                  |
| `concat()`        | Join strings               | `"Hello".concat(" World")`          |
| `repeat()`        | Repeat text                | `"Hi ".repeat(3)`                   |
| `padStart()`      | Pad beginning              | `"5".padStart(3, "0")`              |
| `padEnd()`        | Pad ending                 | `"5".padEnd(3, "0")`                |
| `localeCompare()` | Compare strings            | `"a".localeCompare("b")`            |

---

## 32. Important Point: Methods Don't Change the Original String

Most string methods return a new string.

```javascript
let name = "sandip";

name.toUpperCase();

console.log(name);
```

Output:

```text
sandip
```

To keep the result:

```javascript
name = name.toUpperCase();

console.log(name);
```

Output:

```text
SANDIP
```

This happens because strings are immutable.

---

## 33. Quick Example

```javascript
let text = "   Hello JavaScript World   ";

console.log(text.trim());
console.log(text.trim().toUpperCase());
console.log(text.trim().toLowerCase());
console.log(text.includes("JavaScript"));
console.log(text.startsWith("   Hello"));
console.log(text.trim().endsWith("World"));
console.log(text.trim().slice(0, 5));
```

---

## 34. String Method Categories

### Changing Case

```javascript
toUpperCase()
toLowerCase()
```

### Removing Whitespace

```javascript
trim()
trimStart()
trimEnd()
```

### Searching

```javascript
includes()
startsWith()
endsWith()
indexOf()
lastIndexOf()
```

### Extracting

```javascript
slice()
substring()
charAt()
at()
```

### Replacing

```javascript
replace()
replaceAll()
```

### Converting

```javascript
split()
```

### Formatting

```javascript
repeat()
padStart()
padEnd()
```

---

## 35. Key Takeaways

* String methods are built into JavaScript.
* Most string methods return a new string.
* Strings are immutable.
* `toUpperCase()` converts text to uppercase.
* `toLowerCase()` converts text to lowercase.
* `trim()` removes whitespace around text.
* `includes()` checks whether text exists.
* `startsWith()` checks the beginning.
* `endsWith()` checks the end.
* `indexOf()` finds the first matching position.
* `slice()` extracts part of a string.
* `replace()` replaces the first matching occurrence.
* `replaceAll()` replaces all matching occurrences.
* `split()` converts a string into an array.
* `at(-1)` can access the last character.
* String methods can be chained together.

---
