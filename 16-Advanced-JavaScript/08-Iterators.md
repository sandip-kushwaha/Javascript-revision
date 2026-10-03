# JavaScript Iterators

An **iterator** is an object that provides a way to access values **one at a time**.

JavaScript uses iterators behind features such as:

* `for...of`
* Spread operator `...`
* `Array.from()`
* `Map`
* `Set`
* Generators
* `Symbol.iterator`

---

# 1. What is an Iterator?

An iterator is an object with a `next()` method.

Example:

```javascript
const iterator = {
    next() {
        return {
            value: 1,
            done: false
        };
    }
};

console.log(iterator.next());
```

Output:

```text
{
    value: 1,
    done: false
}
```

An iterator's `next()` method returns an object containing:

```text
value
done
```

---

# 2. Iterator Result

Every iterator step returns an object like:

```javascript
{
    value: something,
    done: false
}
```

When iteration is complete:

```javascript
{
    value: undefined,
    done: true
}
```

So:

```text
value
    → current value

done
    → whether iteration has finished
```

---

# 3. Simple Custom Iterator

Let's create an iterator that produces:

```text
1
2
3
```

```javascript
const iterator = {
    current: 1,

    next() {
        if (this.current <= 3) {
            return {
                value: this.current++,
                done: false
            };
        }

        return {
            value: undefined,
            done: true
        };
    }
};
```

Use it:

```javascript
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

Output:

```text
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
{ value: undefined, done: true }
```

---

# 4. The `next()` Method

The `next()` method controls the next step of iteration.

Example:

```javascript
const iterator = {
    current: 1,

    next() {
        return {
            value: this.current++,
            done: this.current > 4
        };
    }
};

console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

Each call moves the iterator forward.

---

# 5. Iterator Protocol

JavaScript defines an **iterator protocol**.

An iterator should provide:

```javascript
next()
```

The method should return an object containing:

```javascript
{
    value,
    done
}
```

Example:

```javascript
const iterator = {
    next() {
        return {
            value: "Hello",
            done: false
        };
    }
};
```

---

# 6. Iterable vs Iterator

These two concepts are different.

## Iterator

An iterator has:

```javascript
next()
```

Example:

```javascript
const iterator = {
    next() {
        return {
            value: 1,
            done: true
        };
    }
};
```

## Iterable

An iterable provides:

```javascript
Symbol.iterator
```

which returns an iterator.

Example:

```javascript
const numbers = [1, 2, 3];

console.log(
    typeof numbers[Symbol.iterator]
);
```

Output:

```text
function
```

---

# 7. What is `Symbol.iterator`?

`Symbol.iterator` is a special JavaScript symbol used to define how an object should be iterated.

Example:

```javascript
const numbers = [1, 2, 3];

const iterator =
    numbers[Symbol.iterator]();

console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

Output:

```text
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
{ value: undefined, done: true }
```

The array is iterable because it provides `Symbol.iterator`.

---

# 8. Arrays Are Iterable

Arrays support:

```javascript
Symbol.iterator
```

Example:

```javascript
const numbers = [10, 20, 30];

const iterator =
    numbers[Symbol.iterator]();

console.log(iterator.next().value);
console.log(iterator.next().value);
console.log(iterator.next().value);
```

Output:

```text
10
20
30
```

---

# 9. Strings Are Iterable

Strings are also iterable.

```javascript
const text = "ABC";

const iterator =
    text[Symbol.iterator]();

console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

Output:

```text
{ value: "A", done: false }
{ value: "B", done: false }
{ value: "C", done: false }
```

---

# 10. Maps Are Iterable

A `Map` is iterable.

```javascript
const users = new Map([
    ["id", 1],
    ["name", "Sandip"]
]);

for (const entry of users) {
    console.log(entry);
}
```

Output:

```text
["id", 1]
["name", "Sandip"]
```

---

# 11. Sets Are Iterable

A `Set` is also iterable.

```javascript
const numbers = new Set([
    10,
    20,
    30
]);

for (const number of numbers) {
    console.log(number);
}
```

Output:

```text
10
20
30
```

---

# 12. `for...of` Uses Iterators

When you write:

```javascript
const numbers = [1, 2, 3];

for (const number of numbers) {
    console.log(number);
}
```

