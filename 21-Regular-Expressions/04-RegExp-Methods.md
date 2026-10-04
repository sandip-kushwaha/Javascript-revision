# JavaScript Regular Expressions — Methods

JavaScript provides several methods for working with regular expressions.

The most important ones are:

```text
test()
exec()
match()
matchAll()
search()
replace()
replaceAll()
split()
```

These methods are useful for:

* Searching text
* Validating input
* Extracting information
* Replacing text
* Splitting strings
* Processing API/user data

---

# 1. `test()`

The `test()` method checks whether a pattern matches a string.

It returns:

```text
true
```

or:

```text
false
```

Example:

```javascript
const pattern = /javascript/i;

console.log(
    pattern.test("I love JavaScript")
);
```

Output:

```text
true
```

No match:

```javascript
console.log(
    pattern.test("I love Python")
);
```

Output:

```text
false
```

---

# 2. Basic Validation with `test()`

```javascript
function isValidUsername(username) {
    return /^[a-zA-Z0-9_]{4,15}$/.test(username);
}

console.log(
    isValidUsername("sandip_22")
);
```

Output:

```text
true
```

`test()` is commonly used when you only need to know:

```text
Does it match?
```

---

# 3. `exec()`

The `exec()` method searches for a match and returns detailed match information.

Example:

```javascript
const pattern = /javascript/i;

const result =
    pattern.exec("I love JavaScript");

console.log(result);
```

The result contains information about the match.

Important properties include:

```text
result[0]
result.index
result.input
```

---

# 4. `result[0]`

`result[0]` contains the complete matched text.

```javascript
const pattern = /javascript/i;

const result =
    pattern.exec("I love JavaScript");

console.log(result[0]);
```

Output:

```text
JavaScript
```

---

# 5. `result.index`

The `index` property tells you where the match starts.

```javascript
const pattern = /JavaScript/;

const result =
    pattern.exec("I love JavaScript");

console.log(result.index);
```

The result is the character position where `JavaScript` begins.

Indexes start at:

```text
0
```

---

# 6. `result.input`

The `input` property contains the original string.

```javascript
const pattern = /JavaScript/;

const result =
    pattern.exec("I love JavaScript");

console.log(result.input);
```

Output:

```text
I love JavaScript
```

---

# 7. `exec()` with Capturing Groups

```javascript
const pattern =
    /(\d{4})-(\d{2})-(\d{2})/;

const result =
    pattern.exec("2026-10-04");

console.log(result[0]);
console.log(result[1]);
console.log(result[2]);
console.log(result[3]);
```

The values represent:

```text
result[0] → complete match
result[1] → first captured group
result[2] → second captured group
result[3] → third captured group
```

---

# 8. `exec()` with Global Matching

When using `g`, `exec()` can be called repeatedly to find matches.

```javascript
const pattern = /cat/g;

const text =
    "cat dog cat dog cat";

let result;

while ((result = pattern.exec(text)) !== null) {
    console.log(result[0]);
}
```

Output:

```text
cat
cat
cat
```

The regular expression uses `lastIndex` to continue searching.

---

# 9. `match()`

The `match()` method belongs to strings.

Syntax:

```javascript
string.match(regex);
```

Example:

```javascript
const text =
    "I love JavaScript";

const result =
    text.match(/JavaScript/);

console.log(result);
```

It returns information about the first match.

---

# 10. `match()` Without `g`

```javascript
const text =
    "cat dog cat";

const result =
    text.match(/cat/);

console.log(result);
```

The result contains the first matching occurrence.

---

# 11. `match()` With `g`

With `g`, `match()` returns all matches.

```javascript
const text =
    "cat dog cat dog cat";

const result =
    text.match(/cat/g);

console.log(result);
```

Output:

```text
[
    "cat",
    "cat",
    "cat"
]
```

---

# 12. `match()` with `i`

```javascript
const text =
    "JavaScript javascript JAVASCRIPT";

const result =
    text.match(/javascript/gi);

console.log(result);
```

Result:

```text
[
    "JavaScript",
    "javascript",
    "JAVASCRIPT"
]
```

Here:

```text
g → all matches
i → ignore case
```

---

# 13. `matchAll()`

`matchAll()` returns an iterator containing all matches.

It is especially useful when you need:

* All matches
* Capturing groups
* Match indexes

Example:

```javascript
const text =
    "Name: Sandip, Name: Ram";

const pattern =
    /Name:\s(\w+)/g;

const matches =
    text.matchAll(pattern);

for (const match of matches) {
    console.log(match[1]);
}
```

Output:

```text
Sandip
Ram
```

---

# 14. Why Use `matchAll()`?

Consider:

```javascript
const text =
    "Name: Sandip, Name: Ram";

const pattern =
    /Name:\s(\w+)/g;
```

