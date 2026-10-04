# JavaScript Date Methods

JavaScript provides many methods for reading, changing, comparing, and formatting date values.

This file focuses on practical `Date` methods and useful static methods.

---

# 1. Creating a Date

```javascript
const date = new Date();

console.log(date);
```

Create a specific date:

```javascript
const date = new Date("2026-10-04");

console.log(date);
```

---

# 2. `Date.now()`

Returns the current timestamp in milliseconds.

```javascript
const timestamp = Date.now();

console.log(timestamp);
```

Example:

```javascript
const start = Date.now();

// some operation

const end = Date.now();

console.log(`Time: ${end - start} ms`);
```

---

# 3. `date.getTime()`

Returns the timestamp of a Date object.

```javascript
const date = new Date("2026-10-04");

console.log(date.getTime());
```

Comparison:

```text
Date.now()
    → current timestamp

date.getTime()
    → timestamp of a specific Date object
```

---

# 4. `valueOf()`

`valueOf()` returns the primitive numeric value of a Date.

```javascript
const date = new Date("2026-10-04");

console.log(date.valueOf());
```

For Date objects:

```javascript
date.valueOf();
```

is effectively equivalent to:

```javascript
date.getTime();
```

---

# 5. `Date.parse()`

`Date.parse()` converts a date string into a timestamp.

```javascript
const timestamp = Date.parse("2026-10-04");

console.log(timestamp);
```

You can create a Date from the result:

```javascript
const timestamp = Date.parse("2026-10-04");

const date = new Date(timestamp);

console.log(date);
```

For reliable code, prefer standardized date-time strings such as:

```text
YYYY-MM-DD
YYYY-MM-DDTHH:mm:ss.sssZ
```

---

# 6. `Date.UTC()`

`Date.UTC()` creates a timestamp using UTC components.

```javascript
const timestamp = Date.UTC(
    2026,
    9,
    4
);

console.log(timestamp);
```

Remember that months are zero-based:

```text
0  → January
1  → February
...
9  → October
11 → December
```

Create a Date:

```javascript
const timestamp = Date.UTC(2026, 9, 4);

const date = new Date(timestamp);

console.log(date);
```

---

# 7. Date Getters

Get individual date components:

```javascript
const date = new Date();

console.log(date.getFullYear());
console.log(date.getMonth());
console.log(date.getDate());
console.log(date.getDay());
console.log(date.getHours());
console.log(date.getMinutes());
console.log(date.getSeconds());
console.log(date.getMilliseconds());
```

---

# 8. `getFullYear()`

Returns the year.

```javascript
const date = new Date("2026-10-04");

console.log(date.getFullYear());
```

Output:

```text
2026
```

---

# 9. `getMonth()`

Returns the month from `0` to `11`.

```javascript
const date = new Date("2026-10-04");

console.log(date.getMonth());
```

For October:

```text
9
```

Therefore:

```javascript
const month = date.getMonth() + 1;
```

can be used when you need a human-readable month number.

---

# 10. `getDate()`

Returns the day of the month.

```javascript
const date = new Date("2026-10-04");

console.log(date.getDate());
```

Output:

```text
4
```

---

# 11. `getDay()`

Returns the day of the week.

```javascript
const date = new Date("2026-10-04");

console.log(date.getDay());
```

The values are:

```text
0 → Sunday
1 → Monday
2 → Tuesday
3 → Wednesday
4 → Thursday
5 → Friday
6 → Saturday
```

---

# 12. Time Getters

```javascript
const date = new Date();

date.getHours();

date.getMinutes();

date.getSeconds();

date.getMilliseconds();
```

Example:

```javascript
const hour = date.getHours();
const minute = date.getMinutes();

console.log(`${hour}:${minute}`);
```

---

# 13. UTC Getters

JavaScript also provides UTC versions:

```javascript
date.getUTCFullYear();

date.getUTCMonth();

date.getUTCDate();

date.getUTCDay();

date.getUTCHours();

date.getUTCMinutes();

date.getUTCSeconds();

date.getUTCMilliseconds();
```

Example:

```javascript
const date = new Date();

console.log(date.getHours());
console.log(date.getUTCHours());
```

The values may differ because local time and UTC can use different time zones.

---

# 14. Date Setters

Date values can be modified using setter methods.

```javascript
const date = new Date();

date.setFullYear(2030);
date.setMonth(5);
date.setDate(15);

console.log(date);
```

Common setters:

```text
setFullYear()
setMonth()
setDate()
setHours()
setMinutes()
setSeconds()
setMilliseconds()
```

---

# 15. `setFullYear()`

Changes the year.

```javascript
const date = new Date("2026-10-04");

date.setFullYear(2030);

console.log(date);
```

The year becomes:

```text
2030
```

---

# 16. `setMonth()`

Changes the month.

```javascript
const date = new Date("2026-10-04");

date.setMonth(0);

console.log(date);
```

`0` represents January.

```text
0  → January
1  → February
2  → March
...
```

---

# 17. `setDate()`

Changes the day of the month.

```javascript
const date = new Date("2026-10-04");

date.setDate(20);

console.log(date);
```

