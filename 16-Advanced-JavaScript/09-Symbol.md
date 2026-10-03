# JavaScript Symbols

`Symbol` is a **primitive data type** in JavaScript.

A Symbol creates a **unique value** that can be used as an object property key.

Symbols are especially useful for:

* Unique object properties
* Avoiding property-name collisions
* Metaprogramming
* Custom iteration
* JavaScript protocols
* Well-known symbols such as `Symbol.iterator`

---

# 1. What is a Symbol?

A Symbol is created using:

```javascript
Symbol()
```

Example:

```javascript
const id = Symbol();

console.log(id);
```

Each Symbol is unique.

```javascript
const first = Symbol();
const second = Symbol();

console.log(first === second);
```

Output:

```text
false
```

Even though both were created in the same way, they are different values.

---

# 2. Symbol with a Description

You can provide a description when creating a Symbol.

```javascript
const id = Symbol("id");

console.log(id);
```

The description helps developers understand the purpose of the Symbol.

Example:

```javascript
const userId = Symbol("userId");
const productId = Symbol("productId");
```

The descriptions do not make Symbols equal.

```javascript
const first = Symbol("id");
const second = Symbol("id");

console.log(first === second);
```

Output:

```text
false
```

---

# 3. Symbols Are Primitive Values

JavaScript has these primitive types:

```text
string
number
bigint
boolean
undefined
null
symbol
```

Example:

```javascript
const id = Symbol("id");

console.log(typeof id);
```

Output:

```text
symbol
```

---

# 4. Symbols Are Always Unique

Consider:

```javascript
const a = Symbol("user");
const b = Symbol("user");
const c = Symbol("user");
```

These are three different Symbols.

```javascript
console.log(a === b);
console.log(b === c);
console.log(a === c);
```

Output:

```text
false
false
false
```

The description `"user"` is only descriptive metadata.

---

# 5. Symbol as an Object Property

Symbols can be used as object keys.

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};
```

Access the Symbol property:

```javascript
console.log(user[id]);
```

Output:

```text
101
```

Notice that we use:

```javascript
user[id]
```

not:

```javascript
user.id
```

---

# 6. Why Use Symbol Properties?

Suppose two different parts of an application use the same property name.

```javascript
const user = {
    id: 101
};
```

Another part of the application might also add:

```javascript
user.id = "another value";
```

The original value can be overwritten.

Symbols provide unique property keys:

```javascript
const systemId = Symbol("id");
const pluginId = Symbol("id");

const user = {
    [systemId]: 101,
    [pluginId]: 202
};
```

Both properties can exist because the Symbols are different.

---

# 7. Symbol Property Syntax

Create the Symbol:

```javascript
const id = Symbol("id");
```

Use it as a property:

```javascript
const user = {
    [id]: 101
};
```

Access it:

```javascript
console.log(user[id]);
```

Update it:

```javascript
user[id] = 200;
```

Delete it:

```javascript
delete user[id];
```

---

# 8. Symbol Properties Are Not Normal String Properties

Consider:

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};
```

Now:

```javascript
console.log(Object.keys(user));
```

Output:

```text
["name"]
```

The Symbol property does not appear in `Object.keys()`.

---

# 9. `Object.getOwnPropertySymbols()`

To retrieve an object's own Symbol properties:

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};

console.log(
    Object.getOwnPropertySymbols(user)
);
```

Output contains:

```text
[Symbol(id)]
```

You can access the value:

```javascript
const symbols =
    Object.getOwnPropertySymbols(user);

console.log(user[symbols[0]]);
```

Output:

```text
101
```

---

# 10. `Reflect.ownKeys()`

`Reflect.ownKeys()` returns both:

* String property keys
* Symbol property keys

Example:

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    age: 22,
    [id]: 101
};

console.log(
    Reflect.ownKeys(user)
);
```

The result includes:

```text
name
age
Symbol(id)
```

This makes `Reflect.ownKeys()` useful when you need all own property keys.

---

# 11. Symbol Properties and `for...in`

Symbol properties are not included in normal `for...in` enumeration.

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};

for (const key in user) {
    console.log(key);
}
```

Output:

```text
name
```

The Symbol property is skipped.

---

# 12. Symbol Properties and `Object.entries()`

Symbol properties are also not returned by:

```javascript
Object.entries()
```

Example:

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};

console.log(
    Object.entries(user)
);
```