`match()` with `g` gives:

```text
Name: Sandip
Name: Ram
```

But `matchAll()` also preserves capturing-group information.

This makes `matchAll()` useful when extracting structured data.

---

# 15. Converting `matchAll()` to an Array

`matchAll()` returns an iterator.

You can convert it to an array:

```javascript
const matches = [
    ...text.matchAll(pattern)
];

console.log(matches);
```

Or:

```javascript
const matches =
    Array.from(
        text.matchAll(pattern)
    );
```

---

# 16. `search()`

The `search()` method returns the position of the first match.

Example:

```javascript
const text =
    "I love JavaScript";

const index =
    text.search(/JavaScript/);

console.log(index);
```

It returns the starting index.

If no match is found:

```text
-1
```

---

# 17. `search()` Ignores `g`

The `search()` method returns only the first matching position.

```javascript
const text =
    "cat dog cat";

console.log(
    text.search(/cat/g)
);
```

The `g` flag does not make `search()` return multiple indexes.

---

# 18. `search()` vs `test()`

| Method     | Returns             |
| ---------- | ------------------- |
| `test()`   | `true` / `false`    |
| `search()` | Match index or `-1` |

Example:

```javascript
const pattern = /cat/;

pattern.test("cat dog");
// true

"cat dog".search(pattern);
// 0
```

Use:

```text
test()
→ when you need a Boolean

search()
→ when you need the position
```

---

# 19. `replace()`

The `replace()` method replaces matching text.

Example:

```javascript
const text =
    "Hello Sandip";

const result =
    text.replace(
        /Sandip/,
        "Developer"
    );

console.log(result);
```

Output:

```text
Hello Developer
```

---

# 20. Replace First Match

Without `g`, only the first matching occurrence is replaced.

```javascript
const text =
    "cat cat cat";

const result =
    text.replace(
        /cat/,
        "dog"
    );

console.log(result);
```

Output:

```text
dog cat cat
```

---

# 21. Replace All Matches with `g`

```javascript
const text =
    "cat cat cat";

const result =
    text.replace(
        /cat/g,
        "dog"
    );

console.log(result);
```

Output:

```text
dog dog dog
```

---

# 22. `replace()` with Case-Insensitive Matching

```javascript
const text =
    "JavaScript javascript JAVASCRIPT";

const result =
    text.replace(
        /javascript/gi,
        "JS"
    );

console.log(result);
```

Output:

```text
JS JS JS
```

---

# 23. Replacement String with `$&`

In replacement strings, `$&` represents the complete match.

Example:

```javascript
const text =
    "Hello Sandip";

const result =
    text.replace(
        /Sandip/,
        "Mr. $&"
    );

console.log(result);
```

Output:

```text
Hello Mr. Sandip
```

---

# 24. Replacement String with Capturing Groups

Example:

```javascript
const text =
    "Sandip Kushwaha";

const result =
    text.replace(
        /(\w+)\s(\w+)/,
        "$2, $1"
    );

console.log(result);
```

Output:

```text
Kushwaha, Sandip
```

Here:

```text
$1 → first captured group
$2 → second captured group
```

---

# 25. Replacement Function

`replace()` can also receive a function.

```javascript
const text =
    "10 20 30";

const result =
    text.replace(
        /\d+/g,
        (match) => Number(match) * 2
    );

console.log(result);
```

Output:

```text
20 40 60
```

This is useful when replacement depends on the matched value.

---

# 26. `replaceAll()`

`replaceAll()` replaces every matching occurrence.

Example:

```javascript
const text =
    "cat cat cat";

const result =
    text.replaceAll(
        "cat",
        "dog"
    );

console.log(result);
```

Output:

```text
dog dog dog
```

---

# 27. `replaceAll()` with RegExp

When using a regular expression with `replaceAll()`, the RegExp must have the global `g` flag.

Valid:

```javascript
const result =
    "cat cat".replaceAll(
        /cat/g,
        "dog"
    );
```

Without `g`, a RegExp passed to `replaceAll()` causes an error.

---

# 28. `replace()` vs `replaceAll()`

| Method         | Behavior                                |
| -------------- | --------------------------------------- |
| `replace()`    | Replaces first match unless `g` is used |
| `replaceAll()` | Replaces all matches                    |

Example:

```javascript
"cat cat".replace(/cat/, "dog");
// dog cat
```

```javascript
"cat cat".replace(/cat/g, "dog");
// dog dog
```

```javascript
"cat cat".replaceAll("cat", "dog");
// dog dog
```

---

# 29. `split()`

The `split()` method belongs to strings but can accept a regular expression.

Example:

```javascript
const text =
    "apple,banana,orange";

const result =
    text.split(/,/);

console.log(result);
```