JavaScript conceptually does something similar to:

```javascript
const iterator =
    numbers[Symbol.iterator]();

let result = iterator.next();

while (!result.done) {
    console.log(result.value);

    result = iterator.next();
}
```

This is why `for...of` works with iterable objects.

---

# 13. Spread Operator Uses Iteration

The spread operator can consume iterables.

Example:

```javascript
const numbers = [1, 2, 3];

const copy = [...numbers];

console.log(copy);
```

Output:

```text
[1, 2, 3]
```

Conceptually, JavaScript gets values through the iterable's iterator.

---

# 14. `Array.from()` Uses Iteration

`Array.from()` can create an array from an iterable.

Example:

```javascript
const set = new Set([
    1,
    2,
    3
]);

const numbers = Array.from(set);

console.log(numbers);
```

Output:

```text
[1, 2, 3]
```

---

# 15. Creating a Custom Iterable

We can make our own object iterable.

```javascript
const numbers = {
    start: 1,
    end: 3,

    [Symbol.iterator]() {
        let current = this.start;

        return {
            next: () => {
                if (current <= this.end) {
                    return {
                        value: current++,
                        done: false
                    };
                }

                return {
                    value: undefined,
                    done: true
                };
            }
        };
    }
};
```

Now we can use:

```javascript
for (const number of numbers) {
    console.log(number);
}
```

Output:

```text
1
2
3
```

---

# 16. Custom Iterable Structure

The previous example follows this structure:

```text
Iterable Object
      │
      └── Symbol.iterator
              │
              ↓
          Iterator
              │
              └── next()
                    │
                    ├── value
                    └── done
```

This is the relationship between iterable and iterator.

---

# 17. Iterable Protocol

An object is iterable when it provides:

```javascript
obj[Symbol.iterator]()
```

and that method returns an iterator.

Example:

```javascript
const iterable = {
    [Symbol.iterator]() {
        return {
            next() {
                return {
                    value: 1,
                    done: true
                };
            }
        };
    }
};
```

Now:

```javascript
for (const value of iterable) {
    console.log(value);
}
```

works because the object follows the iterable protocol.

---

# 18. Iterator Protocol vs Iterable Protocol

| Iterator Protocol         | Iterable Protocol            |
| ------------------------- | ---------------------------- |
| Requires `next()`         | Requires `Symbol.iterator`   |
| Returns `{ value, done }` | Returns an iterator          |
| Controls iteration steps  | Defines how iteration begins |
| Used by iterator objects  | Used by iterable objects     |

Some objects, such as generators, satisfy both protocols.

---

# 19. Generator and Iterator

Generators automatically create iterators.

Example:

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

const generator = numbers();
```

The generator provides:

```javascript
generator.next();
```

and also:

```javascript
generator[Symbol.iterator]();
```

So a generator is:

```text
Iterator
+
Iterable
```

---

# 20. Generator as Iterable

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

const generator = numbers();

console.log(
    generator[Symbol.iterator]() === generator
);
```

Output:

```text
true
```

The generator returns itself as its iterator.

---

# 21. Why Iterators Are Useful

Iterators allow JavaScript to process values one at a time.

Instead of requiring every value immediately:

```text
All Values
    ↓
Memory
```

an iterator can provide:

```text
Next Value
    ↓
Process
    ↓
Next Value
    ↓
Process
```

This is useful for:

* Large datasets
* Custom collections
* Lazy processing
* Infinite sequences
* Generators
* Data streams

---

# 22. Lazy Iteration

Iterators are often used for lazy processing.

Example:

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}
```

The values are not all produced immediately.

```javascript
const generator = numbers();

console.log(generator.next());
```

Only the first value is requested.

---

# 23. Infinite Iterator

An iterator can theoretically produce values forever.

Example:

```javascript
function* numbers() {
    let number = 1;

    while (true) {
        yield number++;
    }
}
```

Use it incrementally:

```javascript
const generator = numbers();

