# JavaScript Object Destructuring

**Object destructuring** is a JavaScript feature that allows you to extract properties from an object and store them in variables.

Instead of writing:

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const name = user.name;
const age = user.age;
const city = user.city;
```

You can write:

```javascript
const {
  name,
  age,
  city
} = user;
```

Now:

```javascript
console.log(name);
console.log(age);
console.log(city);
```

Output:

```text
Sandip
22
Birgunj
```

---

# 1. What Is Destructuring?

Destructuring means **extracting values from an object into variables**.

Example:

```javascript
const student = {
  name: "Sandip",
  course: "BSc.CSIT"
};

const {
  name,
  course
} = student;
```

Now:

```javascript
console.log(name);
console.log(course);
```

Output:

```text
Sandip
BSc.CSIT
```

---

# 2. Basic Syntax

```javascript
const {
  property1,
  property2
} = object;
```

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const {
  name,
  age
} = user;
```

The variable names match the object property names.

---

# 3. Destructuring Only Selected Properties

You do not need to extract every property.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj",
  country: "Nepal"
};

const {
  name,
  city
} = user;

console.log(name);
console.log(city);
```

Output:

```text
Sandip
Birgunj
```

`age` and `country` are not extracted.

---

# 4. Property Order Does Not Matter

Object destructuring is based on **property names**, not positions.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const {
  age,
  name
} = user;

console.log(name);
console.log(age);
```

Output:

```text
Sandip
22
```

The order inside `{}` does not need to match the object's order.

---

# 5. Renaming Variables

You can extract a property and give it a different variable name.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const {
  name: userName,
  age: userAge
} = user;

console.log(userName);
console.log(userAge);
```

Output:

```text
Sandip
22
```

### Syntax

```javascript
const {
  property: newVariable
} = object;
```

For example:

```javascript
const {
  name: fullName
} = user;
```

This means:

```text
Object property → name
Variable         → fullName
```

---

# 6. Default Values

You can provide a default value when a property is `undefined`.

```javascript
const user = {
  name: "Sandip"
};

const {
  name,
  age = 22
} = user;

console.log(name);
console.log(age);
```

Output:

```text
Sandip
22
```

The default value is used because `age` is `undefined`.

---

# 7. Default Value Is Used Only for `undefined`

Example:

```javascript
const user = {
  age: null
};

const {
  age = 22
} = user;

console.log(age);
```

Output:

```text
null
```

The default is **not** used for `null`.

Default values are used when the extracted value is `undefined`.

---

# 8. Nested Object Destructuring

You can destructure nested objects.

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj",
    country: "Nepal"
  }
};

const {
  address: {
    city,
    country
  }
} = user;

console.log(city);
console.log(country);
```

Output:

```text
Birgunj
Nepal
```

---

# 9. Nested Destructuring With Renaming

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};

const {
  address: {
    city: userCity
  }
} = user;

console.log(userCity);
```

Output:

```text
Birgunj
```

---

# 10. Destructuring Object Properties Into Existing Variables

If variables already exist, you can destructure into them.

```javascript
let name;
let age;

const user = {
  name: "Sandip",
  age: 22
};

({ name, age } = user);

console.log(name);
console.log(age);
```

Notice the parentheses:

```javascript
({ name, age } = user);
```

They are necessary because JavaScript could otherwise interpret `{}` as a block statement.

---

# 11. Function Parameters With Destructuring

Object destructuring is very common in function parameters.

Without destructuring:

```javascript
function greet(user) {
  console.log(`Hello ${user.name}`);
}

greet({
  name: "Sandip"
});
```

With destructuring:

```javascript
function greet({ name }) {
  console.log(`Hello ${name}`);
}

greet({
  name: "Sandip"
});
```

Output:

```text
Hello Sandip
```

---

# 12. Multiple Destructured Parameters

```javascript
function showUser({ name, age, city }) {
  console.log(name);
  console.log(age);
  console.log(city);
}

showUser({
  name: "Sandip",
  age: 22,
  city: "Birgunj"
});
```

Output:

```text
Sandip
22
Birgunj
```

This is very common when working with functions that receive configuration objects.

---

# 13. Destructuring With Default Parameters

You can combine function parameter defaults and object destructuring.

```javascript
function greet({ name = "Guest" } = {}) {
  console.log(`Hello ${name}`);
}