Output:

```text
[
    "apple",
    "banana",
    "orange"
]
```

---

# 30. Split by Multiple Separators

Suppose:

```javascript
const text =
    "apple,banana;orange|mango";
```

You can split using multiple separators:

```javascript
const result =
    text.split(/[,;|]/);

console.log(result);
```

Output:

```text
[
    "apple",
    "banana",
    "orange",
    "mango"
]
```

---

# 31. Split by Whitespace

```javascript
const text =
    "Hello     Sandip JavaScript";

const words =
    text.trim().split(/\s+/);

console.log(words);
```

Output:

```text
[
    "Hello",
    "Sandip",
    "JavaScript"
]
```

---

# 32. Extract Numbers

```javascript
const text =
    "Price: 500, Quantity: 2";

const numbers =
    text.match(/\d+/g);

console.log(numbers);
```

Output:

```text
[
    "500",
    "2"
]
```

Convert them to numbers:

```javascript
const numbers =
    text
        .match(/\d+/g)
        .map(Number);

console.log(numbers);
```

Result:

```text
[
    500,
    2
]
```

---

# 33. Extract Emails

```javascript
const text =
    "Contact sandip@example.com or ram@example.com";

const pattern =
    /[^\s@]+@[^\s@]+\.[^\s@]+/g;

const emails =
    text.match(pattern);

console.log(emails);
```

Result:

```text
[
    "sandip@example.com",
    "ram@example.com"
]
```

---

# 34. Extract Hashtags

```javascript
const text =
    "Learning #JavaScript #React #NodeJS";

const hashtags =
    text.match(/#[A-Za-z0-9_]+/g);

console.log(hashtags);
```

Result:

```text
[
    "#JavaScript",
    "#React",
    "#NodeJS"
]
```

---

# 35. Extract Mentions

```javascript
const text =
    "Hello @sandip and @ram";

const mentions =
    text.match(/@[A-Za-z0-9_]+/g);

console.log(mentions);
```

Result:

```text
[
    "@sandip",
    "@ram"
]
```

---

# 36. Remove HTML Tags

A simple example:

```javascript
const html =
    "<h1>Hello Sandip</h1>";

const text =
    html.replace(/<[^>]*>/g, "");

console.log(text);
```

Output:

```text
Hello Sandip
```

For real HTML parsing, prefer DOM APIs or an HTML parser rather than relying on regex for complex HTML.

---

# 37. Normalize Multiple Spaces

```javascript
const text =
    "Hello     Sandip     Kushwaha";

const result =
    text.replace(/\s+/g, " ");

console.log(result);
```

Output:

```text
Hello Sandip Kushwaha
```

---

# 38. Remove Leading and Trailing Spaces

```javascript
const text =
    "   Hello Sandip   ";

const result =
    text.replace(/^\s+|\s+$/g, "");

console.log(result);
```

Output:

```text
Hello Sandip
```

In simple cases, prefer:

```javascript
text.trim();
```

---

# 39. Validate a Phone Number

```javascript
function isValidPhone(phone) {
    return /^\d{10}$/.test(phone);
}

console.log(
    isValidPhone("9812345678")
);
```

Result:

```text
true
```

---

# 40. Validate an Email

```javascript
function isValidEmail(email) {
    const pattern =
        /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

    return pattern.test(email);
}

console.log(
    isValidEmail("sandip@example.com")
);
```

Result:

```text
true
```

---

# 41. Validate a Username

```javascript
function isValidUsername(username) {
    const pattern =
        /^[a-zA-Z0-9_]{4,15}$/;

    return pattern.test(username);
}

console.log(
    isValidUsername("sandip_22")
);
```

Result:

```text
true
```

---

# 42. Method Comparison

| Method         | Called On | Main Purpose             |
| -------------- | --------- | ------------------------ |
| `test()`       | RegExp    | Check match              |
| `exec()`       | RegExp    | Get detailed match       |
| `match()`      | String    | Get matches              |
| `matchAll()`   | String    | Get all detailed matches |
| `search()`     | String    | Find first index         |
| `replace()`    | String    | Replace matches          |
| `replaceAll()` | String    | Replace all matches      |
| `split()`      | String    | Split using pattern      |

---

# 43. RegExp vs String Methods

Some methods belong to RegExp:

```javascript
pattern.test(text);

pattern.exec(text);
```

Some methods belong to String:

```javascript
text.match(pattern);

text.matchAll(pattern);

text.search(pattern);

text.replace(pattern, replacement);

text.replaceAll(pattern, replacement);

text.split(pattern);
```

---

# 44. Choosing the Right Method

Use:

```text
test()
```

when you only need:

```text
true / false
```

Use:

```text
exec()
```

when you need detailed match information from a RegExp.

Use:

```text
match()
```

when you want matches from a string.

Use:

```text
matchAll()
```

when you need all matches plus capturing groups.

Use:

```text
search()
```

when you need the first match position.

Use:

```text
replace()
```

when you want to replace matching text.

Use:

```text
replaceAll()
```

when you want every occurrence replaced.

Use:

```text
split()
```

when you want to divide a string using a pattern.

---

# 45. Practical Example — Extract Product IDs

```javascript
const text =
    "Product ID: P100, Product ID: P200";

const pattern =
    /P\d+/g;

const ids =
    text.match(pattern);

console.log(ids);
```

Result:

```text
[
    "P100",
    "P200"
]
```

---

# 46. Practical Example — Convert Product IDs

```javascript
const text =
    "Product ID: P100, Product ID: P200";

const ids =
    text
        .match(/P\d+/g)
        .map((id) =>
            Number(id.slice(1))
        );

console.log(ids);
```

Result:

```text
[
    100,
    200
]
```

---

# 47. Practical Example — Hide Phone Numbers

```javascript
const text =
    "Call 9812345678 for support.";

const result =
    text.replace(
        /\d{10}/g,
        "**********"
    );

console.log(result);
```

Output:

```text
Call ********** for support.
```

---

# 48. Practical Example — Mask Emails

```javascript
const email =
    "sandip@example.com";

const masked =
    email.replace(
        /^(.{2}).*(@.*)$/,
        "$1***$2"
    );

console.log(masked);
```

Result:

```text
sa***@example.com
```

This is a simple masking example.

---

# 49. Practical Example — Find Words

```javascript
const text =
    "JavaScript makes web development powerful.";

const words =
    text.match(/\b[A-Za-z]+\b/g);

console.log(words);
```

Result:

```text
[
    "JavaScript",
    "makes",
    "web",
    "development",
    "powerful"
]
```

---

# 50. Common Mistakes

## Mistake 1 — Forgetting `g`

```javascript
"cat cat".replace(
    /cat/,
    "dog"
);
```

Only the first occurrence changes.

Use:

```javascript
"cat cat".replace(
    /cat/g,
    "dog"
);
```

when all occurrences should change.

---

## Mistake 2 — Using `matchAll()` Without `g`

```javascript
text.matchAll(/cat/);
```

`matchAll()` requires a global regular expression.

Use:

```javascript
text.matchAll(/cat/g);
```

---

## Mistake 3 — Using `replaceAll()` with a Non-Global RegExp

Avoid:

```javascript
text.replaceAll(
    /cat/,
    "dog"
);
```

Use:

```javascript
text.replaceAll(
    /cat/g,
    "dog"
);
```

or simply:

```javascript
text.replaceAll(
    "cat",
    "dog"
);
```

---

## Mistake 4 — Expecting `search()` to Return All Matches

```javascript
text.search(/cat/g);
```

`search()` returns only one index.

For all matches, use:

```javascript
text.match(/cat/g);
```

or:

```javascript
text.matchAll(/cat/g);
```

---

## Mistake 5 — Forgetting `lastIndex`

Global regular expressions can maintain matching state.

```javascript
const pattern = /cat/g;
```

Repeated calls to:

```javascript
pattern.test(text);
```

can produce different results because `lastIndex` changes.

---

# 51. Quick Cheat Sheet

```javascript
// Boolean check
/hello/i.test(text);

// Detailed match
/hello/i.exec(text);

// First match
text.match(/hello/);

// All matches
text.match(/hello/g);

// All detailed matches
text.matchAll(/hello/g);

// First index
text.search(/hello/);

// Replace first
text.replace(/hello/, "hi");

// Replace all
text.replace(/hello/g, "hi");

// Replace all
text.replaceAll("hello", "hi");

// Split
text.split(/\s+/);
```

---

# 52. Final Method Map

```text
Regular Expression
        │
        ├── test()
        │     └── true / false
        │
        ├── exec()
        │     └── detailed match
        │
        └── String methods
              │
              ├── match()
              ├── matchAll()
              ├── search()
              ├── replace()
              ├── replaceAll()
              └── split()
```

---

# Key Takeaways

* `test()` is best for simple validation.
* `exec()` provides detailed match information.
* `match()` retrieves matches from a string.
* `matchAll()` retrieves all detailed matches and is useful with capturing groups.
* `search()` returns the first matching position.
* `replace()` replaces matching text.
* `replaceAll()` replaces every occurrence.
* `split()` can use a regular expression as a separator.
* The `g` flag is important when processing multiple matches.
* `matchAll()` requires a global RegExp.
* `replaceAll()` requires a global RegExp when a RegExp is used.
* Global regular expressions can maintain state through `lastIndex`.
* Use the simplest method that matches the task you need to perform.
