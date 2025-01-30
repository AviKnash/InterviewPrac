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

Sites:-
https://www.toptal.com/react/interview-questions

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

### 9. Why is react important

React uses JSX which allows us to write Javascript and HTMl in one component together. An important part of this is Babel which compiles this code down to pure javascript and then then node uses the V8 engine with JIT ( just in time compiler) to compile javascript to machine code.

### 10. HOC ( Higher Order Component )

A higher order component in React is basically a wrapper around a function that add's additional functionality to this function. For example useMemo is a HOC. Usually can use to add logging too. 

Hooks have generlly replaced HOC's:

1. Hooks allow you to manage state, side effects, and context in a much simpler way directly within the functional component. They keep logic close to where it's being used, making code easier to follow and maintain.
2. With hooks, you can reuse logic without needing to wrap components. You can just call hooks inside your functional components, which leads to cleaner, more declarative code.
3. Debugging is easier with hooks because the logic is contained inside the function component itself, making it more straightforward to trace issues. There's less boilerplate and fewer layers to navigate.
4. HOCs were more commonly used in class-based components, but they still worked with functional components. However, they weren’t as natural or intuitive when using pure functions for React components.

Example of HOC in class based:

```jsx
import React, { Component } from 'react';

// HOC that adds a "count" prop to the wrapped component
function withCounter(WrappedComponent) {
  return class extends Component {
    constructor(props) {
      super(props);
      this.state = {
        count: 0,
      };
    }

    componentDidMount() {
      this.interval = setInterval(() => {
        this.setState(prevState => ({ count: prevState.count + 1 }));
      }, 1000);
    }

    componentWillUnmount() {
      clearInterval(this.interval);
    }

    render() {
      // Pass the "count" state as a prop to the WrappedComponent
      return <WrappedComponent {...this.props} count={this.state.count} />;
    }
  };
}
```

### 11. Debugging performance in React

If a performance issue such as slow rendering is seen within a React app, the first step is to use the Profiler tool provided within the React Developer Tools browser plugin, which is available for Google Chrome and Mozilla Firefox. The Profiler tool allows developers to find components that take a long time to render or are rendering more frequently than necessary.

### 12. StrictMode is a tool added in version 16.3 of React to highlight potential problems in an application. It performs additional checks on the application.

### 13. SSR and CSR

1. SSR is when the page is generated on the server and then sent to the client

### 14. Performance improvements

1. Pagination
2. SSR
3. Sending large files as gzip from api
4. useMemo, useCallback, meme etc...
5. Use lazy loading
6. Use debounce for expensive operations
7. Avoid unnecessary re-renders by splitting context into smaller, more focused providers instead of a single global context.
8. Use React.lazy and dynamic imports to load components on demand.


## Deployment Fundamentals  

### 1. Using github actions

Several steps are involved in general ci/cd

1. Test coverage:- 

Test coverage is the amount of code excueted during testing. It can determine how well a test suite covers the codebase and identify untested parts.
There are different types of test coverage:

- Line Coverage – Percentage of lines executed by tests.
- Branch Coverage – Percentage of code branches (e.g., if conditions) executed.
- Function Coverage – Percentage of functions or methods called by tests.
- Statement Coverage – Percentage of executed statements in the code.

What is an Acceptable Test Coverage?
100% coverage is ideal but not always practical.

Industry standards vary depending on the project:

- Critical systems (finance, healthcare, aviation): 90-100%
- General software applications: 70-90%
- Startups and fast-moving projects: 50-70%
- Legacy codebases: Often lower but improving it over time is key.

TLDR - Test Coverage is basically checking If all code that can be excuted has been imported into the test and tested including the conditional blocks. loops and exceptions.

2. We run code scanning using trivy or sonarcube to check code quality.

- We use Trivy to scan Docker images for vulnerabilities and misconfigurations.
- We use SonarQube to analyze code quality, detect code smells, and enforce best practices.

4. We run the unit tests using Jest, Mocha etc.

- Test reports are generated and stored as artifacts for review.
- Test coverage is measured using Istanbul (NYC) for JavaScript
- The pipeline enforces a minimum test coverage threshold to maintain code quality

5. Build & Package Application

- The application is built using Docker, producing versioned images.
- Images are tagged with git commit hash and latest for traceability.
- Build artifacts (JARs, binaries, or packaged apps) are stored in AWS S3, DigitalOcean Spaces, or Nexu

6. Push to Container Registry

- Docker images are pushed to DigitalOcean Container Registry (DOCR) or Amazon Elastic Container Registry (ECR).
- The pipeline ensures that only verified and tested images are deployed.

7. Deploy to Kubernetes (K8s) or Cloud Environment

- Kubernetes manifests (.yaml files) are applied to update deployments.
- Deployments use rolling updates to ensure zero downtime
- Health checks and readiness probes are validated before routing traffic.

8. Post-Deployment Checks & Monitoring

- Logs and metrics are monitored using Prometheus & Grafana, Datagog or ELK Stack (Elasticsearch, Logstash, Kibana).
- Smoke tests or API tests validate that the deployed app is functional.
- Alerting mechanisms notify the team of issues in real-time.

## USING GITOPS ( Like argoCD and fluxCD )

FLUX VIDEO -> https://www.youtube.com/watch?v=X5W_706-jSY

1. Push Image to GitOps Repository

- Instead of directly applying Kubernetes manifests, the pipeline updates a GitOps repository.
- The kustomization.yaml or Helm values.yaml file is updated with the new image tag.

2. GitOps Tool Deploys to Kubernetes

- ArgoCD or FluxCD detects changes in the GitOps repository and syncs them with the cluster.
- A rolling update is triggered, ensuring zero downtime.
- The Git repository becomes the single source of truth for deployments.

## Using runners

We sometimes use Github runners to update the EC2 instance directly. The workflow updates, builds and update the repo in the machine and then we use pm2 to restart the service.

## Nodejs Fundamentals 

Sites:

https://www.interviewbit.com/node-js-interview-questions/
https://www.youtube.com/watch?v=jxAXonX9Ao4&list=PL1BztTYDF-QPdTvgsjf8HOwO4ZVl_LhxS&index=29

### 1. NodeJs Event Loop

NodeJS event loop helps Nodejs do async tasks while using Javascripts single threading functionality.

1. Nodejs is basically the V8 engine plus LibUV which is written in C++ and is a library that allows the event loop.
2. Event loop has phases:
- Expires timers
- I/O tasks and polling ( basically file reads and writes)
- setImmediate callback
- Closed events ( event closed)

3. It also has the microtask queue which basically:

- Resolved Promises (.then, .catch, .finally)
- Async/Await Callbacks (After await)
- MutationObserver Callbacks
- process.nextTick (Node.js only, executed before other microtasks)

4. The process.nextTick is executed :

- Right after the current synchronous code. <b>setImmediate</b> run After the I/O phase, before next event loop cycle.
- Execustion phase: Microtask Phase (before Promises!) . <b>setImmediate</b> : Check Phase (after I/O events, before setTimeout)