greet();
```

Output:

```text
Hello Guest
```

And:

```javascript
greet({
  name: "Sandip"
});
```

Output:

```text
Hello Sandip
```

---

# 14. Destructuring API Data

Suppose an API returns:

```javascript
const response = {
  name: "Sandip",
  email: "sandip@example.com",
  role: "admin"
};
```

Instead of:

```javascript
console.log(response.name);
console.log(response.email);
console.log(response.role);
```

You can use:

```javascript
const {
  name,
  email,
  role
} = response;

console.log(name);
console.log(email);
console.log(role);
```

This is very common in frontend development.

---

# 15. React Example

In React, props are commonly destructured.

Without destructuring:

```javascript
function UserCard(props) {
  return <h2>{props.name}</h2>;
}
```

With destructuring:

```javascript
function UserCard({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
    </div>
  );
}
```

Example:

```javascript
<UserCard
  name="Sandip"
  age={22}
/>
```

Destructuring makes the component code shorter and easier to read.

---

# 16. Destructuring Object Returned From a Function

A function can return an object.

```javascript
function getUser() {
  return {
    name: "Sandip",
    age: 22
  };
}

const {
  name,
  age
} = getUser();

console.log(name);
console.log(age);
```

Output:

```text
Sandip
22
```

---

# 17. Destructuring With `const`

Most destructuring examples use `const`.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

const {
  name,
  age
} = user;
```

The extracted variables cannot be reassigned.

---

# 18. Destructuring With `let`

You can also use `let`.

```javascript
const user = {
  name: "Sandip",
  age: 22
};

let {
  name,
  age
} = user;

age = 23;

console.log(age);
```

Output:

```text
23
```

---

# 19. Destructuring With `var`

It is also possible with `var`.

```javascript
const user = {
  name: "Sandip"
};

var {
  name
} = user;

console.log(name);
```

However, modern JavaScript generally prefers `const` or `let`.

---

# 20. Rest Property

Object destructuring supports the rest syntax `...`.

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj",
  country: "Nepal"
};

const {
  name,
  ...otherDetails
} = user;

console.log(name);
console.log(otherDetails);
```

Output:

```text
Sandip

{
  age: 22,
  city: "Birgunj",
  country: "Nepal"
}
```

The rest property collects the remaining properties into a new object.

---

# 21. Rest Property Must Be Last

Correct:

```javascript
const {
  name,
  ...details
} = user;
```

Incorrect:

```javascript
const {
  ...details,
  name
} = user;
```

The rest property must be the **last property** in the destructuring pattern.

---

# 22. Renaming + Default Value

You can combine renaming and default values.

```javascript
const user = {
  name: "Sandip"
};

const {
  name: userName,
  age: userAge = 22
} = user;

console.log(userName);
console.log(userAge);
```

Output:

```text
Sandip
22
```

---

# 23. Nested Object With Default Value

```javascript
const user = {
  name: "Sandip"
};

const {
  address = {
    city: "Unknown"
  }
} = user;

console.log(address.city);
```

Output:

```text
Unknown
```

This provides a default object when `address` is `undefined`.

---

# 24. Destructuring Arrays Inside Objects

Objects can contain arrays.

```javascript
const user = {
  name: "Sandip",
  skills: ["JavaScript", "React", "Node.js"]
};

const {
  name,
  skills
} = user;

console.log(name);
console.log(skills);
```

You can also destructure the array:

```javascript
const {
  skills: [firstSkill, secondSkill]
} = user;

console.log(firstSkill);
console.log(secondSkill);
```

Output:

```text
JavaScript
React
```

---

# 25. Hotel Management Example

Consider a hotel table:

```javascript
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "occupied",
  location: "indoor"
};
```

Destructure it:

```javascript
const {
  tableNumber,
  capacity,
  status
} = table;

console.log(tableNumber);
console.log(capacity);
console.log(status);
```

Output:

```text
T-03
6
occupied
```

---

# 26. Food Example

```javascript
const food = {
  name: "Chicken Momo",
  price: 180,
  isVeg: false,
  isAvailable: true
};

const {
  name,
  price,
  isVeg
} = food;

console.log(name);
console.log(price);
console.log(isVeg);
```

Output:

```text
Chicken Momo
180
false
```

---

# 27. Order Example

```javascript
const order = {
  orderNumber: "ORD-001",
  status: "pending",
  totalAmount: 850
};

const {
  orderNumber,
  status,
  totalAmount
} = order;

