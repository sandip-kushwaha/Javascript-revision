# JavaScript Object Properties

Object properties are the **key-value pairs** stored inside a JavaScript object.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  isStudent: true
};
```

Here:

* `name` → property name
* `"Sandip"` → property value
* `age` → property name
* `22` → property value
* `isStudent` → property name
* `true` → property value

---

## 1. What is an Object Property?

A property describes some information about an object.

```javascript
const student = {
  name: "Sandip",
  age: 22,
  course: "BSc.CSIT"
};
```

The object has three properties:

```text
name   → "Sandip"
age    → 22
course → "BSc.CSIT"
```

---

# 2. Accessing Object Properties

There are two main ways to access properties:

1. Dot notation
2. Bracket notation

---

## 2.1 Dot Notation

Use a dot `.` followed by the property name.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

console.log(user.name);
console.log(user.age);
```

Output:

```text
Sandip
22
```

### Syntax

```javascript
object.property
```

Example:

```javascript
console.log(user.name);
```

---

# 3. Bracket Notation

Use square brackets `[]`.

```javascript
const user = {
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

### Syntax

```javascript
object["property"]
```

---

# 4. Dot Notation vs Bracket Notation

### Dot notation

```javascript
user.name;
```

### Bracket notation

```javascript
user["name"];
```

Both access the same property.

```javascript
console.log(user.name);
console.log(user["name"]);
```

Both produce:

```text
Sandip
```

---

# 5. When to Use Bracket Notation

Bracket notation is especially useful when the property name is stored in a variable.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const property = "name";

console.log(user[property]);
```

Output:

```text
Sandip
```

This is called **dynamic property access**.

---

# 6. Dynamic Property Access

You can use a variable to decide which property to access.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const key = "city";

console.log(user[key]);
```

Output:

```text
Birgunj
```

Another example:

```javascript
const key = "age";

console.log(user[key]);
```

Output:

```text
22
```

### Important

This:

```javascript
user[key];
```

is different from:

```javascript
user.key;
```

If:

```javascript
const key = "name";
```

Then:

```javascript
user[key];
```

means:

```javascript
user["name"];
```

But:

```javascript
user.key;
```

looks for a property literally called `"key"`.

---

# 7. Adding New Properties

You can add a property to an existing object.

```javascript
const user = {
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

Using bracket notation:

```javascript
user["city"] = "Birgunj";
```

Now:

```javascript
console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22,
  city: "Birgunj"
}
```

---

# 8. Updating Properties

If a property already exists, assigning a new value updates it.

```javascript
const user = {
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

You can also use bracket notation:

```javascript
user["age"] = 24;
```

---

# 9. Adding and Updating Are Similar

JavaScript does not require a separate syntax for adding and updating properties.

### Property does not exist

```javascript
user.city = "Birgunj";
```

JavaScript adds it.

### Property already exists

```javascript
user.age = 23;
```

JavaScript updates it.

---

# 10. Deleting Properties

Use the `delete` operator.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

delete user.city;

console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22
}
```

You can also use bracket notation:

```javascript
delete user["age"];
```

---

# 11. Checking Whether a Property Exists

Use the `in` operator.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

console.log("name" in user);
```

Output:

```text
true
```

For a property that does not exist:

```javascript
console.log("city" in user);
```

Output:

```text
false
```

### Syntax

```javascript
"propertyName" in object
```

---

# 12. `Object.hasOwn()`

Modern JavaScript provides `Object.hasOwn()` to check whether a property belongs directly to an object.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

console.log(Object.hasOwn(user, "name"));
```

Output:

```text
true
```

```javascript
console.log(Object.hasOwn(user, "city"));
```

Output:

```text
false
```

---

# 13. Own Properties vs Inherited Properties

An object can have:

* its own properties
* inherited properties

Example:

```javascript
const user = {
  name: "Sandip"
};
```

`name` is an own property of `user`.

Some properties may come from the object's prototype.

This is why:

```javascript
"name" in user
```

checks the object and its prototype chain.

While:

```javascript
Object.hasOwn(user, "name")
```

checks whether the property belongs directly to `user`.

For normal application code, `Object.hasOwn()` is often useful when you specifically need to check **own properties**.

---

# 14. `hasOwnProperty()`

You may also see:

```javascript
user.hasOwnProperty("name");
```

Example:

```javascript
const user = {
  name: "Sandip"
};

console.log(user.hasOwnProperty("name"));
```

Output:

```text
true
```

`hasOwnProperty()` is an older/common approach.

Modern JavaScript can use:

```javascript
Object.hasOwn(user, "name");
```

---

# 15. Property Names With Spaces

Property names can contain spaces.

```javascript
const user = {
  "full name": "Sandip Kushwaha"
};
```

You cannot use:

```javascript
user.full name;
```

Instead, use bracket notation:

```javascript
console.log(user["full name"]);
```

Output:

```text
Sandip Kushwaha
```

---

# 16. Property Names With Hyphens

A property can contain a hyphen.

```javascript
const user = {
  "user-name": "Sandip"
};
```

Access it using brackets:

```javascript
console.log(user["user-name"]);
```

---

# 17. Property Names Can Be Numbers

JavaScript object property keys are generally strings or symbols.

For example:

```javascript
const marks = {
  101: 80,
  102: 90
};
```

You can access them using:

```javascript
console.log(marks[101]);
```

Output:

```text
80
```

They are effectively treated as string property keys:

```javascript
console.log(marks["101"]);
```

Output:

```text
80
```

---

# 18. Property Values Can Be Any Data Type

An object property can contain almost any JavaScript value.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  isStudent: true,
  skills: ["JavaScript", "React", "Node.js"],
  address: {
    city: "Birgunj",
    country: "Nepal"
  },
  greet: function () {
    console.log("Hello");
  }
};
```

Properties can contain:

* String
* Number
* Boolean
* Array
* Object
* Function
* `null`
* `undefined`
* Other values

---

# 19. Object Property With an Array

```javascript
const student = {
  name: "Sandip",
  skills: ["JavaScript", "React", "Node.js"]
};