console.log(generator.next().value);
console.log(generator.next().value);
console.log(generator.next().value);
```

Output:

```text
1
2
3
```

Do not attempt to fully consume an infinite iterable.

For example:

```javascript
const values = [...numbers()];
```

would never finish.

---

# 24. Iterator with Custom Object

A useful example is a custom range.

```javascript
const range = {
    start: 1,
    end: 5,

    [Symbol.iterator]() {
        let current = this.start;

        return {
            next: () => {
                if (current <= this.end) {
                    return {
                        value: current++,
                        done: false
                    };
                }

                return {
                    value: undefined,
                    done: true
                };
            }
        };
    }
};
```

Now:

```javascript
console.log([...range]);
```

Output:

```text
[1, 2, 3, 4, 5]
```

---

# 25. Iterator State

An iterator remembers its current state.

Example:

```javascript
const iterator = [10, 20, 30][Symbol.iterator]();

console.log(iterator.next());
console.log(iterator.next());
```

Output:

```text
{ value: 10, done: false }
{ value: 20, done: false }
```

The iterator now points to the next position.

```javascript
console.log(iterator.next());
```

Output:

```text
{ value: 30, done: false }
```

---

# 26. Iterators Are Usually One-Way

An iterator normally moves forward.

Example:

```javascript
const iterator =
    [1, 2, 3][Symbol.iterator]();

iterator.next();
iterator.next();
```

There is no standard:

```javascript
previous()
```

method.

If you need to restart iteration, create a new iterator:

```javascript
const newIterator =
    [1, 2, 3][Symbol.iterator]();
```

---

# 27. Multiple Iterators

An iterable can create multiple independent iterators.

```javascript
const numbers = [1, 2, 3];

const first =
    numbers[Symbol.iterator]();

const second =
    numbers[Symbol.iterator]();

console.log(first.next());
console.log(first.next());

console.log(second.next());
```

Output:

```text
{ value: 1, done: false }
{ value: 2, done: false }

{ value: 1, done: false }
```

Each iterator maintains its own position.

---

# 28. Iterator Consumption

An iterator can be consumed by:

```text
next()
for...of
spread (...)
Array.from()
destructuring
```

Example:

```javascript
const numbers = [1, 2, 3];

const [first, second] = numbers;

console.log(first);
console.log(second);
```

Output:

```text
1
2
```

Array destructuring uses iteration.

---

# 29. Destructuring Uses Iterators

Consider:

```javascript
const numbers = [10, 20, 30];

const [first, second] = numbers;
```

Conceptually, JavaScript gets the first values from the array's iterator.

Result:

```text
first  → 10
second → 20
```

---

# 30. String Iteration

Strings can be iterated using:

```javascript
for...of
```

Example:

```javascript
const text = "Hello";

for (const character of text) {
    console.log(character);
}
```

Output:

```text
H
e
l
l
o
```

This works because strings implement the iterable protocol.

---

# 31. Map Iteration

Maps provide several iterable views.

```javascript
const users = new Map([
    [1, "Sandip"],
    [2, "Ram"]
]);
```

Keys:

```javascript
for (const key of users.keys()) {
    console.log(key);
}
```

Values:

```javascript
for (const value of users.values()) {
    console.log(value);
}
```

Entries:

```javascript
for (const entry of users.entries()) {
    console.log(entry);
}
```

---

# 32. Set Iteration

```javascript
const numbers = new Set([
    10,
    20,
    30
]);

for (const number of numbers) {
    console.log(number);
}
```

A Set's iterator produces each unique value.

---

# 33. `Symbol.iterator` and `for...of`

Consider:

```javascript
const numbers = [1, 2, 3];

for (const number of numbers) {
    console.log(number);
}
```

The important concept is:

```text
for...of
    ↓
Symbol.iterator
    ↓
iterator
    ↓
next()
    ↓
value
```

This is the mechanism behind iterable iteration.

---

# 34. Iterator Completion

When an iterator finishes, it returns:

```javascript
{
    value: undefined,
    done: true
}
```

Example:

```javascript
const iterator =
    [1][Symbol.iterator]();

