# JavaScript Random Numbers

JavaScript provides `Math.random()` for generating pseudo-random numbers.

Random numbers are useful for:

* Random selections
* Games
* Random array elements
* Temporary identifiers
* Simulations
* Random colors
* Random UI values
* Test data

> **Important:** `Math.random()` is not suitable for passwords, authentication tokens, session tokens, or other security-sensitive values.

---

# 1. `Math.random()`

`Math.random()` returns a pseudo-random number between:

```text
0 inclusive
1 exclusive
```

Example:

```javascript
const number = Math.random();

console.log(number);
```

Possible output:

```text
0.284736291
```

Another execution may produce:

```text
0.913827461
```

The exact value is unpredictable for normal application purposes.

---

# 2. Why Is 1 Not Included?

The result follows:

```text
0 <= Math.random() < 1
```

Therefore:

```javascript
Math.random();
```

can produce:

```text
0
```

but it will not produce:

```text
1
```

---

# 3. Random Number from 0 to 1

```javascript
const number = Math.random();

console.log(number);
```

Possible values:

```text
0.0
0.25
0.48
0.73
0.99
```

The value is always less than `1`.

---

# 4. Random Integer from 0 to 9

Use:

```javascript
const number = Math.floor(
    Math.random() * 10
);

console.log(number);
```

Possible results:

```text
0
1
2
3
4
5
6
7
8
9
```

Why?

```text
Math.random()
        ↓
0 to less than 1

× 10
        ↓
0 to less than 10

Math.floor()
        ↓
0 to 9
```

---

# 5. Random Integer from 0 to 99

```javascript
const number = Math.floor(
    Math.random() * 100
);

console.log(number);
```

Possible values:

```text
0 through 99
```

---

# 6. Random Integer from 1 to 10

```javascript
const number =
    Math.floor(Math.random() * 10) + 1;

console.log(number);
```

Possible values:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# 7. Random Integer from 1 to 100

```javascript
const number =
    Math.floor(Math.random() * 100) + 1;

console.log(number);
```

Possible values:

```text
1 through 100
```

---

# 8. Random Integer Between Two Numbers

A useful reusable function:

```javascript
function randomInteger(min, max) {
    return Math.floor(
        Math.random() * (max - min + 1)
    ) + min;
}
```

Example:

```javascript
console.log(
    randomInteger(10, 20)
);
```

Possible results:

```text
10
11
12
...
19
20
```

Both `min` and `max` are included.

---

# 9. How the Formula Works

The formula is:

```javascript
Math.floor(
    Math.random() * (max - min + 1)
) + min
```

Suppose:

```text
min = 10
max = 20
```

Then:

```text
max - min + 1
= 20 - 10 + 1
= 11
```

So there are 11 possible integers:

```text
10 through 20
```

---

# 10. Random Decimal Between Two Numbers

To generate a random decimal:

```javascript
function randomNumber(min, max) {
    return Math.random() * (max - min) + min;
}
```

Example:

```javascript
console.log(
    randomNumber(10, 20)
);
```

Possible output:

```text
13.728491
```

The result is:

```text
10 <= result < 20
```

---

# 11. Random Decimal with Two Decimal Places

```javascript
function randomDecimal(min, max) {
    const number =
        Math.random() * (max - min) + min;

    return Number(number.toFixed(2));
}
```

Example:

```javascript
console.log(
    randomDecimal(10, 20)
);
```

Possible output:

```text
15.72
```

---

# 12. `toFixed()`

`toFixed()` formats a number to a specified number of decimal places.

```javascript
const number = 12.34567;

console.log(
    number.toFixed(2)
);
```

Output:

```text
12.35
```

Note that `toFixed()` returns a string:

```javascript
const result = number.toFixed(2);

console.log(typeof result);
```

Output:

```text
string
```

Convert it back to a number:

```javascript
const result =
    Number(number.toFixed(2));
```

---

# 13. Random Array Element

You can use a random index to select an array element.

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango",
    "Orange"
];

