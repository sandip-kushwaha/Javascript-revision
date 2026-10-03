# JavaScript Constructor Functions

A **constructor function** is a regular JavaScript function designed to create multiple objects with the same structure.

Before ES6 classes were introduced, constructor functions were one of the main ways to implement object-oriented patterns in JavaScript.

They are still useful for understanding:

* `this`
* `new`
* Prototypes
* Object creation
* JavaScript classes

---

# 1. Why Constructor Functions?

Suppose we need several user objects.

Without a constructor:

```javascript
const user1 = {
  name: "Sandip",
  role: "Admin"
};

const user2 = {
  name: "Ram",
  role: "Waiter"
};

const user3 = {
  name: "Hari",
  role: "Kitchen"
};
```

This works, but repeating the structure becomes inconvenient.

A constructor function provides a reusable object-creation pattern.

---

# 2. Basic Constructor Function

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}
```

Now create objects using:

```javascript
const user1 = new User("Sandip", "Admin");
const user2 = new User("Ram", "Waiter");
```

Each call creates a new object.

---

# 3. What Does `new` Do?

When you write:

```javascript
const user = new User("Sandip", "Admin");
```

JavaScript performs several important steps.

Conceptually:

```text
1. Create a new empty object
        ↓
2. Connect the object to User.prototype
        ↓
3. Set `this` to the new object
        ↓
4. Execute the constructor function
        ↓
5. Return the new object
```

---

# 4. `this` Inside a Constructor

Consider:

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}

const user = new User("Sandip", "Admin");
```

Inside the constructor:

```javascript
this
```

refers to the newly created object.

Therefore:

```javascript
this.name = name;
```

creates:

```javascript
user.name
```

---

# 5. Accessing the Created Object

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}

const user = new User("Sandip", "Admin");

console.log(user.name);
console.log(user.role);
```

Output:

```text
Sandip
Admin
```

The constructor has created an object with those properties.

---

# 6. Creating Multiple Objects

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}

const admin = new User("Sandip", "Admin");
const waiter = new User("Ram", "Waiter");
const kitchen = new User("Hari", "Kitchen");

console.log(admin);
console.log(waiter);
console.log(kitchen);
```

Each object has its own property values.

---

# 7. Constructor Function Naming Convention

Constructor functions are usually written using **PascalCase**.

Example:

```javascript
function User() {}
function Product() {}
function Order() {}
function HotelTable() {}
```

Instead of:

```javascript
function user() {}
function product() {}
```

PascalCase helps developers recognize functions intended to be used with `new`.

---

# 8. Constructor With More Properties

```javascript
function Product(name, price, category) {
  this.name = name;
  this.price = price;
  this.category = category;
}

const product = new Product(
  "Laptop",
  80000,
  "Electronics"
);

console.log(product);
```

Result:

```javascript
{
  name: "Laptop",
  price: 80000,
  category: "Electronics"
}
```

---

# 9. Constructor With Default Values

You can use default parameters.

```javascript
function User(name, role = "Customer") {
  this.name = name;
  this.role = role;
}

const user1 = new User("Sandip");
const user2 = new User("Ram", "Admin");

console.log(user1);
console.log(user2);
```

`user1` receives:

```text
role → Customer
```

while `user2` receives:

```text
role → Admin
```

---

# 10. Constructor With Methods

A constructor can also create methods.

```javascript
function User(name) {
  this.name = name;

  this.greet = function () {
    console.log(`Hello ${this.name}`);
  };
}

const user = new User("Sandip");

user.greet();
```

Output:

```text
Hello Sandip
```

However, there is an important problem with this approach.

---

# 11. Problem With Methods Inside Constructor

Consider:

```javascript
function User(name) {
  this.name = name;

  this.greet = function () {
    console.log(`Hello ${this.name}`);
  };
}

const user1 = new User("Sandip");
const user2 = new User("Ram");
```

Each object gets its own separate `greet` function.

Conceptually:

```text
user1 → greet function
user2 → another greet function
```

If many objects are created, this can unnecessarily duplicate methods.

A better solution is to put shared methods on the prototype.

---

# 12. Constructor Functions and Prototypes

Instead of:

```javascript
function User(name) {
  this.name = name;

  this.greet = function () {
    console.log(`Hello ${this.name}`);
  };
}
```

use:

```javascript
function User(name) {
  this.name = name;
}

User.prototype.greet = function () {
  console.log(`Hello ${this.name}`);
};
```

Now:

```javascript
const user1 = new User("Sandip");
const user2 = new User("Ram");

user1.greet();
user2.greet();
```

Both objects can use the same prototype method.

---

# 13. Why Use the Prototype?

The prototype allows objects to share methods.

