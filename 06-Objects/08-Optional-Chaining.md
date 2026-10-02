# JavaScript Optional Chaining

**Optional chaining** allows you to safely access properties or call functions when a value might be `null` or `undefined`.

It uses the operator:

```javascript
?.
```

Without optional chaining, accessing a property from `null` or `undefined` can cause a runtime error.

---

# 1. The Problem

Suppose we have:

```javascript
const user = {
  name: "Sandip"
};

console.log(user.address.city);
```

This causes an error because:

```javascript
user.address
```

is `undefined`.

Trying to access:

```javascript
undefined.city
```

causes a `TypeError`.

---

# 2. Using Optional Chaining

We can write:

```javascript
console.log(user.address?.city);
```

Output:

```text
undefined
```

Instead of throwing an error, optional chaining stops the property access and returns `undefined`.

---

# 3. Basic Syntax

```javascript
object?.property
```

Example:

```javascript
const user = {
  name: "Sandip",
  age: 22
};

console.log(user?.name);
```

Output:

```text
Sandip
```

---

# 4. Optional Chaining With Nested Objects

Consider:

```javascript
const user = {
  name: "Sandip",
  address: {
    city: "Birgunj"
  }
};
```

You can access:

```javascript
console.log(user?.address?.city);
```

Output:

```text
Birgunj
```

Each `?.` safely checks the value before continuing.

---

# 5. Missing Property

```javascript
const user = {
  name: "Sandip"
};

console.log(user?.address?.city);
```

Output:

```text
undefined
```

No error occurs.

---

# 6. `?.` With `null`

```javascript
const user = null;

console.log(user?.name);
```

Output:

```text
undefined
```

Without optional chaining:

```javascript
console.log(user.name);
```

This causes an error because `user` is `null`.

---

# 7. `?.` With `undefined`

```javascript
let user;

console.log(user?.name);
```

Output:

```text
undefined
```

The same applies to `undefined`.

---

# 8. Optional Chaining Only Stops on `null` or `undefined`

Optional chaining does not treat every falsy value as missing.

For example:

```javascript
const user = {
  age: 0,
  name: ""
};

console.log(user?.age);
console.log(user?.name);
```

Output:

```text
0

```

The values are preserved.

This is different from using `&&`.

---

# 9. Optional Chaining vs `&&`

Before optional chaining, developers often wrote:

```javascript
const city = user && user.address && user.address.city;
```

With optional chaining:

```javascript
const city = user?.address?.city;
```

The second version is shorter and easier to read.

---

# 10. Example With API Data

API responses can have optional or missing properties.

For example:

```javascript
const response = {
  user: {
    name: "Sandip"
  }
};
```

Instead of:

```javascript
const city =
  response &&
  response.user &&
  response.user.address &&
  response.user.address.city;
```

you can write:

```javascript
const city = response?.user?.address?.city;
```

Result:

```text
undefined
```

---

# 11. Hotel Management Example

Suppose an order contains:

```javascript
const order = {
  customer: {
    name: "Sandip"
  }
};
```

You can safely access:

```javascript
console.log(order?.customer?.name);
```

Output:

```text
Sandip
```

For a missing phone:

```javascript
console.log(order?.customer?.phone);
```

Output:

```text
undefined
```

---

# 12. Nested Hotel Data

Suppose:

```javascript
const order = {
  table: {
    location: {
      area: "rooftop"
    }
  }
};
```

You can use:

```javascript
const area = order?.table?.location?.area;

console.log(area);
```

Output:

```text
rooftop
```

---

# 13. Missing Nested Data

Suppose:

```javascript
const order = {
  table: {
    number: "T-03"
  }
};
```

Now:

```javascript
const area = order?.table?.location?.area;

console.log(area);
```

Output:

```text
undefined
```

No error occurs.

---

# 14. Optional Chaining With Arrays

You can safely access an array element.

```javascript
const users = [
  {
    name: "Sandip"
  }
];

console.log(users?.[0]?.name);
```

Output:

```text
Sandip
```

---

# 15. Missing Array Element

```javascript
const users = [];

console.log(users?.[0]?.name);
```

Output:

```text
undefined
```

Without optional chaining:

```javascript
console.log(users[0].name);
```

This causes an error because `users[0]` is `undefined`.

---

# 16. Optional Chaining With Dynamic Index

You can use a variable as the array index.

```javascript
const users = [
  {
    name: "Sandip"
  },
  {
    name: "Ram"
  }
];

const index = 1;

console.log(users?.[index]?.name);
```

Output:

```text
Ram
```

---

# 17. Optional Chaining With Objects and Dynamic Properties

You can also use brackets:

```javascript
const user = {
  name: "Sandip"
};

const property = "name";

console.log(user?.[property]);
```

Output:

```text
Sandip
```

---

# 18. Optional Function Call

Optional chaining can also safely call a function that may not exist.

Syntax:

```javascript
object.method?.();
```

Example:

```javascript
const user = {
  name: "Sandip"
};

user.login?.();
```

