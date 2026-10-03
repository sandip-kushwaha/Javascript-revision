# JavaScript Date

The JavaScript `Date` object is used to work with dates and times.

It can be used for:

* Current date and time
* Dates in the past or future
* Comparing dates
* Getting date components
* Formatting dates
* Calculating time differences
* Timestamps

---

# 1. Creating a Date

Create a Date object:

```javascript
const now = new Date();

console.log(now);
```

This creates a Date representing the current date and time.

---

# 2. Current Date and Time

```javascript
const now = new Date();

console.log(now);
```

The exact output depends on the current time and environment.

Example:

```text
2026-10-02T09:30:00.000Z
```

A `Date` object represents a specific point in time.

---

# 3. Date Type

```javascript
const now = new Date();

console.log(typeof now);
```

Output:

```text
object
```

Check whether a value is a Date object:

```javascript
console.log(now instanceof Date);
```

Output:

```text
true
```

---

# 4. Creating a Date from a String

You can create a Date from a date-time string:

```javascript
const date = new Date(
    "2026-10-02T10:30:00"
);

console.log(date);
```

For portable behavior, ISO-style date strings are generally preferable.

Example:

```javascript
const date = new Date(
    "2026-10-02T10:30:00Z"
);
```

The `Z` indicates UTC.

---

# 5. Creating a Date from a Date String

Example:

```javascript
const date = new Date(
    "2026-10-02"
);

console.log(date);
```

For reliable cross-environment behavior, prefer standardized ISO date formats rather than ambiguous formats such as:

```text
10/02/2026
02/10/2026
```

because their interpretation can be unclear.

---

# 6. Creating a Date from Components

You can provide numeric components:

```javascript
const date = new Date(
    2026,
    9,
    2
);

console.log(date);
```

Important:

```text
Year  → 2026
Month → 9
Day   → 2
```

JavaScript months are zero-based.

Therefore:

```text
0  → January
1  → February
2  → March
...
9  → October
11 → December
```

So:

```javascript
new Date(2026, 9, 2);
```

represents October 2, 2026 in the local time zone.

---

# 7. Date Constructor Format

The local-time constructor follows:

```javascript
new Date(
    year,
    monthIndex,
    day,
    hours,
    minutes,
    seconds,
    milliseconds
);
```

Example:

```javascript
const date = new Date(
    2026,
    9,
    2,
    14,
    30,
    0
);
```

The following values are optional:

```text
day
hours
minutes
seconds
milliseconds
```

---

# 8. Month Index

This is one of the most important Date concepts.

```text
January   → 0
February  → 1
March     → 2
April     → 3
May       → 4
June      → 5
July      → 6
August    → 7
September → 8
October   → 9
November  → 10
December  → 11
```

Example:

```javascript
const january =
    new Date(2026, 0, 15);

const december =
    new Date(2026, 11, 15);
```

---

# 9. Date from Timestamp

JavaScript can create a Date from a timestamp.

```javascript
const date = new Date(0);

console.log(date);
```

`0` represents the Unix epoch:

```text
1970-01-01T00:00:00.000Z
```

The exact displayed local time can differ depending on the environment's time zone.

---

# 10. Unix Timestamp

A timestamp represents a point in time as a number of milliseconds since:

```text
1970-01-01T00:00:00.000Z
```

Example:

```javascript
const timestamp =
    Date.now();

console.log(timestamp);
```

The result is a large number such as:

```text
1790933400000
```

The exact value changes with the current time.

---

# 11. Date.now()

Use:

```javascript
Date.now();
```

to get the current timestamp in milliseconds.

Example:

```javascript
const timestamp =
    Date.now();

console.log(timestamp);
```

Unlike:

```javascript
new Date();
```

`Date.now()` returns a number rather than a Date object.

---

# 12. Date Object vs Timestamp

```javascript
const date = new Date();

const timestamp =
    Date.now();
```

Difference:

```text
new Date()
    → Date object

Date.now()
    → number
```

---

# 13. Converting Timestamp to Date

```javascript
const timestamp =
    Date.now();

const date =
    new Date(timestamp);

console.log(date);
```

A timestamp can therefore be converted back into a Date object.

---

# 14. Getting the Current Year

Use:

```javascript
const date = new Date();

console.log(
    date.getFullYear()
);
```

Example output:

```text
2026
```

---

# 15. Getting the Month

Use:

```javascript
const date = new Date();

console.log(
    date.getMonth()
);
```

Remember:

```text
January → 0
December → 11
```

If you need the human-readable month number:

```javascript
const month =
    date.getMonth() + 1;

console.log(month);
```

October becomes:

```text
10
```

