---
title: "Understanding React Lifecycle Methods"
datePublished: Fri Dec 26 2025 14:47:15 GMT+0000 (Coordinated Universal Time)
cuid: cmjmzjogj000002laaglk2c9v
slug: understanding-react-lifecycle-methods
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1766760341535/1f2eb031-c7f9-4197-9ca9-e5073e603742.png
tags: javascript, reactjs, javascript-framework, react-hooks, reactlifecycle

---

In React, every component goes through a series of stages called the **lifecycle**. These stages define how a component is created, updated, and removed. By understanding the React lifecycle, developers can run code at the right moments, manage resources efficiently, and improve application performance.

React components have three main lifecycle phases:

1. **Mounting:** When a component is created and inserted into the DOM.
    
2. **Updating:** When a component re-renders due to changes in state or props.
    
3. **Unmounting:** When a component is removed from the DOM.
    

---

### <mark>1. Mounting</mark>

Mounting is the first stage in a React component’s lifecycle. It occurs when a component is created and inserted into the DOM for the first time. During this phase, React sets up the component, initializes its state, and renders it on the screen.

The key lifecycle methods in this phase are:

1. `constructor()`
    
    The constructor is called before the component is mounted. Its main job is to initialize the component’s state and bind methods.
    
    ```javascript
    constructor(props) {
        super(props);
        this.state = { count: 0 };
        console.log("Constructor called");
    }
    ```
    
2. `getDerivedStateFromProps()`
    
    This is a static method that allows the state to be updated based on props. It runs before every render.
    
    ```javascript
    static getDerivedStateFromProps(props, state) {
        if (props.value !== state.value) {
            return { value: props.value };
        }
        return null;
    }
    ```
    
3. `render()`
    
    The `render()` method defines what the UI should look like. It returns the JSX that is displayed on the screen.
    
    ```javascript
    render() {
        return <div><h1>Hello, React Lifecycle!</h1></div>;
    }
    ```
    
4. `componentDidMount()`
    
    This method runs once, immediately after the component has been mounted. It is commonly used for tasks like fetching data or interacting with the DOM.
    
    ```javascript
    componentDidMount() {
        console.log("Component has been mounted");
        fetch("https://api.example.com/data")
            .then(res => res.json())
            .then(data => this.setState({ data }));
    }
    ```
    

---

### <mark>2. Updating</mark>

Updating happens when a component’s **state** or **props** change. React re-renders the component to reflect these updates. This phase is important for optimizing performance and responding to changes in data.

Key methods in this phase for **class components** are:

1. `getDerivedStateFromProps()`
    
      
    Called before `render()` to synchronize state with updated props. It runs every time a component is about to re-render.
    
    ```javascript
    static getDerivedStateFromProps(props, state) {
        if (props.value !== state.value) {
            return { value: props.value };
        }
        return null;
    }
    ```
    
2. `setState()`
    
      
    Used to update the component’s state. Calling `setState` triggers a re-render.
    
    ```javascript
    this.setState((prevState, props) => ({
        count: prevState.count + props.diff
    }));
    ```
    
3. `shouldComponentUpdate()`
    
      
    Decides whether the component should re-render. Returning `false` prevents unnecessary updates, improving performance.
    
    ```javascript
    shouldComponentUpdate(nextProps, nextState) {
        return nextProps.value !== this.props.value;
    }
    ```
    
4. `getSnapshotBeforeUpdate()`
    
      
    Runs just before the DOM updates. It captures information from the DOM (like scroll position) before changes happen. The returned value is passed to `componentDidUpdate`.
    
5. `componentDidUpdate()`
    
      
    Runs after the component has re-rendered. It’s useful for performing side effects like fetching new data or interacting with the DOM after an update.
    
    ```javascript
    componentDidUpdate(prevProps, prevState) {
        if (this.state.count !== prevState.count) {
            console.log("Count updated:", this.state.count);
        }
    }
    ```
    

---

### <mark>3. Unmounting</mark>

Unmounting occurs when a component is removed from the DOM. This phase is used to **clean up** any resources that the component was using, like timers, event listeners, or network requests. Proper cleanup prevents memory leaks and unexpected behavior.

When we say a component is **“removed from the DOM”**, it basically means the component is no longer being displayed on the page. This can happen in several scenarios, such as:

1. **Navigating to another page or route**
    
    * For example, in a React app using React Router, if you go from `/home` to `/about`, the components of the `/home` page are unmounted because they are no longer needed.
        
2. **Conditional rendering**
    
    * If a component is shown based on a condition, like `showModal && <Modal />`, and `showModal` becomes `false`, the `<Modal />` component is removed from the DOM.
        
3. **Removing a component from a list**
    
    * If you have a dynamic list of items and you delete one, the corresponding component for that item is unmounted.
        

The main lifecycle method in this phase for **class components** is:

`componentWillUnmount()`  
This method is called just before a component is removed from the DOM. It’s typically used for cleanup tasks.

```javascript
componentWillUnmount() {
    // Stop any running intervals or timers
    clearInterval(this.timer);

    // Remove event listeners
    window.removeEventListener('resize', this.handleResize);
}
```

---

Example :