const index = Math.floor(
    Math.random() * fruits.length
);

const fruit = fruits[index];

console.log(fruit);
```

Possible output:

```text
Apple
```

or:

```text
Mango
```

or another element.

---

# 14. Reusable Random Array Function

```javascript
function randomElement(array) {
    const index = Math.floor(
        Math.random() * array.length
    );

    return array[index];
}
```

Example:

```javascript
const colors = [
    "red",
    "blue",
    "green",
    "yellow"
];

console.log(
    randomElement(colors)
);
```

---

# 15. Handle Empty Arrays

If the array is empty:

```javascript
const items = [];

console.log(
    randomElement(items)
);
```

the result will be:

```text
undefined
```

A safer function:

```javascript
function randomElement(array) {
    if (array.length === 0) {
        return undefined;
    }

    const index = Math.floor(
        Math.random() * array.length
    );

    return array[index];
}
```

---

# 16. Random Boolean

You can generate a random Boolean:

```javascript
const value =
    Math.random() < 0.5;

console.log(value);
```

Possible results:

```text
true
false
```

A reusable function:

```javascript
function randomBoolean() {
    return Math.random() < 0.5;
}
```

---

# 17. Random Boolean with Custom Probability

Suppose you want a 70% probability of `true`:

```javascript
function randomBoolean(probability = 0.5) {
    return Math.random() < probability;
}
```

Example:

```javascript
const result = randomBoolean(0.7);

console.log(result);
```

Here:

```text
0.7 → approximately 70% true
0.3 → approximately 30% true
```

This is useful for simulations and game logic.

---

# 18. Random Character

Create a string containing possible characters:

```javascript
const characters =
    "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

const index = Math.floor(
    Math.random() * characters.length
);

const character =
    characters[index];

console.log(character);
```

---

# 19. Random Character Function

```javascript
function randomCharacter(characters) {
    const index = Math.floor(
        Math.random() * characters.length
    );

    return characters[index];
}
```

Example:

```javascript
console.log(
    randomCharacter("ABCDEFG")
);
```

Possible output:

```text
A
B
C
D
E
F
G
```

---

# 20. Random String

For non-security-sensitive purposes:

```javascript
function randomString(length) {
    const characters =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ" +
        "abcdefghijklmnopqrstuvwxyz" +
        "0123456789";

    let result = "";

    for (let i = 0; i < length; i++) {
        const index = Math.floor(
            Math.random() * characters.length
        );

        result += characters[index];
    }

    return result;
}
```

Example:

```javascript
console.log(
    randomString(8)
);
```

Possible output:

```text
aG72kPq9
```

This can be useful for temporary UI data or demonstrations.

---

# 21. Do Not Use `Math.random()` for Security

Do not use:

```javascript
Math.random();
```

for:

* Passwords
* Authentication tokens
* Session tokens
* Password reset tokens
* API secrets
* Cryptographic keys
* Security-sensitive identifiers

`Math.random()` is designed for general-purpose pseudo-random values, not cryptographic security.

---

# 22. Secure Random Values in the Browser

For security-sensitive browser code, use the Web Crypto API.

Example:

```javascript
const array =
    new Uint32Array(1);

crypto.getRandomValues(array);