If `login` does not exist, JavaScript returns:

```text
undefined
```

instead of throwing an error.

---

# 19. Function Exists

```javascript
const user = {
  name: "Sandip",
  greet() {
    console.log("Hello!");
  }
};

user.greet?.();
```

Output:

```text
Hello!
```

---

# 20. Function Does Not Exist

```javascript
const user = {
  name: "Sandip"
};

user.greet?.();
```

No error occurs.

The result is:

```text
undefined
```

---

# 21. Calling an Optional Callback

This is useful when working with functions.

Suppose:

```javascript
function processUser(user, callback) {
  console.log(user);

  callback?.();
}
```

Now you can call:

```javascript
processUser(
  "Sandip",
  () => {
    console.log("Completed");
  }
);
```

Output:

```text
Sandip
Completed
```

You can also call:

```javascript
processUser("Sandip");
```

The missing callback does not cause an error.

---

# 22. Optional Chaining With Methods

You can safely access a method:

```javascript
const user = {
  name: "Sandip"
};

const result = user.getName?.();

console.log(result);
```

Since `getName` does not exist, the result is:

```text
undefined
```

---

# 23. Optional Chaining With Arrays of Objects

Suppose:

```javascript
const orders = [
  {
    customer: {
      name: "Sandip"
    }
  }
];
```

Access:

```javascript
console.log(
  orders?.[0]?.customer?.name
);
```

Output:

```text
Sandip
```

If the array is empty:

```javascript
const orders = [];

console.log(
  orders?.[0]?.customer?.name
);
```

Output:

```text
undefined
```

---

# 24. Combining `?.` With `??`

Optional chaining works very well with the **nullish coalescing operator**.

For example:

```javascript
const user = {};

const city =
  user?.address?.city ?? "Unknown";

console.log(city);
```

Output:

```text
Unknown
```

Here:

```javascript
user?.address?.city
```

returns `undefined`.

Then:

```javascript
?? "Unknown"
```

provides a fallback value.

---

# 25. API Example With Default Value

```javascript
const response = {
  user: {
    name: "Sandip"
  }
};

const city =
  response?.user?.address?.city ?? "Not provided";

console.log(city);
```

Output:

```text
Not provided
```

---

# 26. Optional Chaining in React

Optional chaining is very common in React applications.

Suppose API data is loaded asynchronously:

```javascript
const user = data?.user;
```

You can safely access:

```javascript
const name = data?.user?.name;
```

Instead of:

```javascript
const name = data.user.name;
```

When `data` has not loaded yet, the first version does not throw an error.

---

# 27. React Example

```jsx
function UserProfile({ user }) {
  return (
    <div>
      <h2>{user?.name}</h2>
      <p>{user?.address?.city}</p>
    </div>
  );
}
```

If `address` is missing, React can render:

```text
undefined
```

instead of JavaScript throwing an error while accessing the nested property.

In a real UI, you can combine it with a fallback:

```jsx
<p>{user?.address?.city ?? "City not available"}</p>
```

---

# 28. API Response Example

Imagine an API returns:

```javascript
const data = {
  user: {
    name: "Sandip",
    profile: {
      username: "sandip"
    }
  }
};
```

You can write:

```javascript
const username =
  data?.user?.profile?.username;

console.log(username);
```

Output:

```text
sandip
```

---

# 29. When API Data Is Missing

```javascript
const data = {
  user: {
    name: "Sandip"
  }
};

const username =
  data?.user?.profile?.username;

console.log(username);
```

Output:

```text
undefined
```

Then:

```javascript
const username =
  data?.user?.profile?.username ?? "Guest";
```

Output:

```text
Guest
```

---

# 30. Optional Chaining Does Not Hide All Errors

Optional chaining only protects the part of the expression where it is used.

For example:

```javascript
const user = null;

console.log(user?.address.city);
```

This is not equivalent to:

```javascript
console.log(user?.address?.city);
```

Use `?.` at each potentially nullish level:

```javascript
user?.address?.city
```

---

# 31. Important Difference

Consider:

```javascript
user?.address.city
```

If `user` exists but `address` is `undefined`, the `.city` access can still fail.

Safer:

```javascript
user?.address?.city
```

So when multiple levels may be missing, use optional chaining where needed.

---

# 32. Optional Chaining Does Not Work Everywhere

You cannot use optional chaining on the left side of an assignment.

This is invalid:

```javascript
user?.name = "Sandip";
```

JavaScript does not allow optional chaining as an assignment target.

Instead, check the object first:

```javascript
if (user) {
  user.name = "Sandip";
}
```

---

# 33. Optional Chaining and `delete`

Optional chaining can be used with `delete`.

```javascript
const user = {
  name: "Sandip"
};

delete user?.name;

console.log(user);
```

Result:

```javascript
{}
```

---

# 34. Optional Chaining With `typeof`

Optional chaining can also be useful when checking a nested property:

```javascript
const user = {};

console.log(
  typeof user?.address?.city
);
```

Output:

```text
undefined
```