console.log(student.skills);
```

Output:

```text
["JavaScript", "React", "Node.js"]
```

Access an array item:

```javascript
console.log(student.skills[0]);
```

Output:

```text
JavaScript
```

---

# 20. Object Property With Another Object

Objects can contain other objects.

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj",
    country: "Nepal"
  }
};
```

Access nested properties:

```javascript
console.log(user.address.city);
```

Output:

```text
Birgunj
```

Using brackets:

```javascript
console.log(user["address"]["city"]);
```

---

# 21. Missing Properties

If you access a property that does not exist, JavaScript returns:

```javascript
undefined
```

Example:

```javascript
const user = {
  name: "Sandip"
};

console.log(user.age);
```

Output:

```text
undefined
```

This does not automatically create the property.

```javascript
console.log("age" in user);
```

Output:

```text
false
```

---

# 22. Property Exists With `undefined`

Be careful with this situation:

```javascript
const user = {
  name: "Sandip",
  age: undefined
};
```

Now:

```javascript
console.log(user.age);
```

Output:

```text
undefined
```

But the property actually exists.

```javascript
console.log("age" in user);
```

Output:

```text
true
```

And:

```javascript
console.log(Object.hasOwn(user, "age"));
```

Output:

```text
true
```

So:

```text
property value === undefined
```

does not necessarily mean:

```text
property does not exist
```

---

# 23. Checking Property Before Using It

You can check whether a property exists:

```javascript
if ("email" in user) {
  console.log(user.email);
}
```

Or for an own property:

```javascript
if (Object.hasOwn(user, "email")) {
  console.log(user.email);
}
```

---

# 24. Computed Property Names

You can create a property using a variable.

```javascript
const key = "name";

const user = {
  [key]: "Sandip"
};

console.log(user.name);
```

Output:

```text
Sandip
```

Another example:

```javascript
const field = "email";

const user = {
  [field]: "sandip@example.com"
};

console.log(user.email);
```

---

# 25. Dynamic Property Creation

This is useful when working with forms and APIs.

```javascript
const user = {};

const field = "name";
const value = "Sandip";

user[field] = value;

console.log(user);
```

Result:

```javascript
{
  name: "Sandip"
}
```

Another example:

```javascript
const field = "email";
const value = "sandip@example.com";

user[field] = value;
```

Now:

```javascript
console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  email: "sandip@example.com"
}
```

---

# 26. Hotel Management Example

Consider a hotel table:

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "occupied",
  location: "indoor"
};
```

Access properties:

```javascript
console.log(table.tableNumber);
console.log(table.capacity);
console.log(table.status);
```

Update status:

```javascript
table.status = "available";
```

Add a property:

```javascript
table.isActive = true;
```

Delete a property:

```javascript
delete table.location;
```

---

# 27. Food Example

```javascript
const food = {
  name: "Chicken Momo",
  price: 180,
  isVeg: false,
  isAvailable: true
};
```

Update price:

```javascript
food.price = 200;
```

Update availability:

```javascript
food.isAvailable = false;
```

Add preparation time:

```javascript
food.preparationTime = 20;
```

Check property:

```javascript
console.log(Object.hasOwn(food, "price"));
```

Output:

```text
true
```

---

# 28. Order Example

```javascript
const order = {
  orderNumber: "ORD-001",
  status: "pending",
  totalAmount: 850
};
```

Update status:

```javascript
order.status = "confirmed";
```

Update total:

```javascript
order.totalAmount = 900;
```

Add customer information:

```javascript
order.customerName = "Sandip";
```

---

# 29. Object Properties and `const`

You can modify properties of an object declared with `const`.

```javascript
const user = {
  name: "Sandip"
};