console.log(iterator.next());
console.log(iterator.next());
```

Output:

```text
{ value: 1, done: false }
{ value: undefined, done: true }
```

Calling `next()` again generally continues returning a completed result:

```javascript
console.log(iterator.next());
```

Output:

```text
{ value: undefined, done: true }
```

---

# 35. Iterator vs Array

| Iterator                         | Array                                                          |
| -------------------------------- | -------------------------------------------------------------- |
| Produces values step by step     | Stores values                                                  |
| Has `next()`                     | Has indexes                                                    |
| Can be lazy                      | Usually eager                                                  |
| Can represent infinite sequences | Finite collection                                              |
| Tracks iteration state           | Collection itself does not track one shared iteration position |
| Useful for custom iteration      | Useful for storing collections                                 |

---

# 36. Iterator vs Generator

| Iterator                                         | Generator                                  |
| ------------------------------------------------ | ------------------------------------------ |
| Object following iterator protocol               | Special generator function/object          |
| `next()` must be implemented manually            | `next()` is created automatically          |
| More implementation code                         | Less implementation code                   |
| Can be custom-built                              | Uses `function*`                           |
| Can be iterable if `Symbol.iterator` is provided | Generator object is iterable automatically |

Example iterator:

```javascript
const iterator = {
    next() {
        return {
            value: 1,
            done: true
        };
    }
};
```

Generator:

```javascript
function* numbers() {
    yield 1;
}
```

---

# 37. Async Iterators

JavaScript also supports **asynchronous iteration**.

Async iterators use:

```javascript
Symbol.asyncIterator
```

and:

```javascript
next()
```

returns a Promise.

Example concept:

```javascript
const asyncIterable = {
    [Symbol.asyncIterator]() {
        return {
            async next() {
                return {
                    value: 1,
                    done: true
                };
            }
        };
    }
};
```

Consume it with:

```javascript
for await (const value of asyncIterable) {
    console.log(value);
}
```

---

# 38. Async Iterator vs Iterator

| Iterator                | Async Iterator           |
| ----------------------- | ------------------------ |
| `Symbol.iterator`       | `Symbol.asyncIterator`   |
| `next()` returns result | `next()` returns Promise |
| `for...of`              | `for await...of`         |
| Synchronous iteration   | Asynchronous iteration   |

---

# 39. Async Generator as Async Iterator

An async generator automatically provides async iteration.

```javascript
async function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}
```

Consume it:

```javascript
async function main() {
    for await (const number of numbers()) {
        console.log(number);
    }
}

main();
```

The async generator handles the async iterator protocol automatically.

---

# 40. Creating an Iterable Class

Classes can implement custom iteration.

```javascript
class Numbers {
    constructor(start, end) {
        this.start = start;
        this.end = end;
    }

    *[Symbol.iterator]() {
        for (
            let number = this.start;
            number <= this.end;
            number++
        ) {
            yield number;
        }
    }
}
```

Use it:

```javascript
const numbers = new Numbers(1, 5);

for (const number of numbers) {
    console.log(number);
}
```

Output:

```text
1
2
3
4
5
```

---

# 41. Iterator with `return()`

Some iterators can provide additional control methods, but the core iterator protocol requires only:

```javascript
next()
```

Generators additionally provide:

```javascript
return()
throw()
```

For ordinary custom iterators, these methods are optional unless your use case requires them.

---

# 42. Important Built-in Iterables

Common JavaScript iterables include:

```text
Array
String
Map
Set
TypedArray
arguments
NodeList
Generator objects
```

Many browser APIs also expose iterable collections.

---

# 43. Common Operations That Use Iteration

JavaScript uses the iterable protocol in several places.

### `for...of`

```javascript
for (const value of iterable) {
    console.log(value);
}
```

### Spread

```javascript
const array = [...iterable];
```

### `Array.from()`

```javascript
const array = Array.from(iterable);
```

### Destructuring

```javascript
const [first] = iterable;
```

These operations need an iterable object.

---

# 44. Non-Iterable Example

A plain object is not iterable by default.

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

This does not work:

```javascript
for (const value of user) {
    console.log(value);
}
```

JavaScript throws a `TypeError` because the object does not provide the required iterator.

For objects, use:

```javascript
Object.keys(user);
Object.values(user);
Object.entries(user);
```

Example:

```javascript
for (const [key, value] of Object.entries(user)) {
    console.log(key, value);
}
```

---

# 45. Making an Object Iterable

We can add `Symbol.iterator` to a normal object.

```javascript
const user = {
    name: "Sandip",
    age: 22,

    *[Symbol.iterator]() {
        yield this.name;
        yield this.age;
    }
};
```

Now:

```javascript
for (const value of user) {
    console.log(value);
}
```

Output:

```text
Sandip
22
```

---

# 46. Practical Example — Pagination

A custom iterable can represent page numbers.

```javascript
const pages = {
    start: 1,
    end: 5,

    *[Symbol.iterator]() {
        for (
            let page = this.start;
            page <= this.end;
            page++
        ) {
            yield page;
        }
    }
};

