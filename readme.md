# Frontend Developer Interview Questions

## ReactJS

### Question 1: What is React and why is it used?

**Answer:** React is a JavaScript library for building user interfaces, particularly for web applications. It allows developers to create reusable UI components that manage their own state. React is used because it enables efficient rendering through a virtual DOM, promotes component-based architecture for maintainable code, and has a large ecosystem of tools and libraries. For example, a simple React component looks like this:

```jsx
import React from "react";

function HelloWorld() {
  return <h1>Hello, World!</h1>;
}

export default HelloWorld;
```

### Question 2: Explain JSX and its benefits.

**Answer:** JSX is a syntax extension for JavaScript that allows you to write HTML-like code within JavaScript. It gets transpiled to JavaScript function calls. Benefits include improved readability, easier debugging, and prevention of injection attacks. Example:

```jsx
const element = <h1>Hello, {name}!</h1>;
```

This transpiles to `React.createElement('h1', null, 'Hello, ', name, '!')`.

### Question 3: Describe the component lifecycle in class components.

**Answer:** Class components have lifecycle methods: `constructor` for initialization, `componentDidMount` for side effects after mounting, `componentDidUpdate` for updates, `componentWillUnmount` for cleanup. Example:

```jsx
class MyComponent extends React.Component {
  componentDidMount() {
    console.log("Component mounted");
  }
  render() {
    return <div>Hello</div>;
  }
}
```

### Question 4: What are React Hooks and why were they introduced?

**Answer:** Hooks are functions that let you use state and lifecycle features in functional components. Introduced to simplify code, avoid class complexity, and enable reuse of stateful logic. `useState` manages state:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

### Question 5: Explain useEffect and its use cases.

**Answer:** `useEffect` handles side effects in functional components, similar to lifecycle methods. It runs after render. Use cases: data fetching, subscriptions. Example:

```jsx
useEffect(() => {
  fetchData();
  return () => cleanup(); // Cleanup on unmount
}, [dependency]);
```

### Question 6: What is the difference between props and state?

**Answer:** Props are read-only data passed from parent to child. State is mutable data managed within the component. Props for configuration, state for interactivity. Example:

```jsx
function Child({ message }) {
  // props
  const [count, setCount] = useState(0); // state
  return (
    <div>
      {message} {count}
    </div>
  );
}
```

### Question 7: How does the Virtual DOM work in React?

**Answer:** Virtual DOM is a lightweight copy of the real DOM. React compares virtual trees to find changes, then updates only the real DOM differences. This optimizes performance. Example: When state changes, React re-renders virtually, diffs, and patches.

### Question 8: What is reconciliation in React?

**Answer:** Reconciliation is the process where React updates the DOM to match the virtual DOM. It uses a diffing algorithm to minimize changes. Keys help identify elements in lists.

### Question 9: Why are keys important in React lists?

**Answer:** Keys help React identify which items have changed, added, or removed. They improve performance and prevent bugs. Example:

```jsx
const items = ["a", "b", "c"];
return (
  <ul>
    {items.map((item) => (
      <li key={item}>{item}</li>
    ))}
  </ul>
);
```

### Question 10: Explain Higher-Order Components (HOCs).

**Answer:** HOCs are functions that take a component and return a new component with additional props or behavior. Used for code reuse. Example:

```jsx
function withLogging(WrappedComponent) {
  return function (props) {
    console.log("Rendering", WrappedComponent.name);
    return <WrappedComponent {...props} />;
  };
}
```

### Question 11: What are render props?

**Answer:** Render props is a pattern where a component's prop is a function that returns JSX. It allows sharing logic between components. Example:

```jsx
class MouseTracker extends React.Component {
  render() {
    return this.props.render(this.state);
  }
}
<MouseTracker render={(mouse) => <p>{mouse.x}</p>} />;
```

### Question 12: How does the Context API work?

**Answer:** Context provides a way to pass data through the component tree without props drilling. Create context, provide value, consume in children. Example:

```jsx
const ThemeContext = React.createContext("light");
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
function Toolbar() {
  return (
    <ThemeContext.Consumer>
      {(value) => <div>{value}</div>}
    </ThemeContext.Consumer>
  );
}
```

### Question 13: Compare Redux and Context API for state management.

**Answer:** Redux is a predictable state container with actions, reducers, middleware. Context is simpler for small apps. Redux for complex, global state; Context for theme, auth.

### Question 14: How does React Router work?

**Answer:** React Router enables navigation in single-page apps. It uses `BrowserRouter`, `Route`, `Link`. Example:

```jsx
import { BrowserRouter as Router, Route, Link } from "react-router-dom";
<Router>
  <Link to="/home">Home</Link>
  <Route path="/home" component={Home} />
</Router>;
```

### Question 15: What are controlled and uncontrolled components?

**Answer:** Controlled components have state managed by React (value from state). Uncontrolled use refs for DOM access. Controlled for validation, uncontrolled for simple forms.

```jsx
// Controlled
<input value={this.state.value} onChange={this.handleChange} />

// Uncontrolled
<input ref={this.inputRef} />
```

### Question 16: Explain error boundaries in React.

**Answer:** Error boundaries catch JavaScript errors in the component tree. Use `componentDidCatch` or `getDerivedStateFromError`. Example:

```jsx
class ErrorBoundary extends React.Component {
  componentDidCatch(error, info) {
    this.setState({ hasError: true });
  }
  render() {
    if (this.state.hasError) return <h1>Something went wrong.</h1>;
    return this.props.children;
  }
}
```

### Question 17: What are React Portals?

**Answer:** Portals render children into a DOM node outside the parent component. Useful for modals, tooltips. Example:

```jsx
ReactDOM.createPortal(this.props.children, domNode);
```

### Question 18: How does React Suspense work?

**Answer:** Suspense lets components "wait" for something before rendering. Used with lazy loading. Example:

```jsx
const LazyComponent = React.lazy(() => import("./LazyComponent"));
<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>;
```

### Question 19: Explain memoization in React (React.memo, useMemo, useCallback).

**Answer:** Memoization prevents unnecessary re-renders. `React.memo` for components, `useMemo` for values, `useCallback` for functions. Example:

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
const memoizedCallback = useCallback(() => doSomething(a, b), [a, b]);
```

### Question 20: What are custom hooks and when to use them?

**Answer:** Custom hooks are reusable functions using built-in hooks. Use for shared logic. Example:

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url).then(setData);
  }, [url]);
  return data;
}
```

### Question 21: How do you test React components?

**Answer:** Use Jest and React Testing Library. Test behavior, not implementation. Example:

```jsx
import { render, screen } from "@testing-library/react";
test("renders learn react link", () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

### Question 22: What is server-side rendering in React and how is it achieved with Next.js?

**Answer:** SSR renders React on the server for faster initial loads and SEO. Next.js provides it out-of-the-box. Example: Pages in `pages/` are SSR by default.

## JavaScript

### Question 1: What are closures in JavaScript?

**Answer:** Closures are functions that remember the scope in which they were created. They access outer variables. Example:

```javascript
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}
const counter = outer();
console.log(counter()); // 1
```

### Question 2: Explain prototypes and prototypal inheritance.

**Answer:** Prototypes are objects from which other objects inherit properties. Inheritance via `__proto__` or `Object.create`. Example:

```javascript
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function () {
  return "Hello " + this.name;
};
const p = new Person("Alice");
console.log(p.greet());
```

### Question 3: What is the difference between var, let, and const?

**Answer:** `var` is function-scoped, hoisted. `let` and `const` are block-scoped. `const` for constants. Example:

```javascript
if (true) {
  var x = 1; // global
  let y = 2; // block
  const z = 3; // block constant
}
```

### Question 4: How do promises work in JavaScript?

**Answer:** Promises represent asynchronous operations. States: pending, fulfilled, rejected. Methods: then, catch. Example:

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done"), 1000);
});
promise.then((result) => console.log(result));
```

