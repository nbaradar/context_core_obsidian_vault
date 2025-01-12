>[!info] Quick Notes
>- **Functional Components** are the preferred modern approach (use 'function' keyword)
>- For **single-page applications (SPAs)**, you’ll likely use **React Router** for navigation
>- To **share state between components**, you often **"lift state up"** to a common parent.

---
## **What is React?**
- React is a **JavaScript library for building user interfaces**.
- It allows you to build UI components that are reusable and declarative.
	- In the context of React, "declarative" means that ==developers describe what the user interface (UI) should look like based on its current state, without explicitly stating how to achieve that state==; essentially, you tell React what you want the UI to be, and React handles the necessary updates to the DOM to make it happen, making the code more readable and maintainable.
- React is component-based and uses a **virtual DOM** to efficiently update the UI.

---
## **Core Concepts You Should Know**
#### **1. Components**
- **What**: Building blocks of a React application. Each piece of the UI (e.g., a button, form, or dropdown) is a component.
- **Types**:
    - **Functional Components** (modern approach, uses `function` keyword).
    - **Class Components** (older, less common in modern development).
- **Example**:
    
    ```jsx
    function Greeting() {
        return <h1>Hello, World!</h1>;
    }
    ```
#### **2. JSX**
- **What**: A syntax extension that lets you write HTML-like code in JavaScript.
- **Key Rules**:
    - Always return a **single parent element** (use a `<div>` or `<>` for grouping).
    - Use `{}` for embedding JavaScript expressions.
- **Example**:
    ```jsx
    function Greeting() {
        const name = "Nader";
        return <h1>Hello, {name}!</h1>;
    }
    ```
#### **3. Props**
- **What**: Short for "properties," these are inputs to components that allow them to be dynamic.
- **How**: Passed to components as attributes.
- **Example**:
    ```jsx
    function Greeting({ name }) {
        return <h1>Hello, {name}!</h1>;
    }
    
    // Usage
    <Greeting name="Nader" />
    ```
#### **4. State**
- **What**: A way to manage data within a component that can change over time (e.g., user input).
- **How**: In functional components, you use the `useState` hook.
- **Example**:
    ```jsx
    import React, { useState } from 'react';
    
    function Counter() {
        const [count, setCount] = useState(0);
    
        return (
            <div>
                <p>Count: {count}</p>
                <button onClick={() => setCount(count + 1)}>Increment</button>
            </div>
        );
    }
    ```
#### **5. Events**
- **What**: React handles DOM events using camelCase syntax (e.g., `onClick`, `onChange`).
- **Example**:
    ```jsx
    function Button() {
        function handleClick() {
            alert('Button clicked!');
        }
    
        return <button onClick={handleClick}>Click Me</button>;
    }
    ```
#### **6. Hooks**
- **What**: Special functions that let you "hook into" React features like state and lifecycle.
- **Common Hooks**:
    - `useState`: Manage local state.
    - `useEffect`: Handle side effects like fetching data.
- **Example** (`useEffect` for data fetching):
    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function App() {
        const [data, setData] = useState([]);
    
        useEffect(() => {
            fetch('https://api.example.com/data')
                .then((response) => response.json())
                .then((data) => setData(data));
        }, []); // Empty dependency array means it runs once after render
    
        return (
            <ul>
                {data.map((item) => (
                    <li key={item.id}>{item.name}</li>
                ))}
            </ul>
        );
    }
    ```
#### **7. Routing**
- For single-page applications (SPAs), you’ll likely use **React Router** for navigation.
- Example:    
    ```bash
    npm install react-router-dom
    ```

    ```jsx
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    
    function App() {
        return (
            <Router>
                <Switch>
                    <Route path="/" exact component={Home} />
                    <Route path="/about" component={About} />
                </Switch>
            </Router>
        );
    }
    ```
#### **8. Lifting State Up**
- To share state between components, you often "lift state up" to a common parent.
- **Example**:
    ```jsx
    function Parent() {
        const [value, setValue] = useState("");
    
        return (
            <div>
                <Input value={value} onChange={setValue} />
                <p>You typed: {value}</p>
            </div>
        );
    }
    
    function Input({ value, onChange }) {
        return (
            <input
                type="text"
                value={value}
                onChange={(e) => onChange(e.target.value)}
            />
        );
    }
    ```

---
## **React Workflow**
1. **Create Components**: Break down your UI into reusable pieces.
2. **Use Props and State**: Pass data between components using `props` and manage dynamic data using `state`.
3. **Fetch Data**: Use `useEffect` for API calls.
4. **Styling**:
    - Use plain CSS, a library like Tailwind, or CSS-in-JS solutions like `styled-components`.
5. **Test and Iterate**: Use tools like React DevTools to debug and improve.
---
