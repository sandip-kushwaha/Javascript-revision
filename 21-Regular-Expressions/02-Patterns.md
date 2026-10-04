# JavaScript Regular Expressions — Patterns

Regular expression patterns allow you to describe more specific text structures.

This file focuses on:

* Character sets
* Quantifiers
* Groups
* Alternation
* Optional characters
* Repeated characters
* Practical validation patterns

---

# 1. Character Set

A character set uses square brackets:

```javascript
/[abc]/
```

It matches one character from:

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

# 2. Character Ranges

You can define ranges.

Lowercase:

```javascript
/[a-z]/
```

Uppercase:

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
    /[A-Z]/.test("Sandip")
);
```

Output:

```text
true
```

---

# 3. Multiple Ranges

You can combine ranges:

```javascript
/[a-zA-Z0-9]/
```

This allows:

```text
lowercase letters
uppercase letters
numbers
```

Example:

```javascript
const pattern =
    /^[a-zA-Z0-9]+$/;

console.log(
    pattern.test("Sandip123")
);
```

Output:

```text
true
```

---

# 4. Negated Character Set

Use `^` inside `[]` to exclude characters.

```javascript
/[^0-9]/
```

This matches a character that is not a digit.

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

---

# 5. Excluding Specific Characters

```javascript
/[^abc]/
```

This matches any character except:

```text
a
b
c
```

Example:

```javascript
console.log(
    /[^abc]/.test("hello")
);
```

Output:

```text
true
```

---

# 6. Quantifiers

Quantifiers specify how many times a pattern can occur.

Common quantifiers:

```text
* 
+
?
{n}
{n,}
{n,m}
```

---

# 7. `*` Quantifier

`*` means:

```text
zero or more
```

Example:

```javascript
/ab*/
```

This can match:

```text
a
ab
abb
abbb
abbbb
```

Example:

```javascript
console.log(
    /ab*/.test("abb")
);
```

Output:

```text
true
```

---

# 8. `+` Quantifier

`+` means:

```text
one or more
```

Example:

```javascript
/ab+/
```

Matches:

```text
ab
abb
abbb
```

But not:

```text
a
```

Example:

```javascript
console.log(
    /ab+/.test("abbb")
);
```

Output:

```text
true
```

---

# 9. `?` Quantifier

`?` means:

```text
zero or one
```

Example:

```javascript
/colou?r/
```

This can match:

```text
color
colour
```

Example:

```javascript
console.log(
    /colou?r/.test("colour")
);
```

Output:

```text
true
```

---

# 10. Exact Count `{n}`

`{n}` requires exactly `n` occurrences.

Example:

```javascript
/\d{4}/
```

This matches four digits.

```javascript
console.log(
    /\d{4}/.test("2026")
);
```

Output:

```text
true
```

---

# 11. Minimum Count `{n,}`

`{n,}` means at least `n` occurrences.

Example:

```javascript
/\d{3,}/
```

Matches:

```text
123
1234
12345
```

Example:

```javascript
console.log(
    /^\d{3,}$/.test("12345")
);
```

Output:

```text
true
```

---

# 12. Range `{n,m}`

`{n,m}` means between `n` and `m` occurrences.

Example:

```javascript
/\d{2,4}/
```

Matches:

```text
12
123
1234
```

A useful validation:

```javascript
/^\d{2,4}$/
```

This requires the entire string to contain between 2 and 4 digits.

---

# 13. Quantifier Summary

| Pattern  | Meaning          |
| -------- | ---------------- |
| `a*`     | Zero or more `a` |
| `a+`     | One or more `a`  |
| `a?`     | Zero or one `a`  |
| `a{3}`   | Exactly 3 `a`    |
| `a{3,}`  | At least 3 `a`   |
| `a{3,5}` | 3 to 5 `a`       |

---

# 14. Combining Character Sets and Quantifiers

Example:

```javascript
/^[a-z]+$/
```

Meaning:

```text
^
→ start

[a-z]
→ lowercase letter

+
→ one or more

