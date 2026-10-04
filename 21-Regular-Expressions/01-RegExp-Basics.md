# JavaScript Regular Expressions — Basics

Regular Expressions, commonly called **RegExp** or **regex**, are patterns used to search, match, and manipulate text.

They are useful for:

* Form validation
* Searching text
* Finding patterns
* Extracting information
* Replacing text
* Checking usernames
* Validating simple input formats

---

# 1. What is a Regular Expression?

A regular expression describes a pattern.

Example:

```javascript
const pattern = /hello/;
```

This pattern searches for:

```text
hello
```

Example:

```javascript
const text = "Hello JavaScript";

console.log(
    /JavaScript/.test(text)
);
```

Output:

```text
true
```

---

# 2. Creating a Regular Expression

There are two common ways to create a RegExp.

## Literal Syntax

```javascript
const pattern = /hello/;
```

This is the most common syntax.

---

## RegExp Constructor

```javascript
const pattern = new RegExp("hello");
```

Both create a regular expression.

```javascript
/hello/
```

and:

```javascript
new RegExp("hello");
```

represent the same basic pattern.

---

# 3. `test()`

The `test()` method checks whether a pattern exists in a string.

```javascript
const pattern = /JavaScript/;

console.log(
    pattern.test("I am learning JavaScript")
);
```

Output:

```text
true
```

If there is no match:

```javascript
console.log(
    pattern.test("I am learning Python")
);
```

Output:

```text
false
```

---

# 4. Case Sensitivity

Regular expressions are case-sensitive by default.

```javascript
const pattern = /javascript/;

console.log(
    pattern.test("JavaScript")
);
```

Output:

```text
false
```

Because:

```text
javascript
```

and:

```text
JavaScript
```

have different capitalization.

---

# 5. Case-Insensitive Matching

Use the `i` flag:

```javascript
const pattern = /javascript/i;

console.log(
    pattern.test("JavaScript")
);
```

Output:

```text
true
```

The `i` flag makes matching case-insensitive.

---

# 6. Matching Exact Text

```javascript
const pattern = /Sandip/;

console.log(
    pattern.test("Hello Sandip")
);
```

Output:

```text
true
```

The pattern:

```javascript
/Sandip/
```

looks for the text `Sandip` anywhere in the string.

---

# 7. Regular Expression with Variables

```javascript
const username = "Sandip";

const pattern = /Sandip/;

console.log(
    pattern.test(username)
);
```

Output:

```text
true
```

---

# 8. The `g` Flag

The `g` flag means **global matching**.

```javascript
const pattern = /apple/g;

const text =
    "apple apple orange apple";

console.log(
    text.match(pattern)
);
```

Output:

```text
[
    "apple",
    "apple",
    "apple"
]
```

Without `g`, `match()` returns only the first match.

---

# 9. The `m` Flag

The `m` flag enables multiline behavior for anchors such as:

```text
^
$
```

Example:

```javascript
const pattern = /^JavaScript/m;

const text = `
Python
JavaScript
`;

console.log(
    pattern.test(text)
);
```

The `m` flag allows `^` and `$` to work with individual lines rather than only the entire input.

---

# 10. Common RegExp Flags

| Flag | Meaning                      |
| ---- | ---------------------------- |
| `i`  | Case-insensitive             |
| `g`  | Global matching              |
| `m`  | Multiline                    |
| `s`  | Dot matches line terminators |
| `u`  | Unicode-aware matching       |
| `y`  | Sticky matching              |
| `d`  | Include match indices        |

Flags can be combined:

```javascript
const pattern = /javascript/gi;
```

This means:

```text
g → find globally
i → ignore case
```

---

# 11. Character Matching

A regular expression can match individual characters.

```javascript
const pattern = /a/;

console.log(
    pattern.test("Sandip")
);
```

Output:

```text
true
```

The string contains:

```text
a
```

---

# 12. Character Set `[]`

Square brackets define a set of possible characters.

```javascript
const pattern = /[abc]/;
```

This matches any one of:

```text
a
b
c
```

Example:

```javascript
console.log(
    /[abc]/.test("apple")
);
```

Output:

```text
true
```

---

# 13. Character Range

You can define a range.

Lowercase letters:

```javascript
/[a-z]/
```

Uppercase letters:

```javascript
/[A-Z]/
```

Digits:

```javascript
/[0-9]/
```

Example:

```javascript
console.log(
    /[0-9]/.test("Room 25")
);
```

Output:

```text
true
```

---

# 14. Combining Character Ranges

To match letters:

```javascript
/[a-zA-Z]/
```

To match letters or numbers:

```javascript
/[a-zA-Z0-9]/
```

Example:

```javascript
const pattern = /[a-zA-Z0-9]/;

console.log(
    pattern.test("Sandip123")
);
```

Output:

```text
true
```

---

# 15. Negated Character Set

Use `^` inside square brackets to mean "not these characters".

```javascript
/[^0-9]/
```

This matches any character that is not a digit.

Example:

```javascript
console.log(
    /[^0-9]/.test("123a")
);
```

Output:

```text
true
```

Because `a` is not a digit.

---

# 16. Dot `.`

The dot generally matches any character except line terminators.

```javascript
const pattern = /h.t/;
```

It can match:

```text
hat
het
hit
hot
hut
```

Example:

```javascript
console.log(
    /h.t/.test("hot")
);
```

Output:

```text
true
```

---

# 17. Escaping Special Characters

Some characters have special meanings in regex.

Examples:

```text
.
*
+
?
^
$
(
)
[
]
{
}
|
\
```

To match a special character literally, escape it with `\`.

Example:

```javascript
const pattern = /\./;
```

This searches for an actual period.

```javascript
console.log(
    /\./.test("hello.com")
);
```

Output:

```text
true
```

---

# 18. Matching a Literal `$`

Because `$` is a special regex character, escape it:

```javascript
const pattern = /\$/;

console.log(
    pattern.test("$100")
);
```

Output:

```text
true
```

---

# 19. Digit Shortcut `\d`

`\d` matches a digit.

It is equivalent to:

```javascript
[0-9]
```

Example:

```javascript
console.log(
    /\d/.test("Room 25")
);
```

Output:

```text
true
```

---

# 20. Non-Digit `\D`

`\D` matches a character that is not a digit.

Equivalent conceptually to:

```javascript
[^0-9]
```

Example:

```javascript
console.log(
    /\D/.test("123a")
);
```

Output:

```text
true
```

---

# 21. Word Character `\w`

`\w` commonly matches:

```text
letters
digits
underscore
```

Equivalent to:

```text
[A-Za-z0-9_]
```

Example:

```javascript
console.log(
    /\w/.test("Sandip")
);
```

Output:

```text
true
```

---

# 22. Non-Word Character `\W`

`\W` matches a character that is not a word character.

Example:

```javascript
console.log(
    /\W/.test("Hello!")
);
```

Output:

```text
true
```

The `!` character is not a word character.

---

# 23. Whitespace `\s`

`\s` matches whitespace characters.

Examples include:

```text
space
tab
line break
```

Example:

```javascript
console.log(
    /\s/.test("Hello World")
);
```

Output:

```text
true
```

---

# 24. Non-Whitespace `\S`

`\S` matches a non-whitespace character.

```javascript
console.log(
    /\S/.test(" Hello")
);
```

Output:

```text
true
```

The string contains non-whitespace characters.

---

# 25. Word Boundary `\b`

`\b` matches a boundary between a word character and a non-word character.

Example:

```javascript
const pattern = /\bcat\b/;

console.log(
    pattern.test("The cat is here")
);
```

Output:

```text
true
```

But:

```javascript
console.log(
    pattern.test("category")
);
```

Output:

```text
false
```

Because `cat` is part of a larger word.

---

# 26. Start Anchor `^`

`^` matches the beginning of the input.

```javascript
const pattern = /^Hello/;
```

Example:

```javascript
console.log(
    pattern.test("Hello Sandip")
);
```

Output:

```text
true
```

But:

```javascript
console.log(
    pattern.test("Hi Hello")
);
```

Output:

```text
false
```

---

# 27. End Anchor `$`

`$` matches the end of the input.

```javascript
const pattern = /World$/;
```

Example:

```javascript
console.log(
    pattern.test("Hello World")
);
```

Output:

```text
true
```

But:

```javascript
console.log(
    pattern.test("World Hello")
);
```

Output:

```text
false
```

---

# 28. Start and End Together

Use:

```javascript
/^Hello$/
```

to require the entire string to be exactly:

```text
Hello
```

Example:

```javascript
console.log(
    /^Hello$/.test("Hello")
);
```

Output:

```text
true
```

But:

```javascript
console.log(
    /^Hello$/.test("Hello Sandip")
);
```

Output:

```text
false
```

---

# 29. Basic Email Pattern

A simple email pattern can be:

```javascript
const pattern =
    /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
```

Example:

```javascript
const email =
    "sandip@example.com";

