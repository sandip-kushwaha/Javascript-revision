# JavaScript Constructor

## What is a Constructor?

A **constructor** is a special method inside a JavaScript class that runs automatically when an object is created with `new`.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user.name);
```

Output:

```text
Sandip
```

The constructor is mainly used to **initialize an object's properties**.

---

# 1. Basic Constructor Syntax

```js
class User {
  constructor(name) {
    this.name = name;
  }
}
```

Create an object:

```js
const user = new User("Sandip");
```

The flow is:

```text
new User("Sandip")
        ↓
constructor(name)
        ↓
this.name = "Sandip"
        ↓
new object
```

---

# 2. Constructor Runs Automatically

You normally don't call the constructor directly.

```js
class User {
  constructor(name) {
    console.log("Constructor executed");
    this.name = name;
  }
}

const user = new User("Sandip");
```

Output:

```text
Constructor executed
```

The constructor runs because of:

```js
new User("Sandip");
```

---

# 3. Constructor Parameters

A constructor can accept multiple parameters.

```js
class User {
  constructor(name, email, role) {
    this.name = name;
    this.email = email;
    this.role = role;
  }
}

const user = new User(
  "Sandip",
  "sandip@example.com",
  "admin"
);

console.log(user);
```

The resulting object contains:

```text
name
email
role
```

---

# 4. `this` Inside Constructor

Inside a constructor, `this` refers to the newly created instance.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");
```

Conceptually:

```text
new User()
    ↓
new object
    ↓
this = new object
    ↓
this.name = "Sandip"
```

So:

```js
console.log(user.name);
```

returns:

```text
Sandip
```

---

# 5. Multiple Instances

A single constructor can initialize many objects.

```js
class User {
  constructor(name, role) {
    this.name = name;
    this.role = role;
  }
}

const user1 = new User("Sandip", "Admin");
const user2 = new User("Ram", "Waiter");

console.log(user1);
console.log(user2);
```

Each instance has its own data.

```text
user1
├── name: Sandip
└── role: Admin

user2
├── name: Ram
└── role: Waiter
```

---

# 6. Default Constructor

If you do not define a constructor, JavaScript provides a default constructor behavior.

```js
class User {}

const user = new User();

console.log(user);
```

The object can still be created.

For a class without a parent, it behaves roughly like:

```js
constructor(...args) {}
```

---

# 7. Default Constructor in Inheritance

If a child class does not define a constructor, JavaScript provides a default constructor that effectively forwards arguments to the parent.

Example:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {}

const admin = new Admin("Sandip");

console.log(admin.name);
```

Output:

```text
Sandip
```

Conceptually, the child behaves as if it had:

```js
constructor(...args) {
  super(...args);
}
```

---

# 8. Constructor with Default Parameters

Constructors can use default parameters.

```js
class User {
  constructor(name, role = "User") {
    this.name = name;
    this.role = role;
  }
}

const user1 = new User("Sandip");
const user2 = new User("Ram", "Admin");

console.log(user1.role);
console.log(user2.role);
```

Output:

```text
User
Admin
```

---

# 9. Constructor Validation

You can validate values while creating an object.

```js
class User {
  constructor(name) {
    if (!name) {
      throw new Error("Name is required");
    }

    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user.name);
```

If the value is missing:

```js
new User();
```

an error is thrown.

---

# 10. Constructor with Multiple Properties

A practical example:

```js
class Food {
  constructor(name, price, category) {
    this.name = name;
    this.price = price;
    this.category = category;
  }

  getInfo() {
    return `${this.name} - Rs. ${this.price}`;
  }
}

const food = new Food(
  "Chicken Pizza",
  450,
  "Pizza"
);

console.log(food.getInfo());
```

Output:

```text
Chicken Pizza - Rs. 450
```

The constructor initializes the object's data.

---

# 11. Constructor vs Method

A constructor:

```js
constructor(name) {
  this.name = name;
}
```

runs automatically when using:

```js
new User("Sandip");
```

A normal method:

```js
getName() {
  return this.name;
}
```

must be called explicitly:

```js
user.getName();
```

Comparison:

| Constructor                 | Method                         |
| --------------------------- | ------------------------------ |
| Special class method        | Normal class behavior          |
| Named `constructor`         | Can have any valid method name |
| Runs during object creation | Runs when called               |
| Initializes object          | Performs an operation          |
| One constructor per class   | Multiple methods allowed       |

---

# 12. Constructor and Prototype

Consider:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}
```

The relationship is:

```text
User
 │
 ├── constructor()
 │
 ↓
User.prototype
 │
 └── greet()
```

The constructor initializes instance properties.

The methods are available through the prototype.

---

# 13. Constructor Does Not Mean Method Storage

This:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}
```

does not mean `greet()` is recreated inside every instance.

Instead:

```text
user1
  ↓