$
→ end
```

Therefore, the entire string must contain only lowercase letters.

```javascript
console.log(
    /^[a-z]+$/.test("javascript")
);
```

Output:

```text
true
```

---

# 15. Uppercase Letters Only

```javascript
/^[A-Z]+$/
```

Example:

```javascript
console.log(
    /^[A-Z]+$/.test("JAVASCRIPT")
);
```

Output:

```text
true
```

---

# 16. Letters Only

```javascript
/^[a-zA-Z]+$/
```

Example:

```javascript
console.log(
    /^[a-zA-Z]+$/.test("Sandip")
);
```

Output:

```text
true
```

Numbers are rejected:

```javascript
console.log(
    /^[a-zA-Z]+$/.test("Sandip22")
);
```

Output:

```text
false
```

---

# 17. Letters and Numbers

```javascript
/^[a-zA-Z0-9]+$/
```

Example:

```javascript
console.log(
    /^[a-zA-Z0-9]+$/.test("Sandip22")
);
```

Output:

```text
true
```

---

# 18. Username Pattern

A simple username pattern:

```javascript
/^[a-zA-Z0-9_]+$/
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
    /^[a-zA-Z0-9_]+$/.test("sandip_22")
);
```

Output:

```text
true
```

---

# 19. Username with Length

Suppose a username must contain 4–15 characters:

```javascript
/^[a-zA-Z0-9_]{4,15}$/
```

Example:

```javascript
console.log(
    /^[a-zA-Z0-9_]{4,15}$/.test("sandip_22")
);
```

Output:

```text
true
```

---

# 20. Grouping with Parentheses

Parentheses create a group.

```javascript
/(abc)/
```

The entire `abc` sequence becomes a group.

Groups are especially useful with quantifiers and alternation.

Example:

```javascript
/(ha)+/
```

This matches:

```text
ha
haha
hahaha
```

Example:

```javascript
console.log(
    /(ha)+/.test("hahaha")
);
```

Output:

```text
true
```

---

# 21. Quantifying a Group

Without grouping:

```javascript
/abc+/
```

the `+` applies only to:

```text
c
```

So it matches:

```text
abc
abcc
abccc
```

With grouping:

```javascript
/(abc)+/
```

the `+` applies to the entire group:

```text
abc
abcabc
abcabcabc
```

This distinction is important.

---

# 22. Alternation `|`

The `|` symbol means **OR**.

Example:

```javascript
/cat|dog/
```

Matches either:

```text
cat
dog
```

Example:

```javascript
console.log(
    /cat|dog/.test("I have a dog")
);
```

Output:

```text
true
```

---

# 23. Alternation with Groups

Use parentheses when the alternatives are part of a larger pattern.

```javascript
/^(cat|dog)$/
```

This accepts exactly:

```text
cat
dog
```

Example:

```javascript
console.log(
    /^(cat|dog)$/.test("cat")
);
```

Output:

```text
true
```

---

# 24. Multiple Alternatives

```javascript
/^(red|green|blue)$/
```

This matches exactly one of:

```text
red
green
blue
```

Example:

```javascript
console.log(
    /^(red|green|blue)$/.test("green")
);
```

Output:

```text
true
```

---

# 25. Optional Group

The `?` quantifier can make a group optional.

Example:

```javascript
/^(Mr|Ms)?\s?Sandip$/
```

This can match:

```text
Sandip
Mr Sandip
Ms Sandip
```

---

# 26. Phone Number Pattern

A simple 10-digit phone number:

```javascript
/^\d{10}$/
```

Example:

```javascript
console.log(
    /^\d{10}$/.test("9812345678")
);
```

Output:

```text
true
```

This checks exactly 10 digits.

It does not determine whether the number is actually assigned to someone.

---

# 27. Optional Country Code

A simple pattern allowing an optional `+977`:

```javascript
/^(?:\+977)?\d{10}$/
```

Examples:

```text
9812345678
+9779812345678
```

Both can match.

`(?:...)` creates a non-capturing group.

---

# 28. Non-Capturing Group

Syntax:

```javascript
(?:pattern)
```

Example:

```javascript
/(?:cat|dog)/
```

It groups alternatives without creating a capturing group.

Use it when you need grouping behavior but do not need to retrieve the group's captured value.

---

# 29. Capturing Group

Normal parentheses create a capturing group:

```javascript
/(cat|dog)/
```

Example:

```javascript
const result =
    "I have a cat".match(
        /(cat|dog)/
    );

console.log(result[1]);
```

Output:

```text
cat
```

The captured part can be accessed from the match result.

---

# 30. Multiple Capturing Groups

```javascript
const pattern =
    /(\d{4})-(\d{2})-(\d{2})/;

const result =
    "2026-10-04".match(pattern);

console.log(result[1]);
console.log(result[2]);
console.log(result[3]);
```

Output:

```text
2026
10
04
```

The groups represent:

```text
Group 1 → year
Group 2 → month
Group 3 → day
```

---

# 31. Named Capturing Groups

Modern JavaScript supports named groups.

Syntax:

```javascript
/(?<name>pattern)/
```

Example:

```javascript
const pattern =
    /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;

const result =
    "2026-10-04".match(pattern);

