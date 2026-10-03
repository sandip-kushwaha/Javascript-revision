# JavaScript Destructuring

**Destructuring** is a modern JavaScript feature that allows you to extract values from:

* Arrays
* Objects

and store them in variables.

Instead of writing:

```javascript id="7qz5xy"
const user = {
  name: "Sandip",
  age: 22
};

const name = user.name;
const age = user.age;
```

You can use destructuring:

```javascript id="j4m7az"
const {
  name,
  age
} = user;
```

Now:

```javascript id="r1p5x4"
console.log(name);
console.log(age);
```

Output:

```text id="lq3j4m"
Sandip
22
```

---

# 1. Why Use Destructuring?

Destructuring makes code:

* Shorter
* Cleaner
* Easier to read
* Useful for API responses
* Useful in React
* Useful with function parameters
* Useful with arrays and objects

---

# 2. Array Destructuring

Array destructuring extracts values based on their **position**.

```javascript id="l9gqj7"
const numbers = [10, 20, 30];

const [a, b, c] = numbers;

console.log(a);
console.log(b);
console.log(c);
```

Output:

```text id="h5p8cs"
10
20
30
```

---

# 3. Array Position Matters

Consider:

```javascript id="q5c1x8"
const fruits = [
  "Apple",
  "Mango",
  "Banana"
];

const [first, second, third] = fruits;
```

The result is:

```text id="6yqz2v"
first  → Apple
second → Mango
third  → Banana
```

Array destructuring is **position-based**.

---

# 4. Object Destructuring

Object destructuring extracts values using property names.

```javascript id="e8k1w3"
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const {
  name,
  age,
  city
} = user;

console.log(name);
console.log(age);
console.log(city);
```

Output:

```text id="w7bq1p"
Sandip
22
Birgunj
```

---

# 5. Object Property Order Does Not Matter

For objects, property names are what matter.

```javascript id="r7q2zm"
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

```text id="0d8v2f"
Sandip
22
```

The order of the variables does not matter.

---

# 6. Array Destructuring vs Object Destructuring

### Array

Position matters:

```javascript id="y8i2ru"
const [first, second] = ["A", "B"];
```

```text id="s7g0xj"
first  → A
second → B
```

### Object

Property name matters:

```javascript id="z4c6vn"
const { name, age } = user;
```

```text id="x2h7bm"
name → user.name
age  → user.age
```

---

# 7. Destructuring With `let`

```javascript id="y4qj1n"
let user = {
  name: "Sandip",
  age: 22
};

let {
  name,
  age
} = user;

console.log(name);
console.log(age);
```

---

# 8. Destructuring With `const`

Most destructuring declarations use `const` when the extracted variables do not need reassignment.

```javascript id="w6j9sd"
const user = {
  name: "Sandip",
  age: 22
};

const {
  name,
  age
} = user;
```

---

# 9. Skipping Array Values

You can skip values using commas.

```javascript id="8k5z4m"
const numbers = [
  10,
  20,
  30
];

const [
  first,
  ,
  third
] = numbers;

console.log(first);
console.log(third);
```

Output:

```text id="o6u8cd"
10
30
```

The second value is skipped.

---

# 10. Skipping Multiple Values

```javascript id="m4x1so"
const numbers = [
  10,
  20,
  30,
  40
];

const [
  first,
  ,
  ,
  fourth
] = numbers;

console.log(first);
console.log(fourth);
```

Output:

```text id="3k4r7w"
10
40
```

---

# 11. Array Destructuring With Fewer Variables

You do not need to extract every value.

```javascript id="2y1qwa"
const numbers = [
  10,
  20,
  30
];

const [first, second] = numbers;

console.log(first);
console.log(second);
```

Output:

```text id="z1x5dn"
10
20
```

The third value is ignored.

---

# 12. Missing Array Values

If there is no value at a position, the variable becomes `undefined`.

```javascript id="r3v7kd"
const numbers = [10];

const [first, second] = numbers;

console.log(first);
console.log(second);
```

Output:

```text id="w2x6ya"
10
undefined
```

---

# 13. Default Values in Array Destructuring

You can provide a default value.

```javascript id="j0q3rx"
const numbers = [10];

const [
  first,
  second = 20
] = numbers;

console.log(first);
console.log(second);
```

Output:

```text id="h9c2xm"
10
20
```

The default is used because the second value is `undefined`.

---

# 14. Default Value Is Used Only for `undefined`

Consider:

```javascript id="v3m8ca"
const numbers = [null];

const [value = 10] = numbers;