### Question 5: Explain async/await.

**Answer:** `async` makes a function return a promise. `await` pauses execution until promise resolves. Example:

```javascript
async function fetchData() {
  const data = await fetch("/api/data");
  return data.json();
}
```

### Question 6: What are arrow functions and their differences from regular functions?

**Answer:** Arrow functions are concise, no `this` binding. Lexical `this`. Example:

```javascript
const add = (a, b) => a + b;
const obj = {
  value: 10,
  regular: function () {
    return this.value;
  },
  arrow: () => this.value, // undefined
};
```

### Question 7: How does the event loop work?

**Answer:** Event loop processes tasks in call stack, then microtasks (promises), then macrotasks (setTimeout). Ensures non-blocking.

### Question 8: What is hoisting in JavaScript?

**Answer:** Hoisting moves declarations to top. `var` and functions are hoisted. Example:

```javascript
console.log(a); // undefined
var a = 1;
```

### Question 9: Explain the 'this' keyword.

**Answer:** `this` refers to the object executing the function. Depends on call: global, object, new, call/apply. Example:

```javascript
function show() {
  console.log(this);
}
show(); // window
const obj = { show };
obj.show(); // obj
```

### Question 10: What are ES6 modules?

**Answer:** Modules allow importing/exporting code. `import` and `export`. Example:

```javascript
// module.js
export const pi = 3.14;
// main.js
import { pi } from "./module.js";
```

### Question 11: How do you handle errors in JavaScript?

**Answer:** Use try/catch blocks. Throw custom errors. Example:

```javascript
try {
  riskyCode();
} catch (error) {
  console.error(error);
}
```

### Question 12: What is the spread operator and rest parameters?

**Answer:** Spread expands arrays/objects. Rest collects into array. Example:

```javascript
const arr = [1, 2, 3];
const newArr = [...arr, 4]; // [1,2,3,4]
function sum(...nums) {
  return nums.reduce((a, b) => a + b);
}
```

### Question 13: Explain destructuring assignment.

**Answer:** Destructuring extracts values from arrays/objects. Example:

```javascript
const [a, b] = [1, 2];
const { name, age } = { name: "Alice", age: 30 };
```

### Question 14: What are template literals?

**Answer:** Template literals use backticks for strings with interpolation. Example:

```javascript
const name = "World";
console.log(`Hello ${name}!`);
```

### Question 15: How does setTimeout work?

**Answer:** `setTimeout` schedules a function after delay. Asynchronous. Example:

```javascript
setTimeout(() => console.log("Delayed"), 1000);
```

### Question 16: What is the difference between == and ===?

**Answer:** `==` loose equality with type coercion. `===` strict equality. Prefer `===`. Example:

```javascript
1 == "1"; // true
1 === "1"; // false
```

### Question 17: Explain the Map and Set data structures.

**Answer:** Map is key-value pairs, any type keys. Set is unique values. Example:

```javascript
const map = new Map();
map.set("key", "value");
const set = new Set([1, 2, 2]); // {1, 2}
```

### Question 18: What are generators in JavaScript?

**Answer:** Generators are functions that can pause and resume. Use `function*` and `yield`. Example:

```javascript
function* generator() {
  yield 1;
  yield 2;
}
const gen = generator();
console.log(gen.next().value); // 1
```

### Question 19: How do you work with JSON in JavaScript?

**Answer:** `JSON.stringify` to string, `JSON.parse` to object. Example:

```javascript
const obj = { name: "Alice" };
const json = JSON.stringify(obj);
const parsed = JSON.parse(json);
```

### Question 20: What is the Symbol type?

**Answer:** Symbols are unique identifiers. Example:

```javascript
const sym = Symbol("description");
```

### Question 21: Explain the fetch API.

**Answer:** Fetch is modern way to make HTTP requests. Returns promises. Example:

```javascript
fetch("/api/data")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

### Question 22: What are Web Workers?

**Answer:** Web Workers run scripts in background threads. For heavy computations. Example:

```javascript
const worker = new Worker("worker.js");
worker.postMessage("start");
```

## HTML

### Question 1: What is semantic HTML?

**Answer:** Semantic HTML uses meaningful tags like `<header>`, `<nav>`, `<article>` for structure and accessibility.

### Question 2: Explain the difference between div and span.

**Answer:** `<div>` is block-level, `<span>` is inline. Use for layout vs styling.

### Question 3: What are HTML forms and how to handle them?

**Answer:** Forms collect user input. Use `<form>`, `<input>`, etc. Handle with JavaScript or server.

### Question 4: What is the purpose of the DOCTYPE declaration?

**Answer:** DOCTYPE tells browser the HTML version. `<!DOCTYPE html>` for HTML5.

### Question 5: Explain meta tags.

**Answer:** Meta tags provide metadata. Example: `<meta charset="UTF-8">` for encoding.

### Question 6: What are HTML entities?

**Answer:** Entities represent special characters. Example: `&lt;` for <.

### Question 7: How do you create links in HTML?

**Answer:** Use `<a href="url">text</a>`. Attributes: target, rel.

### Question 8: What is the alt attribute for?

**Answer:** Alt text for images, for accessibility and when image fails.

### Question 9: Explain HTML tables.

**Answer:** Tables with `<table>`, `<tr>`, `<td>`. Use for tabular data.

### Question 10: What are iframes?

**Answer:** Iframes embed another HTML document. `<iframe src="url"></iframe>`.

### Question 11: How do you embed media in HTML?

**Answer:** `<img>`, `<video>`, `<audio>` with src attribute.

### Question 12: What is the viewport meta tag?

**Answer:** Controls layout on mobile. `<meta name="viewport" content="width=device-width">`.

### Question 13: Explain HTML lists.

**Answer:** Ordered `<ol>`, unordered `<ul>`, definition `<dl>`.

### Question 14: What are HTML comments?

**Answer:** `<!-- comment -->` for notes, not rendered.

### Question 15: How do you create a button in HTML?

**Answer:** `<button>Click me</button>` or `<input type="button">`.

### Question 16: What is the role of the head element?

**Answer:** Contains metadata, title, links to styles/scripts.

### Question 17: Explain the canvas element.

**Answer:** `<canvas>` for drawing graphics with JavaScript.

### Question 18: What are data attributes?

**Answer:** `data-*` attributes store custom data. Example: `<div data-id="123"></div>`.

### Question 19: How do you create a dropdown in HTML?

**Answer:** `<select><option>Item</option></select>`.

### Question 20: What is the difference between id and class?

**Answer:** Id unique, class multiple elements.

### Question 21: Explain the figure and figcaption elements.

**Answer:** `<figure>` for images/diagrams, `<figcaption>` for caption.

### Question 22: What are HTML sections?

**Answer:** `<section>`, `<article>`, `<aside>`, `<header>`, `<footer>` for structure.

## CSS

### Question 1: What is the box model in CSS?

**Answer:** Box model: content, padding, border, margin. `box-sizing: border-box` includes padding/border in width.

### Question 2: Explain Flexbox.

**Answer:** Flexbox for one-dimensional layouts. Container with `display: flex`, items with `justify-content`, `align-items`.

### Question 3: What is CSS Grid?

**Answer:** Grid for two-dimensional layouts. `display: grid`, `grid-template-columns`, etc.

### Question 4: How do you center an element?

**Answer:** Flexbox: `display: flex; justify-content: center; align-items: center;`. Absolute: `position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%)`.

### Question 5: What are CSS selectors?

**Answer:** Selectors target elements: element, class `.`, id `#`, attribute `[attr]`, pseudo `:hover`.