console.log(
    pattern.test(email)
);
```

Output:

```text
true
```

This is useful for basic client-side validation, but email syntax is more complicated than this simple pattern.

---

# 30. Number Validation

Match a string containing only digits:

```javascript
const pattern = /^\d+$/;
```

Example:

```javascript
console.log(
    pattern.test("12345")
);
```

Output:

```text
true
```

But:

```javascript
console.log(
    pattern.test("123abc")
);
```

Output:

```text
false
```

---

# 31. Username Validation

A simple username pattern:

```javascript
const pattern =
    /^[a-zA-Z0-9_]+$/;
```

This allows:

```text
letters
numbers
underscore
```

Example:

```javascript
console.log(
    pattern.test("sandip_22")
);
```

Output:

```text
true
```

---

# 32. Password Pattern

A simple example requiring at least 8 characters:

```javascript
const pattern =
    /^.{8,}$/;
```

Example:

```javascript
console.log(
    pattern.test("Sandip123")
);
```

Output:

```text
true
```

This only checks length. A real password policy may require additional rules.

---

# 33. Testing Form Input

```javascript
const username =
    document.querySelector("#username");

const pattern =
    /^[a-zA-Z0-9_]+$/;

if (pattern.test(username.value)) {
    console.log("Valid username");
} else {
    console.log("Invalid username");
}
```

This can be used for basic frontend validation.

---

# 34. `RegExp.prototype.test()`

The `test()` method returns:

```text
true
```

or:

```text
false
```

Example:

```javascript
const pattern = /\d+/;

console.log(
    pattern.test("Room 25")
);
```

Output:

```text
true
```

It is useful when you only need to know whether a pattern exists.

---

# 35. `String.prototype.match()`

Strings also have a `match()` method.

```javascript
const text =
    "JavaScript is powerful";

const result =
    text.match(/JavaScript/);

console.log(result);
```

If a match exists, an array-like match result is returned.

If there is no match:

```javascript
const result =
    text.match(/Python/);

console.log(result);
```

Result:

```text
null
```

---

# 36. `match()` with Global Matching

```javascript
const text =
    "apple apple orange apple";

const result =
    text.match(/apple/g);

console.log(result);
```

Output:

```text
[
    "apple",
    "apple",
    "apple"
]
```

The `g` flag finds all matches.

---

# 37. `search()`

`search()` returns the index of the first match.

```javascript
const text =
    "I love JavaScript";

console.log(
    text.search(/JavaScript/)
);
```

The result is the starting index of the match.

If there is no match:

```javascript
text.search(/Python/);
```

returns:

```text
-1
```

---

# 38. `replace()`

Regular expressions can be used with `replace()`.

```javascript
const text =
    "Hello JavaScript";

const result =
    text.replace(
        /JavaScript/,
        "World"
    );

console.log(result);
```

Output:

```text
Hello World
```

---

# 39. `replaceAll()` with RegExp

You can replace all matching occurrences.

```javascript
const text =
    "apple apple apple";

const result =
    text.replaceAll(
        /apple/g,
        "orange"
    );

console.log(result);
```

Output:

```text
orange orange orange
```

---

# 40. Regex with `matchAll()`

`matchAll()` returns an iterator containing detailed match information.

Example:

```javascript
const text =
    "Room 12, Room 25";

const matches =
    text.matchAll(/\d+/g);

for (const match of matches) {
    console.log(match[0]);
}
```

Output:

```text
12
25
```

---

# 41. Common Basic Patterns

| Pattern     | Meaning                 |
| ----------- | ----------------------- |
| `/abc/`     | Contains `abc`          |
| `/abc/i`    | `abc`, case-insensitive |
| `/abc/g`    | Find all `abc` matches  |
| `/[a-z]/`   | Lowercase letter        |
| `/[A-Z]/`   | Uppercase letter        |
| `/[0-9]/`   | Digit                   |
| `/\d/`      | Digit                   |
| `/\D/`      | Non-digit               |
| `/\w/`      | Word character          |
| `/\W/`      | Non-word character      |
| `/\s/`      | Whitespace              |
| `/\S/`      | Non-whitespace          |
| `/^abc/`    | Starts with `abc`       |
| `/abc$/`    | Ends with `abc`         |
| `/\bcat\b/` | Whole word `cat`        |

---

# 42. Regex Methods Summary

## RegExp Methods

```javascript
pattern.test(text);
pattern.exec(text);
```

## String Methods

```javascript
text.match(pattern);
text.matchAll(pattern);
text.search(pattern);
text.replace(pattern, replacement);
text.replaceAll(pattern, replacement);
text.split(pattern);
```

---

# 43. RegExp Object Properties

A RegExp object provides useful properties.

```javascript
const pattern = /javascript/gi;