Only normal enumerable string-keyed properties are included.

---

# 13. Symbol Properties and `Object.getOwnPropertySymbols()`

Use:

```javascript
Object.getOwnPropertySymbols()
```

when you specifically want Symbol keys.

Example:

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};

const symbols =
    Object.getOwnPropertySymbols(user);

for (const symbol of symbols) {
    console.log(symbol);
}
```

---

# 14. Symbol Keys Are Not Secret

A common misconception is that Symbol properties are private.

They are **not truly private**.

For example:

```javascript
const id = Symbol("id");

const user = {
    [id]: 101
};
```

The property can still be discovered:

```javascript
Object.getOwnPropertySymbols(user);
```

So Symbols provide:

```text
Uniqueness
```

not:

```text
Security
```

---

# 15. Symbol vs String Property

Compare:

```javascript
const user = {
    name: "Sandip"
};
```

and:

```javascript
const id = Symbol("id");

const user = {
    [id]: 101
};
```

| String Key                          | Symbol Key                                      |
| ----------------------------------- | ----------------------------------------------- |
| `"name"`                            | `Symbol("id")`                                  |
| Easy to enumerate                   | Hidden from common string-key enumeration       |
| Can collide with same property name | Unique Symbol prevents accidental key collision |
| Common object property              | Useful for special/internal metadata            |

---

# 16. Symbol Registry

Normally:

```javascript
Symbol("id") !== Symbol("id")
```

But JavaScript provides a **global Symbol registry**.

Use:

```javascript
Symbol.for()
```

Example:

```javascript
const first = Symbol.for("userId");
const second = Symbol.for("userId");

console.log(first === second);
```

Output:

```text
true
```

The same registry key returns the same Symbol.

---

# 17. `Symbol.for()`

Syntax:

```javascript
Symbol.for("key")
```

Example:

```javascript
const id = Symbol.for("userId");

console.log(id);
```

If a Symbol with the same registry key already exists, JavaScript returns that Symbol.

Otherwise, it creates and stores one.

---

# 18. `Symbol.keyFor()`

To retrieve the registry key of a global Symbol:

```javascript
const id = Symbol.for("userId");

console.log(
    Symbol.keyFor(id)
);
```

Output:

```text
userId
```

---

# 19. `Symbol()` vs `Symbol.for()`

These are different.

### `Symbol()`

Creates a new unique Symbol every time:

```javascript
const a = Symbol("id");
const b = Symbol("id");

console.log(a === b);
```

Output:

```text
false
```

### `Symbol.for()`

Uses the global Symbol registry:

```javascript
const a = Symbol.for("id");
const b = Symbol.for("id");

console.log(a === b);
```

Output:

```text
true
```

---

# 20. `Symbol.keyFor()` Limitation

`Symbol.keyFor()` only works with Symbols from the global registry.

Example:

```javascript
const id = Symbol("userId");

console.log(
    Symbol.keyFor(id)
);
```

Output:

```text
undefined
```

Because:

```javascript
Symbol("userId")
```

was not created using:

```javascript
Symbol.for()
```

---

# 21. Symbol and Type Conversion

Symbols have some special conversion rules.

You can explicitly convert a Symbol to a string:

```javascript
const id = Symbol("id");

console.log(String(id));
```

Output:

```text
Symbol(id)
```

But implicit conversion to string can cause an error.

For example:

```javascript
const id = Symbol("id");

console.log("User ID: " + id);
```

This throws a `TypeError`.

Use explicit conversion instead:

```javascript
console.log(
    "User ID: " + String(id)
);
```

---

# 22. Symbol and Numbers

A Symbol cannot be converted to a number using:

```javascript
Number()
```

Example:

```javascript
const id = Symbol("id");

Number(id);
```

This throws a `TypeError`.

Symbols are intentionally separate from numeric values.

---

# 23. Symbols Cannot Be Used with Arithmetic

This is invalid:

```javascript
const id = Symbol("id");