---

# 16. Getting the Day of the Month

Use:

```javascript
const date = new Date();

console.log(
    date.getDate()
);
```

For example:

```text
2
```

means the second day of the month.

---

# 17. Getting the Day of the Week

Use:

```javascript
const date = new Date();

console.log(
    date.getDay()
);
```

Values:

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

# 18. Getting Hours

Use:

```javascript
const date = new Date();

console.log(
    date.getHours()
);
```

This returns the local hour from:

```text
0
```

through:

```text
23
```

---

# 19. Getting Minutes

```javascript
const date = new Date();

console.log(
    date.getMinutes()
);
```

Range:

```text
0 → 59
```

---

# 20. Getting Seconds

```javascript
const date = new Date();

console.log(
    date.getSeconds()
);
```

Range:

```text
0 → 59
```

---

# 21. Getting Milliseconds

```javascript
const date = new Date();

console.log(
    date.getMilliseconds()
);
```

Range:

```text
0 → 999
```

---

# 22. Date Getters Summary

| Method              | Returns                  |
| ------------------- | ------------------------ |
| `getFullYear()`     | Local year               |
| `getMonth()`        | Local month index `0–11` |
| `getDate()`         | Day of month             |
| `getDay()`          | Day of week `0–6`        |
| `getHours()`        | Local hour               |
| `getMinutes()`      | Local minutes            |
| `getSeconds()`      | Local seconds            |
| `getMilliseconds()` | Local milliseconds       |

---

# 23. UTC Getters

JavaScript also provides UTC versions.

Examples:

```javascript
const date = new Date();

date.getUTCFullYear();

date.getUTCMonth();

date.getUTCDate();

date.getUTCHours();

date.getUTCMinutes();

date.getUTCSeconds();
```

These read components using UTC rather than the local time zone.

---

# 24. Local Time vs UTC

For example:

```javascript
const date = new Date();

console.log(
    date.getHours()
);

console.log(
    date.getUTCHours()
);
```

The values can differ depending on the local time zone.

This distinction is important when building applications used by people in different countries.

---

# 25. Setting the Year

Use:

```javascript
const date = new Date();

date.setFullYear(2030);

console.log(date);
```

The Date object is modified.

---

# 26. Setting the Month

Use:

```javascript
const date = new Date();

date.setMonth(5);
```

Remember:

```text
5 → June
```

because months are zero-based.

---

# 27. Setting the Date

Use:

```javascript
const date = new Date();

date.setDate(15);
```

This changes the day of the month.

---

# 28. Setting the Time

Hours:

```javascript
date.setHours(10);
```

Minutes:

```javascript
date.setMinutes(30);
```

Seconds:

```javascript
date.setSeconds(45);
```

Milliseconds:

```javascript
date.setMilliseconds(500);
```

---

# 29. Date Setter Summary

| Method              | Purpose          |
| ------------------- | ---------------- |
| `setFullYear()`     | Set local year   |
| `setMonth()`        | Set local month  |
| `setDate()`         | Set day of month |
| `setHours()`        | Set hours        |
| `setMinutes()`      | Set minutes      |
| `setSeconds()`      | Set seconds      |
| `setMilliseconds()` | Set milliseconds |

---

# 30. Formatting a Date

The simplest option is:

```javascript
const date = new Date();

console.log(
    date.toString()
);
```

This produces a human-readable representation based on the environment.

---

# 31. toISOString()

`toISOString()` produces a standardized ISO 8601 representation in UTC.

```javascript
const date = new Date();

console.log(
    date.toISOString()
);
```

Example:

```text
2026-10-02T09:30:00.000Z
```

This format is commonly used in:

* APIs
* Databases
* Logs
* Data exchange

---

# 32. toDateString()

Use:

```javascript
const date = new Date();

console.log(
    date.toDateString()
);
```

Example:

```text
Fri Oct 02 2026
```

This contains the date portion without the time.

---

# 33. toTimeString()

Use:

```javascript
const date = new Date();

console.log(
    date.toTimeString()
);
```

This provides a human-readable local time representation.

---

# 34. toUTCString()

Use:

```javascript
const date = new Date();

console.log(
    date.toUTCString()
);
```

This represents the Date using UTC.

---

# 35. toLocaleDateString()

For user-friendly date formatting:

```javascript
const date = new Date();

console.log(
    date.toLocaleDateString()
);
```

The exact output depends on the user's locale.

You can specify a locale:

```javascript
console.log(
    date.toLocaleDateString("en-US")
);
```

---

# 36. toLocaleString()

For both date and time:

```javascript
const date = new Date();

console.log(
    date.toLocaleString()
);
```