User.prototype.greet

user2
  ↓
User.prototype.greet
```

Both instances can use the shared prototype method.

---

# 14. Constructor with Arrays

Be careful when using arrays as constructor defaults.

Good:

```js
class Order {
  constructor(items = []) {
    this.items = items;
  }
}

const order1 = new Order();
const order2 = new Order();

order1.items.push("Pizza");

console.log(order1.items);
console.log(order2.items);
```

Output:

```text
["Pizza"]
[]
```

Each constructor call gets a new default array because `[]` is evaluated for that call.

---

# 15. Constructor with Objects

The same idea applies to objects:

```js
class User {
  constructor(settings = {}) {
    this.settings = settings;
  }
}

const user = new User();

user.settings.theme = "dark";

console.log(user.settings);
```

The constructor stores the object reference in the instance.

---

# 16. Constructor and Object References

Consider:

```js
const settings = {
  theme: "dark"
};

class User {
  constructor(settings) {
    this.settings = settings;
  }
}

const user1 = new User(settings);
const user2 = new User(settings);
```

Both objects reference the same `settings` object.

```text
user1.settings ──┐
                 ↓
              settings
                 ↑
user2.settings ──┘
```

Therefore:

```js
user1.settings.theme = "light";

console.log(user2.settings.theme);
```

Output:

```text
light
```

The constructor does not automatically deep-copy objects.

---

# 17. Constructor Inheritance

Consider:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  constructor(name, permissions) {
    super(name);
    this.permissions = permissions;
  }
}
```

The child constructor calls:

```js
super(name);
```

This executes the parent constructor.

---

# 18. Why `super()` Is Required

In a derived class:

```js
class Admin extends User {
  constructor(name) {
    this.name = name;
  }
}
```

This is invalid because `this` cannot be used before the parent constructor has initialized the derived instance.

Use:

```js
class Admin extends User {
  constructor(name) {
    super(name);
  }
}
```

After `super()`:

```js
this
```

can be used.

---

# 19. Parent Constructor with Child Data

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

class Admin extends User {
  constructor(name, permissions) {
    super(name);

    this.permissions = permissions;
  }
}

const admin = new Admin(
  "Sandip",
  ["manage-users", "manage-food"]
);

console.log(admin.name);
console.log(admin.permissions);
```

The process is:

```text
new Admin()
     ↓
Admin constructor
     ↓
super(name)
     ↓
User constructor
     ↓
this.name
     ↓
Admin continues
     ↓
this.permissions
```

---

# 20. Calling a Parent Method from Constructor

A child constructor can use methods after `super()`.

```js
class User {
  constructor(name) {
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

class Admin extends User {
  constructor(name) {
    super(name);

    console.log(this.getName());
  }
}

const admin = new Admin("Sandip");
```

Output:

```text
Sandip
```

---

# 21. Constructor Return Behavior

Normally, constructors initialize and return the newly created instance automatically.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Sandip");

console.log(user);
```

You normally do not write:

```js
return this;
```

---

# 22. Returning an Object from a Constructor

A constructor can explicitly return an object.

```js
class User {
  constructor(name) {
    this.name = name;

    return {
      customName: name
    };
  }
}

const user = new User("Sandip");

console.log(user);
```

The explicitly returned object can replace the normal instance.

Because of this, returning objects from constructors should be done intentionally.

---

# 23. Returning a Primitive

Returning a primitive from a constructor does not replace the created instance.

```js
class User {
  constructor(name) {
    this.name = name;

    return "Hello";
  }
}

const user = new User("Sandip");

console.log(user.name);
```

Output:

```text
Sandip
```

The object is still returned.

For class constructors, an explicitly returned **object** can replace the instance, while a primitive return is ignored.

---

# 24. Constructor and Private Fields

Private fields can be initialized in a constructor.

```js
class BankAccount {
  #balance;

  constructor(initialBalance = 0) {
    this.#balance = initialBalance;
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount(1000);

console.log(account.getBalance());
```

Output:

```text
1000
```

The private field cannot be accessed directly from outside the class.

---

# 25. Constructor with Computed Data

The constructor can also prepare derived values.

```js
class Product {
  constructor(name, price, quantity) {
    this.name = name;
    this.price = price;
    this.quantity = quantity;
    this.total = price * quantity;
  }
}

const product = new Product(
  "Keyboard",
  2500,
  2
);

console.log(product.total);
```

Output:

```text
5000
```

---

# 26. Practical Hotel Example

```js
class HotelTable {
  constructor(
    tableNumber,
    capacity,
    location = "indoor"
  ) {
    this.tableNumber = tableNumber;
    this.capacity = capacity;
    this.location = location;
    this.status = "available";
  }

  occupy() {
    this.status = "occupied";
  }

  getInfo() {
    return {
      tableNumber: this.tableNumber,
      capacity: this.capacity,
      location: this.location,
      status: this.status
    };
  }
}

const table = new HotelTable(
  "T-03",
  6,
  "rooftop"
);

console.log(table.getInfo());
```

The constructor initializes:

```text
tableNumber
capacity
location
status
```

---

# 27. Practical Order Example

```js
class Order {
  constructor(tableNumber, customerName) {
    this.tableNumber = tableNumber;
    this.customerName = customerName;
    this.items = [];
    this.status = "pending";
  }

  addItem(item) {
    this.items.push(item);
  }

  confirm() {
    this.status = "confirmed";
  }
}

const order = new Order(
  "T-03",
  "Sandip"
);

order.addItem("Chicken Pizza");
order.confirm();

console.log(order);
```

The constructor creates the initial order state.

---

# 28. Constructor Naming Rule

In a class, the constructor must be named exactly:

```js
constructor
```

Correct:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}
```

Incorrect:

```js
class User {
  User(name) {
    this.name = name;
  }
}
```

`User()` in the second example is treated as a normal method, not a constructor.

---

# 29. Only One Constructor

A class cannot have multiple constructors.

Incorrect:

```js
class User {
  constructor(name) {}