console.log(value);
```

Output:

```text id="5q2n7v"
null
```

The default does not replace `null`.

It only applies when the value is `undefined`.

---

# 15. Rest With Array Destructuring

You can collect remaining values using `...`.

```javascript id="z7f5hm"
const numbers = [
  10,
  20,
  30,
  40
];

const [
  first,
  ...remaining
] = numbers;

console.log(first);
console.log(remaining);
```

Output:

```text id="n6v1qx"
10
[20, 30, 40]
```

---

# 16. Rest Must Be Last

This is valid:

```javascript id="z2n5yc"
const [first, ...remaining] = numbers;
```

This is invalid:

```javascript id="m7v3pq"
const [...remaining, last] = numbers;
```

The rest element must be the last element in an array destructuring pattern.

---

# 17. Object Destructuring With Default Values

```javascript id="t8x4ma"
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

```text id="e1k7wc"
Sandip
22
```

---

# 18. Object Destructuring With Missing Property

```javascript id="x4p2rz"
const user = {
  name: "Sandip"
};

const {
  age
} = user;

console.log(age);
```

Output:

```text id="x9c5mv"
undefined
```

---

# 19. Renaming Object Properties

Sometimes you want a different variable name.

Suppose:

```javascript id="1h3nqf"
const user = {
  name: "Sandip",
  age: 22
};
```

You can write:

```javascript id="6z8y4d"
const {
  name: fullName,
  age: userAge
} = user;

console.log(fullName);
console.log(userAge);
```

Output:

```text id="q0r3sv"
Sandip
22
```

The syntax is:

```javascript id="r5q8cy"
propertyName: variableName
```

---

# 20. Renaming Is Not Assignment

This:

```javascript id="x7b1pa"
const {
  name: fullName
} = user;
```

means:

```text id="8w2m6k"
user.name → fullName
```

It does not create or modify a property called `fullName` in the original object.

---

# 21. Object Rest

You can collect the remaining object properties using `...`.

```javascript id="4q9m7a"
const user = {
  name: "Sandip",
  age: 22,
  city: "Birgunj"
};

const {
  name,
  ...otherDetails
} = user;

console.log(name);
console.log(otherDetails);
```

Output:

```text id="p1v6kx"
Sandip
{
  age: 22,
  city: "Birgunj"
}
```

---

# 22. Object Rest Must Be Last

Valid:

```javascript id="r2w8mc"
const {
  name,
  ...details
} = user;
```

Invalid:

```javascript id="k7y4np"
const {
  ...details,
  name
} = user;
```

The rest property must be last.

---

# 23. Nested Object Destructuring

Suppose:

```javascript id="9x1m4c"
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj",
    country: "Nepal"
  }
};
```

You can destructure nested properties:

```javascript id="v6t2pq"
const {
  name,
  address: {
    city,
    country
  }
} = user;

console.log(name);
console.log(city);
console.log(country);
```

Output:

```text id="b8y5ks"
Sandip
Birgunj
Nepal
```

---

# 24. Nested Object With Rename

```javascript id="f4r6xj"
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

```text id="j9p3wx"
Birgunj
```

---

# 25. Nested Object With Default Value

```javascript id="k5d2vb"
const user = {
  name: "Sandip"
};

const {
  address: {
    city = "Unknown"
  } = {}
} = user;

console.log(city);
```

Output:

```text id="7n4xqz"
Unknown
```

The `= {}` protects the destructuring when `address` itself is missing.

---

# 26. Nested Array Destructuring

```javascript id="p3k8yz"
const data = [
  "Sandip",
  [22, "Birgunj"]
];

const [
  name,
  [age, city]
] = data;

console.log(name);
console.log(age);
console.log(city);
```

Output:

```text id="q2v7mx"
Sandip
22
Birgunj
```

---

# 27. Destructuring Function Parameters

Destructuring can be used directly in function parameters.

```javascript id="w6p2rm"
function displayUser({ name, age }) {
  console.log(name);
  console.log(age);
}

const user = {
  name: "Sandip",
  age: 22
};

displayUser(user);
```

Output:

```text id="a9k4tz"
Sandip
22
```

---

# 28. Array Destructuring in Function Parameters

```javascript id="c8n3vy"
function displayNumbers([a, b, c]) {
  console.log(a);
  console.log(b);
  console.log(c);
}

displayNumbers([10, 20, 30]);
```

Output:

```text id="m7q2xk"
10
20
30
```

---

# 29. Function Parameter Default

You can provide a default object:

```javascript id="q4w7ns"
function displayUser({
  name = "Guest"
} = {}) {
  console.log(name);
}