### Question 6: Explain specificity in CSS.

**Answer:** Specificity determines which rule applies. Inline > id > class > element.

### Question 7: What are CSS animations?

**Answer:** `@keyframes` define animation, `animation` property applies. Example:

```css
@keyframes slide {
  from {
    left: 0;
  }
  to {
    left: 100px;
  }
}
div {
  animation: slide 2s;
}
```

### Question 8: How do you handle responsive design?

**Answer:** Media queries: `@media (max-width: 600px) { ... }`. Flexible units: %, em, rem, vw.

### Question 9: What is the difference between em and rem?

**Answer:** `em` relative to parent font-size, `rem` to root.

### Question 10: Explain CSS preprocessors like Sass.

**Answer:** Sass extends CSS with variables, nesting, mixins. Example:

```scss
$primary: blue;
.button {
  color: $primary;
}
```

### Question 11: What are pseudo-elements and pseudo-classes?

**Answer:** Pseudo-classes `:hover`, pseudo-elements `::before` for styling parts.

### Question 12: How do you create a CSS triangle?

**Answer:** Use borders: `width: 0; height: 0; border-left: 50px solid transparent; border-right: 50px solid transparent; border-bottom: 100px solid red;`

### Question 13: What is z-index?

**Answer:** Z-index controls stacking order. Higher values on top.

### Question 14: Explain CSS transitions.

**Answer:** Transitions animate property changes. `transition: property duration;`

### Question 15: What are CSS variables?

**Answer:** Custom properties: `--var: value;`, use `var(--var)`.

### Question 16: How do you optimize CSS?

**Answer:** Minify, remove unused, use shorthand, avoid deep selectors.

### Question 17: What is BEM methodology?

**Answer:** Block Element Modifier: `.block__element--modifier` for naming.

### Question 18: Explain CSS-in-JS.

**Answer:** Libraries like styled-components write CSS in JS. Example:

```jsx
const Button = styled.button`
  color: red;
`;
```

### Question 19: What are CSS frameworks like Bootstrap?

**Answer:** Frameworks provide pre-built components. Bootstrap uses classes for grids, buttons.

### Question 20: How do you handle CSS for print?

**Answer:** `@media print { ... }` for print styles.

### Question 21: What is the difference between display: none and visibility: hidden?

**Answer:** `display: none` removes from layout, `visibility: hidden` hides but occupies space.

### Question 22: Explain CSS floats.

**Answer:** Floats position elements left/right. Use `float: left;`, clear with `clear: both;`.

## Accessibility

### Question 1: What is web accessibility?

**Answer:** Accessibility ensures websites usable by people with disabilities. Follow WCAG guidelines.

### Question 2: Explain ARIA roles.

**Answer:** ARIA attributes enhance semantics. `role="button"` for custom buttons.

### Question 3: What are screen readers?

**Answer:** Software that reads content aloud for visually impaired users.

### Question 4: How do you make images accessible?

**Answer:** Use `alt` attribute. Decorative images: `alt=""`.

### Question 5: What is focus management?

**Answer:** Ensure keyboard navigation. Use `tabindex`, manage focus in modals.

### Question 6: Explain color contrast.

**Answer:** Sufficient contrast between text and background for readability.

### Question 7: What are skip links?

**Answer:** Links to skip navigation. `<a href="#main">Skip to main content</a>`

### Question 8: How do you handle forms for accessibility?

**Answer:** Use `<label>`, `aria-describedby` for errors.

### Question 9: What is the lang attribute?

**Answer:** `<html lang="en">` specifies language for screen readers.

### Question 10: Explain heading hierarchy.

**Answer:** Use `<h1>` to `<h6>` in order for structure.

### Question 11: What are landmarks in HTML?

**Answer:** `<main>`, `<nav>`, `<aside>` for navigation.

### Question 12: How do you test accessibility?

**Answer:** Use tools like Lighthouse, axe, screen readers.

### Question 13: What is the tabindex attribute?

**Answer:** Controls tab order. `tabindex="0"` for focusable, `-1` for programmatic.

### Question 14: Explain live regions.

**Answer:** `aria-live` announces dynamic content changes.

### Question 15: What are accessible modals?

**Answer:** Trap focus, close with Escape, announce opening.

### Question 16: How do you handle videos for accessibility?

**Answer:** Provide captions, transcripts, audio descriptions.

### Question 17: What is the role of alt text in SVGs?

**Answer:** Use `<title>` and `<desc>` in SVG.

### Question 18: Explain keyboard navigation.

**Answer:** Ensure all interactive elements reachable with Tab, operable with Enter/Space.

### Question 19: What are ARIA labels?

**Answer:** `aria-label` provides accessible name.

### Question 20: How do you make tables accessible?

**Answer:** Use `<th>`, `scope` attribute.

### Question 21: What is the difference between aria-hidden and display: none?

**Answer:** `aria-hidden="true"` hides from screen readers, `display: none` hides visually and from readers.

### Question 22: Explain inclusive design.

**Answer:** Design for diverse users from start.

## Security

### Question 1: What is XSS and how to prevent it?

**Answer:** Cross-Site Scripting injects malicious scripts. Prevent: Sanitize input, use CSP, escape output.

### Question 2: Explain CSRF.

**Answer:** Cross-Site Request Forgery tricks user into unwanted actions. Prevent: CSRF tokens, SameSite cookies.

### Question 3: What is Content Security Policy (CSP)?

**Answer:** CSP restricts resource loading. `<meta http-equiv="Content-Security-Policy" content="default-src 'self'">`

### Question 4: How do you secure cookies?

**Answer:** Use `HttpOnly`, `Secure`, `SameSite` flags.

### Question 5: What is HTTPS and why use it?

**Answer:** HTTPS encrypts data. Prevents man-in-the-middle. Use SSL certificates.

### Question 6: Explain SQL injection in frontend context.

**Answer:** Though backend, frontend should validate input. Use prepared statements on server.

### Question 7: What are security headers?

**Answer:** Headers like X-Frame-Options, X-Content-Type-Options prevent attacks.

### Question 8: How do you handle sensitive data?

**Answer:** Never store in localStorage. Use secure storage, encrypt.

### Question 9: What is clickjacking?

**Answer:** Tricking users into clicking hidden elements. Prevent with X-Frame-Options.

### Question 10: Explain CORS.

**Answer:** Cross-Origin Resource Sharing controls cross-domain requests. Server sets headers.

### Question 11: What is the principle of least privilege?

**Answer:** Grant minimal permissions needed.

### Question 12: How do you validate user input?

**Answer:** Client-side with regex, server-side validation.

### Question 13: What are security audits?

**Answer:** Regular checks for vulnerabilities using tools like OWASP.

### Question 14: Explain password security.

**Answer:** Use strong passwords, hash with bcrypt, enforce policies.

### Question 15: What is two-factor authentication?

**Answer:** Adds second verification layer.