The date becomes October 20, 2026.

---

# 18. Date Overflow

JavaScript automatically normalizes invalid date components.

For example:

```javascript
const date = new Date("2026-10-04");

date.setDate(35);

console.log(date);
```

Instead of throwing an error, JavaScript moves into the following month.

This behavior can be useful when performing date calculations.

---

# 19. Month Overflow

The same behavior applies to months.

```javascript
const date = new Date("2026-10-04");

date.setMonth(12);

console.log(date);
```

Because:

```text
0 → January
11 → December
12 → January of the next year
```

JavaScript automatically normalizes the date.

---

# 20. Setting Time

```javascript
const date = new Date();

date.setHours(10);
date.setMinutes(30);
date.setSeconds(0);
date.setMilliseconds(0);

console.log(date);
```

You can also set multiple components:

```javascript
date.setHours(10, 30, 0, 0);
```

---

# 21. UTC Setters

UTC versions are also available:

```javascript
date.setUTCFullYear();

date.setUTCMonth();

date.setUTCDate();

date.setUTCHours();

date.setUTCMinutes();

date.setUTCSeconds();

date.setUTCMilliseconds();
```

Example:

```javascript
const date = new Date();

date.setUTCHours(12);

console.log(date);
```

Use UTC setters when you specifically want to modify UTC components.

---

# 22. `toISOString()`

Returns a standardized UTC date-time string.

```javascript
const date = new Date();

console.log(date.toISOString());
```

Example format:

```text
2026-10-04T03:30:00.000Z
```

This format is especially useful for:

* APIs
* Databases
* Logs
* Data exchange

---

# 23. `toJSON()`

`toJSON()` returns a JSON-compatible date string.

```javascript
const date = new Date();

console.log(date.toJSON());
```

For normal valid Date objects, this produces an ISO-style UTC string.

It is commonly seen when serializing objects:

```javascript
const user = {
    name: "Sandip",
    createdAt: new Date()
};

console.log(JSON.stringify(user));
```

The Date is automatically converted into a JSON date string.

---

# 24. `toUTCString()`

Returns a date string using UTC.

```javascript
const date = new Date();

console.log(date.toUTCString());
```

Example format:

```text
Sun, 04 Oct 2026 03:30:00 GMT
```

---

# 25. `toDateString()`

Returns only the date portion in a readable format.

```javascript
const date = new Date();

console.log(date.toDateString());
```

Example:

```text
Sun Oct 04 2026
```

---

# 26. `toTimeString()`

Returns the local time portion.

```javascript
const date = new Date();

console.log(date.toTimeString());
```

Example:

```text
09:15:00 GMT+0545 (Nepal Time)
```

The exact output depends on the environment and local time zone.

---

# 27. `toLocaleDateString()`

Useful for displaying dates to users.

```javascript
const date = new Date();

console.log(
    date.toLocaleDateString()
);
```

You can specify a locale:

```javascript
console.log(
    date.toLocaleDateString("en-US")
);
```

Another locale:

```javascript
console.log(
    date.toLocaleDateString("en-GB")
);
```

The formatting can differ between locales.

---

# 28. `toLocaleString()`

Displays both date and time using locale-sensitive formatting.

```javascript
const date = new Date();

console.log(
    date.toLocaleString()
);
```

Specify options:

```javascript
console.log(
    date.toLocaleString("en-US", {
        dateStyle: "medium",
        timeStyle: "short"
    })
);
```

Possible output:

```text
Oct 4, 2026, 9:15 AM
```

---

# 29. `Intl.DateTimeFormat`

For repeated or customized date formatting, `Intl.DateTimeFormat` is useful.

```javascript
const formatter = new Intl.DateTimeFormat(
    "en-US",
    {
        dateStyle: "long"
    }
);

console.log(
    formatter.format(new Date())
);
```

Example:

```text
October 4, 2026
```

With time:

```javascript
const formatter = new Intl.DateTimeFormat(
    "en-US",
    {
        dateStyle: "medium",
        timeStyle: "short"
    }
);

console.log(
    formatter.format(new Date())
);
```

---

# 30. Cloning a Date

Date objects are mutable.

If you want a separate Date object, create a copy:

```javascript
const original = new Date();

const copy = new Date(original);

copy.setFullYear(2030);

console.log(original);
console.log(copy);
```

Changing `copy` does not modify `original`.

---

# 31. Avoiding Accidental Mutation

Consider:

```javascript
const original = new Date();

function changeDate(date) {
    date.setDate(date.getDate() + 1);

    return date;
}

changeDate(original);
```

The original Date object has been modified.

To avoid this:

```javascript
function getNextDay(date) {
    const copy = new Date(date);

    copy.setDate(copy.getDate() + 1);

    return copy;
}
```

Now:

```javascript
const original = new Date();

const nextDay = getNextDay(original);
```

The original remains unchanged.

---

# 32. Comparing Dates

Dates can be compared using timestamps.

```javascript
const first = new Date("2026-10-04");
const second = new Date("2026-10-10");

console.log(first < second);
```

Output:

```text
true
```

You can also use:

```javascript
first.getTime() < second.getTime();
```