displayUser();
```

Output:

```text id="d1x8rp"
Guest
```

The `= {}` handles the case where no argument is provided.

---

# 30. API Response Example

Suppose an API returns:

```javascript id="j8p2vf"
const response = {
  data: {
    user: {
      name: "Sandip",
      email: "sandip@example.com"
    }
  }
};
```

You can write:

```javascript id="n5w3kc"
const {
  data: {
    user: {
      name,
      email
    }
  }
} = response;

console.log(name);
console.log(email);
```

This can make deeply nested API data easier to work with.

---

# 31. Hotel Management Example

Suppose an order is:

```javascript id="x2v6qk"
const order = {
  orderNumber: "ORD-001",
  status: "preparing",
  totalAmount: 850
};
```

Instead of:

```javascript id="p4k7sm"
console.log(order.orderNumber);
console.log(order.status);
console.log(order.totalAmount);
```

Use:

```javascript id="g3n8wp"
const {
  orderNumber,
  status,
  totalAmount
} = order;

console.log(orderNumber);
console.log(status);
console.log(totalAmount);
```

---

# 32. Hotel Table Example

```javascript id="f8m3xq"
const table = {
  tableNumber: "T-03",
  capacity: 6,
  status: "occupied"
};

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

```text id="k5z7nb"
T-03
6
occupied
```

---

# 33. Food Example

```javascript id="r6q1mv"
const food = {
  name: "Chicken Momo",
  price: 180,
  isVeg: false
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

```text id="n2w9cx"
Chicken Momo
180
false
```

---

# 34. React Props Example

Destructuring is commonly used with React props.

Instead of:

```jsx id="x7q4nc"
function UserCard(props) {
  return (
    <h2>{props.name}</h2>
  );
}
```

You can write:

```jsx id="c5m8vp"
function UserCard({ name }) {
  return (
    <h2>{name}</h2>
  );
}
```

This directly extracts `name` from the props object.

---

# 35. React Multiple Props

```jsx id="n4r6wy"
function UserCard({
  name,
  age,
  city
}) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
      <p>{city}</p>
    </div>
  );
}
```

Usage:

```jsx id="b8t2qm"
<UserCard
  name="Sandip"
  age={22}
  city="Birgunj"
/>
```

---

# 36. React `useState()` Example

A common example is:

```javascript id="f5k7zc"
const [count, setCount] = useState(0);
```

This uses **array destructuring**.

`useState()` returns an array similar to:

```javascript id="p9m2xv"
[
  currentValue,
  updateFunction
]
```

So:

```javascript id="r3w6kn"
const [count, setCount] = useState(0);
```

extracts the two values by position.

---

# 37. React `useContext()` Example

Suppose:

```javascript id="q7v4mc"
const {
  user,
  logout
} = useAuth();
```

If `useAuth()` returns:

```javascript id="y2n8rp"
{
  user: {...},
  logout: function
}
```

object destructuring extracts the properties.

---

# 38. Swapping Variables

Array destructuring makes swapping values simple.

```javascript id="m6p3xz"
let a = 10;
let b = 20;

[a, b] = [b, a];

console.log(a);
console.log(b);
```

Output:

```text id="z4q8vn"
20
10
```

No temporary variable is required.

---

# 39. Destructuring Strings

Strings are iterable, so they can be destructured.

```javascript id="w8k2mc"
const [first, second, third] = "JavaScript";

console.log(first);
console.log(second);
console.log(third);
```

Output:

```text id="c6r4xp"
J
a
v
```

---

# 40. Destructuring a Function Return Value

Suppose:

```javascript id="y5n7qb"
function getUser() {
  return [
    "Sandip",
    22
  ];
}

const [name, age] = getUser();

console.log(name);
console.log(age);
```

Output:

```text id="k3x9mv"
Sandip
22
```

---

# 41. Destructuring an Object Returned by a Function

```javascript id="v4p8nc"
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

---

# 42. Destructuring With `Object.entries()`

Suppose:

```javascript id="q6w3xm"
const user = {
  name: "Sandip",
  age: 22
};
```

Using `Object.entries()`:

```javascript id="c2m7vp"
for (const [key, value] of Object.entries(user)) {
  console.log(key, value);
}
```

Output:

```text id="j9r5xb"
name Sandip
age 22
```

The `[key, value]` part is array destructuring.

---

# 43. Destructuring With `map()`

```javascript id="t5x8qm"
const users = [
  {
    name: "Sandip",
    age: 22
  },
  {
    name: "Ram",
    age: 23
  }
];

const names = users.map(
  ({ name }) => name
);

console.log(names);
```

Output:

```text id="w3n6kc"
["Sandip", "Ram"]
```