user.name = "Ram";

console.log(user.name);
```

Output:

```text
Ram
```

But you cannot reassign the object itself:

```javascript
const user = {
  name: "Sandip"
};

user = {
  name: "Ram"
};
```

This causes an error.

`const` protects the variable binding, not the contents of the object.

---

# 30. Object Properties Are Mutable

Objects are mutable by default.

```javascript
const product = {
  name: "Laptop",
  price: 80000
};

product.price = 75000;
```

The object has been modified.

```javascript
console.log(product.price);
```

Output:

```text
75000
```

---

# 31. Property References

Objects are reference values.

```javascript
const user1 = {
  name: "Sandip"
};

const user2 = user1;

user2.name = "Ram";

console.log(user1.name);
```

Output:

```text
Ram
```

Both variables refer to the same object.

```text
user1 ──┐
        ├──> { name: "Ram" }
user2 ──┘
```

---

# 32. Copying an Object

Using spread syntax creates a shallow copy:

```javascript
const user1 = {
  name: "Sandip",
  age: 22
};

const user2 = {
  ...user1
};

user2.name = "Ram";

console.log(user1.name);
console.log(user2.name);
```

Output:

```text
Sandip
Ram
```

The objects are separate at the top level.

---

# 33. Property Shorthand

When the variable name and property name are the same, you can use shorthand.

```javascript
const name = "Sandip";
const age = 22;

const user = {
  name,
  age
};

console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  age: 22
}
```

Instead of:

```javascript
const user = {
  name: name,
  age: age
};
```

---

# 34. Property Names From Variables

You can combine computed properties with variables.

```javascript
const propertyName = "username";
const propertyValue = "sandip";

const user = {
  [propertyName]: propertyValue
};

console.log(user);
```

Result:

```javascript
{
  username: "sandip"
}
```

---

# 35. Property Access With Variables

This is very common when processing API data or forms.

```javascript
const user = {
  name: "Sandip",
  email: "sandip@example.com",
  age: 22
};

function getProperty(object, property) {
  return object[property];
}

console.log(getProperty(user, "name"));
console.log(getProperty(user, "email"));
```

Output:

```text
Sandip
sandip@example.com
```

---

# 36. Common Mistakes

## Mistake 1: Using a variable with dot notation

```javascript
const key = "name";

console.log(user.key);
```

This looks for:

```text
user["key"]
```

Use:

```javascript
console.log(user[key]);
```

---

## Mistake 2: Forgetting quotes in bracket notation

Incorrect:

```javascript
user[name];
```

If `name` is not a variable, use:

```javascript
user["name"];
```

---

## Mistake 3: Trying to access properties with spaces using dot notation

Incorrect:

```javascript
user.full name;
```

Correct:

```javascript
user["full name"];
```

---

## Mistake 4: Assuming `undefined` means the property does not exist

```javascript
const user = {
  age: undefined
};
```

The property exists even though its value is `undefined`.

Use:

```javascript
Object.hasOwn(user, "age");
```

when you need to check ownership.

---

# 37. Property Access Cheat Sheet

| Operation          | Syntax                       |
| ------------------ | ---------------------------- |
| Dot access         | `user.name`                  |
| Bracket access     | `user["name"]`               |
| Dynamic access     | `user[key]`                  |
| Add property       | `user.age = 22`              |
| Update property    | `user.age = 23`              |
| Delete property    | `delete user.age`            |
| Check property     | `"age" in user`              |
| Check own property | `Object.hasOwn(user, "age")` |
| Nested property    | `user.address.city`          |
| Dynamic property   | `user[key]`                  |
| Computed property  | `{ [key]: value }`           |

---

# 38. Key Takeaways

* An object contains **properties** in key-value form.
* Use **dot notation** for simple property names.
* Use **bracket notation** for dynamic or special property names.
* You can add properties using assignment.
* You can update properties using assignment.
* Use `delete` to remove a property.
* Use `in` to check whether a property exists anywhere on the object/prototype chain.
* Use `Object.hasOwn()` to check whether a property belongs directly to the object.
* A missing property normally returns `undefined`.
* A property can exist while its value is `undefined`.
* Property values can be strings, numbers, arrays, objects, functions, and other JavaScript values.
* Objects declared with `const` can still have their properties changed.
* Objects are reference values.
* Bracket notation is especially useful for dynamic property access.
* Computed property names allow variables to determine property names.

---

## Quick Example

```javascript
const user = {
  name: "Sandip",
  age: 22
};

// Read
console.log(user.name);

// Add
user.city = "Birgunj";

// Update
user.age = 23;

// Dynamic access
const key = "city";
console.log(user[key]);

// Check
console.log(Object.hasOwn(user, "name"));

// Delete
delete user.city;

console.log(user);
```

---