console.log(id + 1);
```

It causes a `TypeError`.

Similarly:

```javascript
id * 2;
```

is invalid.

A Symbol is designed for unique identification and language-level protocols, not arithmetic.

---

# 24. Symbol Description

A Symbol can expose its description through:

```javascript
symbol.description
```

Example:

```javascript
const id = Symbol("userId");

console.log(id.description);
```

Output:

```text
userId
```

If no description was provided:

```javascript
const id = Symbol();

console.log(id.description);
```

Output:

```text
undefined
```

---

# 25. Symbols and `Object.getOwnPropertyNames()`

Consider:

```javascript
const id = Symbol("id");

const user = {
    name: "Sandip",
    [id]: 101
};
```

Then:

```javascript
console.log(
    Object.getOwnPropertyNames(user)
);
```

returns the string-keyed property names.

It does not include the Symbol property.

Use:

```javascript
Object.getOwnPropertySymbols(user);
```

for Symbol keys.

Or:

```javascript
Reflect.ownKeys(user);
```

for both.

---

# 26. Well-Known Symbols

JavaScript provides predefined Symbols called **well-known Symbols**.

They allow objects to customize built-in JavaScript behavior.

Important examples include:

```text
Symbol.iterator
Symbol.asyncIterator
Symbol.toPrimitive
Symbol.toStringTag
Symbol.hasInstance
Symbol.isConcatSpreadable
Symbol.species
Symbol.match
Symbol.replace
Symbol.search
Symbol.split
```

---

# 27. `Symbol.iterator`

`Symbol.iterator` defines how an object is iterated.

Example:

```javascript
const numbers = [1, 2, 3];

const iterator =
    numbers[Symbol.iterator]();

console.log(iterator.next());
```

This is the protocol used by:

```text
for...of
spread
Array.from()
destructuring
```

---

# 28. Custom `Symbol.iterator`

We can make an object iterable.

```javascript
const numbers = {
    start: 1,
    end: 3,

    *[Symbol.iterator]() {
        for (
            let value = this.start;
            value <= this.end;
            value++
        ) {
            yield value;
        }
    }
};
```

Now:

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

# 29. `Symbol.asyncIterator`

`Symbol.asyncIterator` defines asynchronous iteration.

It is used with:

```javascript
for await...of
```

Example:

```javascript
const data = {
    async *[Symbol.asyncIterator]() {
        yield 1;
        yield 2;
        yield 3;
    }
};
```

Consume it:

```javascript
async function main() {
    for await (const value of data) {
        console.log(value);
    }
}

main();
```

---

# 30. `Symbol.toPrimitive`

`Symbol.toPrimitive` controls how an object is converted to a primitive value.

Example:

```javascript
const user = {
    name: "Sandip",

    [Symbol.toPrimitive](hint) {
        if (hint === "string") {
            return this.name;
        }

        return 1;
    }
};
```

Now JavaScript can ask the object for an appropriate primitive representation depending on the conversion context.

---

# 31. `Symbol.toStringTag`

`Symbol.toStringTag` controls the tag used by:

```javascript
Object.prototype.toString()
```

Example:

```javascript
const user = {
    [Symbol.toStringTag]: "User"
};

console.log(
    Object.prototype.toString.call(user)
);
```

Output:

```text
[object User]
```

This can provide a custom descriptive tag.

---

# 32. `Symbol.hasInstance`

`Symbol.hasInstance` can customize the behavior of:

```javascript
instanceof
```

Example:

```javascript
class User {
    static [Symbol.hasInstance](value) {
        return value &&
            typeof value.name === "string";
    }
}

console.log(
    { name: "Sandip" } instanceof User
);
```

Output:

```text
true
```

This allows a class to define its own instance-checking behavior.

---

# 33. `Symbol.isConcatSpreadable`

`Symbol.isConcatSpreadable` controls whether an object should be flattened by:

```javascript
Array.prototype.concat()
```

Example:

```javascript
const values = [1, 2];

values[Symbol.isConcatSpreadable] = false;

