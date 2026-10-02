# JavaScript Object Basics

An **object** is a data structure used to store related data and functionality using **key-value pairs**.

Objects are one of the most important concepts in JavaScript.

For example, a user can have:

```text
name
email
age
role
```

Instead of storing them separately:

```javascript
let name = "Sandip";
let email = "sandip@example.com";
let age = 22;
let role = "developer";
```

We can group them into an object:

```javascript
let user = {
    name: "Sandip",
    email: "sandip@example.com",
    age: 22,
    role: "developer"
};
```

---

## 1. What is an Object?

An object stores data in **key-value pairs**.

```javascript
let user = {
    name: "Sandip",
    age: 22
};
```

Here:

```text
name → key
Sandip → value

age → key
22 → value
```

The general structure is:

```javascript
let objectName = {
    key: value,
    key: value
};
```

---

## 2. Creating an Object

The most common way to create an object is using curly braces `{}`.

```javascript
let person = {
    name: "Sandip",
    age: 22,
    city: "Birgunj"
};
```

The object contains three properties:

```text
name
age
city
```

---

## 3. Object Properties

The data stored inside an object is called a **property**.

```javascript
let user = {
    name: "Sandip",
    age: 22,
    isActive: true
};
```

Properties:

```text
name
age
isActive
```

Their values are:

```text
"Sandip"
22
true
```

---

## 4. Different Data Types in Objects

Object properties can contain different data types.

```javascript
let user = {
    name: "Sandip",       // String
    age: 22,              // Number
    isStudent: true,      // Boolean
    address: null,        // Null
    phone: undefined      // Undefined
};
```

Objects can also contain arrays, objects, and functions.

---

## 5. Accessing Object Properties

There are two common ways to access properties:

1. Dot notation
2. Bracket notation

---

## 6. Dot Notation

Use a dot `.` followed by the property name.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

console.log(user.name);
```

Output:

```text
Sandip
```

Another example:

```javascript
console.log(user.age);
```

Output:

```text
22
```

---

## 7. Bracket Notation

You can also use square brackets.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

console.log(user["name"]);
console.log(user["age"]);
```

Output:

```text
Sandip
22
```

---

## 8. Dot Notation vs Bracket Notation

### Dot notation

```javascript
user.name;
```

### Bracket notation

```javascript
user["name"];
```

Both access the same property.

Dot notation is usually simpler.

Bracket notation is especially useful when the property name is stored in a variable or contains characters that are not valid in normal dot notation.

---

## 9. Using a Variable with Bracket Notation

Suppose the property name is stored in a variable.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

let property = "name";

console.log(user[property]);
```

Output:

```text
Sandip
```

This would not work the same way:

```javascript
console.log(user.property);
```

That looks for a property literally named `property`.

---

## 10. Adding a New Property

You can add a property after creating the object.

```javascript
let user = {
    name: "Sandip"
};

user.age = 22;

console.log(user);
```

Result:

```javascript
{
    name: "Sandip",
    age: 22
}
```

---

## 11. Adding Properties with Bracket Notation

```javascript
let user = {
    name: "Sandip"
};

user["age"] = 22;

console.log(user);
```

---

## 12. Updating a Property

You can change an existing property's value.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

user.age = 23;

console.log(user.age);
```

Output:

```text
23
```

---

## 13. Updating a String Property

```javascript
let user = {
    name: "Sandip"
};

user.name = "Prasad";

console.log(user.name);
```

Output:

```text
Prasad
```

---

## 14. Deleting a Property

Use the `delete` operator.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

delete user.age;

console.log(user);
```

Result:

```javascript
{
    name: "Sandip"
}
```

---

## 15. Checking Whether a Property Exists

You can use the `in` operator.

```javascript
let user = {
    name: "Sandip",
    age: 22
};

console.log("name" in user);
```

Output:

```text
true
```

Example:

```javascript
console.log("email" in user);
```

Output:

```text
false
```

---

## 16. Accessing a Property That Doesn't Exist

If a property does not exist, JavaScript returns `undefined`.

```javascript
let user = {
    name: "Sandip"
};

