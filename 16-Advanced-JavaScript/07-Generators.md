# JavaScript Generators

Generators are special JavaScript functions that can **pause their execution and resume it later**.

They are useful when you want to:

* Produce values one at a time
* Create custom iterators
* Process large data lazily
* Control execution step by step
* Work with sequences
* Build asynchronous data streams with async generators

---

# 1. What is a Generator?

A generator is a special function written using:

```javascript
function*
```

Example:

```javascript
function* generateNumbers() {
    yield 1;
    yield 2;
    yield 3;
}
```

Calling the generator function does **not immediately execute its body**.

Instead, it returns a generator object:

```javascript
const generator = generateNumbers();

console.log(generator);
```

The generator starts executing when you call:

```javascript
generator.next();
```

---

# 2. Basic Generator Example

```javascript
function* generateNumbers() {
    yield 1;
    yield 2;
    yield 3;
}

const generator = generateNumbers();

console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
console.log(generator.next());
```

Output:

```text
{ value: 1, done: false }
{ value: 2, done: false }
{ value: 3, done: false }
{ value: undefined, done: true }
```

Each call to `next()` resumes the generator until it reaches the next `yield`.

---

# 3. `yield`

The `yield` keyword pauses a generator.

```javascript
function* numbers() {
    yield 10;

    yield 20;

    yield 30;
}
```

Execution happens step by step:

```text
generator.next()
       ↓
yield 10
       ↓
pause

generator.next()
       ↓
yield 20
       ↓
pause

generator.next()
       ↓
yield 30
       ↓
pause

generator.next()
       ↓
generator finished
```

---

# 4. `next()`

The `next()` method resumes the generator.

```javascript
function* numbers() {
    yield 10;
    yield 20;
}

const generator = numbers();

console.log(generator.next());
```

Output:

```javascript
{
    value: 10,
    done: false
}
```

Call it again:

```javascript
console.log(generator.next());
```

Output:

```javascript
{
    value: 20,
    done: false
}
```

Call it after completion:

```javascript
console.log(generator.next());
```

Output:

```javascript
{
    value: undefined,
    done: true
}
```

---

# 5. Understanding `value`

The `value` property contains the value produced by `yield`.

```javascript
function* numbers() {
    yield 100;
}

const generator = numbers();

const result = generator.next();

console.log(result.value);
```

Output:

```text
100
```

---

# 6. Understanding `done`

The `done` property tells us whether the generator has finished.

```text
done: false
```

means:

```text
Generator still has more work.
```

And:

```text
done: true
```

means:

```text
Generator has finished.
```

Example:

```javascript
function* numbers() {
    yield 1;
}

const generator = numbers();

console.log(generator.next());
// { value: 1, done: false }

console.log(generator.next());
// { value: undefined, done: true }
```

---

# 7. Generator Execution is Lazy

Generators are **lazy**.

This means values are produced only when requested.

Example:

```javascript
function* numbers() {
    console.log("Generating 1");
    yield 1;

    console.log("Generating 2");
    yield 2;

    console.log("Generating 3");
    yield 3;
}

const generator = numbers();

console.log("Generator created");

console.log(generator.next());

console.log(generator.next());
```

Output:

```text
Generator created
Generating 1
{ value: 1, done: false }
Generating 2
{ value: 2, done: false }
```

The third value is not generated because we never requested it.

---

# 8. Generator Does Not Execute Immediately

Consider:

```javascript
function* test() {
    console.log("Hello");

    yield 10;
}

const generator = test();

console.log("After creation");
```

Output:

```text
After creation
```

`"Hello"` is not printed yet.

Now:

```javascript
generator.next();
```

Output:

```text
Hello
```

The generator starts only when `next()` is called.

---

# 9. Generator vs Normal Function

Normal function:

```javascript
function getNumber() {
    return 10;
}

const result = getNumber();

console.log(result);
```

The function runs and returns immediately.

Generator:

```javascript
function* getNumbers() {
    yield 10;
    yield 20;
    yield 30;
}

const generator = getNumbers();
```

The generator pauses between values.

| Normal Function                  | Generator                  |
| -------------------------------- | -------------------------- |
| Uses `return`                    | Uses `yield`               |
| Usually finishes in one call     | Can pause and resume       |
| Returns a value                  | Returns a generator object |
| Executes immediately when called | Starts on `next()`         |
| One normal result                | Can produce many values    |

---

# 10. Multiple `yield` Statements

A generator can contain many `yield` statements.

