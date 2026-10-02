# JavaScript `sort()` Method

The `sort()` method is used to **sort the elements of an array**.

It changes the **original array**.

---

## 1. Basic Example

```javascript
const fruits = ["Banana", "Apple", "Orange"];

fruits.sort();

console.log(fruits);
```

Output:

```text
["Apple", "Banana", "Orange"]
```

By default, `sort()` sorts values as **strings**.

---

## 2. Sorting Numbers

This can cause a problem:

```javascript
const numbers = [10, 5, 20, 2];

numbers.sort();

console.log(numbers);
```

Output:

```text
[10, 2, 20, 5]
```

Why?

Because JavaScript converts the numbers to strings and compares them.

To correctly sort numbers, use a comparison function.

### Ascending Order

```javascript
const numbers = [10, 5, 20, 2];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output:

```text
[2, 5, 10, 20]
```

### Descending Order

```javascript
numbers.sort((a, b) => b - a);

console.log(numbers);
```

Output:

```text
[20, 10, 5, 2]
```

---

## 3. How the Comparison Function Works

```javascript
(a, b) => a - b
```

The result determines the order:

```text
negative → a comes before b
zero     → keep their order
positive → b comes before a
```

Example:

```javascript
5 - 10 = -5
```

So `5` comes before `10`.

---

## 4. Sort Strings

```javascript
const names = ["Ram", "Hari", "Shyam"];

names.sort();

console.log(names);
```

Output:

```text
["Hari", "Ram", "Shyam"]
```

---

## 5. Reverse String Order

Use `sort()` followed by `reverse()`:

```javascript
const names = ["Ram", "Hari", "Shyam"];

names.sort().reverse();

console.log(names);
```

Output:

```text
["Shyam", "Ram", "Hari"]
```

---

## 6. Sort Objects by Number

Suppose:

```javascript
const students = [
    { name: "Ram", marks: 70 },
    { name: "Hari", marks: 90 },
    { name: "Shyam", marks: 80 }
];
```

### Ascending

```javascript
students.sort((a, b) => a.marks - b.marks);
```

Result:

```text
Ram → 70
Shyam → 80
Hari → 90
```

### Descending

```javascript
students.sort((a, b) => b.marks - a.marks);
```

---

## 7. Sort Objects by Name

```javascript
const users = [
    { name: "Shyam" },
    { name: "Ram" },
    { name: "Hari" }
];

users.sort((a, b) => {
    return a.name.localeCompare(b.name);
});
```

Result:

```text
Hari
Ram
Shyam
```

`localeCompare()` is useful for comparing strings.

---

## 8. Case-Insensitive Sorting

```javascript
const names = ["ram", "Hari", "shyam", "Bikash"];

names.sort((a, b) => {
    return a.toLowerCase().localeCompare(b.toLowerCase());
});

console.log(names);
```

This avoids basic uppercase/lowercase ordering differences.

---

## 9. `sort()` Changes the Original Array

```javascript
const numbers = [3, 1, 2];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output:

```text
[1, 2, 3]
```

The original array has changed.

---

## 10. Keep the Original Array Unchanged

Create a copy first:

```javascript
const numbers = [3, 1, 2];

const sortedNumbers = [...numbers].sort((a, b) => a - b);

console.log(numbers);
console.log(sortedNumbers);
```

Output:

```text
[3, 1, 2]
[1, 2, 3]
```

You can also use:

```javascript
const sortedNumbers = numbers.slice().sort((a, b) => a - b);
```

---

## 11. Hotel Food Example

```javascript
const foods = [
    { name: "Pizza", price: 500 },
    { name: "Momo", price: 150 },
    { name: "Burger", price: 300 }
];
```

Sort by price:

```javascript
foods.sort((a, b) => a.price - b.price);
```

Result:

```text
Momo → 150
Burger → 300
Pizza → 500
```

---

## 12. Sort by Highest Price

```javascript
foods.sort((a, b) => b.price - a.price);
```

Result:

```text
Pizza → 500
Burger → 300
Momo → 150
```

---

## 13. Sort by Multiple Conditions

For example, sort users by age:

```javascript
const users = [
    { name: "Ram", age: 20 },
    { name: "Hari", age: 20 },
    { name: "Shyam", age: 18 }
];
```

```javascript
users.sort((a, b) => {
    if (a.age !== b.age) {
        return a.age - b.age;
    }

    return a.name.localeCompare(b.name);
});
```

First sorts by age, then by name when ages are equal.

---

## 14. Important: `sort()` Returns the Array

```javascript
const numbers = [3, 1, 2];

const result = numbers.sort((a, b) => a - b);

console.log(result);
```

Output:

```text
[1, 2, 3]
```

But remember that the original array is also changed.

---

## 15. `sort()` with Empty Array

```javascript
const numbers = [];

numbers.sort();

console.log(numbers);
```

Output:

```text
[]
```

No error occurs.

---

## 16. Common Mistakes

### Mistake 1: Sorting numbers without a comparator

Wrong:

```javascript
numbers.sort();
```

Correct:

```javascript
numbers.sort((a, b) => a - b);
```

### Mistake 2: Forgetting that `sort()` mutates

```javascript
const sorted = numbers.sort();
```

This also changes `numbers`.

Use:

```javascript
const sorted = [...numbers].sort();
```

when you want to preserve the original.

---

## 17. `sort()` vs `reverse()`

`sort()` arranges elements:

```javascript
numbers.sort((a, b) => a - b);
```

`reverse()` reverses the current order:

```javascript
numbers.reverse();
```

Example:

```javascript
const numbers = [1, 2, 3];

numbers.reverse();

console.log(numbers);
```

Output:

```text
[3, 2, 1]
```

Both methods modify the original array.

---

## 18. Quick Comparison

| Method      | Purpose            | Mutates Original? |
| ----------- | ------------------ | ----------------- |
| `sort()`    | Sort elements      | Yes               |
| `reverse()` | Reverse elements   | Yes               |
| `slice()`   | Copy part of array | No                |
| `map()`     | Transform elements | No                |
| `filter()`  | Select elements    | No                |

---

## 19. Quick Revision

### String sorting

```javascript
names.sort();
```

### Numbers ascending

```javascript
numbers.sort((a, b) => a - b);
```

### Numbers descending

```javascript
numbers.sort((a, b) => b - a);
```

### Object numbers

```javascript
users.sort((a, b) => a.age - b.age);
```

### Object strings

```javascript
users.sort((a, b) => a.name.localeCompare(b.name));
```

### Preserve original array

```javascript
const sorted = [...numbers].sort((a, b) => a - b);
```

---

## 20. Key Takeaways

* `sort()` sorts array elements.
* By default, values are compared as strings.
* Use `(a, b) => a - b` for numbers in ascending order.
* Use `(a, b) => b - a` for numbers in descending order.
* `localeCompare()` is useful for strings.
* `sort()` changes the original array.
* Use `[...array].sort()` when you want a sorted copy.
* `reverse()` reverses the array order.

---