### Question 16: How do you handle API keys?

**Answer:** Store securely, not in code. Use environment variables.

### Question 17: What is a man-in-the-middle attack?

**Answer:** Attacker intercepts communication. Prevent with HTTPS.

### Question 18: Explain session management.

**Answer:** Secure sessions with timeouts, regeneration.

### Question 19: What are security best practices for forms?

**Answer:** Validate, sanitize, use POST for sensitive data.

### Question 20: How do you prevent brute force attacks?

**Answer:** Rate limiting, CAPTCHA.

### Question 21: What is the OWASP Top 10?

**Answer:** List of top web vulnerabilities.

### Question 22: Explain secure coding practices.

**Answer:** Input validation, error handling, least privilege.

## Performance Optimization

### Question 1: What is critical rendering path?

**Answer:** Steps to render page: HTML, CSS, JS parsing, rendering.

### Question 2: How do you optimize images?

**Answer:** Compress, use WebP, lazy load, responsive images.

### Question 3: Explain code splitting.

**Answer:** Split code into chunks. Use dynamic imports.

### Question 4: What is lazy loading?

**Answer:** Load resources on demand. For images: `loading="lazy"`.

### Question 5: How do you minimize render-blocking resources?

**Answer:** Inline critical CSS, defer JS, async scripts.

### Question 6: What is the PRPL pattern?

**Answer:** Push critical, Render initial, Pre-cache, Lazy load.

### Question 7: Explain caching strategies.

**Answer:** Browser cache, CDN, service workers for PWA.

### Question 8: How do you optimize JavaScript?

**Answer:** Minify, tree shake, avoid global variables.

### Question 9: What is the impact of large DOM?

**Answer:** Slows rendering. Keep DOM small, virtualize lists.

### Question 10: Explain bundle analysis.

**Answer:** Use tools like webpack-bundle-analyzer to identify large chunks.

### Question 11: What are performance budgets?

**Answer:** Limits on bundle size, load times.

### Question 12: How do you handle long tasks?

**Answer:** Break into smaller tasks, use web workers.

### Question 13: What is the RAIL model?

**Answer:** Response <100ms, Animation 16ms, Idle <50ms, Load <1s.

### Question 14: Explain server-side rendering benefits.

**Answer:** Faster initial load, better SEO.

### Question 15: How do you optimize fonts?

**Answer:** Use font-display: swap, preload, subset.

### Question 16: What is the purpose of preloading?

**Answer:** `<link rel="preload" href="script.js">` loads critical resources early.

### Question 17: Explain the use of CDN.

**Answer:** Content Delivery Network caches and serves from nearest server.

### Question 18: How do you measure performance?

**Answer:** Use Lighthouse, Web Vitals, Performance API.

### Question 19: What are Core Web Vitals?

**Answer:** LCP, FID, CLS for user experience.

### Question 20: How do you optimize for mobile?

**Answer:** Responsive design, touch events, minimize network.

### Question 21: Explain the impact of third-party scripts.

**Answer:** Can slow down. Load asynchronously, lazy load.

### Question 22: What is progressive enhancement?

**Answer:** Build basic functionality first, enhance with JS.

## Build Optimization

### Question 1: What is Webpack?

**Answer:** Module bundler. Configures entry, output, loaders, plugins.

### Question 2: Explain Babel.

**Answer:** Transpiles modern JS to compatible versions.

### Question 3: What are loaders in Webpack?

**Answer:** Transform files. E.g., babel-loader for JS.

### Question 4: How do you set up a build pipeline?

**Answer:** Use Webpack, scripts in package.json.

### Question 5: What is tree shaking?

**Answer:** Removes unused code from bundles.

### Question 6: Explain code minification.

**Answer:** Reduces file size by removing whitespace, renaming variables.

### Question 7: What are source maps?

**Answer:** Map minified code to original for debugging.

### Question 8: How do you handle environment variables?

**Answer:** Use webpack.DefinePlugin or dotenv.

### Question 9: What is hot module replacement?

**Answer:** Updates modules without full reload.

### Question 10: Explain asset optimization.

**Answer:** Compress images, fonts in build.

### Question 11: What are build tools like Vite?

**Answer:** Fast build tool with ES modules.

### Question 12: How do you configure multiple environments?

**Answer:** Different configs for dev/prod.

### Question 13: What is the role of package.json?

**Answer:** Defines dependencies, scripts.

### Question 14: Explain npm scripts.

**Answer:** Run commands like "build": "webpack".

### Question 15: What is CI/CD for frontend?

**Answer:** Automate build, test, deploy.

### Question 16: How do you optimize bundle size?

**Answer:** Tree shake, split chunks, lazy load.

### Question 17: What are plugins in Webpack?

**Answer:** Extend functionality, e.g., HtmlWebpackPlugin.

### Question 18: Explain the difference between dev and prod builds.

**Answer:** Dev: source maps, hot reload. Prod: minified, optimized.

### Question 19: How do you handle polyfills?

**Answer:** Use core-js, babel-polyfill for older browsers.

### Question 20: What is the purpose of a build tool?

**Answer:** Automate compilation, bundling, optimization.

### Question 21: Explain module resolution.

**Answer:** How bundler finds modules.

### Question 22: How do you debug build issues?

**Answer:** Check console, use --verbose, inspect bundles.

## Other Important Related Topics

### Question 1: What is the DOM?

**Answer:** Document Object Model, tree representation of HTML.

### Question 2: Explain the BOM.

**Answer:** Browser Object Model, window, navigator, etc.

### Question 3: What are Web APIs?

**Answer:** APIs like Geolocation, Web Storage, Canvas.

### Question 4: How does localStorage work?

**Answer:** Stores key-value pairs persistently. `localStorage.setItem('key', 'value')`.

### Question 5: What is sessionStorage?

**Answer:** Similar to localStorage but per session.

### Question 6: Explain the Fetch API vs XMLHttpRequest.

**Answer:** Fetch is promise-based, modern. XHR is callback-based.

### Question 7: What are service workers?

**Answer:** Scripts for caching, background sync in PWAs.

### Question 8: How do you implement PWA?

**Answer:** Manifest, service worker, HTTPS.

### Question 9: What is Git and basic commands?

**Answer:** Version control. `git add`, `git commit`, `git push`.

### Question 10: Explain branching in Git.

**Answer:** `git branch`, `git checkout` for parallel development.

### Question 11: What are pull requests?

**Answer:** Propose changes for review.

### Question 12: How do you handle merge conflicts?

**Answer:** Edit files, `git add`, `git commit`.

### Question 13: What is testing in frontend?

**Answer:** Unit, integration, e2e with Jest, Cypress.

### Question 14: Explain TDD.

**Answer:** Test-Driven Development: write test first.

### Question 15: What are package managers?

**Answer:** npm, yarn for dependencies.

### Question 16: How do you manage dependencies?

**Answer:** `npm install`, check for vulnerabilities.

### Question 17: What is TypeScript?

**Answer:** Superset of JS with types. `let x: number = 5;`

### Question 18: Explain type inference.

**Answer:** TS infers types automatically.

### Question 19: What are interfaces in TS?

**Answer:** Define object shapes. `interface User { name: string; }`

### Question 20: How do you handle errors in async code?

**Answer:** Try/catch with async/await.

### Question 21: What is the event delegation?

**Answer:** Attach listener to parent, handle for children.

### Question 22: Explain the observer pattern.

**Answer:** Objects subscribe to events. Example: EventEmitter.