console.log(user.age);
```

Output:

```text
undefined
```

This does not automatically create the property.

---

## 17. Object with Nested Data

Objects can contain other objects.

```javascript
let user = {
    name: "Sandip",
    address: {
        city: "Birgunj",
        country: "Nepal"
    }
};
```

Access the nested object:

```javascript
console.log(user.address);
```

Access the city:

```javascript
console.log(user.address.city);
```

Output:

```text
Birgunj
```

---

## 18. Object with an Array

An object can contain an array.

```javascript
let user = {
    name: "Sandip",
    skills: ["JavaScript", "React", "Node.js"]
};
```

Access the array:

```javascript
console.log(user.skills);
```

Access an array item:

```javascript
console.log(user.skills[0]);
```

Output:

```text
JavaScript
```

---

## 19. Object with Different Data

A real application object can contain many types.

```javascript
let user = {
    name: "Sandip",
    age: 22,
    email: "sandip@example.com",
    isActive: true,
    skills: ["JavaScript", "React", "Node.js"],
    address: {
        city: "Birgunj",
        country: "Nepal"
    }
};
```

---

## 20. Object with a Function

A function stored inside an object is called a **method**.

```javascript
let user = {
    name: "Sandip",

    greet: function () {
        console.log("Hello");
    }
};
```

Call the method:

```javascript
user.greet();
```

Output:

```text
Hello
```

Methods will be covered in more detail in:

```text
06-Objects/03-Object-Methods.md
```

---

## 21. Shorthand Property Names

If the variable name and property name are the same, you can use shorthand syntax.

Without shorthand:

```javascript
let name = "Sandip";
let age = 22;

let user = {
    name: name,
    age: age
};
```

With shorthand:

```javascript
let name = "Sandip";
let age = 22;

let user = {
    name,
    age
};
```

Both create:

```javascript
{
    name: "Sandip",
    age: 22
}
```

---

## 22. Object Property Names

Property names are usually written as identifiers.

```javascript
let user = {
    name: "Sandip",
    age: 22
};
```

They can also be written using quotes.

```javascript
let user = {
    "first-name": "Sandip",
    "user-role": "developer"
};
```

Properties containing characters such as `-` need bracket notation:

```javascript
console.log(user["first-name"]);
```

---

## 23. Computed Property Names

You can create a property name dynamically.

```javascript
let key = "name";

let user = {
    [key]: "Sandip"
};

console.log(user.name);
```

Output:

```text
Sandip
```

The expression inside `[]` determines the property name.

---

## 24. Numeric Property Names

Property names can also be numbers.

```javascript
let data = {
    1: "One",
    2: "Two"
};

console.log(data[1]);
```

Output:

```text
One
```

Object property keys are generally strings or symbols, so numeric-looking keys are handled as property names.

---

## 25. Duplicate Property Names

If an object has duplicate property names, the later value replaces the earlier one.

```javascript
let user = {
    name: "Sandip",
    name: "Prasad"
};

console.log(user.name);
```

Output:

```text
Prasad
```

Avoid duplicate property names unless you have a specific reason.

---

## 26. Objects with `const`

You can create an object using `const`.

```javascript
const user = {
    name: "Sandip",
    age: 22
};
```

You can still change its properties:

```javascript
user.age = 23;

console.log(user.age);
```

Output:

```text
23
```

But you cannot reassign the entire object:

```javascript
user = {
    name: "Prasad"
};
```

This causes an error because the `const` variable cannot be reassigned.

---

## 27. Important `const` Object Concept

Remember:

```javascript
const user = {
    name: "Sandip"
};

user.name = "Prasad"; // Allowed
```

But:

```javascript
user = {}; // Not allowed
```

`const` prevents reassignment of the variable, not modification of the object it references.

---

## 28. Objects Are Reference Values

Consider:

```javascript
let user1 = {
    name: "Sandip"
};

let user2 = user1;

user2.name = "Prasad";

console.log(user1.name);
```

Output:

```text
Prasad
```

Why?

Both variables refer to the same object.

Conceptually:

```text
user1 ──┐
        ├──> { name: "Prasad" }
user2 ──┘
```

This concept becomes important when working with copies and object mutation.

---

## 29. Comparing Objects

Two separate objects are not equal just because they contain the same data.

```javascript
let user1 = {
    name: "Sandip"
};

let user2 = {
    name: "Sandip"
};

console.log(user1 === user2);
```

Output:

```text
false
```

They are two different object references.

But:

```javascript
let user1 = {
    name: "Sandip"
};

let user2 = user1;

