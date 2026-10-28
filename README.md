React Made Simple • Beginner Guide Page 1
React Made Simple
A beginner-friendly guide to Components, Props, State, Hooks, Context API and React
Router
What you will learn
• How React breaks a website into reusable components.
• How props pass information and state stores changing information.
• How hooks such as useState, useEffect and useRef work.
• How Context API shares data without passing props through every level.
• How React Router displays different pages without a full browser reload.
How to use this guide: Read the concept, study the small code example, then try changing one thing yourself.
Examples use modern React function components and JavaScript.
Quick mental model
Component = a reusable piece of UI Props = information coming in State = information that can change
Hooks = React features used inside function components
React Made Simple • Beginner Guide Page 2
Contents
• 1. React in one minute
• 2. Components
• 3. Props
• 4. State and useState
• 5. Hooks: useEffect, useRef, useMemo, useCallback
• 6. Context API
• 7. React Router
• 8. How the concepts work together
• 9. Common mistakes and quick revision
1. React in one minute
React is a JavaScript library for building user interfaces. Instead of writing one huge page, you build small
components and combine them. When data changes, React updates the relevant UI.
Example: A shopping website might have Header, SearchBar, ProductCard, Cart and Footer components. Each
component has a clear job.
A tiny React component
function Welcome() {
 return <h1>Hello, React!</h1>;
}
export default Welcome;
The function returns JSX: HTML-like syntax written inside JavaScript. React uses it to describe what should appear
on the screen.
JSX basics
• Return one parent element, or wrap elements in a fragment: <> ... .
• Use className instead of HTML class.
• Use curly braces to insert JavaScript expressions: {2 + 2}.
• Component names start with a capital letter, such as Welcome or ProductCard.
2. Components
A component is a reusable function that describes part of the user interface. Components can be as small as a
button or as large as a complete page.
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
React Made Simple • Beginner Guide Page 3
Here, App uses Greeting twice. Change Greeting once and both instances use the updated component.
Component with a little structure
function ProductCard() {
 return (
 <article>
 <h2>Wireless Mouse</h2>
 <p>Price: ■799</p>
 <button>View product</button>
 </article>
 );
}
Good practice: Keep components focused, give them meaningful names, and extract repeated UI into reusable
components.
Remember: A component is used like a custom HTML tag: .
3. Props
Props (short for properties) are inputs passed from a parent component to a child component. They let the same
component display different information.
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
 <UserCard name="Ayesha" role="Frontend Developer" />
 <UserCard name="Rohan" role="Student" />
 </>
 );
}
The parent sends name and role. UserCard receives them and displays the values. The curly braces in the function
parameter use JavaScript destructuring.
Important rules for props
• Props flow from parent to child.
• Treat props as read-only; a child should not change its own props.
• Props can contain strings, numbers, arrays, objects, functions or JSX.
• Use props when a component needs information or a callback from its parent.
function SaveButton({ onSave }) {
 return <button onClick={onSave}>Save</button>;
}
function App() {
 function saveData() {
 alert("Saved!");
 }
 return <SaveButton onSave={saveData} />;
}
A function can be passed as a prop. This lets a child tell its parent that something happened.
4. State and useState
React Made Simple • Beginner Guide Page 4
State is a component's memory: data that can change over time and affect what appears on the screen. Examples
include a counter value, whether a menu is open, or items in a cart.
import { useState } from "react";
function Counter() {
 const [count, setCount] = useState(0);
 return (
 <section>
 <p>Count: {count}</p>
 <button onClick={() => setCount(count + 1)}>
 Add one
 </button>
 </section>
 );
}
Understand this line
const [count, setCount] = useState(0);
• count is the current state value.
• setCount is the function used to request a state update.
• 0 is the initial value.
• When state changes, React renders the component again so the UI can reflect the new value.
State vs props
Props State
Passed in by a parent. Owned by the component (or its state owner).
Read-only from the receiving component's point of view. Updated using its setter, such as setCount.
Useful for configuring reusable components. Useful for values that change over time.
Updating based on previous state: use the updater form when the next value depends on the previous value.
setCount(previousCount => previousCount + 1);
Do not mutate state objects or arrays directly. Create a new object or array instead.
5. Hooks
Hooks are special React functions that let function components use React features such as state, effects, refs and
context. Hook names usually start with use.
Rules of Hooks: call hooks at the top level of a React function component or custom hook. Do not call them inside
loops, conditions, or ordinary nested functions.
useEffect — synchronize with external systems
useEffect is commonly used for things such as fetching data, subscribing to events, or setting up a timer. It is not
needed for every calculation or button click.
import { useEffect, useState } from "react";
function Example() {
 const [message, setMessage] = useState("Loading...");
 useEffect(() => {
 document.title = "React Example";
 setMessage("Page is ready");
 }, []);
React Made Simple • Beginner Guide Page 5
 return <p>{message}</p>;
}
The empty dependency array [] means this effect runs after the component first mounts, with cleanup if provided. If you use reactive
values inside an effect, include the relevant dependencies. Effects may run an extra setup/cleanup cycle in development Strict Mode.
useRef — keep a value or access a DOM element
import { useRef } from "react";
function SearchBox() {
 const inputRef = useRef(null);
 function focusInput() {
 inputRef.current.focus();
 }
 return (
 <>
 <input ref={inputRef} placeholder="Search..." />
 <button onClick={focusInput}>Focus search</button>
 </>
 );
}
A ref can point to a DOM element. Changing ref.current does not trigger a re-render, so use state instead when a
change must update the UI.
useMemo and useCallback — performance tools
const sortedItems = useMemo(
 () => expensiveSort(items),
 [items]
);
const handleSave = useCallback(() => {
 saveItem(itemId);
}, [itemId]);
useMemo caches a calculated value; useCallback caches a function reference. They are optimization tools, not
requirements for every component. Start with clear code and add them when useful.
Custom hooks
function useOnlineStatus() {
 // Put reusable hook logic here.
 // Return the information the component needs.
}
A custom hook is a JavaScript function whose name starts with use and which can call other hooks. It helps share
logic between components; it does not automatically share one common state instance.
6. Context API
Context lets a parent make information available to many descendants without manually passing it through every
intermediate component. It is useful for app-wide or section-wide values such as theme, language or signed-in user
details.
Step 1: Create context
import { createContext, useContext } from "react";
const ThemeContext = createContext("light");
Step 2: Provide a value
function App() {
 return (
 <ThemeContext.Provider value="dark">
 <Toolbar />
React Made Simple • Beginner Guide Page 6
 </ThemeContext.Provider>
 );
}
function Toolbar() {
 return <ProfileButton />;
}
Step 3: Read the value where needed
function ProfileButton() {
 const theme = useContext(ThemeContext);
 return <button className={theme}>
 Theme: {theme}
 </button>;
}
The ProfileButton can read the nearest provider's value even though Toolbar does not receive or forward a theme
prop.
Modern React note: React 19 also supports <ThemeContext value="dark">... as a provider. The .Provider form shown above works in
earlier React versions too.
When should you use Context?
• Use it when many components need the same value.
• Keep state in a provider or parent and pass the value through Context.
• Avoid putting every tiny value into Context; props can be simpler for nearby components.
• Context is not a replacement for all state management or for server data-fetching tools.
7. React Router
React Router maps URL paths to components. It allows a React app to show different views—such as Home, About
and Contact—while navigating without loading a completely new HTML document for every internal route.
Install the package in your project terminal:
npm install react-router
For a typical browser app using current React Router declarative APIs, a basic setup can look like this:
import {
 BrowserRouter,
 Routes,
 Route,
 Link,
 useNavigate
} from "react-router";
function Home() {
 return <h1>Home page</h1>;
}
function About() {
 return <h1>About page</h1>;
}
function NotFound() {
 return <h1>Page not found</h1>;
}
function App() {
 return (
 <BrowserRouter>
 <nav>
 <Link to="/">Home</Link>{" "}
 <Link to="/about">About</Link>
React Made Simple • Beginner Guide Page 7
 </nav>
 <Routes>
 <Route path="/" element={<Home />} />
 <Route path="/about" element={<About />} />
 <Route path="*" element={<NotFound />} />
 </Routes>
 </BrowserRouter>
 );
}
In some existing projects or tutorials, imports come from react-router-dom. Follow the API and version used by your installed React
Router package; do not mix examples from different major versions.
What each router part does
• BrowserRouter: connects routing to the browser URL/history.
• Routes: chooses the matching route.
• Route: maps a path to an element/component.
• Link: navigates to a path without a full page reload.
• useNavigate: navigates programmatically, for example after saving a form.
• useParams: reads dynamic URL pieces such as a product ID.
Dynamic route example
<Route path="/products/:productId" element={<ProductDetails />} />
import { useParams } from "react-router";
function ProductDetails() {
 const { productId } = useParams();
 return <p>Product ID: {productId}</p>;
}
If the URL is /products/42, productId will be the string "42". Convert it to a number only if your logic needs a number.
Navigate after an action
function SaveAndGo() {
 const navigate = useNavigate();
 function handleSave() {
 // Save data here.
 navigate("/about");
 }
 return <button onClick={handleSave}>Save and continue</button>;
}
For production deployment, configure the host to serve your app's entry HTML for valid client-side routes. Otherwise,
refreshing a nested URL may return a server 404.
8. How everything works together
Imagine a product page. The route chooses the page, components build its UI, props provide product data, state
tracks the cart or selected quantity, hooks synchronize or manage React features, and Context can share the cart or
theme across distant components.
App (Router)
■■■ Header
■ ■■■ CartCount ← shared cart context
■■■ ProductPage
 ■■■ ProductCard ← props: name, price
 ■■■ Add button → state update