console.log(pattern.source);
console.log(pattern.flags);
```

Output:

```text
javascript
gi
```

Other properties include:

```javascript
pattern.global;
pattern.ignoreCase;
pattern.multiline;
pattern.unicode;
pattern.sticky;
```

---

# 44. Literal vs Constructor

Literal:

```javascript
const pattern = /hello/i;
```

Constructor:

```javascript
const pattern =
    new RegExp("hello", "i");
```

Use the literal form when the pattern is known when writing the code.

Use `RegExp()` when the pattern needs to be created dynamically.

Example:

```javascript
const keyword = "JavaScript";

const pattern =
    new RegExp(keyword, "i");

console.log(
    pattern.test("I love JavaScript")
);
```

---

# 45. Escaping Dynamic Values

When inserting arbitrary user text into a dynamically constructed regular expression, special regex characters must be escaped first.

For example, user input might contain:

```text
.
*
+
?
```

These have special meanings in regex.

Do not directly treat arbitrary user input as a regex pattern without considering escaping.

---

# 46. Simple Validation Example

```javascript
function isValidUsername(username) {
    const pattern =
        /^[a-zA-Z0-9_]+$/;

    return pattern.test(username);
}

console.log(
    isValidUsername("sandip_22")
);
```

Output:

```text
true
```

---

# 47. Practical Example — Extract Numbers

```javascript
const text =
    "I have 2 rooms and 15 chairs.";

const numbers =
    text.match(/\d+/g);

console.log(numbers);
```

Output:

```text
[
    "2",
    "15"
]
```

The returned values are strings.

Convert them to numbers:

```javascript
const numbers =
    text
        .match(/\d+/g)
        .map(Number);
```

Result:

```text
[2, 15]
```

---

# 48. Practical Example — Find Words

```javascript
const text =
    "JavaScript makes web development easier.";

const words =
    text.match(/\b\w+\b/g);

console.log(words);
```

This extracts word-like sequences from the string.

---

# 49. Common Mistakes

## Mistake 1 — Forgetting Case Sensitivity

```javascript
/hello/.test("Hello");
```

returns:

```text
false
```

Use:

```javascript
/hello/i
```

when case should not matter.

---

## Mistake 2 — Forgetting `g`

```javascript
"cat cat".match(/cat/);
```

finds the first match.

Use:

```javascript
"cat cat".match(/cat/g);
```

to find all matches.

---

## Mistake 3 — Forgetting Anchors

This:

```javascript
/\d+/
```

can match digits inside a larger string.

For only digits:

```javascript
/^\d+$/
```

---

## Mistake 4 — Confusing `\d` with `\D`

```text
\d → digit
\D → non-digit
```

---

## Mistake 5 — Forgetting to Escape Special Characters

To match a literal period:

```javascript
/\./
```

not:

```javascript
/./
```

because `.` has a special regex meaning.

---

# 50. Quick Cheat Sheet

```javascript
// Basic regex
/hello/

// Case-insensitive
/hello/i

// Global
/hello/g

// Character set
/[abc]/

// Character range
/[a-z]/
/[A-Z]/
/[0-9]/

// Digit
/\d/

// Non-digit
/\D/

// Word character
/\w/

// Non-word character
/\W/

// Whitespace
/\s/

// Non-whitespace
/\S/

// Start
/^hello/

// End
/hello$/

// Exact string
/^hello$/

// Whole word
/\bcat\b/

// Test
/hello/.test("hello")

// Match
"hello".match(/hello/)

// Search
"hello".search(/hello/)

// Replace
"hello".replace(/hello/, "hi")
```

---

# Key Takeaways

* Regular expressions describe patterns in text.
* `/pattern/` is the common regex literal syntax.
* `RegExp()` is useful for dynamically created patterns.
* `test()` returns `true` or `false`.
* `i` makes matching case-insensitive.
* `g` finds multiple matches.
* `^` represents the beginning of a string or line depending on mode.
* `$` represents the end of a string or line depending on mode.
* `[]` defines a character set.
* `\d` matches digits.
* `\w` matches word characters.
* `\s` matches whitespace.
* `\b` represents a word boundary.
* Special regex characters need escaping when matched literally.
* `match()`, `search()`, `replace()`, and `matchAll()` work with regular expressions.
* Regex is useful for validation, searching, extraction, and text replacement.