---

# 35. Optional Chaining With `null`

```javascript
const user = null;

const name = user?.name;

console.log(name);
```

Output:

```text
undefined
```

---

# 36. Optional Chaining With `undefined`

```javascript
let user;

const name = user?.name;

console.log(name);
```

Output:

```text
undefined
```

---

# 37. Optional Chaining Does Not Mean "Check Truthiness"

This is important.

Consider:

```javascript
const user = {
  age: 0,
  active: false,
  name: ""
};
```

Optional chaining preserves these values:

```javascript
console.log(user?.age);
console.log(user?.active);
console.log(user?.name);
```

Output:

```text
0
false

```

It only stops when the value before `?.` is:

```text
null
```

or:

```text
undefined
```

---

# 38. `?.` With `??`

A very common pattern is:

```javascript
const value = object?.property ?? defaultValue;
```

Example:

```javascript
const user = {};

const name = user?.name ?? "Guest";

console.log(name);
```

Output:

```text
Guest
```

Another example:

```javascript
const user = {
  name: ""
};

const name = user?.name ?? "Guest";

console.log(name);
```

Output:

```text
```

The empty string is preserved because `??` only falls back for `null` or `undefined`.

---

# 39. Hotel Management Example

Suppose an order response is:

```javascript
const order = {
  customer: {
    name: "Sandip"
  },
  table: {
    tableNumber: "T-03"
  }
};
```

You can safely access:

```javascript
const customerName =
  order?.customer?.name;

const tableNumber =
  order?.table?.tableNumber;

const phone =
  order?.customer?.phone ?? "Not provided";

console.log(customerName);
console.log(tableNumber);
console.log(phone);
```

Output:

```text
Sandip
T-03
Not provided
```

---

# 40. Food Example

Suppose:

```javascript
const food = {
  name: "Chicken Momo",
  category: {
    name: "Momo"
  }
};
```

Access:

```javascript
const categoryName =
  food?.category?.name;

console.log(categoryName);
```

Output:

```text
Momo
```

If category is missing:

```javascript
const food = {
  name: "Chicken Momo"
};

const categoryName =
  food?.category?.name ?? "Uncategorized";
```

Result:

```text
Uncategorized
```

---

# 41. Common API Pattern

A common pattern in frontend applications is:

```javascript
const userName =
  response?.data?.user?.fullName ?? "Guest";
```

This protects against missing:

```text
response
data
user
fullName
```

and provides:

```text
Guest
```

when the final value is `null` or `undefined`.

---

# 42. Optional Chaining vs Traditional Checks

### Traditional

```javascript
let city;

if (
  user &&
  user.address &&
  user.address.city
) {
  city = user.address.city;
}
```

### Optional chaining

```javascript
const city = user?.address?.city;
```

The second version is much shorter.

If you also need a default:

```javascript
const city =
  user?.address?.city ?? "Unknown";
```

---

# 43. Common Mistakes

## Mistake 1: Using only one `?`

```javascript
user?.address.city
```

If `address` itself can be missing, use:

```javascript
user?.address?.city
```

---

## Mistake 2: Confusing `?.` with `??`

Optional chaining:

```javascript
user?.name
```

safely accesses a property.

Nullish coalescing:

```javascript
user?.name ?? "Guest"
```

provides a fallback for `null` or `undefined`.

They often work together.

---

## Mistake 3: Thinking `?.` handles all falsy values

It does not.

These are valid values:

```javascript
0
false
""
```

Optional chaining does not replace them with `undefined`.

---

## Mistake 4: Using it everywhere

Optional chaining is useful when a value can genuinely be missing.

Do not use it blindly when a property is required and its absence should indicate a programming error.

---

# 44. Cheat Sheet

### Basic property

```javascript
user?.name
```

### Nested property

```javascript
user?.address?.city
```

### Array element

```javascript
users?.[0]
```

### Dynamic index

```javascript
users?.[index]
```

### Dynamic property

```javascript
user?.[property]
```

### Optional function call

```javascript
user.login?.()
```

### With fallback

```javascript
user?.name ?? "Guest"
```

### API response

```javascript
response?.data?.user?.name
```

---

# 45. Key Takeaways

* Optional chaining uses `?.`.
* It safely accesses properties that may not exist.
* It prevents errors caused by accessing properties on `null` or `undefined`.
* It returns `undefined` when the optional chain short-circuits.
* It works with nested objects.
* It works with arrays.
* It works with dynamic properties.
* It can safely call optional functions using `?.()`.
* It works very well with `??`.
* `?.` checks for `null` or `undefined`, not all falsy values.
* Use `?.` at each potentially missing level.
* Optional chaining cannot be used as an assignment target.
* It is commonly used with API responses and React applications.

---

## Simple Rule to Remember

```text
?.  → safely access

??  → provide fallback
```

Example:

```javascript
const city =
  user?.address?.city ?? "Unknown";
```

Meaning:

```text
Safely get city.
If city is null or undefined,
use "Unknown".
```

---