---

# 33. Checking Equal Dates

Two separate Date objects are not equal by reference:

```javascript
const a = new Date("2026-10-04");
const b = new Date("2026-10-04");

console.log(a === b);
```

Output:

```text
false
```

Compare their timestamps:

```javascript
console.log(
    a.getTime() === b.getTime()
);
```

Output:

```text
true
```

---

# 34. Checking an Invalid Date

Invalid Date objects can be detected using `Number.isNaN()` with `getTime()`.

```javascript
const date = new Date("invalid");

console.log(
    Number.isNaN(date.getTime())
);
```

Output:

```text
true
```

A reusable function:

```javascript
function isValidDate(date) {
    return (
        date instanceof Date &&
        !Number.isNaN(date.getTime())
    );
}
```

---

# 35. Date Methods Summary

| Method                 | Purpose                          |
| ---------------------- | -------------------------------- |
| `Date.now()`           | Current timestamp                |
| `Date.parse()`         | Parse date string into timestamp |
| `Date.UTC()`           | Create UTC timestamp             |
| `getTime()`            | Date timestamp                   |
| `valueOf()`            | Date primitive value             |
| `getFullYear()`        | Local year                       |
| `getMonth()`           | Local month                      |
| `getDate()`            | Day of month                     |
| `getDay()`             | Day of week                      |
| `getHours()`           | Local hour                       |
| `getUTC...()`          | UTC components                   |
| `setFullYear()`        | Change year                      |
| `setMonth()`           | Change month                     |
| `setDate()`            | Change day                       |
| `setHours()`           | Change hour                      |
| `toISOString()`        | ISO UTC string                   |
| `toJSON()`             | JSON-compatible date             |
| `toUTCString()`        | UTC string                       |
| `toLocaleDateString()` | Localized date                   |
| `toLocaleString()`     | Localized date and time          |

---

# 36. Practical Example — Order Created Time

For a backend application:

```javascript
const order = {
    orderId: "ORD-1001",
    createdAt: new Date()
};

console.log(order.createdAt.toISOString());
```

ISO timestamps are useful when sending data through APIs.

---

# 37. Practical Example — Order Expiration

```javascript
const createdAt = new Date();

const expiresAt = new Date(createdAt);

expiresAt.setHours(
    expiresAt.getHours() + 2
);

console.log(
    expiresAt.toISOString()
);
```

The copied Date prevents the original `createdAt` from being changed.

---

# 38. Practical Example — Format Date for UI

```javascript
const date = new Date();

const formatted = date.toLocaleString(
    "en-US",
    {
        dateStyle: "medium",
        timeStyle: "short"
    }
);

console.log(formatted);
```

This is useful for displaying:

```text
Created At
Updated At
Order Time
Booking Time
Payment Time
```

---

# 39. Common Mistakes

## Mistake 1 — Forgetting zero-based months

```javascript
new Date(2026, 9, 4);
```

means:

```text
October 4, 2026
```

not September.

---

## Mistake 2 — Comparing Date objects directly

Avoid:

```javascript
date1 === date2;
```

Use:

```javascript
date1.getTime() === date2.getTime();
```

---

## Mistake 3 — Accidentally mutating a Date

This changes the original:

```javascript
date.setDate(
    date.getDate() + 1
);
```

Create a copy when necessary:

```javascript
const copy = new Date(date);
```

---

## Mistake 4 — Mixing local and UTC methods

Avoid unintentionally mixing:

```javascript
getHours()
```

with:

```javascript
getUTCHours()
```

Know whether your application is working with local time or UTC.

---

# 40. Quick Cheat Sheet

```javascript
const date = new Date();

// Static methods
Date.now();
Date.parse("2026-10-04");
Date.UTC(2026, 9, 4);

// Get
date.getTime();
date.valueOf();

date.getFullYear();
date.getMonth();
date.getDate();
date.getDay();

date.getHours();
date.getMinutes();
date.getSeconds();

// UTC
date.getUTCFullYear();
date.getUTCMonth();
date.getUTCDate();
date.getUTCHours();

// Set
date.setFullYear(2030);
date.setMonth(0);
date.setDate(15);
date.setHours(10);

// Format
date.toISOString();
date.toJSON();
date.toUTCString();
date.toDateString();
date.toTimeString();

date.toLocaleDateString();
date.toLocaleString();
```

---

# Key Takeaways

* `Date.now()` returns the current timestamp.
* `getTime()` returns a Date's timestamp.
* `valueOf()` returns the Date's primitive numeric value.
* `Date.parse()` converts a date string into a timestamp.
* `Date.UTC()` creates a timestamp using UTC components.
* `getMonth()` and `setMonth()` use zero-based months.
* Date setters can automatically normalize overflowing values.
* `getUTC...()` and `setUTC...()` work with UTC components.
* `toISOString()` is useful for APIs and database timestamps.
* `toLocaleString()` and `Intl.DateTimeFormat` are useful for user-facing dates.
* Date objects are mutable, so clone them when you need to preserve the original.
* Compare Date objects using timestamps rather than object references.
* Always consider the difference between local time and UTC.
