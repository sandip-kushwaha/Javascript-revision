# JavaScript Regular Expressions — Flags

Regular expression flags change how a pattern behaves.

Basic syntax:

```javascript
/pattern/flags
```

Example:

```javascript
/hello/i
```

Here:

```text
hello → pattern
i     → flag
```

JavaScript provides several useful flags:

```text
g
i
m
s
u
y
d
```

---

# 1. `i` — Case-Insensitive

The `i` flag ignores uppercase and lowercase differences.

Without `i`:

```javascript
/hello/.test("Hello");
```

Output:

```text
false
```

With `i`:

```javascript
/hello/i.test("Hello");
```

Output:

```text
true
```

It also matches:

```text
hello
Hello
HELLO
HeLLo
```

---

# 2. `g` — Global

The `g` flag finds all matches instead of stopping after the first match.

Example:

```javascript
const text = "cat dog cat";

console.log(
    text.match(/cat/)
);
```

Result:

```text
["cat"]
```

With `g`:

```javascript
console.log(
    text.match(/cat/g)
);
```

Result:

```text
["cat", "cat"]
```

---

# 3. `g` with `replace()`

Without `g`:

```javascript
const text = "cat cat cat";

const result =
    text.replace(/cat/, "dog");

console.log(result);
```

Output:

```text
dog cat cat
```

With `g`:

```javascript
const result =
    text.replace(/cat/g, "dog");

console.log(result);
```

Output:

```text
dog dog dog
```

---

# 4. `m` — Multiline

The `m` flag changes how `^` and `$` work.

Without `m`, `^` and `$` refer to the beginning and end of the entire input.

Example:

```javascript
const text =
`Hello
World`;

console.log(
    /^World/.test(text)
);
```

Output:

```text
false
```

With `m`:

```javascript
console.log(
    /^World/m.test(text)
);
```

Output:

```text
true
```

With `m`:

```text
^ → beginning of each line
$ → end of each line
```

---

# 5. `s` — DotAll

Normally, `.` does not match line terminators.

Example:

```javascript
const text =
`Hello
World`;

console.log(
    /Hello.World/.test(text)
);
```

Output:

```text
false
```

With `s`:

```javascript
console.log(
    /Hello.World/s.test(text)
);
```

Output:

```text
true
```

The `s` flag allows `.` to match line terminators.

---

# 6. `u` — Unicode

The `u` flag enables Unicode-aware regular expression behavior.

Example:

```javascript
const pattern = /\u{1F600}/u;

console.log(
    pattern.test("😀")
);
```

Output:

```text
true
```

The `u` flag is especially useful when working with Unicode characters and Unicode code points.

---

# 7. `y` — Sticky

The `y` flag makes the regular expression match only at the current `lastIndex` position.

Example:

```javascript
const pattern = /hello/y;

pattern.lastIndex = 0;

console.log(
    pattern.test("hello world")
);
```

Output:

```text
true
```

Move the position:

```javascript
pattern.lastIndex = 6;

console.log(
    pattern.test("hello world")
);
```

Output:

```text
false
```

The pattern is looking for `hello` specifically at position `6`, where the text contains `world`.

---

# 8. `g` vs `y`

Both flags are related to repeated matching, but they behave differently.

```text
g
→ searches forward for the next match

y
→ requires the match at the current lastIndex
```

Example:

```javascript
const globalPattern = /cat/g;
const stickyPattern = /cat/y;
```

The sticky pattern is useful when processing text sequentially.

---

# 9. `d` — Has Indices

The `d` flag makes match results include the start and end positions of matched text.

Example:

```javascript
const pattern = /cat/d;

const result =
    "I have a cat".match(pattern);

console.log(result.indices);
```

The result contains the indices of the match.

Conceptually:

```text
[start, end]
```

For:

```text
I have a cat
```

the match `"cat"` has a corresponding start and end position.

---

# 10. Combining Flags

Multiple flags can be used together.

Example:

```javascript
/hello/gi
```

This means:

```text
g → find all matches
i → ignore case
```

Example:

```javascript
const text =
    "Hello hello HELLO";

console.log(
    text.match(/hello/gi)
);
```

Result:

```text
[
    "Hello",
    "hello",
    "HELLO"
]
```

---

# 11. `g` + `i`

A common combination:

```javascript
/hello/gi
```

Example:

```javascript
const text =
    "Hello HELLO hello";

const result =
    text.match(/hello/gi);

console.log(result);
```

