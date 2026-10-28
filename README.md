# ⚛️ React Made Simple
### A Beginner-Friendly Guide to React Fundamentals

<p align="center">
  <img src="https://img.shields.io/badge/React-Basics-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React Basics" />
  <img src="https://img.shields.io/badge/Level-Beginner-2ea44f?style=for-the-badge" alt="Beginner Level" />
  <img src="https://img.shields.io/badge/Language-JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
</p>

Welcome to **React Made Simple**! 🚀

This repository contains easy-to-understand explanations, practical examples, and important concepts to help beginners learn React step by step.

---

## 📚 Table of Contents

1. [Introduction to React](#-1-introduction-to-react)
2. [Components](#-2-components)
3. [Props](#-3-props)
4. [State and useState](#-4-state-and-usestate)
5. [React Hooks](#-5-react-hooks)
6. [Context API](#-6-context-api)
7. [React Router](#-7-react-router)
8. [How Everything Works Together](#-8-how-everything-works-together)
9. [Common Mistakes](#-9-common-mistakes)
10. [Practice Tasks](#-10-practice-tasks)

---

## 💡 1. Introduction to React

React is a JavaScript library used to build interactive user interfaces.

Instead of building an entire website in one large file, React allows us to divide the UI into small, reusable pieces called **components**.

### Example

```jsx
function Welcome() {
  return <h1>Hello, React!</h1>;
}

export default Welcome;
```

### Why React?

- ♻️ Reusable components
- ⚡ Efficient UI updates
- 🧩 Organized code
- 🔄 State-driven interfaces
- 🌐 Suitable for modern web applications

---

## 🧩 2. Components

A component is a reusable piece of UI.

For example, a website may contain a Navbar, Footer, Product Card, and Login Form.

```jsx
function Greeting() {
  return <h2>Welcome back!</h2>;
}

function App() {
  return (
    <main>
      <Greeting />
      <Greeting />
    </main>
  );
}

export default App;
```

**Key points:**

- Component names start with a capital letter.
- Components are usually JavaScript functions.
- Components return JSX.
- Components can be reused wherever needed.

---

## 📦 3. Props

**Props** are used to pass information from a parent component to a child component.

Think of props as inputs to a function.

```jsx
function UserCard({ name, role }) {
  return (
    <section>
      <h2>{name}</h2>
      <p>{role}</p>
    </section>
  );
}

function App() {
  return (
    <>
      <UserCard
        name="Ayesha"
        role="Frontend Developer"
      />

      <UserCard
        name="Rohan"
        role="Student"
      />
    </>
  );
}
```

### Important points

- Props pass data from parent to child.
- Props should be treated as read-only.
- Different props allow the same component to display different information.
- Functions can also be passed as props.

---

## 🔢 4. State and useState

**State** stores information that can change while a component is being used.

Examples include counters, form inputs, menus, and shopping cart quantities.

### Example: Counter

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>

      <button
        onClick={() => setCount(previous => previous + 1)}
      >
        Add One
      </button>
    </div>
  );
}

export default Counter;
```

### Understanding the syntax

| Part | Meaning |
|---|---|
| `count` | Current state value |
| `setCount` | Function used to update state |
| `0` | Initial value |
| `useState()` | React Hook for state |

### Props vs State

| Props | State |
|---|---|
| Passed from a parent | Managed by the component or its owner |
| Read-only for the receiving component | Updated using a setter |
| Used to configure components | Used for changing information |

---

## 🪝 5. React Hooks

Hooks allow function components to use React features.

### `useState`

Manages state.

```jsx
const [name, setName] = useState("Alex");
```

### `useEffect`

Synchronizes a component with external systems, such as timers, subscriptions, or browser APIs.

```jsx
import { useEffect } from "react";

useEffect(() => {
  document.title = "React Basics";
}, []);
```

### `useRef`

Stores a mutable reference or points to a DOM element.

```jsx
import { useRef } from "react";

function SearchBox() {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} />

      <button onClick={() => inputRef.current.focus()}>
        Focus Input
      </button>
    </>
  );
}
```

### `useMemo`

Caches a calculated value when useful for performance.

```jsx
const result = useMemo(() => calculateValue(items), [items]);
```

### `useCallback`

Caches a function reference when useful for performance.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

### Rules of Hooks

- Call Hooks at the top level of a function component or custom Hook.
- Do not call Hooks inside loops or conditions.
- Hook names usually start with `use`.
- Use performance Hooks only when they provide a benefit.

---

## 🌍 6. Context API

Context API allows information to be shared with multiple components without passing props through every intermediate component.

It is useful for themes, language settings, and authenticated user information.

### Step 1: Create Context

```jsx
import { createContext } from "react";

const ThemeContext = createContext("light");
```

### Step 2: Provide a value

```jsx
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

### Step 3: Read the value

```jsx
import { useContext } from "react";

function Toolbar() {
  const theme = useContext(ThemeContext);

  return <h2>Current theme: {theme}</h2>;
}
```

### Why use Context API?

- Avoids unnecessary prop passing through intermediate components.
- Makes shared values easier to access.
- Useful when many components need the same information.

**Remember:** Props are often simpler when only a few nearby components need data.

---

## 🛣️ 7. React Router

React Router helps display different pages based on the URL without a full browser page reload for each internal navigation.

For example:

- `/` → Home
- `/about` → About
- `/contact` → Contact

### Install React Router

```bash
npm install react-router
```

### Example

```jsx
import {
  BrowserRouter,
  Routes,
  Route,
  Link
} from "react-router";

function Home() {
  return <h1>Home Page</h1>;
}

function About() {
  return <h1>About Page</h1>;
}

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        {" | "}
        <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

### Important Router Concepts

| Concept | Purpose |
|---|---|
| `BrowserRouter` | Connects routing to browser navigation |
| `Routes` | Selects the matching route |
| `Route` | Maps a URL path to a component |
| `Link` | Navigates between routes |
| `useNavigate` | Navigates programmatically |
| `useParams` | Reads dynamic URL parameters |

> **Note:** This example uses the current React Router declarative API. Older tutorials may use imports from `react-router-dom`. Follow the API version installed in your project.

---

## 🔗 8. How Everything Works Together

Imagine a shopping website:

```text
App
│
├── Header
│   └── CartCount
│
└── ProductPage
    └── ProductCard
        ├── Product Name (Props)
        ├── Product Price (Props)
        └── Add to Cart (State Update)
```

| Requirement | React Feature |
|---|---|
| Reuse a UI section | Components |
| Pass data to a component | Props |
| Update the UI when data changes | State |
| Use React features in functions | Hooks |
| Share information with descendants | Context API |
| Display different pages | React Router |

---

## ⚠️ 9. Common Mistakes

- ❌ Changing props directly.
- ❌ Modifying state arrays or objects directly.
- ❌ Calling Hooks inside conditions or loops.
- ❌ Using `useEffect` for every calculation.
- ❌ Forgetting effect dependencies or cleanup where needed.
- ❌ Using Context when ordinary props would be simpler.
- ❌ Forgetting server fallback configuration when deploying a routed SPA.

---

## 🧪 10. Practice Tasks

Try these exercises to strengthen your understanding:

- [ ] Create a reusable `ProfileCard` component.
- [ ] Pass a name, college, and skills using props.
- [ ] Build a counter using `useState`.
- [ ] Create a show/hide password feature.
- [ ] Build a light/dark theme using Context API.
- [ ] Create Home, About, and Contact routes.
- [ ] Create a dynamic route such as `/students/:studentId`.
- [ ] Build a small product listing page using all these concepts.

---

## 📖 Recommended Learning Resources

- [React Official Documentation](https://react.dev/)
- [React Learn](https://react.dev/learn)
- [React Router Documentation](https://reactrouter.com/)
- [JavaScript Guide — MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)

---

<p align="center">
  <b>Keep Learning. Keep Building. Keep Growing. 🚀</b>
  <br />
  Made for React beginners.
</p>