console.log(array[0]);
```

`crypto.getRandomValues()` is designed for cryptographically strong random values.

---

# 23. Secure Random Integer

A basic approach using Web Crypto:

```javascript
function secureRandomUint32() {
    const array =
        new Uint32Array(1);

    crypto.getRandomValues(array);

    return array[0];
}
```

Example:

```javascript
console.log(
    secureRandomUint32()
);
```

---

# 24. Random Hex Color

Generate a random color:

```javascript
function randomColor() {
    const number =
        Math.floor(
            Math.random() * 0x1000000
        );

    return `#${number
        .toString(16)
        .padStart(6, "0")}`;
}
```

Example:

```javascript
console.log(
    randomColor()
);
```

Possible result:

```text
#3fa82c
```

---

# 25. Random RGB Color

```javascript
function randomRGB() {
    const red =
        Math.floor(Math.random() * 256);

    const green =
        Math.floor(Math.random() * 256);

    const blue =
        Math.floor(Math.random() * 256);

    return `rgb(${red}, ${green}, ${blue})`;
}
```

Example:

```javascript
console.log(
    randomRGB()
);
```

Possible result:

```text
rgb(45, 180, 92)
```

---

# 26. Random Dice Roll

A six-sided dice can be simulated with:

```javascript
function rollDice() {
    return Math.floor(
        Math.random() * 6
    ) + 1;
}
```

Example:

```javascript
console.log(
    rollDice()
);
```

Possible values:

```text
1
2
3
4
5
6
```

---

# 27. Random Coin Toss

```javascript
function tossCoin() {
    return Math.random() < 0.5
        ? "Heads"
        : "Tails";
}
```

Example:

```javascript
console.log(
    tossCoin()
);
```

---

# 28. Random Number for OTP-Like Demo

For a demonstration only:

```javascript
function generateDemoCode() {
    return Math.floor(
        100000 +
        Math.random() * 900000
    );
}

console.log(
    generateDemoCode()
);
```

Possible result:

```text
583214
```

Do **not** use this implementation for real authentication or OTP systems.

For real security-sensitive codes, use a cryptographically secure random source.

---

# 29. Random Date

Generate a random date between two dates:

```javascript
function randomDate(start, end) {
    const startTime = start.getTime();
    const endTime = end.getTime();

    const randomTime =
        startTime +
        Math.random() *
        (endTime - startTime);

    return new Date(randomTime);
}
```

Example:

```javascript
const start =
    new Date("2026-01-01");

const end =
    new Date("2026-12-31");

console.log(
    randomDate(start, end)
);
```

This can be useful for generating test or demo data.

---

# 30. Random Item from Weighted Choices

Sometimes values should not have equal probability.

Example:

```javascript
function weightedChoice() {
    const random = Math.random();

    if (random < 0.7) {
        return "Common";
    }

    if (random < 0.9) {
        return "Rare";
    }

    return "Very Rare";
}
```

Approximate probabilities:

```text
Common     → 70%
Rare       → 20%
Very Rare  → 10%
```

This pattern is useful in simulations and games.

---

# 31. Random Number and Array Index

A common pattern is:

```javascript
const index = Math.floor(
    Math.random() * array.length
);
```

Remember:

```text
array.length
    ↓
number of elements

Math.random()
    ↓
random decimal

Math.floor()
    ↓
valid integer index
```

For:

```javascript
const fruits = [
    "Apple",
    "Banana",
    "Mango"
];
```

valid indexes are:

```text
0
1
2
```

---

# 32. Random Integer Formula

For inclusive `min` and `max`:

```javascript
Math.floor(
    Math.random() * (max - min + 1)
) + min
```

Example:

```javascript
const number =
    Math.floor(
        Math.random() * (20 - 10 + 1)
    ) + 10;
```

Possible values:

```text
10 through 20
```

---

# 33. Random Decimal Formula

For:

```text
min <= value < max
```

use:

```javascript
Math.random() * (max - min) + min
```

Example:

```javascript
const number =
    Math.random() * (20 - 10) + 10;
```

Possible values:

```text
10 <= value < 20
```

---

# 34. Common Random Number Patterns

```javascript
// 0 to less than 1
Math.random();

// 0 to 9
Math.floor(Math.random() * 10);

// 1 to 10
Math.floor(Math.random() * 10) + 1;

// 1 to 100
Math.floor(Math.random() * 100) + 1;

// min to max
Math.floor(
    Math.random() * (max - min + 1)
) + min;

