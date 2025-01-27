# InterviewPrac

A quick reference guide for JavaScript concepts to prepare for interviews.

---

## JavaScript Fundamentals  

### 1. `let`, `const`, and `var` Scopes  
- **`let` and `const`:**  
  Block-scoped. Accessible only within the block `{}` where they are declared (e.g., within loops, if statements).  

- **`var`:**  
  Function-scoped. Accessible throughout the function where it is declared, even outside blocks.

---

### 2. Function Declarations and Hoisting  
- **Function Declarations:**  
  Functions declared using the `function` keyword are hoisted, meaning they can be called even before their declaration in the code.  

  ```javascript
  // Example
  greet(); // Outputs: "Hello!"

  function greet() {
    console.log("Hello!");
  }
  
### 3. Anonymous and Arrow Functions
**Definition:** Functions declared using `const`, `let`, or `var` (e.g., arrow functions) are not hoisted. They can only be called after their declaration.

```javascript
// Example
greet(); // Error: Cannot access 'greet' before initialization

const greet = () => {
  console.log("Hello!");
};
```

### 4. Closures
Definition:
A closure is a function that retains access to its outer scope even after the outer function has finished executing.


// Example

```javascript
function outerFunction(outerVar) {
  return function innerFunction(innerVar) {
    console.log(`Outer: ${outerVar}, Inner: ${innerVar}`);
  };
}

const newFunction = outerFunction("Outer Scope");
newFunction("Inner Scope"); // Outputs: Outer: Outer Scope, Inner: Inner Scope

```

### 5. Prototypal Inheritance
Definition:
JavaScript uses prototypal inheritance, meaning objects can inherit properties and methods from other objects via the prototype chain.


// Example
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log(`Hello, my name is ${this.name}`);
};

const person1 = new Person("Alice");
person1.greet(); // Outputs: Hello, my name is Alice
```

### 6. Promises and Async/Await
Promises:
A Promise represents a value that may be available now, in the future, or never.


// Example
```javascript
const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Data received");
  }, 1000);
});

fetchData.then((data) => console.log(data)); // Outputs: Data received
```

### Async/Await:
A cleaner syntax for working with promises.


// Example
```javascript

async function fetchData() {
  const data = await new Promise((resolve) =>
    setTimeout(() => resolve("Data received"), 1000)
  );
  console.log(data);
}

fetchData(); // Outputs: Data received
```

### 7. Spread and Rest Operators
Spread (...): Expands an array or object.

```javascript

const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4];
console.log(arr2); // [1, 2, 3, 4]
Rest (...): Collects multiple elements into a single array.

function sum(...numbers) {
  return numbers.reduce((acc, num) => acc + num, 0);
}

console.log(sum(1, 2, 3)); // 6
```

### 8. Destructuring
Definition:
A way to unpack values from arrays or properties from objects into distinct variables.


// Example with Arrays
```javascript

const [a, b] = [1, 2];
console.log(a, b); // Outputs: 1, 2

// Example with Objects
const { name, age } = { name: "Alice", age: 25 };
console.log(name, age); // Outputs: Alice, 25
```
