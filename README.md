# InterviewPrac

A quick reference guide for concepts to prepare for interviews.

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

## React Fundamentals  

### 1. All Hooks

React provides several hooks that enable the use of state, lifecycle methods, and context in functional components. Common hooks include:

- **`useState`**: Allows adding state to a functional component.
- **`useEffect`**: Handles side effects like fetching data, subscriptions, or manually changing the DOM.
- **`useContext`**: Consumes context values without using the `Context.Consumer` wrapper.
- **`useReducer`**: Manages more complex state logic compared to `useState`.
- **`useMemo`**: Optimizes performance by memoizing the result of an expensive computation.
- **`useCallback`**: Memoizes functions to prevent unnecessary re-creations.
- **`useRef`**: Creates a mutable reference object that persists across renders, often used for accessing DOM elements.
- **`useLayoutEffect`**: Similar to `useEffect`, but fires synchronously after all DOM mutations.
- **`useImperativeHandle`**: Customizes the instance value that is exposed when using `React.forwardRef`.

---

### 2. useEffect

`useEffect` is used to handle side effects in functional components. It acts as a combination of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in class components.  

- If the dependency array is **empty**, the effect runs **only once** (similar to `componentDidMount`).
- If there are dependencies in the array, the effect will run **whenever the values in the dependency array change**.
- Returning a cleanup function allows handling logic like unsubscribing or cleaning up timers (similar to `componentWillUnmount`).

Example:
```jsx
useEffect(() => {
  console.log("Component mounted or dependency changed");

  return () => {
    console.log("Cleanup logic");
  };
}, [dependency]);
```

### 3. React Reconciliation Algorithm

The React reconciliation algorithm determines how changes in the Virtual DOM are applied to the actual DOM efficiently.

React maintains two Virtual DOMs: the current Virtual DOM and the updated Virtual DOM.
It compares the two Virtual DOMs (a process called "diffing") and identifies the minimum number of changes required.
These changes are then applied to the real DOM in the most efficient way possible.
This prevents unnecessary updates and improves performance since interacting with the real DOM is expensive.
Key Concepts:

Key Attribute: Helps React identify which elements have changed, been added, or removed.
Batch Updates: React groups multiple updates together to minimize re-renders.
Fiber Architecture: React uses a fiber architecture to break rendering work into chunks and prioritize updates, ensuring smoother user experiences.

### 4. React uses JSX

JSX is a syntax extension for JavaScript that resembles HTML. It is used to describe what the UI should look like and is eventually transpiled to React's `createElement` calls.
Key Points:

JSX allows embedding expressions using {}.
JSX attributes are written in camelCase (e.g., className instead of class).
Fragments (<> </>) can be used to group multiple elements without adding an extra DOM node.

### 5. Keys in React

Keys are used by React to uniquely identify elements in a list. They help React determine which items have changed, been added, or removed.

A key must be unique among sibling elements.
It improves performance during re-rendering.

### 6.  Controlled vs Uncontrolled Components

Controlled Components: Components where form data is handled by React state. React has full control over the form elements' value.

```jsx
function ControlledInput() {
  const [value, setValue] = useState("");
  return (
    <input value={value} onChange={(e) => setValue(e.target.value)} />
  );
}
```

Uncontrolled Components: Components where form data is handled by the DOM itself. Refs are typically used to access the value.

```jsx
function UncontrolledInput() {
  const inputRef = useRef();
  const handleSubmit = () => {
    alert(inputRef.current.value);
  };
  return <input ref={inputRef} />;
}
```

### 7. Difference Between Context API and Redux

1. Context API

- Best for simple, small to medium applications.
- Rerenders all child components when the value in the Provider changes.
- No middleware support for advanced features like logging or async operations.
- Lightweight and built into React.

2. Redux

- Best for complex, large-scale applications with deeply nested state.
- Updates only the components connected to specific pieces of the state using connect or useSelector.
- Supports middleware for advanced use cases like async actions and debugging.
- Requires additional setup and boilerplate compared to Context.

### 8. Security

1. Content Security Policy (CSP)

Implement CSP headers to restrict the sources from which your application can load resources like scripts, images, and styles.

2. Avoid Using Local Storage for Sensitive Data

Use secure cookies with HttpOnly and Secure flags for storing sensitive tokens or session information.

3. Limit Error Messages in Production

Do not expose sensitive information in error messages or stack traces in the production environment.

4. Authentication and Authorization

Use robust authentication mechanisms like OAuth, JWT, or session-based auth.
Ensure role-based access control (RBAC) and Atttribute bases access control ( ABAC) to protect specific routes and data.

5. Rate Limiting and Throttling
   
Apply rate limiting on API endpoints to protect against brute force attacks.
