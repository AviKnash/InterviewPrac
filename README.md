# InterviewPrac

A quick reference guide for concepts to prepare for interviews.

---

## JavaScript Fundamentals  

### 1. `let`, `const`, and `var` Scopes  
- **`let` and `const`:**  
  Block-scoped. Accessible only within the block `{}` where they are declared (e.g., within loops, if statements). let and const are also hoisted but it's set as TDZ ( Temporary Dead Zone) where the value is not accessible and will return a Reference Error if accessed before.

- **`var`:**  
  Function-scoped. Accessible throughout the function where it is declared, even outside blocks. var is initialized with undefined so it will return undefined If logged before a value is casted.

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

### 9. All ES6 features ( V Important )

Check this site: https://www.geeksforgeeks.org/introduction-to-es6/

## React Fundamentals  

React advnaced concepts site -> https://www.youtube.com/watch?v=qTDnwmMF5q8&list=PL6dw1BPCcLC4n-4o-t1kQZH0NJeZtpmGp

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

### 14. Portals

React.createPortal() is generally used to overaly a component and pass it through. THis is usually used for Modals or dialog boxes.

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
GitOps Video -> https://www.youtube.com/watch?v=SmXVFwkfpEw&list=PLamZM2ehvxwzSQMfcerapxw5Y2cDiF_FM

1. Push Image to GitOps Repository

- Instead of directly applying Kubernetes manifests, the pipeline updates a GitOps repository.
- The kustomization.yaml or Helm values.yaml file is updated with the new image tag.

2. GitOps Tool Deploys to Kubernetes

- ArgoCD or FluxCD detects changes in the GitOps repository and syncs them with the cluster.
- A rolling update is triggered, ensuring zero downtime.
- The Git repository becomes the single source of truth for deployments.

## Using runners

We sometimes use Github runners to update the EC2 instance directly. The workflow updates, builds and update the repo in the machine and then we use pm2 to restart the service.

### ECS fargate 

# Continuous Deployment (CD) with Amazon ECS and Fargate

## 1. **Amazon ECS with Fargate + AWS CodePipeline + AWS CodeBuild**

AWS provides a set of managed services that work seamlessly with ECS and Fargate for automating the CD process:

### **AWS CodePipeline**:
CodePipeline is a fully managed CI/CD service that automates the build, test, and deployment process. It can integrate with your ECS and Fargate setup, making it a common choice for deploying applications.

### **AWS CodeBuild**:
CodeBuild is a fully managed build service that compiles source code, runs tests, and produces deployable artifacts. You can use CodeBuild to build Docker images from your source code and push them to **Amazon ECR** (Elastic Container Registry).

### **Amazon ECS**:
Once the Docker image is built and stored in Amazon ECR, ECS can pull this image and deploy it to **Fargate**, which runs the containers.

### **Typical Workflow**:
1. **Source Stage**: CodePipeline monitors a source repository (e.g., **GitHub**, **CodeCommit**, or **S3**). When a new commit is pushed, the pipeline is triggered.
2. **Build Stage**: AWS CodeBuild is triggered, and it builds a Docker image based on your source code. The image is pushed to **Amazon ECR**.
3. **Deploy Stage**: The updated Docker image is deployed to ECS using **AWS CodeDeploy** or directly through ECS service updates. **Fargate** runs the containers in an ECS task.

### **Benefits**:
- Fully managed AWS services.
- Integrated with ECS and Fargate for containerized deployments.
- Easy to set up with automatic scaling and rolling updates.

---

## 2. **GitHub Actions + Amazon ECS + Fargate**

If you're using **GitHub** for version control, you can use **GitHub Actions** to automate your CD pipeline:

- **GitHub Actions** provides a workflow engine that can be configured to build, test, and deploy code to ECS/Fargate.
- Use the `aws-actions/configure-aws-credentials` GitHub Action to authenticate with AWS, and then use ECS CLI or AWS SDKs to update ECS services with new Docker images.

### **Example Workflow**:
1. On each push to a branch (e.g., `main`), **GitHub Actions** triggers a build process.
2. A **Docker image** is built and pushed to **Amazon ECR**.
3. **GitHub Actions** uses the **AWS CLI** or **AWS SDK** to deploy the updated Docker image to **ECS/Fargate**.

---

## 3. **CircleCI + Amazon ECS + Fargate**

**CircleCI** is another popular CI/CD service that can be used to automate the deployment of applications to ECS:

### **Source Repository**:
- CircleCI integrates with **GitHub** or **Bitbucket** to trigger a pipeline on code changes.
  
### **Build and Test**:
- CircleCI can use **Docker** to build your container image and push it to **ECR**.

### **Deployment**:
- CircleCI can then deploy the image to **ECS** using **AWS CLI** or **AWS ECS deployment configurations**.

---

## 4. **Jenkins + Amazon ECS + Fargate**

You can also use **Jenkins**, a popular open-source CI/CD tool, for automating deployments to ECS with Fargate:

### **Source Repository**:
- Jenkins can be configured to listen to changes in your Git repository.

### **Build**:
- Jenkins can use **Docker** to build the container image and push it to **ECR**.

### **Deploy**:
- Jenkins can deploy the Docker image to ECS using **AWS CLI**, the **ECS plugin for Jenkins**, or **AWS SDK**.


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

### 1. Nodejs worker threads, child_processes and clusters

# Node.js Worker Threads, Child Processes, and Clusters

## 1. Worker Threads
Worker Threads in Node.js allow running JavaScript in parallel threads. They share memory with the main thread but run independently.

### Usage
```js
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(__filename);
  worker.on('message', (msg) => console.log(`Message from worker: ${msg}`));
  worker.postMessage('Hello Worker');
} else {
  parentPort.on('message', (msg) => {
    parentPort.postMessage(`Received: ${msg}`);
  });
}
```

## 2. Child Processes
Child Processes allow running separate Node.js instances. They do not share memory but can communicate via IPC.

```javascript
const { fork } = require('child_process');

const child = fork('child.js');
child.on('message', (msg) => console.log(`From Child: ${msg}`));
child.send('Hello Child');\
```

# Types of Child Processes in Node.js

Node.js provides several ways to create child processes using the `child_process` module. The four main methods are:

## 1. `exec()`
`exec()` runs a command in a shell and buffers the output.

### Usage:
```js
const { exec } = require('child_process');

exec('ls -la', (error, stdout, stderr) => {
  if (error) {
    console.error(`Error: ${error.message}`);
    return;
  }
  console.log(`Output:\n${stdout}`);
});
```
When to Use?
Running shell commands
When output size is small (since it buffers output)

## 2 execFile()

execFile() runs a binary or script without spawning a shell.

```javascript
const { execFile } = require('child_process');

execFile('node', ['-v'], (error, stdout, stderr) => {
  if (error) {
    console.error(`Error: ${error.message}`);
    return;
  }
  console.log(`Node Version: ${stdout}`);
});
```
When to Use?
When running an executable file (e.g., node, python, ffmpeg)
More efficient than exec() as it avoids shell overhead

## 3. spawn()

spawn() launches a new process and streams its output in real-time.

```javascript
const { spawn } = require('child_process');

const ls = spawn('ls', ['-la']);

ls.stdout.on('data', (data) => {
  console.log(`Output: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.error(`Error: ${data}`);
});

ls.on('close', (code) => {
  console.log(`Process exited with code ${code}`);
});
```
### 4. fork()

fork() is a special case of spawn() that creates a new Node.js process and enables communication via IPC.

```javascript
const { fork } = require('child_process');

const child = fork('child.js');

child.on('message', (msg) => {
  console.log(`From Child: ${msg}`);
});

child.send('Hello from Parent');
```
When to Use?
Running separate Node.js scripts
When inter-process communication (IPC) is needed

### 3. Clusters

Clusters allow running multiple instances of a Node.js server across CPU cores.

```javascript
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
} else {
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end('Hello World');
  }).listen(8000);
}
```

## Database Fundamentals

Sites:
https://techtfq.com/blog/top-20-sql-interview-questions

1. 

## Misc backend

### 1. Cognito Auth

Create a User Pool → Handles user sign-up/sign-in.
Create an App Client → Allows your React app to authenticate users.

Use AWS amplify sdk to sign in a user or sign up a user.

1. Handling Session Expiry & Automatic Logout

Cognito issues a session with access, refresh, and ID tokens. When a session expires:

The app can refresh tokens automatically (if available).
If the refresh token is also expired, force logout the user.
Auto-Logout When Session Expires
You can use Auth.currentSession() inside an useEffect hook to check if the session is valid.

```jsx
import { Auth } from 'aws-amplify';
import { useEffect } from 'react';
import { useNavigate } from 'react-router-dom';

function SessionMonitor() {
  const navigate = useNavigate();

  useEffect(() => {
    const checkSession = async () => {
      try {
        await Auth.currentSession(); // Checks if session is still valid
      } catch (error) {
        console.log("Session expired. Logging out...");
        await Auth.signOut(); // Logout user
        navigate('/login'); // Redirect to login page
      }
    };

    const interval = setInterval(checkSession, 60000); // Check session every 1 min
    return () => clearInterval(interval); // Cleanup on unmount
  }, [navigate]);

  return null;
}