You can provide formatting options:

```javascript
const formatted =
    date.toLocaleString(
        "en-US",
        {
            dateStyle: "medium",
            timeStyle: "short"
        }
    );

console.log(formatted);
```

This is useful when displaying dates to users.

---

# 37. Comparing Dates

Dates can be compared using timestamps.

Example:

```javascript
const date1 =
    new Date("2026-01-01");

const date2 =
    new Date("2026-12-01");

console.log(
    date1.getTime() <
    date2.getTime()
);
```

Output:

```text
true
```

---

# 38. getTime()

Use:

```javascript
const date = new Date();

const timestamp =
    date.getTime();

console.log(timestamp);
```

`getTime()` returns the number of milliseconds since the Unix epoch.

---

# 39. Comparing Date Objects

Do not normally compare Date objects directly using `===`.

Example:

```javascript
const date1 =
    new Date("2026-01-01");

const date2 =
    new Date("2026-01-01");

console.log(date1 === date2);
```

Output:

```text
false
```

They are two different Date objects.

Compare their timestamps instead:

```javascript
console.log(
    date1.getTime() ===
    date2.getTime()
);
```

Output:

```text
true
```

---

# 40. Calculating Date Difference

Suppose:

```javascript
const start =
    new Date("2026-01-01");

const end =
    new Date("2026-01-10");
```

Calculate milliseconds:

```javascript
const difference =
    end.getTime() -
    start.getTime();

console.log(difference);
```

Convert to days:

```javascript
const days =
    difference /
    (1000 * 60 * 60 * 24);

console.log(days);
```

Output:

```text
9
```

---

# 41. Date Difference Units

Remember:

```text
1 second
    = 1000 milliseconds

1 minute
    = 60 seconds

1 hour
    = 60 minutes

1 day
    = 24 hours
```

Therefore:

```javascript
1000 * 60 * 60 * 24
```

represents the number of milliseconds in 24 hours.

---

# 42. Adding Days

You can modify a Date:

```javascript
const date = new Date();

date.setDate(
    date.getDate() + 7
);

console.log(date);
```

This moves the date forward by seven calendar days.

---

# 43. Subtracting Days

```javascript
const date = new Date();

date.setDate(
    date.getDate() - 7
);

console.log(date);
```

This moves the date backward by seven calendar days.

---

# 44. Adding Hours

```javascript
const date = new Date();

date.setHours(
    date.getHours() + 2
);

console.log(date);
```

This moves the Date forward by two hours.

---

# 45. Date Validation

You can check whether a Date is invalid.

Example:

```javascript
const date =
    new Date("invalid");

console.log(
    Number.isNaN(
        date.getTime()
    )
);
```

Output:

```text
true
```

A valid Date produces a numeric timestamp.

---

# 46. Invalid Date

Example:

```javascript
const date =
    new Date("Hello");

console.log(date);
```

The result is an invalid Date.

Check:

```javascript
console.log(
    Number.isNaN(
        date.getTime()
    )
);
```

Output:

```text
true
```

---

# 47. Practical Example — Current Year

```javascript
function getCurrentYear() {
    return new Date().getFullYear();
}

console.log(
    getCurrentYear()
);
```

Useful for:

```text
Copyright
Reports
Dashboard
Footer
```

---

# 48. Practical Example — Expiration Date

```javascript
const expiration =
    new Date();

expiration.setDate(
    expiration.getDate() + 30
);

console.log(
    expiration.toISOString()
);
```

This creates a Date approximately 30 calendar days after the current date.

---

# 49. Practical Example — Age Calculation

```javascript
function calculateAge(birthDate) {
    const today = new Date();
    const birth = new Date(birthDate);

    let age =
        today.getFullYear() -
        birth.getFullYear();

    const monthDifference =
        today.getMonth() -
        birth.getMonth();

    if (
        monthDifference < 0 ||
        (
            monthDifference === 0 &&
            today.getDate() < birth.getDate()
        )
    ) {
        age--;
    }

    return age;
}
```

Usage:

```javascript
console.log(
    calculateAge("2000-10-02")
);
```

This calculates the completed age based on today's local date.

---

# 50. Practical Example — Date Comparison

```javascript
function isExpired(expirationDate) {
    const expiration =
        new Date(expirationDate);

    return expiration.getTime()
        < Date.now();
}
```

Usage:

```javascript
console.log(
    isExpired("2025-01-01")
);
```

This compares the expiration timestamp with the current timestamp.

---

# 51. Practical Example — Format Date

```javascript
function formatDate(date) {
    return new Date(date)
        .toLocaleDateString(
            "en-US",
            {
                year: "numeric",
                month: "long",
                day: "numeric"
            }
        );
}
```