console.log(orderNumber);
console.log(status);
console.log(totalAmount);
```

Output:

```text
ORD-001
pending
850
```

---

# 28. Destructuring `this` Properties

Inside a method, you can also destructure properties from `this`.

```javascript
const user = {
  name: "Sandip",
  age: 22,

  introduce() {
    const {
      name,
      age
    } = this;

    console.log(`I am ${name} and I am ${age} years old.`);
  }
};

user.introduce();
```

Output:

```text
I am Sandip and I am 22 years old.
```

---

# 29. Destructuring and Property Names

The variable name normally matches the property name.

```javascript
const user = {
  name: "Sandip"
};

const {
  name
} = user;
```

But you can rename it:

```javascript
const {
  name: fullName
} = user;
```

Now:

```javascript
console.log(fullName);
```

Output:

```text
Sandip
```

There is no variable called `name` in this example.

---

# 30. Common Mistakes

## Mistake 1: Using a variable that was not created

```javascript
const user = {
  name: "Sandip"
};

const {
  name: fullName
} = user;

console.log(name);
```

This is incorrect because the variable created is:

```javascript
fullName
```

Use:

```javascript
console.log(fullName);
```

---

## Mistake 2: Destructuring a missing nested object

This can cause an error:

```javascript
const user = {};

const {
  address: {
    city
  }
} = user;
```

Because `address` is `undefined`.

A default can help:

```javascript
const {
  address: {
    city
  } = {}
} = user;
```

Now `city` becomes `undefined`.

---

## Mistake 3: Forgetting parentheses with existing variables

This can be interpreted as a block:

```javascript
{ name, age } = user;
```

Use:

```javascript
({ name, age } = user);
```

---

## Mistake 4: Putting rest before other properties

Incorrect:

```javascript
const {
  ...details,
  name
} = user;
```

Correct:

```javascript
const {
  name,
  ...details
} = user;
```

---

# 31. Destructuring vs Normal Access

### Normal access

```javascript
const user = {
  name: "Sandip",
  age: 22
};

console.log(user.name);
console.log(user.age);
```

### Destructuring

```javascript
const {
  name,
  age
} = user;

console.log(name);
console.log(age);
```

Destructuring is especially useful when you need multiple properties from the same object.

---

# 32. Object Destructuring Cheat Sheet

| Feature                | Example                                   |
| ---------------------- | ----------------------------------------- |
| Basic                  | `const { name } = user`                   |
| Multiple               | `const { name, age } = user`              |
| Rename                 | `const { name: fullName } = user`         |
| Default                | `const { age = 22 } = user`               |
| Nested                 | `const { address: { city } } = user`      |
| Rest                   | `const { name, ...details } = user`       |
| Function parameter     | `function greet({ name }) {}`             |
| Existing variables     | `({ name, age } = user)`                  |
| Array inside object    | `const { skills } = user`                 |
| Dynamic/default nested | `const { address: { city } = {} } = user` |

---

# 33. Why Object Destructuring Is Useful

Object destructuring is commonly used in:

* React props
* API responses
* Function parameters
* Configuration objects
* Node.js applications
* Express request data
* MongoDB results
* State management
* JavaScript modules

Example:

```javascript
function createUser({ name, email, role = "user" }) {
  return {
    name,
    email,
    role
  };
}

const user = createUser({
  name: "Sandip",
  email: "sandip@example.com"
});

console.log(user);
```

Result:

```javascript
{
  name: "Sandip",
  email: "sandip@example.com",
  role: "user"
}
```

---

# 34. Key Takeaways

* Object destructuring extracts properties into variables.
* It uses `{}`.
* Property names normally determine which values are extracted.
* Object property order does not matter.
* You can rename extracted variables.
* You can provide default values.
* Default values apply when the value is `undefined`.
* You can destructure nested objects.
* You can use destructuring directly in function parameters.
* The rest property `...` collects remaining properties.
* The rest property must be last.
* Object destructuring is very common in React and Node.js.
* Destructuring makes code shorter and easier to read.

---

## Quick Example

```javascript
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj",
  role: "admin"
};

const {
  name,
  age,
  city,
  role
} = user;

console.log(name);
console.log(age);
console.log(city);
console.log(role);
```

Output:

```text
Sandip
22
Birgunj
admin
```

With renaming and rest:

```javascript
const {
  name: fullName,
  ...details
} = user;

console.log(fullName);
console.log(details);
```

Output:

```text
Sandip

{
  age: 22,
  city: "Birgunj",
  role: "admin"
}
```

---