export default SessionMonitor;
```

Cognito automatically handles refresh token using Auth.currentSession() or we can use the following code to get a new token manually.

```jsx
async function refreshToken() {
  try {
    const session = await Auth.currentSession();
    const newToken = session.getAccessToken().getJwtToken();
    console.log("Refreshed token:", newToken);
  } catch (error) {
    console.error("Session expired. Please log in again.");
  }
}
```

### 2. Auth with JWT and session

Site:- 
JWT and Session: https://www.youtube.com/watch?v=fyTxwIa-1U0

1. JWT signing is usually done with HMAC, RSA or ECDSA.
2. HMAC is a symetric signing token basically same key is used to sign and check the token
3. RSA and ECDSA are assymetric. They have a private key to sign the token and public key to verify it. Making it more secure.
4. JWT tokens are checked in the middleware usually.

### 3. Refresh tokens and session tokens

It's awlways better to use short lived session tokens and long lived refresh tokens in case the token gets stolen. Try using:-

1. HttpOnly Cookies (Best Practice)
2. 
- HttpOnly cookies are not accessible to JavaScript running in the browser, which prevents cross-site scripting (XSS) attacks from stealing the refresh token.
- The token is sent with each request automatically by the browser, making it easy to handle in authenticated routes.

# Typescript Fundamentals

### 1. Generics

```
function identity<T>(arg: T): T {
  return arg;
}

const result = identity<number>(42);
```
The function will return 42.

Explanation:

The <T> syntax defines a generic type parameter, allowing the function to work with multiple types.
When calling identity<number>(42), T is replaced with number, making arg: number and returning number.
The function becomes function identity(arg: number): number.

### 2.  keyof and Mapped Types

```
type Person = {
  name: string;
  age: number;
};

type PersonKeys = keyof Person;
let key: PersonKeys = "name"; 

```
Output: No error, because "name" is a valid key of Person.

Explanation:

keyof Person results in "name" | "age", meaning PersonKeys can only be "name" or "age".
Assigning key = "name" is valid, but key = "gender" would cause an error

### 3. Utility Types

```
interface User {
  id: number;
  name: string;
  email: string;
}

const updateUser = (id: number, userData: ???) => {
  // Update logic
};
```

Examples: Partial, ReadOnly, Record.

Explanation:

Partial<T> makes all properties optional, so userData may contain id, name, email, or a subset of them.

### 4. Readonly & Immutable Objects

```
interface Car {
  brand: string;
  year: number;
}

const myCar: Readonly<Car> = { brand: "Toyota", year: 2022 };
myCar.year = 2023; // What happens here?

```
Error: "Cannot assign to 'year' because it is a read-only property."

Explanation:

Readonly<T> makes all properties immutable.
myCar.year = 2023; is not allowed because year is read-only.

### 5. Interface vs Type

Feature	                          interface	       type
Can be extended	                     ✅ (extends)	  ✅ (& operator)
Can be implemented by classes        ✅	            ❌
Can define unions/intersections	     ❌	            ✅
Can be merged (declaration merging)	 ✅	            ❌

# Architectural Design Patterns

Architectural design patterns help define the structure and organization of software applications. Here are some common ones:

## 1. Layered Architecture (N-Tier)
**Description**: Organizes an application into layers with distinct responsibilities (e.g., Presentation, Business Logic, Data Access).  
**Use Cases**: Enterprise applications, MVC (Model-View-Controller) frameworks.

## 2. Microservices Architecture
**Description**: Breaks an application into small, loosely coupled services that communicate via APIs.  
**Use Cases**: Scalable web applications, cloud-based systems.

## 3. Monolithic Architecture
**Description**: A single, unified application where all components are tightly integrated.  
**Use Cases**: Simple applications, startups, internal tools.

## 4. Event-Driven Architecture
**Description**: Uses events to trigger and communicate between services asynchronously.  
**Use Cases**: Real-time applications, IoT systems, complex workflows.

## 5. Serverless Architecture
**Description**: Applications run on managed cloud services, scaling automatically without managing infrastructure.  
**Use Cases**: APIs, background jobs, and lightweight cloud-based applications.

## 6. Microkernel Architecture (Plugin-Based)
**Description**: A core system with optional plugins/modules for extensibility.  
**Use Cases**: IDEs (e.g., VS Code), workflow engines, extensible software.

## 7. Model-View-Controller (MVC)
**Description**: Separates application logic into Model (data), View (UI), and Controller (business logic).  
**Use Cases**: Web frameworks like React, Angular, Django, and Rails.

## 8. Model-View-ViewModel (MVVM)
**Description**: Similar to MVC, but uses a ViewModel to handle UI logic and data binding.  
**Use Cases**: Frontend frameworks like Angular and React with state management.

## 9. Hexagonal Architecture (Ports and Adapters)
**Description**: Decouples the core business logic from external dependencies via interfaces.  
**Use Cases**: Applications needing high testability and maintainability.

## 10. CQRS (Command Query Responsibility Segregation)
**Description**: Separates read and write operations to optimize performance and scalability.  
**Use Cases**: High-performance data processing systems.

## 11. Event Sourcing
**Description**: Stores application state as a sequence of events rather than a current state.  
**Use Cases**: Banking, auditing, and systems requiring a full history of changes.

## 12. Pipeline Architecture
**Description**: Processes data through a series of stages or filters.  
**Use Cases**: Data processing, ETL (Extract, Transform, Load) pipelines.

# Cloud Design Patterns

Refer these -> 
Azure has the best set - https://learn.microsoft.com/en-us/azure/architecture/patterns/
AWS for AWS specific ones' - https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/introduction.html