Result:

```text
[
    "Hello",
    "HELLO",
    "hello"
]
```

---

# 12. `m` + `i`

You can combine multiline and case-insensitive matching.

```javascript
const text =
`Hello
WORLD
hello`;

const pattern =
    /^hello$/gim;

console.log(
    text.match(pattern)
);
```

Result:

```text
[
    "Hello",
    "hello"
]
```

Here:

```text
g → all matching lines
i → ignore case
m → ^ and $ work per line
```

---

# 13. `g` + `m`

Example:

```javascript
const text =
`apple
banana
apple`;

const result =
    text.match(/^apple$/gm);

console.log(result);
```

Result:

```text
[
    "apple",
    "apple"
]
```

The pattern checks each line because of `m` and returns all matches because of `g`.

---

# 14. `s` + `i`

Example:

```javascript
const text =
`Hello
WORLD`;

const pattern =
    /hello.world/is;

console.log(
    pattern.test(text)
);
```

Output:

```text
true
```

Here:

```text
i → ignores case
s → . matches the line break
```

---

# 15. Checking Flags

A RegExp object provides a `flags` property.

```javascript
const pattern =
    /hello/gi;

console.log(pattern.flags);
```

Output:

```text
gi
```

---

# 16. Individual RegExp Flag Properties

JavaScript also provides properties for individual flags.

```javascript
const pattern =
    /hello/gi;

console.log(pattern.global);
console.log(pattern.ignoreCase);
console.log(pattern.multiline);
console.log(pattern.dotAll);
console.log(pattern.unicode);
console.log(pattern.sticky);
```

Results:

```text
true
true
false
false
false
false
```

---

# 17. Flag Comparison

| Flag | Purpose                |
| ---- | ---------------------- |
| `g`  | Global matching        |
| `i`  | Case-insensitive       |
| `m`  | Multiline              |
| `s`  | DotAll                 |
| `u`  | Unicode-aware matching |
| `y`  | Sticky matching        |
| `d`  | Match indices          |

---

# 18. Commonly Used Flags

In everyday JavaScript development, the most common flags are:

```text
g
i
m
```

Examples:

```javascript
/hello/g
```

Find all matches.

```javascript
/hello/i
```

Ignore case.

```javascript
/^hello$/m
```

Treat each line separately for `^` and `$`.

---

# 19. Search Without Case Sensitivity

Suppose a search feature should match:

```text
JavaScript
javascript
JAVASCRIPT
Javascript
```

Use:

```javascript
const pattern =
    /javascript/i;
```

Example:

```javascript
console.log(
    /javascript/i.test("JavaScript")
);
```

Output:

```text
true
```

---

# 20. Replace All Case Variations

```javascript
const text =
    "JavaScript javascript JAVASCRIPT";

const result =
    text.replace(/javascript/gi, "JS");

console.log(result);
```

Output:

```text
JS JS JS
```

---

# 21. Multiline Text

Consider:

```javascript
const text =
`JavaScript
Python
JavaScript
C++`;
```

Find lines containing JavaScript:

```javascript
const result =
    text.match(/^JavaScript$/gm);

console.log(result);
```

Result:

```text
[
    "JavaScript",
    "JavaScript"
]
```

---

# 22. DotAll Example

Suppose text contains multiple lines:

```javascript
const text =
`Hello
JavaScript`;
```

Normally:

```javascript
/Hello.JavaScript/
```

does not match because `.` does not normally match the line break.

With `s`:

```javascript
/Hello.JavaScript/s
```

it can match across the line break.

---

# 23. Flags with Constructor Syntax

Flags can also be provided when creating a RegExp object.

```javascript
const pattern =
    new RegExp("hello", "gi");
```

This is equivalent to:

```javascript
const pattern =
    /hello/gi;
```

---

# 24. Dynamic Pattern with Flags

```javascript
const word = "javascript";

const pattern =
    new RegExp(word, "gi");

const text =
    "JavaScript JAVASCRIPT";

console.log(
    text.match(pattern)
);
```

Result:

```text
[
    "JavaScript",
    "JAVASCRIPT"
]
```

---

# 25. `lastIndex`

Some regular expression operations use the `lastIndex` property, especially with `g` and `y`.

Example:

```javascript
const pattern = /cat/g;

console.log(pattern.lastIndex);
```

Initially:

```text
0
```

After a successful `exec()`:

```javascript
const text =
    "cat cat";

console.log(
    pattern.exec(text)
);

console.log(pattern.lastIndex);
```