console.log(result.groups.year);
console.log(result.groups.month);
console.log(result.groups.day);
```

Output:

```text
2026
10
04
```

Named groups make complex patterns easier to understand.

---

# 32. Backreference

A backreference refers to text captured by an earlier group.

Example:

```javascript
/^(\w+)\s+\1$/
```

This can match repeated words:

```text
hello hello
```

Example:

```javascript
console.log(
    /^(\w+)\s+\1$/.test("hello hello")
);
```

Output:

```text
true
```

But:

```javascript
console.log(
    /^(\w+)\s+\1$/.test("hello world")
);
```

Output:

```text
false
```

---

# 33. Non-Capturing vs Capturing Groups

| Syntax         | Purpose               |
| -------------- | --------------------- |
| `(abc)`        | Capturing group       |
| `(?:abc)`      | Non-capturing group   |
| `(?<name>abc)` | Named capturing group |

Use capturing groups when you need the matched part later.

Use non-capturing groups when you only need grouping.

---

# 34. Decimal Number Pattern

A basic positive decimal pattern:

```javascript
/^\d+(\.\d+)?$/
```

This can match:

```text
10
10.5
100
100.25
```

Explanation:

```text
\d+
    → one or more digits

(\.\d+)?
    → optional decimal portion
```

---

# 35. Positive Integer Pattern

```javascript
/^\d+$/
```

Matches:

```text
123
456
1000
```

Does not match:

```text
12.5
-10
abc
```

---

# 36. Positive Decimal Pattern

```javascript
/^\d+(\.\d+)?$/
```

Matches:

```text
10
10.5
99.99
```

Does not match:

```text
-10
abc
```

---

# 37. Signed Number Pattern

A simple signed number pattern:

```javascript
/^-?\d+(\.\d+)?$/
```

The `-?` means the minus sign is optional.

Matches:

```text
10
-10
10.5
-10.5
```

---

# 38. Optional Decimal Part

Consider:

```javascript
\d+(\.\d+)?
```

The decimal section:

```text
(\.\d+)?
```

is optional.

Therefore:

```text
100
100.50
```

both can match.

---

# 39. Date Pattern

A basic `YYYY-MM-DD` format:

```javascript
/^\d{4}-\d{2}-\d{2}$/
```

Example:

```javascript
console.log(
    /^\d{4}-\d{2}-\d{2}$/.test(
        "2026-10-04"
    )
);
```

Output:

```text
true
```

This checks the format only.

It does not prove that the date is a real calendar date.

For example:

```text
2026-99-99
```

has the correct format but is not a valid date.

---

# 40. Time Pattern

A basic `HH:MM` format:

```javascript
/^\d{2}:\d{2}$/
```

Matches:

```text
09:30
18:45
```

Again, this checks the structure, not whether the hour and minute values are valid.

---

# 41. Simple URL Pattern

A basic pattern:

```javascript
/^https?:\/\/.+$/
```

This checks that a string starts with:

```text
http://
```

or:

```text
https://
```

Example:

```javascript
console.log(
    /^https?:\/\/.+$/.test(
        "https://example.com"
    )
);
```

Output:

```text
true
```

Complex URL validation is better handled with the `URL` API when possible.

---

# 42. Simple Email Pattern

A commonly used basic pattern:

```javascript
/^[^\s@]+@[^\s@]+\.[^\s@]+$/
```

Example:

```javascript
const email =
    "sandip@example.com";

console.log(
    /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
);
```

Output:

```text
true
```

This is suitable for basic form validation, not a complete implementation of every valid email syntax.

---

# 43. Password Pattern — Minimum Length

At least 8 characters:

```javascript
/^.{8,}$/
```

Example:

```javascript
console.log(
    /^.{8,}$/.test("Sandip123")
);
```

Output:

```text
true
```

---

# 44. Password with Character Requirements

A simple pattern requiring:

* At least 8 characters
* At least one lowercase letter
* At least one uppercase letter
* At least one digit

```javascript
/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/
```

Example:

```javascript
const password =
    "Sandip123";

console.log(
    /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/
        .test(password)
);
```

Output:

```text
true
```

---

# 45. Lookahead

Lookahead checks whether a pattern exists without consuming those characters.

Positive lookahead:

```text
(?=pattern)
```

Example:

```javascript
/(?=.*\d)/
```

This requires at least one digit somewhere in the string.

Example:

```javascript
console.log(
    /^(?=.*\d).+$/.test("Sandip2")
);
```

Output:

```text
true
```

---

# 46. Negative Lookahead

Negative lookahead:

```text
(?!pattern)
```

means the specified pattern must not occur at that position.

Example:

```javascript
/^(?!admin$).+$/
```

This rejects exactly:

```text
admin
```

but can accept:

```text
admin123
```

---

# 47. Password Pattern with Special Character

A stronger example:

```javascript
/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]).{8,}$/
```

This requires:

```text
lowercase
uppercase
digit
special character
minimum 8 characters
```

Example:

```javascript
const password =
    "Sandip@123";

