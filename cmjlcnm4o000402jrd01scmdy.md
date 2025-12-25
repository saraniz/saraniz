---
title: "Understanding React Components: A Beginner’s Guide"
datePublished: Thu Dec 25 2025 11:18:41 GMT+0000 (Coordinated Universal Time)
cuid: cmjlcnm4o000402jrd01scmdy
slug: understanding-react-components-a-beginners-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1766661458666/eb911db7-7c3a-422e-a22c-f25d32d09ef7.png
tags: javascript, reactjs, javascript-framework, components, reacthooks, react-componets, react-libraries

---

React is a popular JavaScript library for building user interfaces. At the heart of every React application are components. Components are reusable, independent pieces of code that define what appears on the screen and how it behaves. Understanding components is essential for creating organized, efficient, and maintainable React applications.

## What Are React Components?

A React component is a **self-contained block of code** that can be a **function** or a **class**. Each component handles its own **logic** and **UI rendering**. Components can receive **inputs** called **props** and manage **dynamic data** using **state**.

‘prop’ stands for properties. They are used to pass data from parent component to child component. And also they are read-only. That means child components cannot change them. Props are used to make components reusable because the same component can behave differently depending on the props.

```javascript
//component
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Using the component
<Greeting name="Amie" />
<Greeting name="John" />
```

Here, `name` is a prop. The `Greeting` component can display different names depending on what is passed.

State is a special object that holds dynamic data for a component. Unlike props states are mutable, meaning it can be changed. It allows a component to remember information and update the UI when that information changes. Managed inside the component. Can be changed using functions like setState in a class component or useState in a functional component. Changes in state cause the component to re-render to reflect the updated data.

```javascript
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // 0 is the initial state

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

Here, `count` is the state. Clicking the button updates the state, and React automatically updates the displayed number.

The key advantages of React components are:

* Components are **reusable**, reducing code duplication.
    
* Each component is **independent**, so changing one does not affect others.
    
* Only components with updated data are **re-rendered**, improving performance.
    

Example for component:

```javascript
import React from 'react';

// Functional component
function Greeting() {
  return <h1>Hello, welcome to React!</h1>;
}

export default Greeting;
```

**Code Explanation:**

* `Greeting` is a **functional component**.
    
* It returns **JSX**, a syntax similar to HTML, which React uses to render elements.
    
* The component can be displayed in the browser using `ReactDOM.render`.
    

---

## Types of React Components

React components are mainly of two types: **functional components** and **class components**.

### <mark>1. Functional Components</mark>

Functional components are simple **JavaScript functions** that return React elements.

* They are easier to write and understand.
    
* Can manage state using **React Hooks**.
    
* Faster because they do not require the `this` keyword.
    

```javascript
function Greet(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

### <mark>2. Class Components</mark>

A **class component** is a **JavaScript class** that **extends** `React.Component`. It is a way to create a React component using the **class syntax** from ES6.

```javascript
import React from "react";

class Greet extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

The class must have a `render()` method. The `render()` method **returns the JSX** that defines what should appear on the screen.

And also class components can **store dynamic data** inside `this.state`. To update state, you use `this.setState()`.

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 }; // initial state
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increase</button>
      </div>
    );
  }
}
```

`this.state` = stores the data. `this.setState()` = updates the state and **re-renders** the component.

A **component lifecycle** in React describes the **different stages a component goes through from creation to removal**. Class components have **lifecycle methods**, which are functions called at different stages of a component’s life. They are,

1. `componentDidMount()` – runs after the component is added to the screen.
    
2. `componentDidUpdate()` – runs after the component updates (state or props change).
    
3. `componentWillUnmount()` – runs just before the component is removed from the screen.
    

```javascript
class Timer extends React.Component {
  componentDidMount() {
    console.log("Timer mounted");
  }

  componentDidUpdate() {
    console.log("Timer updated");
  }

  componentWillUnmount() {
    console.log("Timer removed");
  }

  render() {
    return <h1>Timer</h1>;
  }
}
```

So as you can see, class components are useful but more complex than functional components.

---

## Rendering Components

**Rendering** means **displaying the component’s UI on the screen** (in the browser). In React, components return **JSX**, which React converts into **HTML elements** and shows them inside a specific place in the DOM.

### How Components are Rendered

1. **Using** `ReactDOM.render()`
    

* This method **attaches a React component to an HTML element**.
    
* The first argument is the component you want to render.
    
* The second argument is the **DOM element** where it should appear.
    

```javascript
import React from "react";
import ReactDOM from "react-dom";

function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Render the component inside the element with id 'root'
ReactDOM.render(<Greeting name="Pooja" />, document.getElementById('root'));

//  <Greeting name="Pooja" /> = the component we want to display.
//  document.getElementById('root') = the HTML element where the component will appear.
```

2. **Rendering Components Inside Other Components**
    

* Components can also be **nested inside other components**, instead of rendering directly with `ReactDOM.render()`.
    

```javascript
function App() {
  return (
    <div>
      <Greeting name="Pooja" />
      <Greeting name="Amie" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));

//  Here, App is a parent component containing two Greeting components.
```

---

## Components Inside Components

React allows **nesting components** to create modular applications.

* Components can be reused multiple times.
    
* Props can pass data to nested components for dynamic content.
    

```javascript
function Header() {
  return <h1>Welcome to My Site</h1>;
}

function Footer() {
  return <p>© 2024 My Company</p>;
}

function App() {
  return (
    <div>
      <Header />
      <p>This is the main content.</p>
      <Footer />
    </div>
  );
}

export default App;
```

Here are some best practices when creating components.

1. **Keep Components Small**: Each component should perform a single task.
    
2. **Prefer Functional Components**: Use class components only when necessary.
    
3. **Validate Props**: Use PropTypes to ensure correct data is passed.
    
4. **Lift State Wisely**: Share state at the nearest common ancestor if multiple components need it.
    

React components are the foundation of every React application. By breaking the UI into **reusable, independent pieces**, components make it easier to **organize, maintain, and scale** your app. Understanding how to use **props, state, and nested components** allows developers to build dynamic and interactive interfaces efficiently.

Mastering components is the first step toward becoming proficient in React, and with practice, you can create **clean, modular, and high-performing web applications**.