The `lastIndex` value moves to the position after the matched text.

---

# 26. `exec()` with Global Matching

```javascript
const pattern = /cat/g;

const text =
    "cat dog cat";

console.log(
    pattern.exec(text)
);

console.log(
    pattern.exec(text)
);
```

The first call finds the first match.

The next call continues from the updated `lastIndex`.

When there are no more matches:

```text
null
```

is returned and the global regex resets its search position.

---

# 27. Important Difference: `test()` with `g`

A global RegExp is stateful when used with `test()`.

Example:

```javascript
const pattern = /cat/g;

console.log(
    pattern.test("cat cat")
);

console.log(
    pattern.test("cat cat")
);
```

The results can differ because `lastIndex` changes after successful matches.

For repeated boolean checks where state is not wanted, avoid unnecessary use of `g`.

---

# 28. Flag Ordering

Flags are conventionally written together:

```javascript
/hello/gim
```

The order does not change their meaning, but flags should not be duplicated.

Valid:

```javascript
/hello/gi
```

Invalid:

```javascript
/hello/gii
```

because the same flag cannot appear twice.

---

# 29. Practical Example — Search

```javascript
function searchText(text, keyword) {
    const pattern =
        new RegExp(keyword, "i");

    return pattern.test(text);
}

console.log(
    searchText(
        "JavaScript is powerful",
        "javascript"
    )
);
```

Output:

```text
true
```

The `i` flag makes the search case-insensitive.

---

# 30. Practical Example — Replace

```javascript
function removeWord(text, word) {
    const pattern =
        new RegExp(word, "gi");

    return text.replace(pattern, "");
}

console.log(
    removeWord(
        "JavaScript is JavaScript",
        "javascript"
    )
);
```

Result:

```text
" is "
```

The `g` flag removes all occurrences, while `i` ignores case.

---

# 31. Practical Example — Extract Numbers

```javascript
const text =
    "Order 100, Order 200, Order 300";

const numbers =
    text.match(/\d+/g);

console.log(numbers);
```

Result:

```text
[
    "100",
    "200",
    "300"
]
```

Here:

```text
\d+ → one or more digits
g   → find all matches
```

---

# 32. Practical Example — Find All Words

```javascript
const text =
    "Hello Sandip JavaScript";

const words =
    text.match(/\w+/g);

console.log(words);
```

Result:

```text
[
    "Hello",
    "Sandip",
    "JavaScript"
]
```

---

# 33. Practical Example — Case-Insensitive Username Search

```javascript
const users = [
    "Sandip",
    "Ram",
    "Hari"
];

const pattern =
    /sandip/i;

const result =
    users.filter((user) =>
        pattern.test(user)
    );

console.log(result);
```

Result:

```text
[
    "Sandip"
]
```

---

# 34. Which Flag Should You Use?

Use:

```text
g
```

when you need all matches.

Use:

```text
i
```

when uppercase/lowercase should not matter.

Use:

```text
m
```

when working with multiple lines and `^` or `$`.

Use:

```text
s
```

when `.` should match across line breaks.

Use:

```text
u
```

when Unicode-aware behavior is important.

Use:

```text
y
```

when matching must occur exactly at the current position.

Use:

```text
d
```

when match start/end indices are useful.

---

# 35. Quick Cheat Sheet

```javascript
// Global
/hello/g

// Case-insensitive
/hello/i

// Multiline
/^hello$/m

// DotAll
/hello.world/s

// Unicode
/\u{1F600}/u

// Sticky
/hello/y

// Match indices
/hello/d

// Global + case-insensitive
/hello/gi

// Global + multiline + case-insensitive
/hello/gim

// All numbers
/\d+/g

// All words
/\w+/g

// Replace all case variations
text.replace(/hello/gi, "hi");
```

---

# 36. Key Takeaways

* Flags modify regular expression behavior.
* `g` finds multiple matches.
* `i` ignores case.
* `m` changes `^` and `$` behavior for multiline text.
* `s` allows `.` to match line terminators.
* `u` enables Unicode-aware matching behavior.
* `y` performs sticky matching at `lastIndex`.
* `d` exposes match indices.
* Multiple flags can be combined.
* `g` and `y` can make a RegExp stateful through `lastIndex`.
* Use `new RegExp()` when the pattern or flags need to be created dynamically.
* For common application work, `g`, `i`, and `m` are the flags you will encounter most often.