console.log(
    [0].concat(values)
);
```

The array is treated as a single element instead of being spread into the result.

---

# 34. `Symbol.species`

`Symbol.species` can control which constructor should be used when built-in methods create derived objects.

It is mainly relevant to advanced subclassing of built-in objects such as:

```text
Array
Map
Set
TypedArray
```

Example:

```javascript
class MyArray extends Array {
    static get [Symbol.species]() {
        return Array;
    }
}
```

This is an advanced feature and is less common in everyday application code.

---

# 35. `Symbol.match`

`Symbol.match` controls how an object behaves when used with:

```javascript
String.prototype.match()
```

Example:

```javascript
const matcher = {
    [Symbol.match](text) {
        return text.includes("JavaScript")
            ? ["JavaScript"]
            : null;
    }
};

console.log(
    "I love JavaScript".match(matcher)
);
```

Output:

```text
["JavaScript"]
```

---

# 36. `Symbol.replace`

`Symbol.replace` can customize behavior when an object is used with:

```javascript
String.prototype.replace()
```

Example:

```javascript
const replacer = {
    [Symbol.replace](text) {
        return text.toUpperCase();
    }
};

console.log(
    "hello".replace(replacer)
);
```

Output:

```text
HELLO
```

---

# 37. `Symbol.search`

`Symbol.search` can customize behavior for:

```javascript
String.prototype.search()
```

It allows an object to define how searching should work.

---

# 38. `Symbol.split`

`Symbol.split` can customize behavior for:

```javascript
String.prototype.split()
```

This allows an object to control how a string is divided.

---

# 39. Symbol and Private Fields

Symbols and private class fields are different concepts.

Symbol:

```javascript
const id = Symbol("id");

const user = {
    [id]: 101
};
```

Private class field:

```javascript
class User {
    #password = "secret";
}
```

Private fields provide actual language-level private class state.

Symbols mainly provide:

```text
Unique property keys
```

They should not be treated as a security mechanism.

---

# 40. Symbol vs Private Field

| Symbol                                          | Private Field                                 |
| ----------------------------------------------- | --------------------------------------------- |
| Unique property key                             | Private class member                          |
| Created using `Symbol()`                        | Uses `#`                                      |
| Can be discovered with Symbol reflection        | Not accessible through normal property access |
| Can be shared if the Symbol reference is shared | Controlled by class definition                |
| Useful for protocols and metadata               | Useful for private class state                |

---

# 41. Practical Example — Plugin Metadata

Symbols can help different plugins attach metadata without accidentally using the same string property.

```javascript
const pluginA = Symbol("pluginA");
const pluginB = Symbol("pluginB");

const application = {
    name: "My App",

    [pluginA]: {
        enabled: true
    },

    [pluginB]: {
        version: "1.0"
    }
};
```

Both plugins can store their own properties without using the same string property name.

---

# 42. Practical Example — Unique IDs

```javascript
const userId = Symbol("userId");

const user = {
    name: "Sandip",
    [userId]: 101
};

console.log(user[userId]);
```

The Symbol provides a unique property key.

---

# 43. Practical Example — Custom Iteration

Symbols are important when creating custom iterable objects.

```javascript
const numbers = {
    start: 1,
    end: 5,

    *[Symbol.iterator]() {
        for (
            let number = this.start;
            number <= this.end;
            number++
        ) {
            yield number;
        }
    }
};
```

Now:

```javascript
console.log([...numbers]);
```

Output:

```text
[1, 2, 3, 4, 5]
```

Here:

```text
Symbol.iterator
        ↓
Generator
        ↓
Iterator
        ↓
for...of / spread
```

---

# 44. Symbol Property Enumeration

| Method                           | String Keys | Symbol Keys |
| -------------------------------- | ----------: | ----------: |
| `Object.keys()`                  |         Yes |          No |
| `Object.values()`                |      Values |          No |
| `Object.entries()`               |         Yes |          No |
| `Object.getOwnPropertyNames()`   |         Yes |          No |
| `Object.getOwnPropertySymbols()` |          No |         Yes |
| `Reflect.ownKeys()`              |         Yes |         Yes |
| `for...in`                       |         Yes |          No |

This difference is important when working with advanced JavaScript objects.

---

# 45. Symbol Registry Comparison

```javascript
const a = Symbol("id");
const b = Symbol("id");

console.log(a === b);
```

Result:

```text
false
```

Global registry:

```javascript
const c = Symbol.for("id");
const d = Symbol.for("id");

console.log(c === d);
```

Result:

```text
true
```

Remember:

```text
Symbol()
    → always creates a new Symbol

Symbol.for()
    → uses the global Symbol registry
```

---

# 46. Symbols in Modern JavaScript

You will encounter Symbols especially when learning:

```text
Iterators
Generators
Collections
Metaprogramming
Custom object behavior
Framework internals
JavaScript protocols
```

The most important Symbol to understand first is:

```javascript
Symbol.iterator
```

because it connects directly to:

```text
for...of
spread
Array.from()
destructuring
generators
custom iterables
```

---

# 47. Important Well-Known Symbols Summary

| Symbol                      | Purpose                                 |
| --------------------------- | --------------------------------------- |
| `Symbol.iterator`           | Defines synchronous iteration           |
| `Symbol.asyncIterator`      | Defines asynchronous iteration          |
| `Symbol.toPrimitive`        | Controls object-to-primitive conversion |
| `Symbol.toStringTag`        | Customizes object string tag            |
| `Symbol.hasInstance`        | Customizes `instanceof`                 |
| `Symbol.isConcatSpreadable` | Controls `concat()` spreading           |
| `Symbol.species`            | Controls derived object construction    |
| `Symbol.match`              | Customizes string matching              |
| `Symbol.replace`            | Customizes string replacement           |
| `Symbol.search`             | Customizes string searching             |
| `Symbol.split`              | Customizes string splitting             |

---

# 48. Quick Cheat Sheet

```javascript
// Create Symbol
const id = Symbol("id");

// Check type
typeof id;
// "symbol"

// Symbols are unique
Symbol("id") === Symbol("id");
// false

// Symbol property
const user = {
    [id]: 101
};

// Access Symbol property
user[id];

// Symbol description
id.description;

// Global Symbol registry
const a = Symbol.for("user");
const b = Symbol.for("user");

a === b;
// true

// Get registry key
Symbol.keyFor(a);
// "user"

// Get Symbol keys
Object.getOwnPropertySymbols(user);

// Get all own keys
Reflect.ownKeys(user);
```

---

# 49. Symbol Protocol Flow

```text
Symbol
  │
  ├── Unique Property Keys
  │
  ├── Global Registry
  │   ├── Symbol.for()
  │   └── Symbol.keyFor()
  │
  └── Well-Known Symbols
      │
      ├── Symbol.iterator
      ├── Symbol.asyncIterator
      ├── Symbol.toPrimitive
      ├── Symbol.toStringTag
      ├── Symbol.hasInstance
      ├── Symbol.species
      ├── Symbol.match
      ├── Symbol.replace
      ├── Symbol.search
      └── Symbol.split
```

---

# Key Takeaways

* `Symbol` is a JavaScript primitive data type.
* Every `Symbol()` call creates a unique Symbol.
* Two Symbols with the same description are still different.
* Symbols can be used as object property keys.
* Symbol properties help avoid property-name collisions.
* Symbol properties are not truly private or secure.
* `Object.keys()` does not include Symbol keys.
* `Object.getOwnPropertySymbols()` retrieves Symbol keys.
* `Reflect.ownKeys()` retrieves both string and Symbol keys.
* `Symbol.for()` uses the global Symbol registry.
* `Symbol.keyFor()` retrieves a registry key.
* `Symbol.iterator` defines synchronous iteration.
* `Symbol.asyncIterator` defines asynchronous iteration.
* `Symbol.toPrimitive` controls object-to-primitive conversion.
* `Symbol.toStringTag` customizes the object's string tag.
* `Symbol.hasInstance` can customize `instanceof`.
* Well-known Symbols allow objects to customize JavaScript behavior.
* `Symbol.iterator` is especially important for iterators and generators.
* Symbols are about uniqueness and language protocols, not security.

---

# Symbol Roadmap

```text
Symbol
   │
   ├── Primitive Type
   │
   ├── Unique Values
   │
   ├── Object Property Keys
   │
   ├── Symbol()
   │
   ├── Symbol.for()
   │
   ├── Symbol.keyFor()
   │
   ├── Symbol Description
   │
   └── Well-Known Symbols
       │
       ├── iterator
       ├── asyncIterator
       ├── toPrimitive
       ├── toStringTag
       ├── hasInstance
       ├── species
       ├── match
       ├── replace
       ├── search
       └── split
```

---