```javascript
function* colors() {
    yield "Red";
    yield "Green";
    yield "Blue";
    yield "Yellow";
}

const generator = colors();

console.log(generator.next().value);
console.log(generator.next().value);
console.log(generator.next().value);
console.log(generator.next().value);
```

Output:

```text
Red
Green
Blue
Yellow
```

---

# 11. Using Generators with `for...of`

Generators are iterable.

This means we can use:

```javascript
for...of
```

Example:

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

for (const number of numbers()) {
    console.log(number);
}
```

Output:

```text
1
2
3
```

`for...of` automatically calls `next()` until:

```text
done === true
```

---

# 12. Generator with Spread Operator

A generator can also be consumed using spread syntax.

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

const result = [...numbers()];

console.log(result);
```

Output:

```text
[1, 2, 3]
```

The spread operator consumes the generator until it finishes.

---

# 13. Important Warning with Infinite Generators

Do not spread an infinite generator.

For example:

```javascript
function* infiniteNumbers() {
    let number = 1;

    while (true) {
        yield number++;
    }
}
```

This generator can produce values forever.

You can safely request values one at a time:

```javascript
const generator = infiniteNumbers();

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

But this is dangerous:

```javascript
const numbers = [...infiniteNumbers()];
```

It will never finish because the generator never ends.

---

# 14. Infinite Generator

Generators are useful for creating sequences.

```javascript
function* ids() {
    let id = 1;

    while (true) {
        yield id++;
    }
}

const generator = ids();

console.log(generator.next().value);
console.log(generator.next().value);
console.log(generator.next().value);
console.log(generator.next().value);
```

Output:

```text
1
2
3
4
```

The values are generated only when requested.

---

# 15. Generator with a Range

We can create a reusable range generator.

```javascript
function* range(start, end) {
    for (let number = start; number <= end; number++) {
        yield number;
    }
}