### Question 23: What is the difference between == and === in JavaScript?

**Answer:** == performs type coercion, === does not. For example, 1 == '1' is true, but 1 === '1' is false.

### Question 24: How does JavaScript handle asynchronous operations?

**Answer:** Using callbacks, promises, and async/await. Example:

```javascript
async function fetchData() {
  const data = await fetch("/api/data");
  return data.json();
}
```

### Question 25: What are closures in JavaScript?

**Answer:** Functions that remember their outer scope. Example:

```javascript
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}
const counter = outer();
console.log(counter()); // 1
```

### Question 26: Explain the prototype chain.

**Answer:** Objects inherit from prototypes. Example: Array.prototype.map.

### Question 27: What is the 'this' keyword in JavaScript?

**Answer:** Refers to the current execution context. In methods, it's the object; in functions, it's global or undefined in strict mode.

### Question 28: How do you create a deep copy of an object?

**Answer:** Using JSON.parse(JSON.stringify(obj)) or libraries like Lodash. But beware of functions and circular references.

### Question 29: What are ES6 modules?

**Answer:** import and export syntax for modular code. Example:

```javascript
// module.js
export const pi = 3.14;

// main.js
import { pi } from "./module.js";
```

### Question 30: Explain the difference between let, const, and var.

**Answer:** var is function-scoped, let and const are block-scoped. const cannot be reassigned.

### Question 31: What is the purpose of the 'use strict' directive?

**Answer:** Enables strict mode, catching common errors like undeclared variables.

### Question 32: How do you handle errors in JavaScript?

**Answer:** Using try-catch blocks. Example:

```javascript
try {
  riskyCode();
} catch (error) {
  console.error(error);
}
```

### Question 33: What are promises in JavaScript?