for (const page of pages) {
    console.log(`Loading page ${page}`);
}
```

Output:

```text
Loading page 1
Loading page 2
Loading page 3
Loading page 4
Loading page 5
```

---

# 47. Practical Example — IDs

```javascript
function* createIds(start = 1) {
    let id = start;

    while (true) {
        yield id++;
    }
}

const ids = createIds(100);

console.log(ids.next().value);
console.log(ids.next().value);
console.log(ids.next().value);
```

Output:

```text
100
101
102
```

The generator acts as a lazy iterator.

---

# 48. Iterator Architecture

The overall relationship can be remembered as:

```text
Iterable
   │
   │ Symbol.iterator
   ↓
Iterator
   │
   │ next()
   ↓
{ value, done }
```

For generators:

```text
Generator Function
       │
       │ call
       ↓
Generator Object
       │
       ├── next()
       ├── return()
       ├── throw()
       │
       └── Symbol.iterator
```

---

# 49. Key Differences

## Iterable

```text
Can be iterated
```

Provides:

```javascript
Symbol.iterator
```

## Iterator

```text
Produces values
```

Provides:

```javascript
next()
```

## Generator

```text
Easy way to create an iterator
```

Uses:

```javascript
function*
yield
```

---

# 50. Quick Cheat Sheet

```javascript
// Get an array iterator
const iterator =
    [1, 2, 3][Symbol.iterator]();

// Get next value
iterator.next();

// Result
{
    value: 1,
    done: false
}

// Completed result
{
    value: undefined,
    done: true
}

// Check if an object is iterable
typeof obj[Symbol.iterator] === "function"

// Iterate values
for (const value of iterable) {
    console.log(value);
}

// Spread iterable
const values = [...iterable];

// Convert iterable to array
const values = Array.from(iterable);
```

---

# Iterator Protocol

```text
Iterator
    │
    └── next()
          │
          └── {
                value,
                done
              }
```

# Iterable Protocol

```text
Iterable
    │
    └── [Symbol.iterator]()
                │
                ↓
             Iterator
                │
                └── next()
```

# Async Iterator Protocol

```text
Async Iterable
      │
      └── [Symbol.asyncIterator]()
                    │
                    ↓
              Async Iterator
                    │
                    └── next()
                          │
                          ↓
                       Promise
```

---

# Key Takeaways

* An iterator produces values one at a time.
* An iterator must provide a `next()` method.
* `next()` returns `{ value, done }`.
* `done: true` means iteration is complete.
* An iterable provides `Symbol.iterator`.
* `Symbol.iterator` returns an iterator.
* Arrays are iterable.
* Strings are iterable.
* Maps are iterable.
* Sets are iterable.
* Generators are both iterable and iterable-producing iterator objects.
* `for...of` uses the iterable protocol.
* Spread syntax uses iteration.
* `Array.from()` can consume iterables.
* Destructuring uses iteration.
* Iterators maintain their own iteration state.
* Multiple iterators can independently traverse the same iterable.
* Infinite iterables must be consumed carefully.
* Async iterators use `Symbol.asyncIterator`.
* Async iterators are consumed with `for await...of`.
* Generators provide a convenient way to create iterators.
* Custom iterables can be created using `Symbol.iterator`.

---

# Iterator Roadmap

```text
Iterators
    │
    ├── Iterator
    │   └── next()
    │
    ├── Iterable
    │   └── Symbol.iterator
    │
    ├── Iterator Result
    │   ├── value
    │   └── done
    │
    ├── for...of
    │
    ├── Spread
    │
    ├── Array.from()
    │
    ├── Destructuring
    │
    ├── Generators
    │
    └── Async Iterators
        ├── Symbol.asyncIterator
        └── for await...of
```

---
