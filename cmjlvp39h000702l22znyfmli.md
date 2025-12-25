---
title: "Understanding React Events: A Complete Guide"
datePublished: Thu Dec 25 2025 20:11:42 GMT+0000 (Coordinated Universal Time)
cuid: cmjlvp39h000702l22znyfmli
slug: understanding-react-events-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1766693471562/0ddac1f0-9b16-4601-8400-8f731ba5c547.jpeg
tags: javascript, reactjs, react-events

---

React is a popular JavaScript library for building interactive user interfaces. One of the key features of React is its ability to handle user interactions efficiently through events. In this guide, we will explore React events, their usage, and best practices for handling them.

## What Are React Events?

In React, **events** are actions that happen in the application. These can be:

* Clicking a button
    
* Typing in an input field
    
* Moving the mouse
    
* Submitting a form
    
* Scrolling a section of the page
    

React provides a **synthetic event system**, which is a wrapper around the native browser events. This system ensures that events work consistently across all browsers.

---

## Basic Syntax

React events are added to JSX elements using camelCase attributes. The general syntax is:

```jsx
<element onEvent={handlerFunction} />
```

* `element`: The HTML or React element (like `<button>` or `<input>`).
    
* `onEvent`: The event name in camelCase (e.g., `onClick`, `onChange`).
    
* `handlerFunction`: The function to run when the event occurs.
    

Example:

```jsx
<button onClick={handleClick}>Click Me</button>
```

---

## Common React Event Handlers

| Event | Description |
| --- | --- |
| `onClick` | Triggered when an element is clicked. |
| `onChange` | Triggered when input value changes. |
| `onSubmit` | Triggered when a form is submitted. |
| `onKeyDown` | Triggered when a key is pressed. |
| `onKeyUp` | Triggered when a key is released. |
| `onMouseEnter` | Triggered when the mouse enters an element. |
| `onBlur` | Triggered when an element loses focus. |
| `onScroll` | Triggered when scrolling occurs in an element. |

---

## Handling Events in React

### 1\. Adding Event Handlers

Event handlers are added directly to JSX elements. Unlike HTML, React uses camelCase for event names:

```jsx
import React, { Component } from "react";

class App extends Component {
  state = { message: "Hello, welcome to React!" };

  handleClick = () => {
    this.setState({ message: "You clicked the button!" });
  };

  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
        <button onClick={this.handleClick}>Click Me</button>
      </div>
    );
  }
}

export default App;
```

---

### 2\. Passing Event Handlers as Props

Event handlers can be passed from a parent to a child component as props:

```jsx
function Button({ onClickHandler }) {
  return <button onClick={onClickHandler}>Click Me</button>;
}

function Parent() {
  const handleClick = () => alert("Button clicked!");
  return <Button onClickHandler={handleClick} />;
}
```

This helps child components communicate with parent components.

---

### 3\. Event Propagation

React events follow **bubbling** by default, meaning the event travels from the target element upwards. You can also use `onClickCapture` to handle events during the **capture phase** (before reaching the target).

```jsx
<div onClickCapture={() => console.log("Capture phase")}>
  <button onClick={() => console.log("Bubble phase")}>Click Me</button>
</div>
```

You can control event flow using:

* `event.stopPropagation()`: Stops the event from propagating further.
    
* `event.preventDefault()`: Prevents default browser behavior.
    

---

### 4\. onSubmit Event

The `onSubmit` event handles form submissions:

```jsx
function Form() {
  const [value, setValue] = React.useState("");

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Form submitted with value: ${value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={value} onChange={(e) => setValue(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

Key points:

* Prevents page reload using `event.preventDefault()`.
    
* Allows form validation before submission.
    
* Works with all input elements like `<input>`, `<textarea>`, `<select>`.
    

---

### 5\. onMouseDown Event

The `onMouseDown` event triggers when a mouse button is pressed. It is useful for immediate actions like drag-and-drop:

```jsx
function Box() {
  const [color, setColor] = React.useState("lightblue");

  return (
    <div
      onMouseDown={() =>
        setColor(color === "lightblue" ? "lightcoral" : "lightblue")
      }
      style={{ width: "200px", height: "200px", backgroundColor: color }}
    />
  );
}
```

---

### 6\. onDoubleClick Event

Triggered when a user double-clicks an element. Useful for toggling states or enabling edit modes:

```jsx
function Toggle() {
  const [isEditing, setIsEditing] = React.useState(false);

  return (
    <p onDoubleClick={() => setIsEditing(!isEditing)}>
      {isEditing ? "Edit Mode" : "View Mode"}
    </p>
  );
}
```

---

### 7\. onBlur Event

The `onBlur` event triggers when an element loses focus. Commonly used for input validation:

```jsx
function InputValidation() {
  const [email, setEmail] = React.useState("");
  const [error, setError] = React.useState("");

  const handleBlur = () => {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!regex.test(email)) setError("Enter a valid email");
    else setError("");
  };

  return (
    <div>
      <input
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        onBlur={handleBlur}
      />
      {error && <p>{error}</p>}
    </div>
  );
}
```

---

### 8\. onScroll Event

The `onScroll` event detects scrolling inside an element. Useful for infinite scrolling or dynamic UI changes:

```jsx
function ScrollTracker() {
  const [scrollPos, setScrollPos] = React.useState(0);

  const handleScroll = (e) => {
    setScrollPos(e.target.scrollTop);
  };

  return (
    <div
      onScroll={handleScroll}
      style={{ height: "200px", overflowY: "scroll" }}
    >
      <div style={{ height: "800px" }}>Scroll Position: {scrollPos}</div>
    </div>
  );
}
```

---

## Key Differences Between HTML DOM and React DOM Events

| Feature | HTML DOM | React DOM |
| --- | --- | --- |
| Updates | Directly updates DOM | Updates virtual DOM first, then updates real DOM |
| Event Handling | Directly on DOM | Uses synthetic event system |
| Performance | May be slower with frequent updates | Optimized with virtual DOM |
| Data Binding | Directly attached to elements | Controlled with state and props |

---

React events provide a powerful way to handle user interactions efficiently and consistently across browsers. By understanding different event types like `onClick`, `onSubmit`, `onMouseDown`, `onDoubleClick`, `onBlur`, and `onScroll`, you can build dynamic, responsive applications with interactive UI elements. React’s synthetic event system simplifies cross-browser behavior and allows fine-grained control over event propagation and default actions.