Instead of:

```text
user1
 └── own greet()

user2
 └── own greet()
```

the structure becomes:

```text
user1 ──┐
        ├── User.prototype.greet()
user2 ──┘
```

The method is shared rather than recreated for every instance.

---

# 14. Constructor Property

Every object created using a constructor function can access the constructor through its prototype chain.

Example:

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(user.constructor === User);
```

Output:

```text
true
```

The constructor relationship comes through `User.prototype`.

---

# 15. Constructor Function With Prototype

Complete example:

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}

User.prototype.greet = function () {
  console.log(`Hello ${this.name}`);
};

const admin = new User("Sandip", "Admin");
const waiter = new User("Ram", "Waiter");

admin.greet();
waiter.greet();
```

Output:

```text
Hello Sandip
Hello Ram
```

---

# 16. Prototype Properties

You can also add properties to the prototype.

```javascript
function User(name) {
  this.name = name;
}

User.prototype.type = "User";

const user = new User("Sandip");

console.log(user.name);
console.log(user.type);
```

Output:

```text
Sandip
User
```

`name` belongs directly to the instance.

`type` is found through the prototype.

---

# 17. Own Property vs Prototype Property

```javascript
function User(name) {
  this.name = name;
}

User.prototype.role = "Customer";

const user = new User("Sandip");
```

The object has:

```javascript
user.name
```

as its own property.

But:

```javascript
user.role
```

is found through the prototype chain.

You can check this with:

```javascript
console.log(user.hasOwnProperty("name"));
console.log(user.hasOwnProperty("role"));
```

Output:

```text
true
false
```

---

# 18. Constructor Function With Methods

A practical example:

```javascript
function Order(orderId, total) {
  this.orderId = orderId;
  this.total = total;
}

Order.prototype.getSummary = function () {
  return `${this.orderId}: Rs. ${this.total}`;
};

const order = new Order("ORD-101", 1500);

console.log(order.getSummary());
```

Output:

```text
ORD-101: Rs. 1500
```

---

# 19. Hotel Management Example

```javascript
function HotelTable(tableNumber, capacity, status) {
  this.tableNumber = tableNumber;
  this.capacity = capacity;
  this.status = status;
}

HotelTable.prototype.isAvailable = function () {
  return this.status === "available";
};

const table = new HotelTable(
  3,
  4,
  "available"
);

console.log(table.tableNumber);
console.log(table.isAvailable());
```

Output:

```text
3
true
```

---

# 20. Changing Object Properties

Constructor-created objects can be modified like normal objects.

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}

const user = new User("Sandip", "Admin");

user.role = "Waiter";

console.log(user.role);
```

Output:

```text
Waiter
```

---

# 21. Adding New Properties

You can also add properties after object creation.

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

user.email = "sandip@example.com";

console.log(user);
```

The new property belongs directly to the instance.

---

# 22. Constructor Returning an Object

Normally, a constructor called with `new` returns the newly created object.

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Sandip");
```

However, if a constructor explicitly returns an object, that object can become the result.

```javascript
function User(name) {
  this.name = name;

  return {
    name: "Other User"
  };
}

const user = new User("Sandip");

console.log(user.name);
```

Output:

```text
Other User
```

This is one reason explicit object returns from constructor functions should be used carefully.

---

# 23. Constructor Returning a Primitive

If a constructor explicitly returns a primitive value:

```javascript
function User(name) {
  this.name = name;

  return 100;
}

const user = new User("Sandip");

console.log(user.name);
```

The primitive return value is ignored.

The newly created object is still returned.

---

# 24. Constructor Without `new`

Consider:

```javascript
function User(name) {
  this.name = name;
}

const user = User("Sandip");
```

This is not the intended way to use a constructor function.

Without `new`, the function behaves like an ordinary function.

In strict mode, `this` inside the function is `undefined`, so:

```javascript
this.name = name;
```

causes an error.

Always use:

```javascript
const user = new User("Sandip");
```

when using a constructor function.

---

# 25. Constructor Functions vs Normal Functions

A constructor function:

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Sandip");
```

A normal function:

```javascript
function greet(name) {
  return `Hello ${name}`;
}

const message = greet("Sandip");
```

The important difference is how they are intended to be called.

---

# 26. Checking an Instance

Use:

```javascript
instanceof
```

to check whether an object was created through a constructor's prototype chain.

Example:

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(user instanceof User);
```

Output:

```text
true
```

---

# 27. `instanceof` With Different Constructors

```javascript
function User(name) {
  this.name = name;
}

function Product(name) {
  this.name = name;
}

const user = new User("Sandip");