for (const number of range(1, 5)) {
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

This is a simple example of creating a custom iterable.

---

# 16. Passing Values into a Generator

`next()` can also send a value into a paused generator.

Example:

```javascript
function* demo() {
    const value = yield "First";

    yield value;
}

const generator = demo();

console.log(generator.next());

console.log(generator.next("Hello"));
```

Output:

```text
{ value: "First", done: false }

{ value: "Hello", done: false }
```

The value passed to:

```javascript
next("Hello")
```

becomes the result of the previous `yield` expression.

---

# 17. Understanding `next(value)`

Consider:

```javascript
function* test() {
    const value = yield "Start";

    console.log(value);
}

const generator = test();

generator.next();

generator.next("Hello");
```

Execution:

```text
First next()
    ↓
yield "Start"
    ↓
generator pauses

Second next("Hello")
    ↓
previous yield becomes "Hello"
    ↓
value = "Hello"
```

Important:

The argument passed to the **first** `next()` is ignored because the generator has not reached a paused `yield` yet.

---

# 18. Generator `return()`

A generator has a `return()` method.

It immediately finishes the generator.

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

const generator = numbers();

console.log(generator.next());

console.log(generator.return("Finished"));

console.log(generator.next());
```

Output:

```text
{ value: 1, done: false }

{ value: "Finished", done: true }

{ value: undefined, done: true }
```

After `return()`:

```text
done = true
```

---

# 19. Generator `throw()`

Generators also have a `throw()` method.

It throws an error at the generator's current paused location.

```javascript
function* test() {
    try {
        yield "Start";
    } catch (error) {
        console.log(error.message);
    }
}

const generator = test();

console.log(generator.next());

generator.throw(
    new Error("Something went wrong")
);
```

Output:

```text
{ value: "Start", done: false }

Something went wrong
```

This allows a generator to handle errors internally.

---

# 20. `yield*`

The `yield*` operator delegates to another iterable or generator.

Example:

```javascript
function* numbers() {
    yield* [1, 2, 3];
}

for (const number of numbers()) {
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

# 21. Delegating to Another Generator

```javascript
function* first() {
    yield 1;
    yield 2;
}

function* second() {
    yield* first();

    yield 3;
    yield 4;
}

for (const number of second()) {
    console.log(number);
}
```

Output:

```text
1
2
3
4
```

`yield*` is useful when one generator needs to include values produced by another iterable.

---

# 22. `yield*` with Arrays

`yield*` works with any iterable.

```javascript
function* fruits() {
    yield* ["Apple", "Banana", "Mango"];
}

for (const fruit of fruits()) {
    console.log(fruit);
}
```

Output:

```text
Apple
Banana
Mango
```

---

# 23. Generator as an Iterator

A generator object follows the iterator protocol.

It provides:

```javascript
next()
```

Example:

```javascript
function* numbers() {
    yield 1;
    yield 2;
}

const generator = numbers();

console.log(
    typeof generator.next
);
```

Output:

```text
function
```

Each `next()` call returns an object:

```javascript
{
    value: ...,
    done: ...
}
```

---

# 24. Generator is Also Iterable

A generator can be used with:

```javascript
for...of
```

because generator objects are iterable.

Example:

```javascript
function* numbers() {
    yield 1;
    yield 2;
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

This means the generator can provide its own iterator.

---

# 25. Generator with Objects

Generators can produce objects one at a time.

```javascript
function* users() {
    yield {
        id: 1,
        name: "Sandip"
    };

    yield {
        id: 2,
        name: "Ram"
    };

    yield {
        id: 3,
        name: "Hari"
    };
}

for (const user of users()) {
    console.log(user);
}
```

Output:

```text
{ id: 1, name: "Sandip" }
{ id: 2, name: "Ram" }
{ id: 3, name: "Hari" }
```

---

# 26. Generator for Pagination

Generators can be useful for processing pages one at a time.

Conceptually:

```javascript
function* pages(totalPages) {
    for (let page = 1; page <= totalPages; page++) {
        yield page;
    }
}

for (const page of pages(5)) {
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

The generator controls which page should be processed next.

---

# 27. Generator for Chunks

A generator can produce chunks of an array.

```javascript
function* chunks(array, size) {
    for (let index = 0; index < array.length; index += size) {
        yield array.slice(index, index + size);
    }
}

const data = [
    1, 2, 3,
    4, 5, 6,
    7, 8, 9
];

for (const chunk of chunks(data, 3)) {
    console.log(chunk);
}
```

Output:

```text
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
```

This can be useful when processing large collections incrementally.

---

# 28. Generator with `try...finally`

Generators can also use normal error-handling structures.

```javascript
function* test() {
    try {
        yield 1;
        yield 2;
    } finally {
        console.log("Generator cleanup");
    }
}

const generator = test();

console.log(generator.next());

generator.return();
```

Output:

```text
{ value: 1, done: false }

Generator cleanup
```

The `finally` block can be useful for cleanup when a generator is closed.

---

# 29. Generator Methods in Classes

A class can contain generator methods.

Use:

```javascript
*methodName()
```

Example:

```javascript
class Numbers {
    *generate() {
        yield 1;
        yield 2;
        yield 3;
    }
}

const numbers = new Numbers();

for (const number of numbers.generate()) {
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

# 30. Generator Functions Cannot Be Arrow Functions

Generators use:

```javascript
function*
```

You cannot write a generator as an arrow function.

Valid:

```javascript
function* numbers() {
    yield 1;
}
```

Invalid:

```javascript
const numbers = *() => {
    yield 1;
};
```

Use a generator function declaration or expression instead.

---

# 31. Generator Expressions

A generator can also be assigned to a variable.

```javascript
const numbers = function* () {
    yield 1;
    yield 2;
    yield 3;
};

const generator = numbers();

console.log(generator.next());
```

Output:

```text
{ value: 1, done: false }
```

---

# 32. Generator Function vs Generator Object

These are different.

Generator function:

```javascript
function* numbers() {
    yield 1;
}
```

Generator object:

```javascript
const generator = numbers();
```

The function creates the generator object.

```text
Generator Function
        ↓
    call function
        ↓
Generator Object
        ↓
     next()
        ↓
     yield
```

---

# 33. Generators Are Lazy

One major advantage of generators is lazy evaluation.

Normal array:

```javascript
const numbers = [
    1,
    2,
    3,
    4,
    5
];
```

All values already exist in memory.

Generator:

```javascript
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
    yield 4;
    yield 5;
}
```

Values are produced as needed.

This can be useful for large or potentially infinite sequences.

---

# 34. Memory Efficiency

Consider a large sequence:

```javascript
function* numbers() {
    let number = 1;

    while (number <= 1000000) {
        yield number++;
    }
}
```

The generator does not need to create one million values in an array first.

You can process values incrementally:

```javascript
const generator = numbers();

console.log(generator.next().value);
console.log(generator.next().value);
console.log(generator.next().value);
```

Only requested values are produced.

---

# 35. Generator vs Array

| Generator                        | Array                                      |
| -------------------------------- | ------------------------------------------ |
| Lazy                             | Eager                                      |
| Produces values on demand        | Values already stored                      |
| Can represent infinite sequences | Cannot practically store infinite sequence |
| Uses `yield`                     | Uses array elements                        |
| Consumed with iteration          | Already iterable                           |
| Useful for custom sequences      | Useful for collections                     |

---

# 36. Generator vs Iterator

| Generator                         | Iterator                         |
| --------------------------------- | -------------------------------- |
| Special function syntax           | Protocol/interface pattern       |
| Uses `function*`                  | Can be created manually          |
| Automatically provides `next()`   | Must implement `next()` manually |
| Automatically iterable            | Can be made iterable             |
| Easier to create custom iterators | More control over implementation |

Manual iterator:

```javascript
const iterator = {
    value: 1,

    next() {
        return {
            value: this.value++,
            done: this.value > 3
        };
    }
};

console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
```

Generators make this type of implementation much easier.

---

# 37. Generator vs Async Generator

Normal generator:

```javascript
function* numbers() {
    yield 1;
    yield 2;
}
```

Async generator:

```javascript
async function* numbers() {
    yield 1;
    yield 2;
}
```

| Generator                        | Async Generator               |
| -------------------------------- | ----------------------------- |
| `function*`                      | `async function*`             |
| `next()` returns an object       | `next()` returns a Promise    |
| `for...of`                       | `for await...of`              |
| Synchronous iteration            | Asynchronous iteration        |
| Useful for synchronous sequences | Useful for async data streams |

---

# 38. Async Generators

Async generators are useful when values are produced asynchronously.

Example:

```javascript
async function* getUsers() {
    yield "User 1";

    await new Promise(
        resolve => setTimeout(resolve, 1000)
    );

    yield "User 2";

    await new Promise(
        resolve => setTimeout(resolve, 1000)
    );

    yield "User 3";
}
```

Consume it using:

```javascript
async function displayUsers() {
    for await (const user of getUsers()) {
        console.log(user);
    }
}

displayUsers();
```

Output appears over time:

```text
User 1
User 2
User 3
```

---

# 39. `for await...of`

Use:

```javascript
for await...of
```

to consume asynchronous iterables.

Example:

```javascript
async function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

async function main() {
    for await (const number of numbers()) {
        console.log(number);
    }
}

main();
```

The loop waits for each asynchronous value.

---

# 40. Generators and Asynchronous Code

A normal generator does **not automatically make code asynchronous**.

For example:

```javascript
function* numbers() {
    yield 1;
    yield 2;
}
```

This is still synchronous.

Generators provide:

```text
Pause
Resume
Yield
Iteration control
```

They do not automatically provide:

```text
Parallel execution
Background execution
Asynchronous execution
```

For asynchronous iteration, use:

```javascript
async function*
```

---

# 41. Practical Example — ID Generator

```javascript
function* createIds() {
    let id = 1000;

    while (true) {
        yield id++;
    }
}

const ids = createIds();

const userId1 = ids.next().value;
const userId2 = ids.next().value;
const userId3 = ids.next().value;

console.log(userId1);
console.log(userId2);
console.log(userId3);
```

Output:

```text
1000
1001
1002
```

---

# 42. Practical Example — Status Sequence

Generators can also represent controlled sequences.

```javascript
function* orderStatus() {
    yield "pending";
    yield "confirmed";
    yield "preparing";
    yield "ready";
    yield "completed";
}

const status = orderStatus();

console.log(status.next().value);
console.log(status.next().value);
console.log(status.next().value);
```

Output:

```text
pending
confirmed
preparing
```

The generator moves through the sequence step by step.

---

# 43. Practical Example — Custom Range

```javascript
function* range(start, end, step = 1) {
    for (
        let value = start;
        value <= end;
        value += step
    ) {
        yield value;
    }
}

for (const value of range(0, 10, 2)) {
    console.log(value);
}
```

Output:

```text
0
2
4
6
8
10
```

---

# 44. When to Use Generators

Generators are useful when:

```text
You need lazy values
        ↓
You need custom iteration
        ↓
You need potentially infinite sequences
        ↓
You want to process large data incrementally
        ↓
You need pause/resume behavior
        ↓
You need synchronous or asynchronous data streams
```

Common areas include:

* Custom iterators
* Data processing
* Large datasets
* Pagination
* Streaming
* Sequence generation
* State machines
* Async data streams

---

# 45. When Not to Use Generators

Generators are not necessary for every loop.

For simple data:

```javascript
const numbers = [1, 2, 3];

for (const number of numbers) {
    console.log(number);
}
```

is usually clearer than creating a generator.

Use generators when their lazy or controlled iteration behavior provides a real benefit.

---

# 46. Important Generator Methods

A generator object provides:

```javascript
next()
return()
throw()
```

### `next()`

Resume execution:

```javascript
generator.next();
```

### `return()`

Finish the generator:

```javascript
generator.return();
```

### `throw()`

Throw an error inside the generator:

```javascript
generator.throw(
    new Error("Failed")
);
```

---

# 47. Generator Execution Flow

Example:

```javascript
function* example() {
    console.log("A");

    yield 1;

    console.log("B");

    yield 2;

    console.log("C");
}
```

Execution:

```text
example()
    ↓
Generator object created
    ↓
next()
    ↓
"A"
    ↓
yield 1
    ↓
pause
    ↓
next()
    ↓
"B"
    ↓
yield 2
    ↓
pause
    ↓
next()
    ↓
"C"
    ↓
finished
```

The generator remembers where it paused.

---

# 48. Generator and State

Generators automatically maintain their execution state.

```javascript
function* counter() {
    let count = 1;

    yield count++;

    yield count++;

    yield count++;
}
```

The local variable:

```text
count
```

is preserved while the generator is paused.

```javascript
const generator = counter();

console.log(generator.next().value);
// 1

console.log(generator.next().value);
// 2

console.log(generator.next().value);
// 3
```

---

# 49. Generator and `return`

A generator can explicitly return a final value.

```javascript
function* test() {
    yield 1;
    return "Finished";
}

const generator = test();

console.log(generator.next());

console.log(generator.next());

console.log(generator.next());
```

Output:

```text
{ value: 1, done: false }

{ value: "Finished", done: true }

{ value: undefined, done: true }
```

Notice that the explicit return value has:

```text
done: true
```

Also, `for...of` does not include a generator's final `return` value.

---

# 50. Generators in Node.js and React

Generators are not required for normal React development.

Most React applications commonly use:

```text
Functions
Hooks
Promises
async/await
```

Generators can still be useful for:

* Custom iteration
* Data processing
* Advanced state machines
* Streaming-style workflows
* Libraries that use generator-based patterns

In Node.js, generators can be useful when working with:

* Data sequences
* Large datasets
* Custom iterators
* Streaming-style processing
* Async generators

---

# Generator Quick Cheat Sheet

```javascript
// Generator function
function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

// Create generator
const generator = numbers();

// Get next value
generator.next();

// Get only value
generator.next().value;

// Check completion
generator.next().done;

// Stop generator
generator.return();

// Throw error
generator.throw(
    new Error("Failed")
);

// Delegate to another iterable
function* values() {
    yield* [1, 2, 3];
}

// Consume generator
for (const value of numbers()) {
    console.log(value);
}

// Convert to array
const array = [...numbers()];
```

---

# Async Generator Cheat Sheet

```javascript
async function* numbers() {
    yield 1;
    yield 2;
    yield 3;
}

async function main() {
    for await (const number of numbers()) {
        console.log(number);
    }
}

main();
```

---

# Key Takeaways

* A generator is created using `function*`.
* Calling a generator function returns a generator object.
* Generator execution starts when `next()` is called.
* `yield` pauses generator execution.
* `next()` resumes execution.
* `next()` returns an object containing `value` and `done`.
* `done: true` means the generator has finished.
* Generators are lazy.
* Generator objects are iterators and iterables.
* Generators work with `for...of`.
* Generators can be consumed using the spread operator.
* Infinite generators must be consumed incrementally.
* `next(value)` can send a value into a paused generator.
* `return()` immediately finishes a generator.
* `throw()` can inject an error into a generator.
* `yield*` delegates iteration to another iterable or generator.
* Generator methods can be defined inside classes.
* Generators are not automatically asynchronous.
* `async function*` creates an async generator.
* Async generators are consumed using `for await...of`.
* Generators are useful for lazy data processing and custom iteration.

---

# Generator Roadmap

```text
Generator
    │
    ├── function*
    │
    ├── yield
    │
    ├── next()
    │   ├── value
    │   └── done
    │
    ├── return()
    │
    ├── throw()
    │
    ├── yield*
    │
    ├── Iterators
    │
    ├── Lazy Evaluation
    │
    └── Async Generator
        │
        ├── async function*
        └── for await...of
```

---