// random array element
array[
    Math.floor(
        Math.random() * array.length
    )
];
```

---

# 35. Common Mistake — Using `Math.round()`

Avoid this for uniform integer ranges:

```javascript
Math.round(
    Math.random() * 10
);
```

This can produce:

```text
0 through 10
```

and the endpoints do not have the same probability as the middle values.

For an integer range, prefer:

```javascript
Math.floor(
    Math.random() * 10
);
```

for `0` through `9`.

---

# 36. Common Mistake — Forgetting `+1`

Incorrect for an inclusive range:

```javascript
Math.floor(
    Math.random() * (max - min)
) + min;
```

This excludes `max`.

For an inclusive integer range:

```javascript
Math.floor(
    Math.random() * (max - min + 1)
) + min;
```

---

# 37. Random Number Utility

A simple utility module can contain:

```javascript
export function randomInteger(min, max) {
    return Math.floor(
        Math.random() * (max - min + 1)
    ) + min;
}

export function randomDecimal(min, max) {
    return Math.random() * (max - min) + min;
}

export function randomElement(array) {
    if (array.length === 0) {
        return undefined;
    }

    const index = Math.floor(
        Math.random() * array.length
    );

    return array[index];
}
```

Then import:

```javascript
import {
    randomInteger,
    randomDecimal,
    randomElement
} from "./random.js";
```

---

# 38. Random Numbers in React

Random values can be useful for UI demonstrations.

Example:

```javascript
const colors = [
    "red",
    "blue",
    "green",
    "orange"
];

const randomColor =
    colors[
        Math.floor(
            Math.random() * colors.length
        )
    ];
```

However, avoid generating random values directly during every render when you need the value to remain stable.

For stable state:

```javascript
const [color] = useState(() =>
    randomElement(colors)
);
```

---

# 39. Random Numbers in Node.js

Node.js can use:

```javascript
Math.random();
```

for ordinary non-security-sensitive randomness.

For security-sensitive values, use Node's `crypto` module instead.

Example:

```javascript
import crypto from "node:crypto";

const value =
    crypto.randomBytes(16).toString("hex");

console.log(value);
```

This is appropriate for security-sensitive random byte generation.

---

# 40. Random Number Summary

| Requirement               | Approach                             |
| ------------------------- | ------------------------------------ |
| Decimal `0–1`             | `Math.random()`                      |
| Integer `0–9`             | `Math.floor(Math.random() * 10)`     |
| Integer `1–10`            | `Math.floor(Math.random() * 10) + 1` |
| Integer `min–max`         | Inclusive formula                    |
| Decimal `min–max`         | `Math.random() * (max - min) + min`  |
| Random array item         | Random index                         |
| Random Boolean            | `Math.random() < 0.5`                |
| Secure browser randomness | `crypto.getRandomValues()`           |
| Secure Node.js randomness | `crypto.randomBytes()`               |

---

# 41. Quick Cheat Sheet

```javascript
// Random decimal: 0 <= n < 1
Math.random();

// Random integer: 0–9
Math.floor(Math.random() * 10);

// Random integer: 1–10
Math.floor(Math.random() * 10) + 1;

// Random integer: min–max inclusive
Math.floor(
    Math.random() * (max - min + 1)
) + min;

// Random decimal: min <= n < max
Math.random() * (max - min) + min;

// Random array element
array[
    Math.floor(
        Math.random() * array.length
    )
];

// Random Boolean
Math.random() < 0.5;

// Secure browser randomness
crypto.getRandomValues(array);

// Secure Node.js randomness
crypto.randomBytes(16);
```

---

# Key Takeaways

* `Math.random()` returns a pseudo-random number from `0` inclusive to `1` exclusive.
* Use `Math.floor()` when generating random integer ranges.
* For an inclusive integer range, use `max - min + 1`.
* Random array selection is done using a random valid index.
* `Math.round()` is generally not the right choice for uniform integer ranges.
* `Math.random()` is suitable for ordinary randomness, not security.
* Use Web Crypto APIs for security-sensitive browser randomness.
* Use Node.js `crypto` APIs for security-sensitive backend randomness.
* `toFixed()` is useful when formatting random decimal values.
* Random values can be used for simulations, games, UI effects, and test data.