**Answer:** Objects representing asynchronous operations. States: pending, fulfilled, rejected.

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done"), 1000);
});
```

### Question 34: Explain async/await.

**Answer:** Syntactic sugar over promises for cleaner async code.

### Question 35: What is the event loop in JavaScript?

**Answer:** Mechanism for handling asynchronous callbacks. Call stack, web APIs, callback queue.

### Question 36: How do you optimize JavaScript performance?

**Answer:** Minimize DOM manipulations, use efficient algorithms, lazy loading, code splitting.

### Question 37: What are web workers?

**Answer:** Run scripts in background threads. Example:

```javascript
const worker = new Worker("worker.js");
worker.postMessage("start");
```

### Question 38: Explain the same-origin policy.

**Answer:** Security policy restricting cross-origin requests. CORS allows controlled access.

### Question 39: What is JSON and how is it used?

**Answer:** JavaScript Object Notation for data exchange. Methods: JSON.parse(), JSON.stringify().

### Question 40: How do you debug JavaScript code?

**Answer:** Using browser dev tools, console.log, breakpoints, debugger statement.

### Question 41: What are higher-order functions?

**Answer:** Functions that take other functions as arguments or return them. Example: map, filter.

### Question 42: Explain currying in JavaScript.

**Answer:** Transforming a function with multiple arguments into a sequence of functions with single arguments.

```javascript
const add = (a) => (b) => a + b;
const add5 = add(5);
console.log(add5(3)); // 8
```

### Question 43: What is the difference between null and undefined?

**Answer:** undefined means not assigned, null is an assigned empty value.

### Question 44: How do you check if a variable is an array?

**Answer:** Array.isArray(arr) or arr instanceof Array.

### Question 45: What are template literals?

**Answer:** String literals with interpolation. Example: `Hello ${name}!`

### Question 46: Explain destructuring assignment.

**Answer:** Extract values from arrays/objects. Example:

```javascript
const [a, b] = [1, 2];
const { name } = { name: "John" };
```

### Question 47: What is the spread operator?

**Answer:** Expands iterables. Example: [...arr1, ...arr2]

### Question 48: How do you handle memory leaks in JavaScript?

**Answer:** Avoid global variables, clean up event listeners, use weak references.

### Question 49: What are generators in JavaScript?

**Answer:** Functions that can pause and resume. Example:

```javascript
function* generator() {
  yield 1;
  yield 2;
}
```

### Question 50: Explain the module pattern.

**Answer:** Encapsulate code using IIFEs. Example:

```javascript
const module = (function () {
  let privateVar = "secret";
  return {
    getVar: () => privateVar,
  };
})();
```

### Question 51: What is the difference between synchronous and asynchronous code?

**Answer:** Sync blocks execution, async allows other code to run.

### Question 52: How do you implement debouncing?

**Answer:** Delay function execution. Example:

```javascript
function debounce(func, delay) {
  let timeout;
  return function (...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), delay);
  };
}
```

### Question 53: What is throttling?

**Answer:** Limit function calls. Example:

```javascript
function throttle(func, limit) {
  let inThrottle;
  return function (...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
}
```

### Question 54: Explain the concept of immutability.

**Answer:** Data that cannot be changed after creation. Use Object.freeze or libraries like Immutable.js.

### Question 55: What are service workers?

**Answer:** Scripts running in the background for caching, offline support.

### Question 56: How do you implement lazy loading?

**Answer:** Load resources only when needed. For images: <img loading="lazy">

### Question 57: What is the virtual DOM in React?

**Answer:** Lightweight copy of the real DOM for efficient updates.

### Question 58: Explain React's reconciliation process.

**Answer:** Diffing algorithm to update only changed parts.

### Question 59: What are controlled vs uncontrolled components?

**Answer:** Controlled: state managed by React; Uncontrolled: DOM manages state.

### Question 60: How do you optimize React performance?

**Answer:** Use React.memo, useMemo, useCallback, avoid unnecessary renders.

### Question 61: What is Redux and why use it?

**Answer:** State management library. Predictable state with actions/reducers.

### Question 62: Explain the flux pattern.

**Answer:** Unidirectional data flow: Action -> Dispatcher -> Store -> View.

### Question 63: What are custom hooks in React?

**Answer:** Reusable logic extracted into hooks. Example:

```jsx
function useCounter(initial) {
  const [count, setCount] = useState(initial);
  return [count, () => setCount(count + 1)];
}
```

### Question 64: How do you handle forms in React?

**Answer:** Controlled components with onChange handlers.

### Question 65: What is the context API?

**Answer:** Pass data without prop drilling. Example:

```jsx
const ThemeContext = React.createContext();
```

### Question 66: Explain error boundaries in React.

**Answer:** Catch JavaScript errors in component tree.

### Question 67: What are portals in React?

**Answer:** Render children into a different DOM node.

### Question 68: How do you test React components?

**Answer:** Using Jest and React Testing Library.

### Question 69: What is Next.js?

**Answer:** React framework for SSR, SSG.

### Question 70: Explain server-side rendering.

**Answer:** Render on server for faster initial load.

### Question 71: What is CSS-in-JS?

**Answer:** Write CSS in JavaScript. Libraries: styled-components.

### Question 72: How do you implement responsive design?

**Answer:** Media queries, flexbox, grid.

### Question 73: What are CSS preprocessors?

**Answer:** Sass, Less for advanced features.

### Question 74: Explain the box model.

**Answer:** Content, padding, border, margin.

### Question 75: How do you center an element?

**Answer:** Flexbox: display: flex; justify-content: center; align-items: center;

### Question 76: What is the difference between inline and block elements?

**Answer:** Inline: no line break; Block: full width, line break.

### Question 77: Explain CSS specificity.

**Answer:** Rules for which styles apply: inline > id > class > element.

### Question 78: What are pseudo-classes and pseudo-elements?

**Answer:** :hover, ::before.

### Question 79: How do you animate in CSS?

**Answer:** @keyframes, transition, animation properties.

### Question 80: What is accessibility in web development?

**Answer:** Making sites usable for all, including disabled users.

### Question 81: How do you implement ARIA attributes?

**Answer:** role, aria-label for screen readers.

### Question 82: What is semantic HTML?

**Answer:** Using meaningful tags like <header>, <nav>.

### Question 83: Explain the importance of alt text.

**Answer:** Describes images for screen readers.

### Question 84: How do you ensure keyboard navigation?

**Answer:** tabindex, focus management.

### Question 85: What are security concerns in frontend?

**Answer:** XSS, CSRF, injection attacks.

### Question 86: How do you prevent XSS?

**Answer:** Sanitize input, use Content Security Policy.

### Question 87: What is HTTPS and why use it?

**Answer:** Secure HTTP, encrypts data.

### Question 88: Explain CORS.

**Answer:** Cross-Origin Resource Sharing for safe cross-domain requests.

### Question 89: How do you optimize performance?

**Answer:** Minify code, compress images, use CDN.

### Question 90: What is code splitting?

**Answer:** Split bundle into chunks for faster loading.

### Question 91: Explain lazy loading.

**Answer:** Load resources on demand.

### Question 92: What are critical rendering path optimizations?

**Answer:** Minimize render-blocking resources.

### Question 93: How do you measure performance?

**Answer:** Lighthouse, Web Vitals.

### Question 94: What is tree shaking?

**Answer:** Remove unused code from bundles.

### Question 95: Explain webpack and its role.

**Answer:** Module bundler for building assets.

### Question 96: What are build tools?

**Answer:** Webpack, Vite, Parcel.

### Question 97: How do you set up CI/CD for frontend?

**Answer:** GitHub Actions, Jenkins for automated builds/tests.

### Question 98: What is version control?

**Answer:** Git for tracking changes.

### Question 99: Explain Git workflow.

**Answer:** Branch, commit, push, pull request.

### Question 100: How do you handle large codebases?

**Answer:** Modular architecture, code splitting, micro-frontends.

### Question 101: What are design patterns in frontend?

**Answer:** Singleton, Observer, Factory.

### Question 102: Explain MVC in frontend context.

**Answer:** Model-View-Controller for separation of concerns.

### Question 103: What is the difference between SPA and MPA?

**Answer:** Single Page App: one page; Multi Page App: multiple pages.

### Question 104: How do you implement routing in SPAs?

**Answer:** React Router, Vue Router.

### Question 105: What are PWAs?

**Answer:** Progressive Web Apps: offline, installable.

### Question 106: Explain service workers in PWAs.

**Answer:** Handle caching, background sync.

### Question 107: What is the manifest file in PWAs?

**Answer:** Defines app metadata for installation.

### Question 108: How do you handle state in SPAs?

**Answer:** Local state, global state with Redux/Zustand.

### Question 109: What are micro-frontends?

**Answer:** Break monolith into smaller apps.

### Question 110: Explain the JAMstack.

**Answer:** JavaScript, APIs, Markup for fast sites.

### Question 111: What is headless CMS?

**Answer:** Content management without frontend.

### Question 112: How do you integrate APIs in frontend?

**Answer:** Fetch, Axios for HTTP requests.

### Question 113: What is GraphQL?

**Answer:** Query language for APIs.

### Question 114: Explain REST vs GraphQL.

**Answer:** REST: resource-based; GraphQL: flexible queries.

### Question 115: How do you handle authentication?

**Answer:** JWT, OAuth.

### Question 116: What is OAuth?

**Answer:** Authorization framework.

### Question 117: Explain JWT.

**Answer:** JSON Web Tokens for secure data transmission.

### Question 118: How do you secure API keys?

**Answer:** Environment variables, never in client code.

### Question 119: What are web sockets?

**Answer:** Real-time communication protocol.

### Question 120: How do you implement real-time features?

**Answer:** WebSockets, Socket.io.

### Question 121: What is the DOM?

**Answer:** Document Object Model: tree representation of HTML.

### Question 122: How do you manipulate the DOM?

**Answer:** document.getElementById, addEventListener.

### Question 123: What is the difference between innerHTML and textContent?

**Answer:** innerHTML includes HTML tags, textContent does not.

### Question 124: Explain event bubbling and capturing.

**Answer:** Bubbling: inner to outer; Capturing: outer to inner.

### Question 125: How do you prevent default behavior?

**Answer:** event.preventDefault().

### Question 126: What are custom events?

**Answer:** User-defined events with new CustomEvent().

### Question 127: How do you handle multiple events?

**Answer:** Event delegation.

### Question 128: What is the Shadow DOM?

**Answer:** Encapsulated DOM subtree.

### Question 129: Explain web components.

**Answer:** Custom elements, shadow DOM, templates.

### Question 130: What is the difference between cookies, localStorage, and sessionStorage?

**Answer:** Cookies: server/client; localStorage: persistent; sessionStorage: session-only.

### Question 131: How do you store data locally?

**Answer:** localStorage.setItem, IndexedDB for large data.

### Question 132: What is IndexedDB?

**Answer:** Low-level API for client-side storage.

### Question 133: How do you handle offline functionality?

**Answer:** Service workers, cache API.

### Question 134: What is the cache API?

**Answer:** Programmatic cache for requests/responses.

### Question 135: How do you implement push notifications?

**Answer:** Service workers, Notification API.

### Question 136: What is the geolocation API?

**Answer:** Get user's location.

### Question 137: How do you access the camera?

**Answer:** getUserMedia API.

### Question 138: What is the canvas API?

**Answer:** Draw graphics on the fly.

### Question 139: Explain the Web Audio API.

**Answer:** Process and synthesize audio.

### Question 140: What is the WebRTC?

**Answer:** Real-time communication, video calls.

### Question 141: How do you implement video calls?

**Answer:** WebRTC with peer-to-peer connections.

### Question 142: What is the File API?

**Answer:** Read/write files from web apps.

### Question 143: How do you handle file uploads?

**Answer:** <input type="file">, FormData.

### Question 144: What is the Drag and Drop API?

**Answer:** Enable drag and drop in web apps.

### Question 145: Explain the History API.

**Answer:** Manipulate browser history.

### Question 146: What is the Intersection Observer?

**Answer:** Observe element visibility.

### Question 147: How do you implement infinite scroll?

**Answer:** Intersection Observer for loading more content.

### Question 148: What is the Resize Observer?

**Answer:** Observe element size changes.

### Question 149: Explain the Mutation Observer.

**Answer:** Observe DOM changes.

### Question 150: What is the Performance API?

**Answer:** Measure performance metrics.

### Question 151: How do you profile performance?

**Answer:** Chrome DevTools, Performance tab.

### Question 152: What is the Network tab in DevTools?

**Answer:** Inspect network requests.

### Question 153: How do you debug CSS?

**Answer:** Inspect element, toggle styles.

### Question 154: What is the Console API?

**Answer:** Log messages, run commands.

### Question 155: How do you use breakpoints?

**Answer:** Pause execution at specific lines.

### Question 156: What is the Sources panel?

**Answer:** View and edit source code.

### Question 157: How do you test mobile responsiveness?

**Answer:** Device emulation in DevTools.

### Question 158: What is Lighthouse?

**Answer:** Audit tool for performance, accessibility.

### Question 159: How do you optimize images?

**Answer:** Compress, use WebP, lazy load.

### Question 160: What is the difference between JPG, PNG, SVG?

**Answer:** JPG: lossy; PNG: lossless; SVG: vector.

### Question 161: How do you implement dark mode?

**Answer:** CSS media query prefers-color-scheme.

### Question 162: What is CSS Grid?

**Answer:** 2D layout system.

### Question 163: Explain Flexbox.

**Answer:** 1D layout for flexible items.

### Question 164: How do you create a sticky header?

**Answer:** position: sticky;

### Question 165: What is z-index?

**Answer:** Control stacking order.

### Question 166: How do you handle CSS conflicts?

**Answer:** Use BEM, CSS modules.

### Question 167: What is Tailwind CSS?

**Answer:** Utility-first CSS framework.

### Question 168: Explain component libraries.

**Answer:** Pre-built UI components, e.g., Material-UI.

### Question 169: How do you customize Bootstrap?

**Answer:** Override CSS, use Sass variables.

### Question 170: What is the difference between libraries and frameworks?

**Answer:** Libraries: specific functionality; Frameworks: full structure.

### Question 171: How do you choose a frontend framework?

**Answer:** Based on project needs, team expertise.

### Question 172: What is Vue.js?

**Answer:** Progressive framework for UIs.

### Question 173: Explain Angular.

**Answer:** Full-fledged framework with TypeScript.

### Question 174: How do you migrate from one framework to another?

**Answer:** Incremental migration, rewrite components.

### Question 175: What is Svelte?

**Answer:** Compiler that generates vanilla JS.

### Question 176: Explain the virtual DOM in Vue.

**Answer:** Similar to React, efficient updates.

### Question 177: What are directives in Vue?

**Answer:** Special attributes like v-if, v-for.

### Question 178: How do you handle state in Vue?

**Answer:** Vuex for global state.

### Question 179: What is the composition API in Vue 3?

**Answer:** Alternative to options API with better TypeScript support.

### Question 180: How do you test Vue components?

**Answer:** Vue Test Utils.

### Question 181: What is Angular's dependency injection?

**Answer:** Provide dependencies to components.

### Question 182: Explain Angular's change detection.

**Answer:** Zone.js tracks changes.

### Question 183: What are Angular guards?

**Answer:** Protect routes.

### Question 184: How do you optimize Angular apps?

**Answer:** OnPush change detection, lazy loading.

### Question 185: What is RxJS?

**Answer:** Reactive programming library.

### Question 186: How do you handle observables?

**Answer:** Subscribe, pipe operators.

### Question 187: What is the difference between Observable and Promise?

**Answer:** Observable: multiple values over time; Promise: single value.

### Question 188: How do you implement internationalization?

**Answer:** i18n libraries like react-i18next.

### Question 189: What is the difference between localization and internationalization?

**Answer:** i18n: design for multiple locales; l10n: adapt to specific locale.

### Question 190: How do you handle time zones?

**Answer:** Use libraries like moment.js or Intl.DateTimeFormat.

### Question 191: What is the WebAssembly?

**Answer:** Binary format for high-performance code.

### Question 192: How do you integrate WebAssembly?

**Answer:** Load .wasm files, call functions.

### Question 193: What is the difference between WebAssembly and JavaScript?

**Answer:** WebAssembly: low-level, fast; JS: high-level, flexible.

### Question 194: How do you handle browser compatibility?

**Answer:** Polyfills, transpilers like Babel.

### Question 195: What is the ECMAScript standard?

**Answer:** Specification for JavaScript.

### Question 196: How do you stay updated with frontend trends?

**Answer:** Follow blogs, conferences, newsletters.

### Question 197: What is the role of a frontend architect?

**Answer:** Design system architecture, lead team.

### Question 198: How do you mentor junior developers?

**Answer:** Code reviews, pair programming, knowledge sharing.

### Question 199: What are soft skills for frontend developers?

**Answer:** Communication, problem-solving, adaptability.

### Question 200: How do you prepare for interviews?

**Answer:** Practice coding, review fundamentals, mock interviews.

## Key Definitions

Here are concise definitions of key terms covered in the questions, presented in a professional manner:

- **React**: A declarative, efficient, and flexible JavaScript library for building user interfaces, enabling component-based development with a virtual DOM for optimal performance.
- **JSX**: A syntax extension for JavaScript that allows writing HTML-like code in React components, transpiled to React.createElement calls for seamless integration.
- **Hooks**: Functions in React that enable state and lifecycle management in functional components, promoting cleaner, more reusable code without classes.
- **Virtual DOM**: A lightweight in-memory representation of the real DOM, used by React to compute minimal updates and improve rendering efficiency.
- **Component Lifecycle**: Phases in a React class component's existence (mounting, updating, unmounting), managed via methods like componentDidMount for side effects.
- **State Management**: Handling data that changes over time in applications, often using tools like Redux for predictable, centralized state in complex apps.
- **Props**: Immutable data passed from parent to child components in React, enabling communication and customization without direct mutation.
- **Context API**: A React feature for sharing state across the component tree without prop drilling, ideal for themes or global settings.
- **Redux**: A predictable state container for JavaScript apps, using actions, reducers, and a store to manage complex state logic.
- **JavaScript**: A high-level, interpreted programming language that enables dynamic web content, with features like asynchronous programming via promises and async/await.
- **ES6/ES2015**: A major update to JavaScript introducing features like arrow functions, template literals, destructuring, and modules for modern development.
- **Closures**: Functions that retain access to their lexical scope, enabling data privacy and powerful patterns like factory functions.
- **Promises**: Objects representing the eventual completion or failure of asynchronous operations, chaining with .then() and .catch() for cleaner async code.
- **Async/Await**: Syntactic sugar over promises, allowing asynchronous code to be written synchronously, improving readability and error handling.
- **Event Loop**: JavaScript's concurrency model, managing the call stack, web APIs, and callback queue to handle asynchronous operations without blocking.
- **Prototype Chain**: JavaScript's inheritance mechanism where objects inherit properties and methods from their prototypes, forming a chain up to Object.prototype.
- **Hoisting**: JavaScript behavior where variable and function declarations are moved to the top of their scope during compilation, affecting execution order.
- **Strict Mode**: A restricted variant of JavaScript that catches common errors and enforces better coding practices, enabled with 'use strict'.
- **Modules**: Reusable pieces of code in JavaScript, imported/exported using ES6 syntax for better organization and dependency management.
- **Destructuring**: A convenient way to extract values from arrays or objects into variables, simplifying code and improving readability.
- **Spread Operator**: Syntax for expanding iterables (arrays/objects) into individual elements, useful for copying, merging, and function arguments.
- **Higher-Order Functions**: Functions that take other functions as arguments or return them, enabling functional programming patterns like map and filter.
- **Currying**: Transforming a function with multiple arguments into a sequence of functions each taking a single argument, for partial application.
- **Immutability**: The principle of not changing data after creation, using techniques like Object.freeze to prevent side effects and improve predictability.
- **Debouncing**: A technique to limit function calls by delaying execution until after a period of inactivity, optimizing performance for events like scrolling.
- **Throttling**: Limiting function execution to a maximum rate, ensuring actions like API calls occur at controlled intervals.
- **Web Workers**: Background scripts running in separate threads, allowing heavy computations without blocking the main UI thread.
- **Service Workers**: Event-driven scripts that run in the background, enabling features like caching, push notifications, and offline functionality.
- **Progressive Web Apps (PWAs)**: Web apps that offer native app-like experiences, including offline access, installability, and push notifications.
- **Single Page Application (SPA)**: A web app that loads a single HTML page and dynamically updates content, providing a smoother user experience.
- **Server-Side Rendering (SSR)**: Rendering web pages on the server before sending to the client, improving initial load times and SEO.
- **Static Site Generation (SSG)**: Pre-building pages at build time, resulting in fast, secure sites with minimal server load.
- **CSS-in-JS**: Writing CSS styles within JavaScript, often using libraries like styled-components for dynamic, scoped styling.
- **Responsive Design**: Designing websites to adapt to different screen sizes using media queries, flexbox, and grid layouts.
- **Flexbox**: A CSS layout model for one-dimensional layouts, providing flexible alignment and distribution of space.
- **CSS Grid**: A two-dimensional layout system for creating complex grid-based designs with precise control over rows and columns.
- **Accessibility (a11y)**: Ensuring web content is usable by people with disabilities, following WCAG guidelines with semantic HTML and ARIA attributes.
- **Semantic HTML**: Using meaningful HTML elements like <header>, <nav>, and <article> to convey structure and improve accessibility.
- **ARIA Attributes**: Attributes that enhance accessibility by providing additional context to assistive technologies, such as aria-label.
- **Cross-Site Scripting (XSS)**: A security vulnerability where malicious scripts are injected into web pages, mitigated by input sanitization and CSP.
- **Content Security Policy (CSP)**: A security standard that helps prevent XSS by specifying allowed sources for content like scripts and styles.
- **Cross-Origin Resource Sharing (CORS)**: A mechanism allowing controlled access to resources from different origins, configured via server headers.
- **HTTPS**: Secure HTTP protocol using SSL/TLS encryption to protect data transmission between client and server.
- **Performance Optimization**: Techniques to improve web app speed, including code splitting, lazy loading, and minimizing render-blocking resources.
- **Code Splitting**: Dividing JavaScript bundles into smaller chunks loaded on demand, reducing initial load times.
- **Tree Shaking**: Removing unused code from bundles during build, minimizing file sizes and improving performance.
- **Lazy Loading**: Deferring loading of non-critical resources until needed, such as images or components below the fold.
- **Critical Rendering Path**: The sequence of steps browsers take to render a page, optimized by minimizing CSS/JS blocking and prioritizing above-the-fold content.
- **Webpack**: A static module bundler for modern JavaScript applications, handling asset compilation, optimization, and dependency management.
- **Babel**: A JavaScript transpiler converting modern ES6+ code to backward-compatible versions for older browsers.
- **Linting**: Analyzing code for potential errors and style issues using tools like ESLint, enforcing consistent coding standards.
- **Version Control**: Systems like Git for tracking changes, collaborating, and managing code history across teams.
- **Continuous Integration (CI)**: Automating build, test, and deployment processes to ensure code quality and rapid delivery.
- **Micro-frontends**: An architectural approach splitting monolithic frontends into smaller, independently deployable applications.
- **JAMstack**: A modern web development architecture using JavaScript, APIs, and pre-built Markup for fast, secure, and scalable sites.
- **GraphQL**: A query language for APIs allowing clients to request exactly the data needed, reducing over/under-fetching.
- **REST**: Representational State Transfer, an architectural style for designing networked applications with standard HTTP methods.
- **OAuth**: An open standard for authorization, enabling secure delegated access without sharing credentials.
- **JWT (JSON Web Tokens)**: Compact, URL-safe tokens for securely transmitting information between parties as JSON objects.
- **WebSockets**: A protocol for full-duplex communication over a single TCP connection, enabling real-time data exchange.
- **DOM (Document Object Model)**: A programming interface for web documents, representing the page structure as a tree of objects.
- **Shadow DOM**: A web standard for encapsulating DOM subtrees, enabling style and behavior isolation in web components.
- **Web Components**: A set of web platform APIs for creating reusable custom elements with encapsulated functionality.
- **Canvas API**: A JavaScript API for drawing graphics and animations on the fly within HTML <canvas> elements.
- **WebRTC**: A collection of APIs enabling real-time communication, including peer-to-peer video/audio calls in browsers.
- **Service Worker API**: An API allowing scripts to run in the background, intercepting network requests for caching and offline support.
- **Intersection Observer**: An API for asynchronously observing changes in the intersection of a target element with an ancestor or viewport.
- **Resize Observer**: An API for observing and reacting to changes in the size of DOM elements.
- **Mutation Observer**: An API for watching changes to the DOM tree, such as additions, removals, or attribute changes.
- **Performance API**: A set of standards for measuring and monitoring web application performance, including timing and resource metrics.
- **Lighthouse**: An open-source tool for auditing web page quality, covering performance, accessibility, SEO, and best practices.
- **Web Vitals**: A set of metrics defined by Google to measure user experience quality, focusing on loading, interactivity, and visual stability.
- **IndexedDB**: A low-level API for client-side storage of significant amounts of structured data in web browsers.
- **LocalStorage/SessionStorage**: Web storage APIs for storing key-value pairs locally, with localStorage persisting across sessions.
- **Geolocation API**: An API for retrieving the user's geographical location, with permission-based access.
- **File API**: A set of APIs for reading and manipulating files from web applications, including drag-and-drop and file input handling.
- **Notification API**: An API for displaying notifications to users, often used with service workers for push notifications.
- **Web Audio API**: An API for processing and synthesizing audio in web applications, enabling advanced audio manipulation.
- **WebAssembly (Wasm)**: A binary instruction format for a stack-based virtual machine, enabling high-performance execution of code in browsers.
- **Polyfills**: JavaScript code that implements modern web APIs in older browsers, ensuring cross-browser compatibility.
- **Transpilation**: Converting source code from one language or version to another, like ES6 to ES5 using Babel.
- **TypeScript**: A superset of JavaScript adding static typing, interfaces, and advanced features for scalable development.
- **Sass/SCSS**: CSS preprocessors extending CSS with variables, nesting, and mixins for more maintainable stylesheets.
- **Tailwind CSS**: A utility-first CSS framework providing low-level utility classes for rapid UI development.
- **Bootstrap**: A popular CSS framework offering responsive grid systems, components, and utilities for quick prototyping.
- **Material-UI**: A React component library implementing Google's Material Design principles for consistent UIs.
- **Vue.js**: A progressive JavaScript framework for building user interfaces with a gentle learning curve and reactive data binding.
- **Angular**: A comprehensive framework for building scalable web applications with TypeScript, dependency injection, and two-way data binding.
- **Svelte**: A compiler that generates optimized vanilla JavaScript from declarative components, eliminating virtual DOM overhead.
- **RxJS**: A library for reactive programming using observables, enabling complex asynchronous operations and event handling.
- **Zone.js**: A library used by Angular for change detection, intercepting asynchronous operations to trigger UI updates.
- **i18n (Internationalization)**: Designing software to support multiple languages and regions without code changes.
- **l10n (Localization)**: Adapting software for a specific locale, including translations and cultural adjustments.
- **Web Standards**: Specifications developed by organizations like W3C and WHATWG defining how web technologies should work.
- **Browser DevTools**: Built-in developer tools in browsers for debugging, profiling, and inspecting web applications.
- **ECMAScript**: The standard upon which JavaScript is based, defining the language's syntax, semantics, and libraries.