This extracts `name` directly from each object.

---

# 44. Destructuring With `filter()`

```javascript id="p7m4vx"
const users = [
  {
    name: "Sandip",
    active: true
  },
  {
    name: "Ram",
    active: false
  }
];

const activeUsers = users.filter(
  ({ active }) => active
);

console.log(activeUsers);
```

The callback destructures each object.

---

# 45. Destructuring With `forEach()`

```javascript id="n8q2cw"
const users = [
  {
    name: "Sandip",
    age: 22
  },
  {
    name: "Ram",
    age: 23
  }
];

users.forEach(
  ({ name, age }) => {
    console.log(name, age);
  }
);
```

Output:

```text id="x4m7pz"
Sandip 22
Ram 23
```

---

# 46. Destructuring With Default Values

Object:

```javascript id="a3v6qn"
const user = {
  name: "Sandip"
};

const {
  name,
  role = "user"
} = user;

console.log(name);
console.log(role);
```

Output:

```text id="f9x2mc"
Sandip
user
```

---

# 47. Destructuring and `null`

Be careful when destructuring `null`.

This causes an error:

```javascript id="w5k8zp"
const user = null;

const {
  name
} = user;
```

You cannot destructure properties directly from `null`.

If the value may be missing, handle that case first or provide a suitable fallback.

For example:

```javascript id="m2q7xc"
const user = null;

const {
  name
} = user ?? {};
```

Now `name` becomes:

```text id="j6v3kn"
undefined
```

---

# 48. Destructuring and `undefined`

Similarly:

```javascript id="r8m4vq"
const user = undefined;

const {
  name
} = user ?? {};
```

This safely uses an empty object.

---

# 49. Common Mistakes

## Mistake 1: Confusing array and object destructuring

Array:

```javascript id="h2p7mx"
const [name, age] = user;
```

This expects an iterable.

Object:

```javascript id="v5q9kc"
const { name, age } = user;
```

This accesses object properties.

---

## Mistake 2: Forgetting array position

```javascript id="x3m6pv"
const [first, second] = [
  "Apple",
  "Mango"
];
```

`first` is `"Apple"` because it is the first position.

---

## Mistake 3: Using the wrong property name

```javascript id="n7w4cz"
const user = {
  name: "Sandip"
};

const { username } = user;

console.log(username);
```

Output:

```text id="q6p8xm"
undefined
```

There is no `username` property.

---

## Mistake 4: Forgetting rename syntax

Correct:

```javascript id="j4r8vn"
const {
  name: fullName
} = user;
```

This means:

```text id="b7m2xc"
user.name → fullName
```

---

## Mistake 5: Putting rest before another property

Invalid:

```javascript id="c5q9mw"
const {
  ...details,
  name
} = user;
```

Rest must be last.

---

# 50. Destructuring Cheat Sheet

### Array

```javascript id="p2v6xm"
const [a, b] = array;
```

### Object

```javascript id="k8q4zn"
const { name, age } = user;
```

### Skip array value

```javascript id="y3m7vp"
const [first, , third] = array;
```

### Array default

```javascript id="n5x2qc"
const [name = "Guest"] = array;
```

### Object default

```javascript id="w7r4mk"
const { name = "Guest" } = user;
```

### Rename property

```javascript id="f9p3xz"
const { name: fullName } = user;
```

### Object rest

```javascript id="c6v8qn"
const { name, ...details } = user;
```

### Array rest

```javascript id="j2m5wp"
const [first, ...remaining] = array;
```

### Nested object

```javascript id="r8x4kc"
const {
  address: { city }
} = user;
```

### Function parameter

```javascript id="v6q9mn"
function display({ name, age }) {
  console.log(name, age);
}
```

---

# 51. Key Takeaways

* Destructuring extracts values into variables.
* Array destructuring is position-based.
* Object destructuring is property-name-based.
* Arrays can skip values using commas.
* Default values can be provided.
* Defaults are used when the value is `undefined`.
* Object properties can be renamed.
* Rest syntax can collect remaining values.
* Rest must be last.
* Nested objects and arrays can be destructured.
* Functions can use destructuring in parameters.
* React commonly uses destructuring for props and hook results.
* API responses can become easier to work with using destructuring.
* Destructuring does not modify the original object or array.

---

## Simple Rule

```text
Array  → position matters

Object → property name matters
```

Example:

```javascript id="k4n8vz"
const numbers = [10, 20];

const [a, b] = numbers;
```

```javascript id="q7m2xc"
const user = {
  name: "Sandip",
  age: 22
};

const { name, age } = user;
```

---