A practical decision guide
React Made Simple • Beginner Guide Page 8
• Need to reuse a section of UI? Create a component.
• Need to send data from parent to child? Use props.
• Need changing data that updates the screen? Use state.
• Need to synchronize with a timer, browser API or subscription? Consider useEffect.
• Need to share a value with many descendants? Consider Context.
• Need different UI for different URLs? Use React Router.
9. Common mistakes and quick revision
Mistakes to avoid
• Calling a component like a normal function instead of rendering it as .
• Changing props or mutating state directly.
• Calling hooks inside if statements, loops or event handlers.
• Using useEffect for calculations that can be done directly during render.
• Forgetting effect dependencies or cleanup for subscriptions/timers.
• Using Context when a simple prop would be clearer.
• Using a normal anchor for every internal route when React Router's Link is appropriate.
• Assuming React Router alone configures server fallback for deployed nested routes.
Fast revision
Term In one line
Component Reusable UI building block.
Props Inputs passed from parent to child.
State Changing data that can update the UI.
Hook Function that gives a component React capabilities.
useEffect Synchronizes with external systems.
useRef Stores a mutable reference or points to a DOM node.
Context API Shares a value with descendants without passing props at every level.
React Router Connects URL paths to UI views.
Practice tasks
• Build a ProfileCard component and pass name, college and skills through props.
• Create a counter with + and − buttons using useState.
• Make a show/hide password toggle using state.
• Use Context to switch between light and dark themes.
• Create Home, About and Contact routes with navigation links.
• Add a dynamic route such as /students/:studentId and display its ID.
You do not need to memorize every hook. Understand the problem each tool solves, write small examples, and check
the official documentation when you need details.