console.log(user1 === user2);
```

Output:

```text
true
```

Both variables refer to the same object.

---

## 30. Object Example: Student

```javascript
let student = {
    name: "Sandip",
    age: 22,
    course: "BSc.CSIT",
    university: "Tribhuvan University"
};

console.log(student.name);
console.log(student.course);
```

Output:

```text
Sandip
BSc.CSIT
```

---

## 31. Object Example: Product

```javascript
let product = {
    name: "Laptop",
    price: 80000,
    category: "Electronics",
    inStock: true
};

console.log(product.name);
console.log(product.price);
console.log(product.inStock);
```

---

## 32. Object Example: Hotel Food

```javascript
let food = {
    name: "Chicken Momo",
    price: 250,
    isVeg: false,
    isAvailable: true
};

console.log(food.name);
console.log(food.price);
console.log(food.isAvailable);
```

Output:

```text
Chicken Momo
250
true
```

---

## 33. Object Example: Hotel Table

```javascript
let table = {
    tableNumber: "T-03",
    capacity: 6,
    status: "available",
    location: "indoor"
};

console.log(table.tableNumber);
console.log(table.capacity);
console.log(table.status);
```

---

## 34. Object Example: Order

```javascript
let order = {
    customerName: "Sandip",
    foodName: "Chicken Momo",
    quantity: 2,
    price: 250,
    status: "pending"
};

let total = order.quantity * order.price;

console.log(`Customer: ${order.customerName}`);
console.log(`Food: ${order.foodName}`);
console.log(`Total: Rs. ${total}`);
console.log(`Status: ${order.status}`);
```

Output:

```text
Customer: Sandip
Food: Chicken Momo
Total: Rs. 500
Status: pending
```

---

## 35. Object Constructor Syntax

JavaScript also provides the `Object` constructor.

```javascript
let user = new Object();

user.name = "Sandip";
user.age = 22;

console.log(user);
```

However, object literal syntax is usually simpler:

```javascript
let user = {
    name: "Sandip",
    age: 22
};
```

---

## 36. Empty Object

You can create an empty object.

```javascript
let user = {};

console.log(user);
```

Output:

```text
{}
```

You can add properties later:

```javascript
user.name = "Sandip";
user.age = 22;
```

---

## 37. Checking the Type of an Object

Use `typeof`.

```javascript
let user = {
    name: "Sandip"
};

console.log(typeof user);
```

Output:

```text
object
```

Remember:

```javascript
typeof {};
```

returns:

```text
object
```

---

## 38. Object Structure

A simple object:

```javascript
let user = {
    name: "Sandip",
    age: 22
};
```

Can be visualized as:

```text
user
 │
 └── object
      ├── name → "Sandip"
      └── age  → 22
```

---

## 39. Common Mistakes

### Missing comma

Incorrect:

```javascript
let user = {
    name: "Sandip"
    age: 22
};
```

Correct:

```javascript
let user = {
    name: "Sandip",
    age: 22
};
```

---

### Using the wrong property name

```javascript
let user = {
    name: "Sandip"
};

console.log(user.username);
```

Result:

```text
undefined
```

The property is called `name`, not `username`.

---

### Using dot notation with a variable

```javascript
let key = "name";

console.log(user.key);
```

This looks for a property named `key`.

Use:

```javascript
console.log(user[key]);
```

---

## 40. Object Basics Cheat Sheet

| Task            | Example                |
| --------------- | ---------------------- |
| Create object   | `let user = {}`        |
| Add property    | `user.name = "Sandip"` |
| Access property | `user.name`            |
| Bracket access  | `user["name"]`         |
| Update property | `user.age = 23`        |
| Delete property | `delete user.age`      |
| Check property  | `"name" in user`       |
| Nested property | `user.address.city`    |
| Array property  | `user.skills[0]`       |
| Object type     | `typeof user`          |

---

## 41. Key Takeaways

* Objects store related data using key-value pairs.
* A property consists of a key and a value.
* Objects use `{}`.
* Properties can contain any JavaScript value.
* Use dot notation to access common property names.
* Use bracket notation for dynamic or special property names.
* You can add, update, and delete properties.
* Objects can contain arrays, functions, and other objects.
* Objects can be nested.
* Objects are reference values.
* Two separate objects are not equal with `===`.
* `const` objects can have their properties changed, but the object variable cannot be reassigned.
* Objects are fundamental to JavaScript and are heavily used in APIs, React, Node.js, and MongoDB applications.

---