console.log(user instanceof User);
console.log(user instanceof Product);
```

Output:

```text
true
false
```

---

# 28. Constructor Function and Prototype Chain

When:

```javascript
const user = new User("Sandip");
```

is created, the object is connected to:

```javascript
User.prototype
```

Therefore:

```javascript
user.greet()
```

can find `greet` on:

```javascript
User.prototype
```

if the object does not have its own `greet` property.

---

# 29. Property Lookup

Suppose:

```javascript
function User(name) {
  this.name = name;
}

User.prototype.role = "Customer";

const user = new User("Sandip");
```

When JavaScript evaluates:

```javascript
user.role
```

it checks:

```text
1. user itself
      ↓
2. User.prototype
      ↓
3. Further prototype chain
      ↓
4. undefined if not found
```

This is the **prototype chain**.

---

# 30. Constructor Function Example

```javascript
function Product(name, price) {
  this.name = name;
  this.price = price;
}

Product.prototype.getPrice = function () {
  return this.price;
};

Product.prototype.getDetails = function () {
  return `${this.name}: Rs. ${this.price}`;
};

const laptop = new Product("Laptop", 80000);

console.log(laptop.getPrice());
console.log(laptop.getDetails());
```

Output:

```text
80000
Laptop: Rs. 80000
```

---

# 31. Constructor Functions and Classes

Modern JavaScript provides classes:

```javascript
class User {
  constructor(name, role) {
    this.name = name;
    this.role = role;
  }

  greet() {
    console.log(`Hello ${this.name}`);
  }
}
```

A constructor function version is:

```javascript
function User(name, role) {
  this.name = name;
  this.role = role;
}

User.prototype.greet = function () {
  console.log(`Hello ${this.name}`);
};
```

Both use JavaScript's prototype-based object model.

Classes provide cleaner syntax for this pattern.

---

# 32. Constructor Function vs Class

| Feature            | Constructor Function | Class           |
| ------------------ | -------------------- | --------------- |
| Object creation    | `new`                | `new`           |
| Uses `this`        | Yes                  | Yes             |
| Uses prototypes    | Yes                  | Yes             |
| Syntax             | Function-based       | Class-based     |
| Method definition  | `prototype.method`   | Inside class    |
| Modern readability | Older style          | Usually clearer |

---

# 33. Practical Example: Hotel Staff

```javascript
function Staff(name, role) {
  this.name = name;
  this.role = role;
}

Staff.prototype.getInfo = function () {
  return `${this.name} - ${this.role}`;
};

const admin = new Staff("Sandip", "Admin");
const waiter = new Staff("Ram", "Waiter");
const kitchen = new Staff("Hari", "Kitchen");

console.log(admin.getInfo());
console.log(waiter.getInfo());
console.log(kitchen.getInfo());
```

Output:

```text
Sandip - Admin
Ram - Waiter
Hari - Kitchen
```

All instances share the same `getInfo()` method through the prototype.

---

# 34. Practical Example: Food Item

```javascript
function Food(name, price, isVeg) {
  this.name = name;
  this.price = price;
  this.isVeg = isVeg;
}

Food.prototype.getDetails = function () {
  return `${this.name} - Rs. ${this.price}`;
};

const momo = new Food("Momo", 180, true);

console.log(momo.getDetails());
```

Output:

```text
Momo - Rs. 180
```

---

# 35. Common Mistakes

### Mistake 1: Forgetting `new`

```javascript
const user = User("Sandip");
```

Use:

```javascript
const user = new User("Sandip");
```

---

### Mistake 2: Using lowercase constructor names

Instead of:

```javascript
function user() {}
```

prefer:

```javascript
function User() {}
```

PascalCase communicates that the function is intended as a constructor.

---

### Mistake 3: Creating methods inside every instance unnecessarily

Instead of:

```javascript
function User(name) {
  this.name = name;

  this.greet = function () {
    console.log(this.name);
  };
}
```

shared methods can usually go on:

```javascript
User.prototype
```

---

### Mistake 4: Confusing constructor with prototype

The constructor function:

```javascript
User
```

creates objects.

The prototype:

```javascript
User.prototype
```

provides shared properties and methods.

---

# 36. Key Takeaways

* Constructor functions are reusable object-creation patterns.
* They are normally used with `new`.
* Constructor functions commonly use PascalCase.
* `this` refers to the newly created object when called with `new`.
* `new` creates an object and connects it to the constructor's prototype.
* Properties assigned with `this` become instance properties.
* Shared methods can be placed on the constructor's prototype.
* `instanceof` can check an object's prototype relationship.
* Constructor functions are an older syntax for working with JavaScript's prototype-based object model.
* ES6 classes provide cleaner syntax for many constructor/prototype patterns.
* JavaScript classes still use prototypes internally.

---