```javascript
import React from "react";
import ReactDOM from "react-dom";

// Class component
class Test extends React.Component {
    // Constructor runs first during mounting
    constructor(props) {
        super(props);
        // Initialize state
        this.state = { hello: "World!" };
    }

    // Runs once after the component is mounted to the DOM
    componentDidMount() {
        console.log("componentDidMount()"); // Logs after initial render
    }

    // Method to update the state when link is clicked
    changeState() {
        this.setState({ hello: "Geek!" }); // Triggers re-render
    }

    // Determines whether the component should re-render
    shouldComponentUpdate(nextProps, nextState) {
        console.log("shouldComponentUpdate()"); // Logs before re-render
        return true; // Returning true allows update
    }

    // Runs after the component has re-rendered
    componentDidUpdate() {
        console.log("componentDidUpdate()"); // Logs after state change reflected in DOM
    }

    // Render method outputs the JSX to the DOM
    render() {
        return (
            <div>
                {/* Display current state */}
                <h1>GeeksForGeeks.org, Hello {this.state.hello}</h1>
                
                {/* Link to trigger state change */}
                <h2>
                    <a onClick={this.changeState.bind(this)}>Press Here!</a>
                </h2>
            </div>
        );
    }
}

// Create a root and render the component
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Test />);
```

* `constructor()` → Initializes state.
    
* `componentDidMount()` → Runs after the component mounts.
    
* `changeState()` → Updates the state, triggering a re-render.
    
* `shouldComponentUpdate()` → Checks if re-render is needed.
    
* `componentDidUpdate()` → Runs after the component updates.
    
* `render()` → Returns JSX to display in the DOM.
    

---

## Lifecycle Methods Table

| Method | Phase | Purpose |
| --- | --- | --- |
| `constructor()` | Mounting | Initialize state, bind methods |
| `getDerivedStateFromProps()` | Mounting/Updating | Sync state with props |
| `render()` | Mounting/Updating | Return JSX to display |
| `componentDidMount()` | Mounting | Run side effects like API calls |
| `shouldComponentUpdate()` | Updating | Decide whether to re-render |
| `getSnapshotBeforeUpdate()` | Updating | Capture information before DOM updates |
| `componentDidUpdate()` | Updating | Run actions after updates |
| `componentWillUnmount()` | Unmounting | Cleanup before removal |

---

## Key Lifecycle Methods in Action

### **1\.** `componentDidMount()`

This method runs **once**, immediately after a component is added to the DOM. It’s used for tasks that require the DOM or need to start background processes.

**Common uses:**

* Fetching data from APIs
    
* Setting up event listeners or subscriptions
    
* Initializing libraries that interact with the DOM
    

**Example:**

```javascript
componentDidMount() {
    // Example: start an interval timer
    this.interval = setInterval(() => {
        console.log("Interval running");
    }, 1000);
}
```

### **2\.** `componentWillUnmount()`

This method runs just before the component is removed from the DOM. It’s mainly used to **clean up resources**.

**Common uses:**

* Clearing intervals or timers
    
* Removing event listeners
    
* Canceling network requests
    

**Example:**

```javascript
componentWillUnmount() {
    // Stop the interval timer to prevent memory leaks
    clearInterval(this.interval);
}
```

### **3\.** `componentDidUpdate()`

This method runs after the component updates due to a change in **props** or **state**. It’s useful for reacting to changes or performing side effects.

**Common uses:**

* Reacting to prop or state changes
    
* Fetching new data when props change
    
* Triggering animations after an update
    

**Example:**

```javascript
componentDidUpdate(prevProps) {
    if (this.props.userId !== prevProps.userId) {
        this.fetchData(this.props.userId); // Fetch new data when userId changes
    }
}
```

### **4\.** `shouldComponentUpdate()`

This method decides whether the component should **re-render** when props or state change. Returning `false` can prevent unnecessary updates and improve performance.

**Example:**

```javascript
shouldComponentUpdate(nextProps) {
    // Only re-render if the 'value' prop has changed
    return nextProps.value !== this.props.value;
}
```

## React Class vs Functional Components

| Feature | Class Component | Functional Component |
| --- | --- | --- |
| State | `constructor()` | `useState()` |
| Lifecycle Methods | `componentDidMount()`, `componentDidUpdate()`, `componentWillUnmount()` | `useEffect()` handles all phases |
| Update Handling | `shouldComponentUpdate()`, `componentDidUpdate()` | `useEffect()` with dependency array |
| Cleanup | `componentWillUnmount()` | Cleanup function in `useEffect()` |

The `useEffect` hook lets you perform **side effects** (like fetching data, updating the DOM, or setting up subscriptions) in functional components. It combines the behavior of several class component lifecycle methods into **one hook**.

```javascript
useEffect(() => {
    // Code to run (side effect)

    return () => {
        // Cleanup code (runs on unmount or before next effect)
    };
}, [dependencies]);
```

### **Mapping Class Lifecycle to useEffect**

| Class Method | Functional Equivalent in useEffect | Notes |
| --- | --- | --- |
| `componentDidMount` | `useEffect(() => { ... }, [])` | Empty dependency array means it runs **once after mount** |
| `componentDidUpdate` | `useEffect(() => { ... }, [dep1, dep2])` | Include variables in the dependency array to run effect **when they change** |
| `componentWillUnmount` | `return () => { ... }` inside useEffect | Cleanup runs before unmounting or before the next effect |
| `shouldComponentUpdate` | React.memo or logic inside `useEffect` or state | Conditional rendering or memoization replaces it |

Functional components with hooks are simpler and more readable, while class components give more granular control over lifecycle phases.

---

Understanding the React lifecycle helps in managing component behavior efficiently. Key benefits include:

* **Data Fetching:** Load data at the right stage.
    
* **Performance Optimization:** Skip unnecessary renders.
    
* **Resource Management:** Clean up timers, subscriptions, or listeners.
    
* **State & Props Management:** Update UI reliably when data changes.
    

By mastering lifecycle methods, developers can create responsive, efficient, and maintainable React applications.