Usage:

```javascript
console.log(
    formatDate("2026-10-02")
);
```

Possible output:

```text
October 2, 2026
```

---

# 52. Date in APIs

APIs commonly use ISO strings:

```text
2026-10-02T09:30:00.000Z
```

JavaScript can parse:

```javascript
const date = new Date(
    "2026-10-02T09:30:00.000Z"
);
```

And send:

```javascript
date.toISOString();
```

This provides a consistent machine-readable representation.

---

# 53. Date and Database Applications

In a full-stack application, dates are commonly used for:

```text
createdAt
updatedAt
publishedAt
expiresAt
scheduledAt
deletedAt
lastLogin
```

Example:

```javascript
const order = {
    createdAt: new Date()
};
```

For APIs, serialization commonly produces an ISO string.

---

# 54. Important Time Zone Concept

A Date represents a specific point in time, while formatting methods can display that point using different time zones.

For example:

```javascript
const date =
    new Date(
        "2026-10-02T12:00:00Z"
    );

console.log(
    date.toISOString()
);

console.log(
    date.toString()
);
```

The first is UTC.

The second is displayed using the environment's local time zone.

---

# 55. UTC vs Local Methods

Local:

```javascript
date.getFullYear();
date.getMonth();
date.getDate();
date.getHours();
```

UTC:

```javascript
date.getUTCFullYear();
date.getUTCMonth();
date.getUTCDate();
date.getUTCHours();
```

Use the appropriate method depending on whether your application is working with local calendar values or UTC values.

---

# 56. Common Mistakes

## Mistake 1 — Forgetting zero-based months

Incorrect assumption:

```javascript
new Date(2026, 10, 2);
```

means October.

Actually:

```text
10 → November
```

because:

```text
0 → January
9 → October
10 → November
```

---

## Mistake 2 — Comparing Date objects directly

Avoid:

```javascript
date1 === date2;
```

Use:

```javascript
date1.getTime() ===
date2.getTime();
```

when comparing the represented timestamps.

---

## Mistake 3 — Using ambiguous date strings

Avoid relying on ambiguous formats such as:

```text
10/02/2026
02/10/2026
```

Prefer standardized formats such as:

```text
2026-10-02
```

or:

```text
2026-10-02T10:30:00Z
```

---

## Mistake 4 — Ignoring time zones

An API might return:

```text
2026-10-02T10:00:00Z
```

while the user sees a different local clock time.

Always know whether your data represents:

```text
UTC
Local time
A calendar date without a time
```

---

# 57. Quick Cheat Sheet

```javascript
// Current date/time
new Date();

// Current timestamp
Date.now();

// Timestamp from Date
date.getTime();

// Year
date.getFullYear();

// Month: 0–11
date.getMonth();

// Day of month
date.getDate();

// Day of week: 0–6
date.getDay();

// Hours
date.getHours();

// Minutes
date.getMinutes();

// Seconds
date.getSeconds();

// Milliseconds
date.getMilliseconds();

// ISO format
date.toISOString();

// Local date
date.toLocaleDateString();

// Local date + time
date.toLocaleString();
```

---

# 58. Date Structure

```text
Date
│
├── Create
│   ├── new Date()
│   ├── new Date(string)
│   └── new Date(year, month, ...)
│
├── Read
│   ├── getFullYear()
│   ├── getMonth()
│   ├── getDate()
│   ├── getDay()
│   ├── getHours()
│   └── getMinutes()
│
├── Modify
│   ├── setFullYear()
│   ├── setMonth()
│   ├── setDate()
│   ├── setHours()
│   └── setMinutes()
│
└── Format
    ├── toISOString()
    ├── toString()
    ├── toDateString()
    └── toLocaleString()
```

---

# Key Takeaways

* JavaScript uses the `Date` object for dates and times.
* `new Date()` creates a Date for the current moment.
* `Date.now()` returns the current timestamp in milliseconds.
* JavaScript Date months are zero-based.
* `getMonth()` returns `0` for January and `11` for December.
* `getDay()` returns the weekday from `0` for Sunday through `6` for Saturday.
* `getTime()` returns milliseconds since the Unix epoch.
* `toISOString()` produces a UTC ISO 8601 string.
* `getUTC...()` methods read Date components in UTC.
* `get...()` methods generally read Date components in local time.
* Compare Date objects using their timestamps rather than object identity.
* Use standardized date formats when parsing dates.
* Time zones must be considered when displaying or exchanging date-time data.
* Dates are commonly used for API timestamps, database fields, authentication events, orders, reports, and expiration logic.