console.log(
    /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]).{8,}$/
        .test(password)
);
```

Output:

```text
true
```

---

# 48. Whitespace Pattern

Match one or more whitespace characters:

```javascript
/\s+/
```

Example:

```javascript
const text =
    "Hello     Sandip";

const result =
    text.split(/\s+/);

console.log(result);
```

Result:

```text
[
    "Hello",
    "Sandip"
]
```

---

# 49. Multiple Spaces

Replace multiple spaces with one:

```javascript
const text =
    "Hello     Sandip";

const result =
    text.replace(/\s+/g, " ");

console.log(result);
```

Output:

```text
Hello Sandip
```

---

# 50. Removing Extra Spaces

```javascript
const text =
    "   Hello     Sandip   ";

const result =
    text
        .trim()
        .replace(/\s+/g, " ");

console.log(result);
```

Output:

```text
Hello Sandip
```

This is useful for normalizing user input.

---

# 51. Pattern Comparison

| Pattern   | Meaning             |            |
| --------- | ------------------- | ---------- |
| `[abc]`   | `a`, `b`, or `c`    |            |
| `[a-z]`   | Lowercase letter    |            |
| `[A-Z]`   | Uppercase letter    |            |
| `[0-9]`   | Digit               |            |
| `[^0-9]`  | Not a digit         |            |
| `a*`      | Zero or more        |            |
| `a+`      | One or more         |            |
| `a?`      | Zero or one         |            |
| `a{3}`    | Exactly 3           |            |
| `a{3,}`   | At least 3          |            |
| `a{3,5}`  | 3 to 5              |            |
| `(abc)`   | Capturing group     |            |
| `(?:abc)` | Non-capturing group |            |
| `a        | b`                  | `a` or `b` |
| `^abc`    | Starts with `abc`   |            |
| `abc$`    | Ends with `abc`     |            |

---

# 52. Practical Validation Function

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

The pattern requires:

```text
4–15 characters
letters
numbers
underscore
```

---

# 53. Practical Phone Validation

```javascript
function isValidPhone(phone) {
    return /^\d{10}$/.test(phone);
}

console.log(
    isValidPhone("9812345678")
);
```

This checks the structure of a 10-digit string.

---

# 54. Practical Email Validation

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

---

# 55. Practical Password Validation

```javascript
function isStrongPassword(password) {
    const pattern =
        /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;

    return pattern.test(password);
}

console.log(
    isStrongPassword("Sandip123")
);
```

---

# 56. Important Pattern Concepts

```text
Character Set
     ↓
[a-z]

Quantifier
     ↓
+

Grouping
     ↓
(...)

Alternation
     ↓
|

Anchor
     ↓
^  $

Capturing
     ↓
(...)

Non-Capturing
     ↓
(?:...)

Lookahead
     ↓
(?=...)
(?!...)
```

---

# 57. Quick Cheat Sheet

```javascript
// Letters only
/^[a-zA-Z]+$/

// Lowercase only
/^[a-z]+$/

// Uppercase only
/^[A-Z]+$/

// Numbers only
/^\d+$/

// Letters and numbers
/^[a-zA-Z0-9]+$/

// Username
/^[a-zA-Z0-9_]{4,15}$/

// 10 digits
/^\d{10}$/

// Date format
/^\d{4}-\d{2}-\d{2}$/

// Email
/^[^\s@]+@[^\s@]+\.[^\s@]+$/

// Minimum 8 characters
/^.{8,}$/

// OR
/cat|dog/

// Optional character
/colou?r/

// Repeated group
/(ha)+/

// Exact count
/\d{4}/

// Range count
/\d{2,4}/

// Start
/^hello/

// End
/hello$/

// Whole word
/\bcat\b/
```

---

# Key Takeaways

* Character sets define which characters are allowed.
* `[a-z]` represents lowercase letters.
* `[A-Z]` represents uppercase letters.
* `[0-9]` represents digits.
* `[^...]` excludes characters.
* `*` means zero or more.
* `+` means one or more.
* `?` means zero or one.
* `{n}` specifies an exact count.
* `{n,}` specifies a minimum count.
* `{n,m}` specifies a range.
* Parentheses create groups.
* `|` provides alternatives.
* `(?:...)` creates a non-capturing group.
* Named groups make captured data easier to access.
* Lookaheads allow conditions without consuming characters.
* `^` and `$` are important when validating the entire input.
* Regex patterns should validate the required format without pretending to prove information that the pattern cannot actually verify.