  constructor(name, email) {}
}
```

A class should contain only one `constructor()` method.

If you need different initialization behavior, use default parameters or conditional logic.

Example:

```js
class User {
  constructor(name, email = null) {
    this.name = name;
    this.email = email;
  }
}
```

---

# 30. Constructor with Options Object

For many parameters, an options object can make the constructor easier to maintain.

```js
class User {
  constructor({
    name,
    email,
    role = "User"
  }) {
    this.name = name;
    this.email = email;
    this.role = role;
  }
}

const user = new User({
  name: "Sandip",
  email: "sandip@example.com",
  role: "Admin"
});

console.log(user);
```

This approach is useful when a class has many configuration values.

---

# 31. Constructor and Validation

For important data, validate before storing it.

```js
class Product {
  constructor(name, price) {
    if (!name) {
      throw new Error("Product name is required");
    }

    if (price < 0) {
      throw new Error("Price cannot be negative");
    }

    this.name = name;
    this.price = price;
  }
}
```

Now invalid objects are prevented from being created.

---

# 32. Constructor Best Practices

### Keep initialization clear

```js
constructor(name, role) {
  this.name = name;
  this.role = role;
}
```

### Validate important data

```js
if (!name) {
  throw new Error("Name is required");
}
```

### Use defaults when appropriate

```js
constructor(role = "User") {}
```

### Avoid doing heavy work

A constructor should generally initialize the object rather than perform expensive operations such as large database requests.

### Use methods for behavior

Instead of putting all logic in the constructor:

```js
constructor(name) {
  this.name = name;
}
```

put reusable operations in methods:

```js
getInfo() {
  return this.name;
}
```

---

# 33. Constructor Flow

When you write:

```js
const user = new User("Sandip");
```

the important flow is:

```text
             new User()
                 │
                 ↓
        Create new instance
                 │
                 ↓
       Connect prototype
                 │
                 ↓
       Run constructor()
                 │
                 ↓
        Initialize this
                 │
                 ↓
          Return instance
```

For inheritance:

```text
             new Admin()
                 │
                 ↓
        Admin constructor
                 │
                 ↓
             super()
                 │
                 ↓
         User constructor
                 │
                 ↓
        Parent initialization
                 │
                 ↓
         Child initialization
```

---

# 34. Constructor vs Prototype

The constructor is mainly responsible for **instance initialization**.

The prototype is mainly useful for **shared methods**.

```text
Class
 │
 ├── constructor()
 │      ↓
 │   instance data
 │
 └── prototype
        ↓
     shared methods
```

Example:

```js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}
```

Here:

```text
name
 ↓
instance property

greet()
 ↓
prototype method
```

---

# 35. Key Takeaways

* `constructor()` is a special class method.
* It runs automatically when `new` creates an instance.
* It is mainly used to initialize object properties.
* `this` refers to the instance being created.
* A class can have only one constructor.
* Constructors can accept parameters.
* Constructors can use default parameters.
* Constructors can validate input.
* Child constructors use `super()` to initialize the parent part.
* `this` cannot be used in a derived constructor before `super()`.
* Returning an object from a constructor can replace the normal instance.
* Returning a primitive does not replace the instance.
* Private fields can be initialized inside constructors.
* Constructors should generally focus on initialization.
* Shared methods belong on the prototype rather than being recreated for every instance.

## Simple Mental Model

```text
class User
     │
     ↓
constructor()
     │
     ↓
initialize object
     │
     ↓
instance
     │
     ↓
prototype methods
```
